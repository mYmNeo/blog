---
title: makefile memo
date: 2016-04-28 17:39:32
tags: 
    - linux
    - makefile
---
+ Checks if the first argument is non-empty.If so runs the second argument, otherwise runs the third
```makefile
$(if this-is-not-empty,then!,else!)
```

+ Execute command but not display on standard output
```makefile
@ls .
```
+ tell make to ignore error
```makefile
-rm -f *.*
```
+ The foreach function is very different from other functions. It causes one piece of text to be used repeatedly, each time with a different substitution performed on it. It resembles the for command in the shell sh and the foreach command in the C-shell csh.
```makefile
$(foreach var,list,text)
```