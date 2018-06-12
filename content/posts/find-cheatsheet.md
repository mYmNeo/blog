---
title: find cheatsheet
date: 2016-06-14 09:43:51
tags:
    - linux
    - find
    - cheatsheet
---
# Frequently used option of Find
<!-- more -->
## TEST
|option|description|example|
|----|----|----|
|-name <filename>|find the file which name is filename|find / -name "*.js"|
|-group <group-name>|find the file belongs to group-name|find / -group users|
|-user <user-name>|find the file belongs to user-name|find / -user root|
|-maxdepth <level>|Descend at most levels to find|find / -maxdepth 4|
|-empty|find file is empty and is either a regular file or a directory|find / -empty|
|-path <pattern>|find file name matches shell pattern <pattern>|find / -path "/sr*sc"|
|-perm <mode>|find file's permission bits are exactly mode|find / -perm 0664|
|-perm -<mode>|find all of the permission bits mode are set for the file|find / -perm -644|
|-perm /<mode>|find any of the permission bits mode are set for the file|find / -perm /644|
|-regex <pattern>|find file name matches regular expression <pattern>|find / -regex ".*bar"|
|-size n[cwbkMG]|find file uses n units of space, rounding up.  The following suffixes can be used: `b` for 512-byte blocks (this is the default if no suffix  is used), `c` for bytes, `w` for two-byte words, `k` for Kilobytes (units of 1024 bytes), `M` for Megabytes (units of 1048576 bytes), `G` for Gigabytes (units of 1073741824 bytes)|find / -size 1G|
|-type c|find file is of type c: `b` block (buffered) special,`c` character (unbuffered) special, `d` directory, `p` named pipe (FIFO), `f` regular file, `l` symbolic link; this is never true if the -L option or the -follow option is in effect, unless the symbolic link is broken.  If you want to search for symbolic links when -L is in effect, use -xtype, `s` socket|find / -type d
## ACTION
|option|description|
|----|----|
|-delete|Delete files|
|-exec <commadn>|Execute <command>|
|-fprint <file>|print the full file name into file <file>|
|-print|print the full file name on the standard output, followed by a newline|
|-prune|if the file is a directory, do not descend into it|