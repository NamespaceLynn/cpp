# Lynn's C++ notes
_Work in progress — might `#include <mistakes>`._

## Essentials

### [Value Categories](https://en.cppreference.com/w/cpp/language/value_category.html) <sub>_All categories have value._</sub>
|                  		      | glvalue <br>(identity) | <br>(identityless) |
|--------------------------|------------------------|--------------------|
| **rvalue <br>(movable)** | `xvalue` 				          | `prvalue` 	        |
| **(immovable)** 		       | `lvalue` 				          |                 	  |

`glvalue`: (generalised lvalue) values with an _identity_, encapsulating `lvalues` and `xvalues`.
<br>`rvalue`: (right value) values that can be moved, encapsulating `xvalues` and `prvalues`.
<br>`lvalue`: (right value) values that cannot be moved.
<br>`xvalue`: (eXpiring value) the result of applying `std::move` to an `lvalue`.
<br>`prvalue`: (pure rvalue) values without an _identity_.

> Values have an **_identity_** if they have an accessible address.
> <br>This includes variables, the dereferenced `this` pointer, string literals, etc.
> <br>Values without identity (`prvalues`) include literals, the `this` pointer, temporary objects (often as the result of an expression), etc.
> <br>Such values seize to exist if they are not defined.

> **_Moving_** a variable refers to reusing its resources to construct/assign another object.
> <br>For example, ownership of data pointers is transferred, instead of making a copy of the data.
> <br>Continue reading about move semantics [here](#move-semantics).

### [Move Semantics](https://en.cppreference.com/w/cpp/utility/move.html) <sub>_Now for my next move..._</sub>

`std::move`: converts `lvalues` to `xvalues`.
- TODO
- A copy constructor/assignment operator can take in an `rvalue` if no move constructor/assignment operator is defined. Some STL classes will only use moves if they are marked `noexcept`, and will otherwise prefer to (presumed to be safer) copy operation.
```cpp
struct A
{
    A() : size{ 100 }, data{ new char[size] } {}
    ~A() { delete[] data; }

    // Copy constructor
    // Takes in an lvalue
    A( const A& other )
    {
        size = other.size;
        data = new char[size];
        std::memcpy( data, other.data, size );
    }
    // Move constructor
    // Takes in an rvalue (xvalue and prvalue)
    A( A&& other )
    {
        size = other.size;
        data = other.data;
        other.data = nullptr;
        other.size = 0;
    }

    std::size_t size{ 0 };
    char* data{ nullptr };
};

int main()
{
    A temp{} // Assume we have an object we don't need anymore
    A a1{ temp_a }; // This makes a copy of its resources4
    A a2{ std::move( temp_a ) }; // This reuses the resources
}

``` 
`std::forward`: preserves the value category of a `forwarding reference`.
<br>`Forwarding References`: a parameter preserving value category in tandem with `std::forward`.
- Also known as universal references.
- Used for templated functions, when you want to take in any value category.
- Turns into an `lvalue` when referenced, except if `std::forward` is used.
```cpp
template <typename T>
void fn( T&& forwarding_ref )
{
    // 'forwarding_ref' keeps the value category passed to 'fn'
    other_fn( std::forward<T>( forwarding_ref ) );
    
    // 'forwarding_ref' is passed as an lvalue
    other_fn( forwarding_ref );
}

// Alternatively (since C++20)
void fn( auto&& forwarding_ref )
{
    using T = decltype( forwarding_ref );
    other_fn( std::forward<T>( forwarding_ref ) );
}
```

### Function (Pointers)
_At this point I'm barely functioning..._

### Inheritance
_Base(d).

### Casts
_You C-ing my style?_

</details>

## bool operator<( Essential )
_Less than essential._

### Exception handling

### Decltype

### New & Delete

### Templates

## C++ Standard Library

## C++(++)
 _(beyond C++)_

### Compilation

### Computer Architecture
