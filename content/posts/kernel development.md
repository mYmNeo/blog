# Kernel Development Cheatsheet


- `asmlinkage` macro

The asmlinkage tag is one other thing that we should observe about this simple function. This is a `#define` for some gcc magic that tells the compiler that the function should not expect to find any of its arguments in registers (a common optimization), but only on the CPU's stack. Recall our earlier assertion that system_call consumes its first argument, the system call number, and allows up to four more arguments that are passed along to the real system call. system_call achieves this feat simply by leaving its other arguments (which were passed to it in registers) on the stack. All system calls are marked with the asmlinkage tag, so they all look to the stack for arguments. Of course, in sys_ni_syscall's case, this doesn't make any difference, because sys_ni_syscall doesn't take any arguments, but it's an issue for most other system calls. 

- `__builtin_return_address(0)`

get caller address

- `__user, __kernel` attribute

>Some of the checks performed by Sparse require annotating the source code using the __attribute__ GCC extension, or the Sparse-specific __context__ specifier.[5] Sparse defines the following list of attributes:
>
>address_space(num)
bitwise
force
context(expression,in_context,out_context)

so `__user` indicate the pointer is from user-space, kernel can't dereference it. `__kernel` is objective
