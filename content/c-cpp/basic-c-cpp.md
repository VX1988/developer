---
title: Basic C/C++
type: docs
---

in C++, any non-zero integer is treated as true in a condition.

So if function() returns -2, the condition is true. 

if return 0 then is false.

```cpp
#include <iostream>

int function() {
    return -2;
}

int main() {
    if (function()) {
        std::cout << "function() returned a non-zero value." << std::endl;
    } else {
        std::cout << "function() returned zero." << std::endl;
    }

    return 0;
}

```