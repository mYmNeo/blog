# NVIDIA IOCTL

## SEQ

1. version check
```
char buf[80];
int check_result;

// send op
memset(buf, 0x00, 80);
strncpy(buf+8, $version, 8);

check_result = *(int*)(buf+4);
```