# Lab Report 2: Week 4 - Debugging
In Labs 3 and 4, we explored different unique cases for the **MarkdownParse.java** file, which is designed to return all links (*excluding images*) of a given file. In the following report, we'll take a closer look at the following 3 examples:
1. A file that includes image links  
Ex: `![here's an image!](image.url)`  
2. A file that follows the link format, but with additional text between parentheses and brackets  
Ex: `[thisIsNotALink] Here's a sentence. (notALink)`
3. A file that contains no links at all

With these examples, we systematically tested each case to locate the failure-inducing inputs, symptoms, and bugs in order to make the appropriate changes required to get the expected output.  
## Example 1: Image Links
An expectation of MarkdownParse is to exclude all image links from the output array. For example, in the file [`test-file6.md`](https://github.com/njaurigue/markdown-parse/blob/main/test-file6.md), there is only a single image link. Therefore, MarkdownParse is expected to return an empty array.  

**test-file6.md:**  
```
# title
![link](page.com)
```

**Expected output for test-file6.md:**  
```
[]
```  
Prior to fixing this case, MarkdownParse was including this link in the output, returning:  
![imageLinksFailure](images\lab2-imageLinksFailure.png)  

In order to fix this case, we recognized the reasons that our program was failing. Originally, `test-file6.md` was a failure-inducing input because our program had no ability to differentiate between image links and regular links, and instead included both due to their coherence to the `[imageName](link)` formatting. We recognized the symptom as `[page.com]` being our output, when it should be `[]`. As such, we included code that first checked for an exclamation point, `!`, prior to the opening bracket, `[`, of each link to fix our bug and ensure we only added non-image links:

![imageLinks](images\lab2-imageLinks.png)  

---
[*Back to Main*](https://njaurigue.github.io/cse15l-lab-reports/index.html) 
