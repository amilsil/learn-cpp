# Pointers
A pointer,
* has an address of a variable
* `float *n` -> pointer to a float
* no default
* initialize `float *n = &u`
* `float *s = nullptr`
* get the value by `float f = *n` -> *pointer dereferencing*.
* pointers can reference to pointers `float **s`

**Advice**
* use * at the variable name


# References 
Like a C# reference
* Works on `value types`
* Initialization uses & `int &x = y` -> changing x changes y
* No concept of a `null` reference.
* Can have reference-to-reference.
* Reference from pointer
`
  int *n;
  int &m = *n; refers to the pointer.
`
* pointer to ref is illegal

**Advice**
* use references as function parameters
~~~~
function assign_n(int &n) 
{
	n = 100;
}
~~~~

# Arrays
C-style array is a pointer to the first element

`int numbers[] { 1, 2, 3 };`

* `*numbers` gives the first element
* cannot tell from the array how long it is
* 0-based, multi-dimension support

initialize an array of 10 with first being zero.
`int zeros[10] { 0 };` 

modern array 
## std::array 
* wrapper for an array of known size
* `array<int, 3> values {1, 2, 3}`
* `values.size()` gives the length

## std::vector
When you need to change the size.

# Character Types
## char
* 1 byte
* `char c = 'z'`

## wchar_t
* width is compiler spec

## Alternatives
char16_t
char32_t

Use w variants for unicode support
`wstring`

# Strings
c-style strings are arrays of chars

`char *text = "hello";` 

advice use std::string
