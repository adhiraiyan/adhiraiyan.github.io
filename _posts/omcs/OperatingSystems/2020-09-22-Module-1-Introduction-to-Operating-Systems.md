---
title:  "Module 1: Introduction to Operating Systems"
date:   2020-09-22
categories: ['OMCS']
tags: ['']
image: /img/omcs/.jpg

---
<a name="contents"></a>
- [1.0: Overview](#1)
- [1.1: Interrupts](#1)
- [1.2: Resident Monitor Efficiency, Issues and Enforcement](#1)
- [1.3: CPU and Memory Protection](#1)
- [1.4: Practice Quiz](#1)
<!-- more -->

***
### <a name="0"></a>

An operating system acts as an intermediary between the user of a computer and the computer hardware. The purpose of an
operating system is to provide an environment in which a user can execute programs in a convenient way. The OS manages
the computer's memory and processes as well as all of its software and hardware.

By the end of this module, you will be able to:
- Write two motivations for operating systems
- Describe a simple operating system that serves the two motivations
- Describe buffering, spooling, caching and other strategies to make the OS more efficient
- Describe the mechanisms of CPU and Memory Protection
- Define system calls
- Describe the two modes of operation in an OS
- Describe the mechanism to switch between two modes


<img src="/img/omcs/1.OS/20200922a.PNG" alt="From Image to sensor batman" class="center-image">

***
### <a name="1"></a> Write two motivations for operating systems and describe a simple OS that serves the two motivations.
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

A primitive computer system can have just a CPU and Memory, where memory is an array of registers and each register is
an array of bits. In the CPU you have an arithmetic logical unit. The CPU is connected to the memory using two different
busses, the address bus and the data bus.

One of the functions an OS performs is automation of storage of programs. This automation requires some program that gets
the program you want to run and puts it into memory. This program is called the _Loader_. But how do you load the loader?
You use a _Bootstrap Loader_, this is a loader that loads itself. It loads part of the program manually but then loads
the rest itself. The bootstrap loader is kept in ROM and the area where it is stored is called Boot block. The Boot block
loads the operating system.

The loader understands only binary, so a _compiler_ converts a human readable language into binary code (assembly level).

How to run a program?
- Loader is given binary of a compiler
- Feed compiler program with source code
- It generates binary to some output device
- Binary to input device
- Compiler exited into loader
- Loader starts the binary program
- Program runs and reads data and produce output

From the above steps, every program becomes a series of 1s and 0s so how do you distinguish between the streams of inputs?
Even if you have a control card between programs, what if the program reads all control cards as data. There has to be
some way of controlling the behavior of a program, this is the first motivation of having an operating system.

The second motivating factor is you can't have programs to run infinitely long.


***
### <a name="2"></a> How does CPU Interrupt work?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Program Counter: Stores the address of the next instruction you are going to execute.
Status Register: Has a stack pointer, a mode bit

Whenever you have an interruption, the CPU takes an interrupt and takes the program counter and pushes it into the stack.
Then it searches for something called an _Interrupt Vector_. The interrupt vector stores the address of the program you
want to run. Like you interrupt CPU when you want to run a program and to run this, this program needs to be in memory
somewhere and the CPU needs the address of this program to run and the interrupt vector stores this address. The
program that you run when you take an interrupt is called an _Interrupt Service Routine_ (or Interrupt Handler).
Each interrupt has a number, each number has a corresponding Interrupt vector. In the Table in the OS, there is a listing
of the interrupt number and the IV. So by taking a look at the table, the CPU can figure out the address and the
Interrupt vector is loaded into the program counter. Once the ISR is complete, you go to the stack and get the program
that was running before and put it into the program counter.

These are the steps of an interrupt action:
- Push program counter on stack
- Push status register on stack
- Load program counter from Interrupt Vector
- Load status register from Interrupt Vector
- Once (Interrupt Service Routing) is done
- Return from interrupt
- Pop stack -> status register
- Pop stack -> program counter.

(When popping you pop the status register first because the stack is LIFO)


***
### <a name="2"></a> What are the strategies to make the OS more efficient?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Resident Monitor: Is a primitive operating system. This is an example to realize the two motivations.
1. We don't want to let the program write wherever they want. We don't want other programs to be eaten up as inputs by other programs.
2. We don't want to let programs run for infinitely long time.

To realize these two motivations, one solution is to have a Resident Monitor. Resident Monitor is a program that
monitors every other program. If a program wants to run, it first needs to get permission from the Resident Monitor,
the way it asks for permission is by something called system calls. The Resident monitor can grant or revoke the
request. For example if a program wants to read an input and it makes a system call to the Resident Monitor, the
Resident Monitor first reads the input and sends a signal called input ready to the program. When the program gets the
signal, it comes with a memory address of where the input is stored by the Resident Monitor. So the program doesn't
go to the input device to read the input, it goes to the memory where the input is made ready by the Resident Monitor.
There is a problem here, there isn't a way to ascertain if the program waits for the Resident Monitor or not. So, just
having a Resident Monitor doesn't enforce programs to check with the Resident Monitor. Also if a program has to wait till
it hears back from Resident Monitor, there are huge efficiency issues, because reading and writing input is expensive.
So one idea is to overlap reading and writing with computation. One technique is called buffering. To do that you need
a different type of memory called buffering memory.

Buffering: deals with input data from single program.
Spooling: is when a program is executing, the system buffering the next program. To achieve spooling, you need a
spooling list.
Caching: Use faster memory to store program and data partially.

These three add efficiency to the resident monitor.

To establish bounds so the program doesn't execute without Resident Monitor permission:
    - Hardware based protection
    - Modes of operation:
        - Privilege mode (kernel mode)
        - User mode (application mode)

How to track time in a computer system?

There is a crystal oscillator that acts as a clock. Let's say 2.8GHz and each tick results in an hardware interrupt.
Whereas a software interrupt can occur as a result of a user written application. And you can use this to switch between
programs for say every 1ms.


***
### <a name="3"></a> What are the mechanisms of CPU and Memory Protection?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

CPU protection:
- Hardware enforcement.
- Switching from user to privilege model is supervised by the resident monitor.

Memory protection:
We need to stop programs from executing as they wish and writing wherever they want. There are two approaches to do this:
    1. Tell application that you can't write in Resident Monitor mode. This is application specific.
    2. Tell application that you can only write between certain locations. The second one is better in practice.

To do the second one, we need specialized hardware called Memory Management Unit. When the memory address comes from CPU,
MMU interrupts and checks if it is between base and base+bound then it will execute but if it is not, then it will reject the code.
In MMU you have base and base+bound and this is stored in CPU registers. You can change this base and base+bound but
this function is privileged. You need CPU protection to have memory protection.


***
### <a name="4"></a> What are the two modes of operation in an OS and describe the mechanism to switch between the two modes.
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

The two modes of operation of programs:
- User Mode: Any program written by an application developer in user space where access to privileged instruction is limited.
- Kernels Mode: Any program which can execute privileged instructions
    - Interrupts are privilege model always
    - System calls generate interrupts.

A program is in user mode and to get access to input, it needs to make a system call but system call is in privilege mode.
So how does a program in user mode do this? To do this, we do a software driven interrupt.

System Call: A function call to a privileged function that is part of OS kernel.

What is the difference between a system call and a function call?

The operating system maintains a table of system calls.
What the system calls does is, it moves the system call code to the register and stops there and then the resident monitor
executes the code. This is called CPU protection.
- Hardware enforcement.
- Switching from user to privilege model is supervised by the resident monitor.
