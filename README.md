# Lynn's C++ notes
_Work in progress — might `#include <mistakes>`._

## Essentials

### [Value Categories](https://en.cppreference.com/w/cpp/language/value_category.html) <sub>_All categories are valuable._</sub>
|                  		      | glvalue <br>(identity) | <br>(identityless) |
|--------------------------|------------------------|--------------------|
| **rvalue <br>(movable)** | `xvalue` 				          | `prvalue` 	        |
| **(immovable)** 		       | `lvalue` 				          |                 	  |

`glvalue (generalised lvalue)`: values with an _identity_, encapsulating `lvalues` and `xvalues`.
<br>`rvalue (right value)`: values that can be moved, encapsulating `xvalues` and `prvalues`.
<br>`lvalue (right value)`: values that cannot be moved.
<br>`xvalue (eXpiring value)`: the result of applying `std::move` to an `lvalue`.
<br>`prvalue (pure rvalue)`: values without an _identity_.

> Values have an **_identity_** if they have an accessible address.
> <br>This includes variables, the dereferenced `this` pointer, string literals, etc.
> <br>Values without identity (`prvalues`) include literals, the `this` pointer, temporary objects (often as the result of an expression), etc.
> <br>Such values seize to exist if they are not defined.

> **_Moving_** a variable refers to reusing its resources to construct/assign another object.
> <br>For example, ownership of data pointers is transferred, instead of making a copy of the data.
> <br>Continue reading about move semantics [here](#move-semantics).

### [Move Semantics](https://en.cppreference.com/w/cpp/utility/move.html) <sub>_Now for my next move..._</sub>

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
