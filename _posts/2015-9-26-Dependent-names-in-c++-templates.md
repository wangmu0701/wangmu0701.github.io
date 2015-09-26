---
layout : post
title : Dependent names in C++ template
---
C++ standard 14.6.2/3
>In the definition of a class or class template, the scope of a dependent base class (14.6.2.1) is not examined
>during unqualified name lookup either at the point of definition of the class template or member or during
>an instantiation of the class template or member. 

```c++
typedef double A;
template<class T> class B {
  typedef int A;
};
template<class T> struct X : B<T> {
  A a; // a has type double
};
```
The type name `A` in the definition of `X<T>` binds to the typedef name defined in the global namespace scope,
not to the typedef name defined in the base class `B<T>`.

```c++
struct A {
  struct B { /∗ ... ∗/ };
    int a;
    int Y;
};

int a;

template<class T> struct Y : T {
  struct B { /∗ ... ∗/ };
  B b; // The B defined in Y
  void f(int i) { a = i; } // ::a
  Y* p; // Y<T>
};

Y<A> ya;
```
The members `A::B`, `A::a`, and `A::Y` of the template argument `A` do not affect the binding of names in `Y<A>`.
