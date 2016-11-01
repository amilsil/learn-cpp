# Type Deduction
* c++ 98 had TD only for templates
* c++ 11 has it for auto, universal references, lambdas, decltype
* c++ 14 function return types, lambda init captures

# Template Type Deduction

```cpp
template<typename T>
void f(ParamType param);

f(expr); //deduces both T and ParamType
```

## Non-URef Reference/Pointer Parameters
* A `typename` is never deduced to a reference type.
* When an int& is passed to a int& param, type is **not int&&** but **int&**
```cpp
template<typename T> // a typename will never be a reference type
void f(T& param);

int x = 22;
const int cx = x;
const int& rx = x;

f(x); // T: int, param: int&
f(cx); // T: const int, param: const int&
f(rx); // T: const int, param: const int&
```

* When a param is defined to be `const T`, T is **not** deduced to be const.
```cpp
template<typename T>
void f(const T& param);

int x = 22;
f(x); // T: int, param: const int&
```

* A `typename` is never deduced to a pointer type.

```cpp
template<typename T>
void f(T* param);

int x = 22;
const int *pcx = &x;

f(&x); // T:int, param: int*
f(pcx); // T:const int, param: const int*
```

## auto and Non-URef Reference/Pointer Variables
auto plays as same as T

## Universal references
* **Can refer to both r-values and l-values**
* `T&&` is a **Universal Reference** 
* For l-values of `int`, T becomes `int&`, param becomes `int&`
* For r-values of `int`, T becomes `int`, param becomes `int&&`

```cpp
template<typename T>
void f(T&& param);

int x = 22;
const int cx = x;
const int& rx = x;

f(x); // T:int&, param: int&
f(cx); // T:const int&, param: const int&
f(rx); // T:const int&, param: const int&
f(22); // 22=> rvalue, T:int, param: int&&
```

## By-Value Parameters
* Gives a completely independent values
* Copies the value to a new one

```cpp
template<typename T>
void f(T param);
...
f(x);
f(cx);
f(rx); // T and param are always int;
```

* `auto` works the same way
* `auto` **never** deduced to be a reference.

```cpp
auto v1 = x;
auto v2 = cx;
auto v3 = rx; // all are int.
auto& v4 = x; // v4: int&
auto& v5 = cx; // v5: const int&
```

