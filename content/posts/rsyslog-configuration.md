---
title: rsyslog configuration
date: 2017-02-17 14:25:46
tags:
    - linux
    - log
---
1. configuration file location

```
/etc/rsyslog.conf
/etc/rsyslog.d/
```

2. rotate configuration location

```
/etc/logrotate.d/rsyslog
```

3. rotate options

The following is a list of some of the directives you can specify in your logrotate configuration file:

- weekly — Specifies the rotation of log files to be done weekly. Similar directives include:
    - daily
    - monthly
    - yearly

- compress — Enables compression of rotated log files. Similar directives include:
    - nocompress
    - compresscmd — Specifies the command to be used for compressing.
    - uncompresscmd
    - compressext — Specifies what extension is to be used for compressing.
    - compressoptions — Specifies any options to be passed to the compression program used.
    - delaycompress — Postpones the compression of log files to the next rotation of log files.

- rotate INTEGER  — Specifies the number of rotations a log file undergoes before it is removed or mailed to a specific address. If the value 0 is specified, old log files are removed instead of rotated.

- mail ADDRESS  — This option enables mailing of log files that have been rotated as many times as is defined by the rotate directive to the specified address. Similar directives include:
    - nomail
    - mailfirst — Specifies that the just-rotated log files are to be mailed, instead of the about-to-expire log files.
    - maillast — Specifies that the about-to-expire log files are to be mailed, instead of the just-rotated log files. This is the default option when mail is enabled.

4. FAQ:

- Q: Restart rsyslog since rsyslog configuration is changed, no log output

  A: remove `/var/lib/rsyslog/imjournal.state`, then restart rsyslog