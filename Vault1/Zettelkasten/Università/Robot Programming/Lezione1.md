
![[Recording 20230926111800.webm]]
Date: 2023-09-26
Time: 10:01
Tags: 

---
# Lezione1

![[rp_01_compilers_and_build_systems.pdf]]

There are 3 types of programs:
...

## Native
**Native** execution, the first execution, this is machine dependent. The CPU process instructions sequentially. The machine instructions have a 1 to 1 correspondence with architecture specific alphanumeric opcodes. Another class of language is written in **abstract** language like Java. The code is very simple and can be optimize by the compiler. 
**Interpreters** are programs that directly execute a source file, performing the code execution on the spot. The execution is done during the parsing. Like Python, Matlab, etc. 

Program Files, we are in the Native programs, it's just an execution of a command. This file should contain all the information for the machine to execute, loaded in the machine.  
Program file contains.
- Machine code 
- Meta-information
to generate a memory image for CPU execution.

The compilation process can be vary expensive in order to be compile, because he needs to allocate a big amount for variable we dont even use, but, if he would not take it, he needs to rebuild the structure every time we compile. 
File:
- .h = declaration of the function
- .c .cpp = definition of the function

Example:
``` cpp
#include <iostream>
using namespace std;

int main(int argc, const char** argv) {
	cout << "hello world" << endl;
}
```

\#  is a function on the system (command which allows we to recognize the directive of pre-processor), in this case, its says to find `<iostream>` 


Example:
``` cmd
cpp file1 > file2
```
this means, that the output of file1 will be shown in file2

If we include the same file more times, maybe because one file that we called, calls another file we called, we can add `#pragma once` to include the last file only once.

With the pre-processor we can also use the `#define`. 
``` cpp
#define  nome_macro  valore_macro
```
The pre-processor reads the definition of the MACRO and, whenever it encounters its name within the source file, REPLACES the symbol with the corresponding value, WITHOUT checking the syntactic correctness of the resulting expression.

**Commands**
In order to optimize the code, the compile tries to cut the code, and convert it in assembly code.

- `g++ <option> -c <source file>` (compiler or assembler) generates an object file from a cpp eg. `hello_world.cpp -> hello_world.o`
  the system does this because we need a file that contains all the libraries and the cut part of the cpp file. Its very similar to the executable but it does not have the *entry point*.
- `g++ <option> -o <name> <files>` (linker) links together all files in the command line to generate a program file called `<name>`, it resolves the symbols.

Example:
``` cmd
mkdir compiling_stuff
cd compiling_stuff
emacs hello_world.cpp
g++ -c hello_world.cpp
ls
"we find hello_world.o"
g++ -o hello_world.cpp
```


``` cpp
#include <iostream>

using namespace std;

int main (int argc, const char** argv) {
	cout << "hello world" << endl;
}
```

whit `nm --demangle` we can read all the symbols, and the files that are included. In the print, U is undeclared, T function ... "demangle is an option to look better"
If we use it on .o it returns the variable, where most of them are waiting to be compiled. In the .exe are already compiled.

To call a executor we use `./nameexecutor`.
`ldd ./nameexecutor` can be used to see the library used and which refers to which

![[Recording 20230928094311.webm]]

## Large Builds
When we use a lot of files, we cant compile all the file all the time we modify the program, it takes too much time (like using make, to compile all the file in the folder). If i change a file we can compile only that one, and the ones that depends on that.

The fast way to compile is **Makefiles**, the idea is to receive a description of the file in set of rules. 
Rules in form:
\<target\> : \[tab\] \<dependancies\>
\<tab\> command

eg.
vec3.o . ve3.c ...

## CMake

...



---
# References
