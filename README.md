# Discussion
Chapter 1 &amp; Chapter 2
# Team4---discussion

# 1. LINKERS
**Linker** is a program in a system which helps to link an object modules of program into a single object file.
It performs the process of linking. Linker are also called link editors.
Linking is process of collecting and maintaining piece of code and data into a single file.
Linker also link a particular module into system library.
It takes object modules from assembler as input and forms an executable file as output for loader. Linking is performed at both compile time, when the source code is translated into machine code and load time, when the program is loaded into memory by the loader.
Linking is performed at the last step in compiling a program.


LoaderLinking is of two types:

1.1.**Static Linking**:
--
It is performed during the compilation of source program.
Linking is performed before execution in static linking.
It takes collection of relocatable object file and command-line argument and generate fully linked object file that can be loaded and run. Static linker perform two major task: **Symbol resolution** – It associates each symbol reference with exactly one symbol definition .Every symbol have predefined task.
**Relocation** – It relocate code and data section and modify symbol references to the relocated memory location.
The linker copy all library routines used in the program into executable image.
As a result, it require more memory space.
As it does not require the presence of library on the system when it is run . so, it is faster and more portable.
No failure chance and less error chance.

1.2.**Dynamic linking**:
--
Dynamic linking is performed during the run time.
This linking is accomplished by placing the name of a shareable library in the executable image.
There is more chances of error and failure chances.
It require less memory space as multiple program can share a single copy of the library. Here we can perform code sharing. it means we are using a same object a number of times in the program.
Instead of linking same object again and again into the library, each module share information of an object with other module having same object.
The shared library needed in the linking is stored in virtual memory to save RAM.
In this linking we can also relocate the code for the smooth running of code but all the code is not relocatable.  It fixes the address at run time.

![static & dynamic](https://prepinsta.com/wp-content/uploads/2021/01/Static-vs-Dyanmic-Linking.webp)

| STATIC LINKING| DYNAMIC LINKING |
| ---------- | --------- |
|  Process of copying all library modules used in the program into final executable image | Process of loading the external shared libraries into the program and then bind those shared libraries dynamically to the program |
| Last step of compilation | Occurs at run time |
| Statistically linked files are larger in size | Dynamically linked files are smaller in size |
| Static linking takes constant load time | Dynamic linking takes less load time |
| There will be no compatibility issues with static linking | There will be compatibility issues with dynamic linking |

# 2. Computer system operation: Mode switching

We can define an Operating system as program that runs on the computer providing an interface to the computer user so that they can operate on the computer. But for this operation to be carried out, we found out that there is a channel through which these communications are carried out by transition. This transition involves making a system call, such as read, open, write and many others. The progress occurs such that a user calls these systems called Application Program Interface with appropriate parameters hence triggering an exception or interrupt. This process is called a transition from User to Kernel mode. We are going to discuss how this process is conducted.

![OS](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTEAuR-vV3P8BVm6qLStuAWZvqaY-YsJNeLgw&usqp=CAU)

The only way a user space application can explicitly initiate a switch to kernel mode during normal operation is by making a system call. We can define a Kernel as a system program that controls all programs running on the computer, basically its acting as a bridge between software and hardware of the system.  The mode bit is set to 0 in the kernel mode. It is changed from 0 to 1 when switching from kernel mode to user mode. When a system mode is generated the mode bit is set to Zero. After the competition of an execution, again a system trap is generated and this time the mode bit is set to 1. Therefore, the system control returns to kernel mode and the process execution continues.
We expounded more on how this process goes into the kernel mode through research.  We found out that an application process Calls the Glibc library function which knows the proper way of calling System Call for different architectures. Now the Glibc calls SWI instruction, which puts processor into Supervisor mode by updating Mode bits of CPSR register and jumps to vector address 0x08. Memory Management Unit will now allow kernel Virtual memory access and execution, for this process.  Now, from Vector address 0x08, process execution loads and jumps to SW Interrupt handler routine. In vector switch, System Call Number (SCNO) is extracted from SWI instruction and execution jumps to system call function using SCNO as index in system call table. Finally after System Call execution, in return path, user space registers are restored before starting execution in User Mode.
