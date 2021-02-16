---
date: 2019-04-25 00:00:42
layout: post
title: Reverse engineering
subtitle: Ever wanted to know how convert compiled program to actual code to find vulnerabilities? Well... click on me to find more.
description: Ever wanted to know how convert compiled program to actual code to find vulnerabilities? Well... click on me to find more.
image: /img/2019-04-25.jpg
category: programming
tags:
- Hacking
- Computing
paginate: false
---

### Introduction

I've written a simple C program that checks if a given `int` is a valid key.

> We want to crack this program, without knowing the code.

This way of hacking is called Reverse Engineering because we're trying to deconstruct a program to reveal its designs, architecture, or to extract knowledge from the object; like scientific research, the only difference being that scientific research is about a natural phenomenon.

Let's test this program with a few numbers:
```
user@Server ~/Downloads$ ./key 9
Result: false
user@Server ~/Downloads$ ./key 4
Result: false
user@Server ~/Downloads$ ./key 8
Result: false
user@Server ~/Downloads$
```
_Hmm... I'm not very lucky_

Ok, so now, let's reverse engineer it!

### Assembly
First, I need to tell you about Assembly code. An assembly (or assembler) language, often abbreviated asm, is any low-level programming language in which there is a very strong correspondence between the program's statements and the architecture's machine code instructions.

Each assembly language is specific to a computer architecture and operating system. In contrast, most high-level programming languages are generally portable across multiple architectures but require interpreting or compiling. Assembly language may also be called symbolic machine code.

Assembly language usually has one statement per machine instruction, but assembler directives, macros and symbolic labels of program and memory locations are often also supported.

Assembly code is converted into executable machine code by a utility program referred to as an assembler. The conversion process is referred to as assembly or assembling the source code.

> It's basically a way to visualise operations executed by the processor.

### Debugger
A debugger is a tool to help you debug your code at runtime or by disassembling it. Disassembling mean to convert compiled program to [Assembly](#Assembly) code.

Famous debuggers are `gdb` and `lldb`. We'll use `lldb`, but the process is roughly the same on `gdb`

In our case the `main` function, it looks like this if we use the command `di -n main` in `lldb`:
```
user@Server ~/Downloads$ lldb key
(lldb) target create "key"
Current executable set to 'key' (x86_64).
(lldb) di -n main
key[0x100000ec0] <+0>:   pushq  %rbp
key[0x100000ec1] <+1>:   movq   %rsp, %rbp
key[0x100000ec4] <+4>:   subq   $0x30, %rsp
key[0x100000ec8] <+8>:   movl   $0x0, -0x4(%rbp)
key[0x100000ecf] <+15>:  movl   %edi, -0x8(%rbp)
key[0x100000ed2] <+18>:  movq   %rsi, -0x10(%rbp)
key[0x100000ed6] <+22>:  cmpl   $0x1, -0x8(%rbp)
key[0x100000eda] <+26>:  jne    0x100000ef6               ; <+54>
key[0x100000ee0] <+32>:  leaq   0x9d(%rip), %rdi          ; "Please give a key to verify."
key[0x100000ee7] <+39>:  movb   $0x0, %al
key[0x100000ee9] <+41>:  callq  0x100000f58               ; symbol stub for: printf
key[0x100000eee] <+46>:  movl   %eax, -0x2c(%rbp)
key[0x100000ef1] <+49>:  jmp    0x100000f4a               ; <+138>
key[0x100000ef6] <+54>:  movq   -0x10(%rbp), %rax
key[0x100000efa] <+58>:  movq   0x8(%rax), %rax
key[0x100000efe] <+62>:  movq   %rax, -0x18(%rbp)
key[0x100000f02] <+66>:  movq   -0x18(%rbp), %rdi
key[0x100000f06] <+70>:  callq  0x100000f52               ; symbol stub for: atoi
key[0x100000f0b] <+75>:  movl   %eax, -0x1c(%rbp)
key[0x100000f0e] <+78>:  movl   -0x1c(%rbp), %edi
key[0x100000f11] <+81>:  callq  0x100000e10               ; is_prime
key[0x100000f16] <+86>:  leaq   0x8f(%rip), %rdi          ; "Result: %s\n"
key[0x100000f1d] <+93>:  leaq   0x82(%rip), %rcx          ; "false"
key[0x100000f24] <+100>: leaq   0x76(%rip), %rdx          ; "true"
key[0x100000f2b] <+107>: movl   %eax, -0x20(%rbp)
key[0x100000f2e] <+110>: movl   -0x20(%rbp), %eax
key[0x100000f31] <+113>: cmpl   $0x1, %eax
key[0x100000f34] <+116>: cmoveq %rdx, %rcx
key[0x100000f38] <+120>: movq   %rcx, -0x28(%rbp)
key[0x100000f3c] <+124>: movq   -0x28(%rbp), %rsi
key[0x100000f40] <+128>: movb   $0x0, %al
key[0x100000f42] <+130>: callq  0x100000f58               ; symbol stub for: printf
key[0x100000f47] <+135>: movl   %eax, -0x30(%rbp)
key[0x100000f4a] <+138>: xorl   %eax, %eax
key[0x100000f4c] <+140>: addq   $0x30, %rsp
key[0x100000f50] <+144>: popq   %rbp
key[0x100000f51] <+145>: retq
```
_Pretty ugly right?_

Hopefully, there are some comments on the right that will give us a hint about what this program does.

> Do you see the `is_prime` function called at `0x100000f11`?

This mean the key has to do with prime numbers, so let's check with `23`!
```
(lldb) run 23
Process 7577 launched: '/Users/user/Downloads/key' (x86_64)
Result: true
Process 7577 exited with status = 0 (0x00000000)
```
And it works!

### GUI Disassembler
Ok, so it was a little bit complex, even for a very simple program. Hopefully, there are some GUI debugger like Hopper that will help us convert Assembly to C code:
![Hopper reconstruction for the main function](https://i.imgur.com/Epj8157.jpg)
_`main` function represented_

As we can see, it's pretty readble and looks like the original `main` function. We can do the same with the `is_prime` function, so we could theorically rebuild the program.

## Real program
As I said earlier, I built that program, so here it is:
```c
#include<stdio.h>
#include <stdlib.h>

int is_prime(int num) {
     if (num <= 1) return 0;
     if (num % 2 == 0 && num > 2) return 0;
     for(int i = 3; i < num / 2; i+= 2) {
         if (num % i == 0)
             return 0;
     }
     return 1;
}

int main(int argc, char *argv[]) {
	typedef enum { false, true } bool;
	if (argc == 1) {
		printf("Please give a key to verify.");
	} else {
		char *key = argv[1];
		int k = atoi(key);
		int p = is_prime(k);
		char *r = p == 1 ? "true" : "false";
		printf("Result: %s\n", r);
	}
	return 0;
}
```

The disassembler was close to it.
__Now, you know reverse engineering is about: reconstruction. __
