# Effective-Modern-Cpp

A summary of Scott Meyers' classic "Effective Modern C++"

## Objective
The book is awesome and should be read by every C++ developer. I'd like to put a summary here so that every developer can revise it before they go to bed.

If you have a whole week vocation, buy the [book](http://shop.oreilly.com/product/0636920033707.do) and read it thoroughly!

## Summary

## 1. Deducing Types

### Item 1:  Understand template type deduction.
  
  * During  template  type  deduction, arguments that are references are treated as non-references, i.e., their reference-ness is ignored.
  
  * When deducing types for universal reference parameters, lvalue arguments get special treatment.
  
  * When deducing types for by-value parameters, const and/or volatile arguments are treated as non-const and non-volatile.
  
  * During template type deduction, arguments that are array or function names decay to pointers, unless they’re used to initialize references.

### Item 2:  Understand auto type deduction.

  * auto type deduction is usually the same as template type deduction, but auto type deduction assumes that a braced initializer represents a  std::initializer_list, and template type deduction doesn’t.

  * auto in a function return type or a lambda parameter implies template type deduction, not auto type deduction

### Item 3:  Understand decltype.

  * decltype almost always yields the type of a variable or expression without any modifications.

  * For lvalue expressions of type T other than names, decltype always reports a type of T&.

  * C++14 supports decltype(auto), which, like auto, deduces a type from its initializer, but it performs the type deduction using the decltype rules.

### Item 4:  Know how to view deduced types.
  
  * Deduced types can often be seen using IDE editors, compiler error messages, and the Boost TypeIndex library.

  * The results of some tools may be neither helpful nor accurate, so an understanding of C++’s type deduction rules remains essential.

## 2. auto

### Item 5:  Prefer auto to explicit type declarations.

  * auto variables must be initialized, are generally immune to type mismatches that can lead to portability or efficiency problems, can ease the process of refactoring, and typically require less typing than variables with explicitly specified types.

  * auto-typed variables are subject to the pitfalls described in ### Items 2 and 6.

### Item 6:  Use the explicitly typed initializer idiom when auto deduces undesired types.

  * “Invisible” proxy types can cause auto to deduce the “wrong” type for an initializing expression.

  * The explicitly typed initializer idiom forces auto to deduce the type you want it to have.

## 3. Moving to Modern C++

### Item 7:  Distinguish between () and {} when creating objects.

  * Braced initialization is the most widely usable initialization syntax, it prevents narrowing conversions, and it’s immune to C++’s most vexing parse.

  * During constructor overload resolution, braced initializers are matched to std::initializer_list parameters if at all possible, even if other constructors offer seemingly better matches.

  * An example of where the choice between parentheses and braces can make a significant difference is creating a std::vector\<numeric type\> with two arguments.

  * Choosing between parentheses and braces for object creation inside templates can be challenging.

### Item 8: Prefer nullptr to 0 and NULL.

  * Prefer nullptr to 0 and NULL.

  * Avoid overloading on integral and pointer types.

### Item 9:  Prefer alias declarations to typedefs.

  * typedefs don’t support templatization, but alias declarations do.
  
  * Alias templates avoid the “::type” suffix and, in templates, the “typename” prefix often required to refer to typedefs.
  
  * C++14 offers alias templates for all the C++11 type traits transformations
  
### Item 10:  Prefer scoped enums to unscoped enums.

  * C++98-style enums are now known as unscoped enums.

  * Enumerators of scoped enums are visible only within the enum. They convert to other types only with a cast.

  * Both scoped and unscoped enums support specification of the underlying type. The default underlying type for scoped enums is int. Unscoped enums have no default underlying type.

  * Scoped enums may always be forward-declared. Unscoped enums may be forward-declared only if their declaration specifies an underlying type.

### Item 11:  Prefer deleted functions to private undefined ones.

  *  Prefer deleted functions to private undefined ones.
  
  *  Any function may be deleted, including non-member functions and template instantiations.

### Item 12:  Declare overriding functions override.

  *  Declare overriding functions override.

  *  Member function reference qualifiers make it possible to treat lvalue and rvalue objects (*this) differently.
  
### Item 13:  Prefer const_iterators to iterators.

  *  Prefer const_iterators to iterators.

  *  In maximally generic code, prefer non-member versions of begin, end, rbegin, etc., over their member function counterparts.
  
### Item 14:  Declare functions noexcept if they won’t emit exceptions.

  *  noexcept is part of a function’s interface, and that means that callers may depend on it.

  *  noexcept functions are more optimizable than non-noexcept functions.

  *  noexcept is particularly valuable for the move operations, swap, memory deallocation functions, and destructors.

  *  Most functions are exception-neutral rather than noexcept.

### Item 15:  Use constexpr whenever possible.

  *  constexpr objects are const and are initialized with values known during
compilation.

  *  constexpr functions can produce compile-time results when called with arguments whose values are known during compilation.

  *  constexpr objects and functions may be used in a wider range of contexts than non-constexpr objects and functions.

  *  constexpr is part of an object’s or function’s interface.

### Item 16:  Make const member functions thread safe.

  *  Make const member functions thread safe unless you’re certain they’ll never be used in a concurrent context.

  *  Use of std::atomic variables may offer better performance than a mutex, but they’re suited for manipulation of only a single variable or memory location.

### Item 17:  Understand special member function generation.

  *  The special member functions are those compilers may generate on their own: default constructor, destructor, copy operations, and move operations.

  *  Move operations are generated only for classes lacking explicitly declared move operations, copy operations, and a destructor.

  *  The copy constructor is generated only for classes lacking an explicitly declared copy constructor, and it’s deleted if a move operation is declared. The copy assignment operator is generated only for classes lacking an explicitly declared copy assignment operator, and it’s deleted if a move operation is declared. Generation of the copy operations in classes with an explicitly declared destructor is deprecated.

  *  Member function templates never suppress generation of special member functions.
  
## 4. Smart Pointers

### Item 18:  Use std::unique_ptr for exclusive-ownership resource management.

### Item 19:  Use std::shared_ptr for shared-ownership resource management.

### Item 20:  Use std::weak_ptr for std::shared_ptr-like pointers that can dangle.

### Item 21:  Prefer std::make_unique and std::make_shared to direct use of new.

### Item 22:  When using the Pimpl Idiom, define special member functions in the implementation file.

## 5. Rvalue References, Move Semantics, and Perfect Forwarding

### Item 23:  Understand std::move and std::forward.

### Item 24:  Distinguish universal references from rvalue references.

### Item 25:  Use std::move on rvalue references, std::forward on universal references.

### Item 26:  Avoid overloading on universal references.

### Item 27:  Familiarize yourself with alternatives to overloading on universal references.

### Item 28:  Understand reference collapsing.

### Item 29:  Assume that move operations are not present, not cheap, and not used.

### Item 30:  Familiarize yourself with perfect forwarding failure cases.

## 6. Lambda Expressions

### Item 31:  Avoid default capture modes.

### Item 32:  Use init capture to move objects into closures.

### Item 33:  Use decltype on auto&& parameters to std::forward them.

### Item 34:  Prefer lambdas to std::bind.

## 7. The Concurrency API

### Item 35:  Prefer task-based programming to thread-based.

### Item 36:  Specify std::launch::async if asynchronicity is essential.

### Item 37:  Make std::threads unjoinable on all paths.

### Item 38:  Be aware of varying thread handle destructor behavior.

### Item 39:  Consider void futures for one-shot event communication.

### Item 40:  Use std::atomic for concurrency, volatile for special memory.

## 8. Tweaks

### Item 41:  Consider pass by value for copyable parameters that are cheap to move and always copied.

### Item 42:  Consider emplacement instead of insertion.                       


## Disclaimer

I do not own the copyright of the repository and the copyright belongs to Scott Meyers. The repository is only for personal use.
