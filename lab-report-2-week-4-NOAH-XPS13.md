# Lab Report 2: Week 4 - Debugging
In Labs 3 and 4, we explored different unique cases for the **MarkdownParse.java** file, which is designed to return all links (*excluding images*) of a given file. In the following report, we'll take a closer look at the following 3 examples:
1. A file that includes image links  
Ex: `![here's an image!](image.url)`  
2. A file that follows the link format, but with additional text between parentheses and brackets  
Ex: `[thisIsNotALink] Here's a sentence. (notALink)`
3. A file that contains no links at all

With these examples, we systematically tested each case to locate the failure-inducing inputs, symptoms, and bugs in order to make the appropriate changes required to get the expected output.  

## Example 1: Image Links
An expectation of **MarkdownParse** is to exclude all image links from the output array. For example, in the file [*test-file6.md*](https://github.com/njaurigue/markdown-parse/blob/main/test-file6.md), there is only a single image link. Therefore, **MarkdownParse** is expected to return an empty array.  

**test-file6.md:**  
```
# title

![link](page.com)
```

**Expected output for test-file6.md:**  
```
[]
```  
Prior to fixing this case, **MarkdownParse** was including this link in the output, returning:  

![imageLinksFailure](images\lab2-imageLinksFailure.png)  

In order to fix this case, we recognized the reasons that our program was failing. Originally, *test-file6.md* was a failure-inducing input because our program had no ability to differentiate between image links and regular links, and instead included both due to their coherence to the `[imageName](link)` formatting. We recognized the symptom as `[page.com]` being our output, when it should be `[]`. As such, we included code that first checked for an exclamation point, `!`, prior to the opening bracket, `[`, of each link to fix our bug and ensure we only added non-image links:

![imageLinks](images\lab2-imageLinks.png)  

## Example 2: Link Formatting
**MarkdownParse** utilizes the specific formatting and syntax of markdown files to identify links throughout the file. The formatting for these links is defined as brackets directly followed by parentheses, as shown in the following example:  

```
[imageName](link)
```  

If there were additional text between the closing bracket, `]`, and the opening parentheses, `(`, then the text within the parentheses should not be included in the output. For example, for [*test-file5.md*](https://github.com/njaurigue/markdown-parse/blob/main/test-file5.md), the expected output would be an empty array.  

**test-file5.md:**
```
# title

[stuff]

paragraph

(page.com)
```  

**Expected output for test-file5.md:**
```
[]
```

Instead, as a result of this failure-inducing input, `page.com` was once again included in our output:  

![linkFormattingFailure](images\lab2-linkFormattingFailure.png)  

To resolve this, we first looked at why **MarkdownParse** believed `page.com` was a link. We understood that the order of brackets and parentheses was correct, however the spacing between them was not, resulting in the above symptom. By observing this output, we recognized that `]` and `(` must be adjacent in order to be a vaild link. As such, this bug was fixed by ensuring each potential link had the appropriate space between the closing bracket and opening parentheses with the following code:

![linkFormatting](images\lab2-linkFormatting.png)

## Example 3: Broken Links
In our final example, we observe a file that contains some punctuation required for a complete link, but not all. As a result, we are left with a broken link, which should not be included in the ouput of **MarkdownParse**. The file [*test-file7.md*](https://github.com/njaurigue/markdown-parse/blob/main/test-file7.md) includes an example of this:

**test-file7.md:**
```
)[
```

**Expected output for test-flile7.md:**
```
[]
```

Before implementing our fix, running **MarkdownParse** on *test-file7.md* resulted in no output due to an infinite loop:

![brokenLinksFailure](images\lab2-brokenLinksFailure.png)

Our solution for broken links began with observing the failure-inducing input. Because *test-file7.md* did not include all the necessary punctuation for valid links, `[]()`, the while loop of the original

![brokenLinks](images\lab2-brokenLinks.png)

---
[*Back to Main*](https://njaurigue.github.io/cse15l-lab-reports/index.html)
