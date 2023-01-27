
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

## What is the difference between NULL and nullptr?

`Null` is equivalent to 0 and is type int. `nullptr` represents an actual pointer.


