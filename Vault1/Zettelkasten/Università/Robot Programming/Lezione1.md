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
- .h .hpp -> HEADERS ()
- .c .cpp .S -> SOURCE FILES
- .o -> OBJECT FILES
- .a -> STATIC LIBRARIES
- .so -> SHARED LIBRARIES
- EXECUTABLES

Then **Compiling** and then again **Linking**.

---
# References
