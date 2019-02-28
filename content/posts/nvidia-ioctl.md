# NVIDIA IOCTL

## SEQ

+ version check

```
char buf[80];
int check_result;

// send op
memset(buf, 0x00, 80);
strncpy(buf+8, $version, 8);

ioctl($ctl_fd, 0xc04846d2, buf);

check_result = *(int*)(buf+4);
```

+ system memory

```
size_t block_size_bytes;
char buf[100];
char* endptr;
int fd;

fd = open("/sys/devices/system/memory/block_size_bytes", r, O_RDONLY);

read(fd, buf, 99);
block_size_bytes = strtoul(buf, &endptr, 16, 0);

ioctl($ctl_fd, 0xc00846d6, buf);
```

+ init 3

```
global int init = 0;

ioctl($ctl_fd, 0xc00446ca, &init);
```

+ card information

```
nv_ioctl_card_info_t cards[32];

memset(cards, 0x00, sizeof(cards));

cards[0].flags = 0xffffffff;

ioctl($ctl_fd, 0xca0046c8, cards);
```

+ get seq id

```
int seq_id;
char buf[32];

seq_id = 0;
memset(buf, 0x00, 32);

*((size_t *)buf[16]) = &seq_id;

ioctl($ctl_fd, 0xc020462b, buf);
```

+ init 4

```
char buf[32];
char result[128];

*(int*)buf = seq_id;
*(int*)(buf+4) = seq_id;
*(int*)(buf+8) = 0x214;
*(int64_t*)(buf+16) = (int64_t)result;
*(int64_t*)(buf+24) = 128;

ioctl($ctl_fd, 0xc020462a, buf);
```

+ loop for every device

```
```