Move Semantics
---
Week 1, Lecture 2

* lvalue is a variable or object that persists beyond an expression
    * if you can take the address of a, it is most likely an lvalue.
```cpp

int a = 5;
&a; //valid because a is an lvalue
&(a+1) // invalid because (a+1) is not an lvalue

int* p1 = &a;
&p1;
&(++p1); //valid, preincrements
&(p1++); //invalid, creates a copy


```
![Image 7](img/img3.png)



![Image 7](img/img7.png)


Rule of 5:
- Destructor (~T)
- Copy constructor (T(const T&))
- Copy assignment operator (T& operator=(const T&))
- Move constructor (T(T&&) noexcept)
- Move assignment operator (T& operator=(T&&) noexcept)


## Elision
* c++20, unnamed return value skips over a step
* Needs to be:
    * unnamed
    * constructing something from unnamed return value
```cpp
//use std::move() when moving dynamic memory in a move constructor
int a = new int(5);
int b = std::move(a);
```

* If a function returns a value, it is a rvalue.
* Otherwise if it returns a reference, it is a lvalue.


```cpp
string MakeStr() {
    return string("string1");
}

string MakeStr2() {
    string temp("string2");
    return temp;
}

int main() {
    string r1(MakeStr2());
}
```

