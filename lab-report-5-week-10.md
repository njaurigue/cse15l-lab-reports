# Lab Report 5: Week 10 - Comparing Tests

In our Week 9 Lab, we used a Bash script to run different implementations of `MarkdownParse.java` on hundreds of files and varying test cases. Through this process, we compared our own implementation with the [provided implementation](https://github.com/ucsd-cse15l-w22/markdown-parse) to examine which markdown files produced varying results. In the following report, we'll examine two specific files and how their differing results were produced.  

## Test File 1 - `194.md`  

By using the `diff` command, we can compare our output files from both implementations of `MarkdownParse.java. With this command, we found that line 212 of our test files contained differing outouts:  

**Personal Implementation:** `[]`  
**Provided Implementation:** `[url]`  

Using the command below, we opened up our output files to the specified line to examine which test file resulted in these outputs:

```
vim +212 results1.txt
```  

At this point, we could then see that `194.md` was the test file below which produced the above outputs.  

```
[Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```  


## Test File 2 - `201.md`

Using the `diff` command as mentioned previously, we also found a discrepancy at line 230 of our output files:  

**Personal Implementation:** `[]`  
**Provided Implementation:** `[baz]`  

We then accessed our output file precisely at line 230 with the following command:  

```
vim +230 results1.txt
```  

We then found that `201.md` was the input causing a differing output array for our two implementations of MarkdownParse.java.

At this point

```
[foo]: <bar>(baz)

[foo]
```


---
[*Back to Main*](https://njaurigue.github.io/cse15l-lab-reports/index.html)