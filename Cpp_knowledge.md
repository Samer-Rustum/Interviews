
# to dos
1. memory structure
2. structure of a microcontroller
3. differences between embedded systems/ firmware and general SW
4. Unit testing
5. low level development
6. memory management
7. Interrupts
8. DMA
## What is a mutex?
A mutex or mutual exclusion object is kind of like a lock for threads that prevents threads from accessing a piece of data at the same time. 

--- 

## What are the different data types in CPP?
1. **Basic Datatypes**      | The basic datatype. *eg char, short, int, float ...*
2. **Derived Datatypes**    | Define in terms of other datatypes. *Array, Pointer*
3. **Enumerated Datatypes** | a datatype whose legal values consist of a fixed set of constants.
4. **Void Datatypes**       | Data type that represents nothing (not really a data type)
   
---

## What is a dangling pointer?
A dangling pointer is a pointer to a memory address whose value got deleted somewhere in the program.

---

## What are static variables and functions?
Static variables and functions will have their scope restricted to the function in which they are declared.

Another feature of `static` is keeping the value between function invocations.

---

## What is the difference between `malloc()` and `calloc()`?
Both dynamically allocate memory (at runtime). `calloc()` also initializes that memory block to zeros while `malloc()` does not.

---

## What is the difference between declaring a header file with <> and ""?

<> The compiler searches for the headerfile within the built-in Path.
"" The compiler searchs for the headfile in the local directory.

---

## Store -5 in binary using two's complement
**Binary 5** 0101
**One's complement of 5** 1010
**Two's Complement of 5 (add 1)** 1011

---

## What does the Pragma directive do?

It provides additional information to the compiler *(eg #pragma startup allows to specify functions called upon program startup.)*

---

## Differentiate between Actual Parameters and Format Paramters

Formal parameters are when a variable that represents a value is passed into a function.

Actual paramters are when an actual value is passed into a function.

---

## Can we use the &(Address Operator) on constants?
No

---

## What is the linker?
A linker combines object files into an executable and resolves external references.

---

## What is a preprocessor?
A Preprocessor Directive is considered as a built-in predefined function or macro that acts as a directove to the compiler and it gets executed before the actual C program is executed.

It allows for:
- Inclusion of header files
- macro expansions
- conditional compilation
- line control

---

## Can a C program be compiled or executed in the absence of a main() function?

It can get compliled but it cannot get executed.

---
## What are the Cpp access specifiers?
1. **Public** accessible outside the class
2. **Private** accessible only to the class
3. **Protected** accessible only by the class and its children.

---

##  Is it possible to access a piece of memory outside the scope of its stack frame?

Yes, this is possible through a pointer, but it may result in unwanted behaviour. Once the piece of memory goes out of scope, the compiler can modify it.

### Example
```Cpp
#include <iostream>
int *foo(){
    int i = 1;
    return &i;
}
int main(){
    int *i = foo();
    std::cout<<*i<<std::endl;
    return 0;
}
```

---

## What is the size of a struct?

### Example
```c
struct basicStruct1{
    short a; //2 bytes
    char b; //1 byte
    int c;  //4 bytes
};
//expected size: 7 bytes
struct basicStruct2{
    char a;     //1 byte
    char b;     //1 byte
    int c;      //4 bytes
    short d:    //2 bytes
};
//expected size: 8 bytes
```
### Answer
sizeOf(basicStruct1) = 8 bytes

sizeOf(basicStruct2) = 12 bytes

It's more efficient to store things within blocks of four bytes based on the way that memory addresses work. Therefore, an extra byte is added to the middle of **basicStruct1**, making it 8 bytes.

It is also more efficient for the compiler to keep stuff ordered and not shift them around. That's why 2 bytes are added after **char b** in **basicStruct2** rather than move **short d** to the middle.

---

## What are include guards?

Include guards are a way to ensure that only one copy of a source/header file is used if it is being called by multiple files.

### Example
```cpp
#ifndef FILENAME_H
#define FILENAME_H

#include <somelibrary>
int main(){
    return 0;
};

#endif
```

---


## What is the difference between NULL and nullptr?

`Null` is equivalent to 0 and is type int. `nullptr` represents an actual pointer.


