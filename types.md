# Types
## int
Signed integer, size depends on platform
Not safe for portability

* Initialize all the variables
* Use `<cstdint>` for fixed sizes
* Use sizeof(int) to find out the size of a scalar type.
	`size_t a = sizeof(int);`
* Use int32_t (32 bit type), uint64_t(unsigned 64 bit type)

## float
`float a = 2.f`
different platforms have different sizes

## bool
true false
numeric values are converted automatically to bools when needed.
0 = false, other = true

