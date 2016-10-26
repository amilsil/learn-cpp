# uniform initializations
```
int n { 4 };
string s { "foo" };
vector<int> values {1,2,3};
map<string, string> capitals {
    { "UK"< "London" }
};
Person p { "Dimitri", 23 };
```
## Use initializer_lists for custom initializations
```
struct Exchange 
{
    int rate;
    int values [2];
}

Exchange e { 
    1 // rate ,
    2,3 // values 
};
```
**Solve this by**
```
struct Exchange 
{
    public Exchange(initializer_list<int> args)
    {
        // assign the args any way we want.
    }
}
```

# Auto
```
auto a = 0; //int
auto b = {1,2,3}; // initializer_list

auto meaning_of_life() -> int 
{
    return 42;
}
```

# override/final
```
class Animal
{
    Animal(int legs) {}
    int Walk(int steps) {} // final: make it not overridable
}

class Human : Animal
{
    Human() : Animal(2) {}
    int Walk(int steps) override {} //overrides the walk method.
}
```

# Copy Constructor
```
Human h;
Human h2 { h }; // Call the copy constructor
```

## can remove the copy Constructor by deleting it 
```
class Human 
{
    Human(const Human&) = delete; // delete the copy constructor
}
```

# Lambdas
`[](int n) -> float { /* body */ }`

**for_each can now be used with lambdas**
```
vector<int> scores { 4, 5, 2, 6 };
for_each(begin(scores), end(scores), [](int n)->{
    cout << n << endl;
})
```

**container scope values can be shared with**
```
int x = 10;
auto a = [=](){ cout << x}; // share values 
auto b = [&](){ cout << x}; // share as references
auto c = [=x](){ cout << x }; // share only x
```

in recursion, lambda must be typed instead of `auto`
```
function<int(int)> fac = [&fac](int x) {
    return x < 1? 1: x * fac(x-1);
}
```

# Enum
```enum OldColor 
{
    Red, Green, Blue
}
OldColor c = Green; // ugly
int x = c;
```

**new way**
```
enum class NewColor 
{
    Red, Green
}
NewColor c = NewColor::Red;
```

# Range Based for

for a vector
```
for(auto& a : {1,2,3,4})
{
    cout << a;
}
```

for a map
```
map<string, int> histogram;
for(const auto& kvp: histogram)
{
    cout << kvp.first << ":" << kvp.second;
}
```
# Static Assert 
Is used to assert things at the compile time

```
template<typename T, size_t Size>
class Values 
{
    static_assert(Size > 1, "Use a Scalar gt 1");
    T values[Size];
}

int main() 
{
    Values<int, 1> stuff; // assert error at runtime. 
    return 0;
}
```
* Check if integral
`static_assert(is_integral<T>::value, "Must be integral")`

# Variadic

* Allow any number of type elements
* `typename...` means variadic 
* `T...` means multiple of a type
```
auto sum() { return 0; } // terminater

template<typename H, typename... T>
auto sum(H h, T... t)  
{
    return h + sum(t...);
    // Calls the sum recursively.
    // Until the sum() is called.
}
cout << sum(1, 3.4, 88, 9.3) << endl;
```

## functions returning pairs of values
```
auto sum_product(double a, double b)
{
    return make_pair(a+b, a*b);
}
```
* calling this the old way
```
auto values = sum_product(3,4); // returns a pair
auto sum = get<0>(values); // get the sum
```
* calling new way using `tie(...)`
```
tie(sum, ignore) = sum_product(3,4);
```

# Smart Pointers
old way is **pointers**
```
class Person 
{
    Address *address;
    ~Person(){
        if(address) delete address; 
    }
}
```

new way is **smart pointers**
* No memory-freeing needed.
* Use **pointer de-reference** to access instance members.
* Doesn't live longer than the host
```
class Person 
{
    public:
    unique_ptr<Address> address;
    Person() 
    {
        address = make_unique<Address>();
        cout << address->line1; 
    }
}
```

* **shared pointers** can live longer.
* `make_shared<Address>`

# r-value reference
```
string getName() { return "Amil"; } // returns a **temporary** value
string name1 = getName(); // works
string& name2 = getName(); // error, cannot do this
const string& name3 = getName(); // works, cannot change it though
```
* cannot access a returned values **by-reference**
* accessing by r-value
```
string&& name4 = getName(); // works, by r-value reference.
name4 = "Jack"; // works
```