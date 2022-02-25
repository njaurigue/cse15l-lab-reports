# Lab Report 4: Week 8 - MarkdownParse Testing  
For the last 7 weeks, we've been working with the MarkdownParse program, which which returns all valid links within a given markdown, `.md`, file. Below are two repositories, containing my personal repository of the program along with another student's repository, which we reviewed during our Week 7 lab session.

My Implementation of MarkdownParse:
[https://github.com/njaurigue/markdown-parse](https://github.com/njaurigue/markdown-parse)  

Another Student's Implementation of MarkdownParse (credit - Jared Jose):
[https://github.com/JaredJose/markdown-parse](https://github.com/JaredJose/markdown-parse) 

In the following report, we will review 3 markdown snippets, each with unique cases that will expect different behavior from MarkdownParse. For each snippet, we will examine the expected output, the failing output of our current implementations, and potential changes to produce the expected output.  

## Snippet 1:
```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```    

In this first snippet, the unique behavior being tested with MarkdownParse is the use of code within the link (denoted by a backtick) in lines 1 and 2, as well as unmatched opening and closing brackets in lines 3 and 4. When reviewing the markdown preview window in VSCode, which allows us to visualize the expected behavior for markdown files (especially valid links in this scenario) we find that the links in lines 2, 3, and 4 should all be returned by MarkdownParse, while "url.com" in line 1 is invalid, and should therefore be omitted.  



---
[*Back to Main*](https://njaurigue.github.io/cse15l-lab-reports/index.html)