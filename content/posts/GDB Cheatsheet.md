# GDB Cheatsheet

- Copy Between Memory and a File

```
dump [format] memory filename start_addr end_addr
dump [format] value filename expr

Dump the contents of memory from start_addr to end_addr, or the value of expr, to filename in the given format.

The format parameter may be any one of:

binary
Raw binary form.

ihex
Intel hex format.

srec
Motorola S-record format.

tekhex
Tektronix Hex format.

verilog
Verilog Hex format.
```

- Show more line of source code

```
set listsize xxx
```

