Date: 2023-10-03
Time: 10:11
Tags:

---
# Lezione2

Listen the audio at 10.58 hour, 
we want trasform this file in a binary
In order to compile all the files, we need a CMake
```txt
include_directories(${EIGEN3_INCLUDE_DIR} src/)
```

With this code (a CMakeList.txt), we can create a connection between files
```txt
# add project source code each for the fold we want, in each they need a CMAKE already done
add_subdirectory(src)
```
In each, to add the cpp files, we use a CMakeList.txt, if it doesn't exist, then create it:
``` txt
add_library(messages SHARED
	base_sensor_message.cpp
	example.cpp)
```


We can use to find all the programs that has cpp in the name:
``` cmd
find . -name "*.cpp"
```

Create an executable:
```txt
add_executable(many_objects_in_stack_example
	many_object_in_stack_example.cpp)
```

With ldd we can check the library linked
```cmd
ldd /usr/bin/mp3blaster
```

![[Recording 20231003110832.webm]]



Dinamic library?

Static?

---
# References
