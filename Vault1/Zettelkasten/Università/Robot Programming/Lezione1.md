Date: 2023-10-17
Time: 12:08
Tags: 

---
# Lezione1

There are 3 types of executed code:
- Interpreter  (Python)
- Emulator program (Java)
- Directly by CPU (kernel)

**CPU**
The CPU executes instructions in a sequential manner.
Each instruction is composed of binary digits, and the CPU retrieves instructions and operands from memory.
The machine instructions have a direct mapping with architecture-specific alphanumeric opcodes (as seen in Assembly language), with a one-to-one correspondence.

**Interpreter**
Interpreters are software applications that carry out the immediate parsing and execution of a source file. The execution process occurs concurrently with the parsing process.

## Program Files and Execution
The .exe is a file that contains enough information for someone, to create a memory image, that contains the sequence of the instruction executable by CPU. Exe its an architecture, that contains constants, global variables, so it needs pointers to libraries. So in program we need the code, the data and the metadata. 

## Building a Program File

In order of **files** we have:
- .h .hpp -> HEADERS (declaration of functions, classes...)
- .c .cpp .S -> SOURCE FILES (source code of the program)
- .o -> OBJECT FILES (object files that can be linked to create an executable)
- .a -> STATIC LIBRARIES (pre-compiled object modules that can be linked statically to programs)
- .so -> SHARED LIBRARIES (dynamic library files that can be shared among multiple programs, are loaded into memory only when needed, reducing memory usage)
- EXECUTABLES (final application that can be run by the user, it knows all the info required to be loaded into memory, unlike object files)

Then **Compiling** and then again **Linking**.

==Example==
Having a code:
```cpp
#include <iostream>
using namespace std;

int main(int argc, const char** argv) {
	cout << "hello world" << endl;
}
```

To generate an object file we have to use:
```cmd
g++ <options> -c <source file>
```
To generate a program file, linking all the files in command line:
```cmd
g++ <options> -o <name> <files>
```
It can be used gcc too

This is a **dependency tree**
![[Screenshot from 2023-10-17 16-11-57.png]]
to compile this thing, i need the following commands:
![[Screenshot from 2023-10-17 16-10-30.png]]

If I change 1 file, do I have to compile all again? NO. We can see the time stamp when all the file where produced. But since often, the file depends on a lot of files, we should check that all the sources are older then dependencies. For example, in the tree, `vehicle.o` depends from `vehicle.c` that depends from `vehicle.h` that depends from `surface.h` and so on... So if i change `surface.h`, i have to recompile `vehicle.o` too.
To implement this idea, i have to create a file (**Makefiles**) that declare the **target**, an object file, and what are the **dependencies**, the file which the target depends.
==Example:==
```Makefile
vec3.o : vec3.c vec3.h
		 gcc -std=gnu99 -c -o vec3.o vec3.c
```

We can ask the compiler which file depends on which:
```cmd
gcc (or g++) -MM <source file>
```

==Example:==
```cmd
g++ -MM vehicle.c
```
will generate:
```cmd
vehicle.o: vehicle.c vehicle.h surface.h vec3.h image.h
```
so if we compile vehicle.c we'll get vehicle.o, that use: vehicle.c ...

**MAKEFILE**
![[Screenshot from 2023-10-17 16-36-30.png]]

<<<<<<< HEAD
![[Pasted image 20231017164311.png]]
=======
to call a Makefile i need just to type: make


>>>>>>> origin/main


---
# References
