---
title: audit command cheatsheet
date: 2018-07-03 18:00:00
tags: 
    - linux
    - audit
---

# Audit Cheatsheet

- audit syscall

```bash
auditctl -a exit,always -S <syscall>
```

- audit file

```bash
auditctl -w /etc/shadow -p wa 
```

- extra option

|Tag|Description|
|---|-----------|
|-b backlog|Set max number of outstanding audit buffers allowed (Kernel Default=64) If all buffers are full, the failure flag is consulted by the kernel for action.|
|-e [0..2]|Set enabled flag. When 0 is passed, this can be used to temporarily disable auditing. When 1 is passed as an argument, it will enable auditing. To lock the audit configuration so that it can’t be changed, pass a 2 as the argument. Locking the configuration is intended to be the last command in audit.rules for anyone wishing this feature to be active. Any attempt to change the configuration in this mode will be audited and denied. The configuration can only be changed by rebooting the machine.|
|-f [0..2]|Set failure flag 0=silent 1=printk 2=panic. This option lets you determine how you want the kernel to handle critical errors. Example conditions where this flag is consulted includes: transmission errors to userspace audit daemon, backlog limit exceeded, out of kernel memory, and rate limit exceeded. The default value is 1. Secure environments will probably want to set this to 2.|
|-h|Help|
|-i|Ignore errors when reading rules from a file|
|-l|List all rules 1 per line. This can take a key option (-k), too.|
|-k key|Set a filter key on an audit rule. The filter key is an arbitrary string of text that can be up to 31 bytes long. It can uniquely identify the audit records produced by a rule. Typical use is for when you have several rules that together satisfy a security requirement. The key value can be searched on with ausearch so that no matter which rule triggered the event, you can find its results. The key can also be used on delete all (-D) and list rules (-l) to select rules with a specific key. You may have more than one key on a rule if you want to be able to search logged events in multiple ways or if you have an audispd plugin that uses a key to aid its analysis.|
|-m text|Send a user space message into the audit system. This can only be done by the root user.|
|-p [r\|w\|x\|a]|Set permissions filter for a file system watch. r=read, w=write, x=execute, a=attribute change. These permissions are not the standard file permissions, but rather the kind of syscall that would do this kind of thing. The read & write syscalls are omitted from this set since they would overwhelm the logs. But rather for reads or writes, the open flags are looked at to see what permission was requested.|
|-q mount-point,subtree|If you have an existing directory watch and bind or move mount another subtree in the watched subtree, you need to tell the kernel to make the subtree being mounted equivalent to the directory being watched. If the subtree is already mounted at the time the directory watch is issued, the subtree is automatically tagged for watching. Please note the comma separating the two values. Omitting it will cause errors.|
|-r rate|Set limit in messages/sec (0=none). If this rate is non-zero and is exceeded, the failure flag is consulted by the kernel for action. The default value is 0.|
|-R file|Read rules from a file. The rules must be 1 per line and in the order that they are to be executed in. The rule file must be owned by root and not readable by other users or it will be rejected. The rule file may have comments embedded by starting the line with a ’#’ character. Rules that are read from a file are identical to what you would type on a command line except they are not preceeded by auditctl (since auditctl is the one executing the file).|
|-s|Report status. Note that a pid of 0 indicates that the audit daemon is not running.|
|-t|Trim the subtrees after a mount command.|
|-a list,action|Append rule to the end of list with action. Please note the comma separating the two values. Omitting it will cause errors.|
|-A list,action|Add rule to the beginning list with action.|
|-d list,action|Delete rule from list with action. The rule is deleted only if it exactly matches syscall name and field names.|
|-D|Delete all rules and watches. This can take a key option (-k), too.|
|-S [Syscall name or number\|all]|Any syscall name or number may be used. The word ’all’ may also be used. If this syscall is made by a program, then start an audit record. If a field rule is given and no syscall is specified, it will default to all syscalls. You may also specify multiple syscalls in the same rule by using multiple -S options in the same rule. Doing so improves performance since fewer rules need to be evaluated. If you are on a bi-arch system, like x86_64, you should be aware that auditctl simply takes the text, looks it up for the native arch (in this case b64) and sends that rule to the kernel. If there are no additional arch directives, IT WILL APPLY TO BOTH 32 & 64 BIT SYSCALLS. This can have undesirable effects since there is no guarantee that, for example, the open syscall has the same number on both 32 and 64 bit interfaces. You may want to control this and write 2 rules, one with arch equal to b32 and one with b64 to make sure the kernel finds the events that you intend.|
|-F [n=v \| n!=v \| n<v \| n>v \| n<=v \| n>=v \| n&v \| n&=v]|Build a rule field: name, operation, value. You may have up to 64 fields passed on a single command line. Each one must start with -F. Each field equation is anded with each other to trigger an audit record. There are 8 operators supported - equal, not equal, less than, greater than, less than or equal, and greater than or equal, bit mask, and bit test respectively. Bit test will "and" the values and check that they are equal, bit mask just "ands" the values. Fields that take a user ID may instead have the user’s name; the program will convert the name to user ID. The same is true of group names.|
|-w path|Insert a watch for the file system object at path. You cannot insert a watch to the top level directory. This is prohibited by the kernel. Wildcards are not supported either and will generate a warning. The way that watches work is by tracking the inode internally. If you place a watch on a file, its the same as using the -F path option on a syscall rule. If you place a watch on a directory, its the same as using the -F dir option on a syscall rule. The -w form of writing watches is for backwards compatibility and the syscall based form is more expressive. Unlike most syscall auditing rules, watches do not impact performance based on the number of rules sent to the kernel. The only valid options when using a watch are the -p and -k. If you need to anything fancy like audit a specific user accessing a file, then use the syscall auditing form with the path or dir fields. See the EXAMPLES section for an example of converting one form to another.|
|-W path|Remove a watch for the file system object at path.|

**-a list**

|Tag|Description|
|---|-----------|
|task|Add a rule to the per task list. This rule list is used only at the time a task is created -- when fork() or clone() are called by the parent task. When using this list, you should only use fields that are known at task creation time, such as the uid, gid, etc.|
|entry|Add a rule to the syscall entry list. This list is used upon entry to a system call to determine if an audit event should be created.|
|exit|Add a rule to the syscall exit list. This list is used upon exit from a system call to determine if an audit event should be created.|
|user|Add a rule to the user message filter list. This list is used by the kernel to filter events originating in user space before relaying them to the audit daemon. It should be noted that the only fields that are valid are: uid, auid, gid, and pid. All other fields will be treated as non-matching.|
|exclude|Add a rule to the event type exclusion filter list. This list is used to filter events that you do not want to see. For example, if you do not want to see any avc messages, you would using this list to record that. The message type that you do not wish to see is given with the msgtype field.|

**-a action**

|Tag|Description|
|---|-----------|
|never|No audit records will be generated. This can be used to suppress event generation. In general, you want suppressions at the top of the list instead of the bottom. This is because the event triggers on the first matching rule.|
|always|Allocate an audit context, always fill it in at syscall entry time, and always write out a record at syscall exit time.|

**-F field**

|Tag|Description|
|---|-----------|
|a0, a1, a2, a3|Respectively, the first 4 arguments to a syscall. Note that string arguments are not supported. This is because the kernel is passed a pointer to the string. Triggering on a pointer address value is not likely to work. So, when using this, you should only use on numeric values. This is most likely to be used on platforms that multiplex socket or IPC operations.|
|arch|The CPU architecture of the syscall. The arch can be found doing ’uname -m’. If you do not know the arch of your machine but you want to use the 32 bit syscall table and your machine supports 32 bit, you can also use b32 for the arch. The same applies to the 64 bit syscall table, you can use b64. In this way, you can write rules that are somewhat arch independent because the family type will be auto detected. However, syscalls can be arch specific and what is available on x86_64, may not be available on ppc. The arch directive should preceed the -S option so that auditctl knows which internal table to use to look up the syscall numbers.|
|auid|The original ID the user logged in with. Its an abbreviation of audit uid. Sometimes its referred to as loginuid. Either the text or number may be used.|
|devmajor|Device Major Number|
|devminor|Device Minor Number|
|dir|Full Path of Directory to watch. This will place a recursive watch on the directory and its whole subtree. Should only be used on exit list. See "-w".|
|egid|Effective Group ID|
|euid|Effective User ID|
|exit|Exit value from a syscall. If the exit code is an errno, you may use the text representation, too.|
|fsgid|Filesystem Group ID|
|fsuid|Filesystem User ID|
|filetype|The target file’s type. Can be either file, dir, socket, symlink, char, block, or fifo.|
|gid|Group ID|
|inode|Inode Number|
|key|This is another way of setting a filter key. See discussion above for -k option.|
|msgtype|This is used to match the message type number. It should only be used on the exclude filter list.|
|obj_user|Resource’s SE Linux User|
|obj_role|Resource’s SE Linux Role|
|obj_type|Resource’s SE Linux Type|
|obj_lev_low|Resource’s SE Linux Low Level|
|obj_lev_high|Resource’s SE Linux High Level|
|path|Full Path of File to watch. Should only be used on exit list.|
|perm|Permission filter for file operations. See "-p". Should only be used on exit list. You can use this without specifying a syscall and the kernel will select the syscalls that satisfy the permissions being requested.|
|pers|OS Personality Number|
|pid|Process ID|
|ppid|Parent’s Process ID|
|subj_user|Program’s SE Linux User|
|subj_role|Program’s SE Linux Role|
|subj_type|Program’s SE Linux Type|
|subj_sen|Program’s SE Linux Sensitivity|
|subj_clr|Program’s SE Linux Clearance|
|sgid|Saved Group ID. See getresgid(2) man page.|
|success|If the exit value is >= 0 this is true/yes otherwise its false/no. When writing a rule, use a 1 for true/yes and a 0 for false/no|
|suid|Saved User ID. See getresuid(2) man page.|
|uid|User ID|