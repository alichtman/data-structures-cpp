**Encapsulation**

Interface in the .h file.
Implementation in the .cpp file.

Remember include guards in the .h file!
```cpp
#ifndef NAME_H
#define NAME_H

#endif
```

**Memory Management**

Stack grows downward, starting at highest going to lowest. Read up the stack from lowest to highest memory address.
Heap grows up. Allocated with `new` keyword. Never automatically reclaimed.

For each `new` call, there should be a `delete` call. Remember to set variable to `NULL` after deleting.

Special case for deleting arrays: `delete [] arr;`

**Pointers**

A pointer variable holds a memory address.

Size of a pointer is 8 bytes.

Warning: `int* ptr, notPtr` creates one `int*` and one `int`

```cpp
int val = 5;
int* ptr = &val; // ptr points to val
```

**Reference Variables**

`&` operator.
Variable that refers to memory of existing variable. Only way to name memory on heap.
Never creates its own memory.

**Overloading Operators**

`bool Class::operator<(const Class &var);`

**Constructors**

Automatic Default Constructor -- Provided if no other copy constructors defined. "Soft" copy of all variables (copies memory addresses, not value).

Copy Constructor -- Returns deep copy of object

```cpp
Sphere(const Sphere& a) {
	memberVar_ = a.memberVar_;
}
```

Assignment Operator (=) called when assigning new value to existing object. Needs a self-destruct check.
Copy Constructor called when creating new object from existing object.

**Rule of Three**

If any of these three are needed, all three must be defined.

1. Copy Constructor
2. Destructor
3. Assignment operator `(=)`

**Passing Parameters**

1. Pass by Value -- `func(Sphere a)`
	+ Slow, makes a new copy of the entire object.
	+ Does not modify original.
	+ Always valid object passed in.
2. Pass by Pointer -- `func(Sphere* a)`
	+ Faster than PbV, only copies the memory address.
	+ Modifies original.
	+ NULL pointer potentially passed in.
3. Pass by Reference -- `func(Sphere& a)`
	+ Fastest, no copying at all.
	+ Allows direct manipulation of data.
	+ Always valid object passed in.

**Const**

1. Function parameters -- `int func(const Sphere a)`
	+ Guarantees value passed in will not be changed.

2. Class function declarations -- `int func(Sphere a) const;`
	+ Guaranteed not to modify the state of the class.


**Inheritance**

`class Derived: public Base {}`

1. If you need a custom constructor to construct Base object, Initializer List required to construct Derived class.
2. Derived inherits public functions of Base directly, and protected data indirectly (may have to use getters). (?)

+ Constructors called from Base to Derived.
+ Destructors called from Derived to Base.

+ `virtual` keyword allows derived classes to override function behavior.
+ `virtual Class::func() = 0` is pure virtual. Requires derived class to implement function.

+ Constructors can not be virtual.
+ Destructor in Base *should* be virtual.

**Templates**

+ Allow functions and classes to operate with generic class types
+ Checked at compile time

**Iterators**

+ Allow us to traverse data regardless of underlying structure.
+ Declared in `public` block of class.

**Functors**

+ Objects that can be called like a function.
+ If it has an overloaded `()` operator, likely a functor.
+ Functors can track state (?)
