---
layout : post
title : Copy Assignment Or Copy Constructor
---

```c++
#include <iostream>

class A {
 public:
   A(int x): _x(x) {}
   A(const A& other) {
     this->_x = other._x;
   }
   A& operator = (const A& other) {
     this->_x = other._x;
   }
 private:
   int _x;
};
int main() {
  A a(1);
  A b = a;
  A c;
  c = a;
}
```
In g++ 4.7.2 the code `A b = a` will trigger the copy constructor not default constructor and then the copy assignment.
Is this designed to be like this?
