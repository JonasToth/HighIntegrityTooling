#### 1.2.1 Ensure that all statements are reachable
- clang-static analyzer - dead-store
- i think there is no dead code check but i felt like there was one

#### 1.2.2 Ensure that no expression or sub-expression is redundant
- todo
- i dont think what how that could be done in one check, maybe this is something alot places will warn for?

#### 1.3.4 Do not use deprecated STL library features
- this would be done with many checkers that can transform as well?

### 2.2 Trigraph sequences

#### 2.3.1 Do not use the C comment delimiters /* … */
- preprocessor could do that
- todo

#### 2.3.2 Do not comment out code 
- heuristic?
- todo, i thinnk cppcheck has something on it

#### 2.4.1 Ensure that each identifier is distinct from any other visible identifier
- todo
- i saw a similar check once in codereview, but i might be wrong
- heuristic and maybe high false positive rate

#### 2.5.1 Do not concatenate strings with different encoding prefixes
- todo?

#### 2.5.2 Do not use octal constants (other than zero)
- should be ez, but unsure for that
- todo

#### 3.4.2 Do not assign the address of a variable to a pointer with a greater lifetime
- lifetime analysis? this is CSA area i guess

#### 3.4.3 Use RAII for resources
- this is guideline, many cheks deal with it

#### 3.5.1 Do not make any assumptions about the internal representation of a value or object
- todo
- check for unions
- check for bad pointer arithmetic? -> pro-bounds in cppcoreguidelines

### 4.2 Integral conversions
#### 4.2.1 Ensure that the U suffix is applied to a literal used in a context requiring an unsigned integral expression
- todo

#### 5.1.1 Use symbolic names instead of literal values in code
- code review? is there a way to make some automation on that topic?

#### 5.1.2 Do not rely on the sequence of evaluation within an expression
- order of evaluation, clang diagnostics? UBSan?

#### 5.1.3 Use parentheses in expressions to specify the intent of the expression
- todo

#### 5.1.4 Do not capture variables implicitly in a lambda
- todo

#### 5.1.5 Include a (possibly empty) parameter list in every lambda expression
- todo - clang-format?

#### 5.1.6 Do not code side effects into the right-hand operands of: &&, ||, sizeof, typeid or a function passed to condition_variable::wait 
- start point could be misc-assert-side-effect

#### 5.2.2 Ensure that functions do not call themselves, either directly or indirectly
- i dont know, is there a callgraph analysis method?
- so recursion is forbidden?

#### 5.3.1 Do not apply unary minus to operands of unsigned type
- i think this should be ez

#### 5.4.2 Do not cast an expression to an enumeration type
- todo but is it necessary? casting is bad anyway and enforced already

#### 5.4.3 Do not convert from a base class to a derived class
- todo but maybe already covered by cast checker

#### 5.7.2 Ensure that a pointer to member that is a virtual function is only compared (==) with nullptr 
- todo

#### 5.8.1 Do not use the conditional operator (?:) as a sub-expression
- todo

#### 6.1.3 Ensure that a non-empty case statement block does not fall through to the next label
- -Wimplicit-fallthrough
- warnings seems buggy, investigate

#### 6.2.2 Ensure that a loop has a single loop counter, an optional control variable, and is not degenerate
- hmmm, complicated?
- todo

#### 6.2.3 Do not alter a control or counter variable more than once in a loop
- not ez, but visiting the compound stmt could be done, see readability-function-size
- todo

#### 6.2.4 Only modify a for loop counter in the for expression 
- should be done ez as well
- todo

#### 6.3.1 Ensure that the label(s) for a jump statement or a switch condition appear later, in the same or an enclosing block
- cppcoreguidelines-avoid-goto requires forward jumps for gotos
- switch stuff not implemented

#### 6.4.1 Postpone variable definitions as long as possible
- todo

#### 7.1.1 Declare each identifier on a separate line in a separate declaration
- there is one already, i did not find it atm
- todo

#### 7.1.2 Use const whenever possible
- very valuable to have a checker that will do const correctness with automatic fixing
- readability-non-const-parameter only for function arguments

#### 7.1.3 Do not place type specifiers before non-type specifiers in a declaration
- todo

#### 7.1.4 Place CV-qualifiers on the right hand side of the type they apply to
- clang-format area i think
- todo

#### 7.1.5 Do not inline large functions
- hm, is this something for readability-function-size?
- todo

#### 7.1.6 Use class types or typedefs to abstract scalar quantities and standard integer types
- use of uint8 and so on
- todo

#### 7.1.7 Use a trailing return type in preference to type disambiguation using typename
- minor check,not so relevant
- todo

#### 7.1.9 Do not explicitly specify the return type of a lambda
- todo

#### 7.2.1 Use an explicit enumeration base and ensure that it is large enough to store all enumerators
- does the compiler already warn for this?
- todo

#### 7.2.2 Initialize none, the first only or all enumerators in an enumeration 
- minor check?
- todo

#### 7.3.1 Do not use using directives
- todo, ez

### 7.4 Linkage specifications
- maybe clang-modularize deals with it?

#### 7.4.1 Ensure that any objects, functions or types to be used from a single translation unit are defined in an unnamed namespace in the main source file
- todo?

#### 7.4.2 Ensure that an inline function, a function template, or a type used from multiple translation units is defined in a single header file
- todo?

#### 7.4.3 Ensure that an object or a function used from multiple translation units is declared in a single header file 
- todo?

#### 8.1.1 Do not use multiple levels of pointer indirection
- todo, type checking on declarations

#### 8.2.3 Pass small objects with a trivial copy constructor by value
- todo

#### 8.2.4 Do not pass std::unique_ptr by const reference 
- todo, type checking in functionDecl arguments

#### 8.3.3 Do not use default arguments
- todo
- google-default-arguments as a starting point
    
#### 8.3.4 Define =delete functions with parameters of type rvalue reference to const 
- todo

#### 8.4.1 Do not access an invalid object or an object with indeterminate value
-  todo?
- warning for uninitialized variables should the compiler do
- access freed memory is CSA, and maybe impossible to determine statically?
- misc-use-after-move

#### 8.4.2 Ensure that a braced aggregate initializer matches the layout of the aggregate object 
- todo

#### 9.1.1 Declare static any member function that does not require this.  Alternatively, declare const any member function that does not modify the externally visible state of the object
- todo
- especially the const part is a general issue (automatically mark methods
  const if possible), i think this check is especially valuable

#### 9.1.2 Make default arguments the same or absent when overriding a virtual function
- todo

#### 9.1.3 Do not return non-const handles to class data from const member functions
- todo, EZ? and very valuable belonging safety

#### 9.1.4 Do not write member functions which return non-const handles to data less accessible than the member function
- feels like general version of 9.1.3, should be implemented in the same
  check
- todo

#### 9.1.5 Do not introduce virtual functions in a final class 

- -Wabstract-final-class for new abstract virtual methods in a final class
- todo: warn for newly introduced and implemented methods

### 9.2 Bit-fields
- todo

#### 10.1.1 Ensure that access to base class subobjects does not require explicit disambiguation
- todo
- check for necessaity of a virtual base class

#### 10.3.1 Ensure that a derived class has at most one base class which is not an interface class
- todo
- check inheritence properties

#### 11.1.1 Declare all data members private
- todo
- EZ, just check for class, and warn for all data public data members 
- execption are extern "C" { struct }

#### 11.2.1 Do not use friend declarations
- todo
- EZ warn for friends

### 12.1 Conversions
- google-explicit-constructor
- maybe modification, but doesnt seem like it

### 12.2 Destructors
- todo

#### 12.4.1 Do not use the dynamic type of an object unless the object is fully constructed
- todo
- maybe something for undefinedbehavioursanitizer?

#### 12.4.3 Do not specify both an NSDMI and a member initializer in a constructor for the same non static member
- todo

#### 12.5.3 Ensure that a user defined move/copy constructor only moves/copies base and member objects
- todo

#### 12.5.5 Correctly reset moved-from handles to resources in the move constructor
- todo?

#### 12.5.6 Use an atomic, non-throwing swap operation to implement the copy and move assignment operators
- todo

#### 12.5.8 Make the copy assignment operator of an abstract class protected or define it =delete 
- todo

#### 13.1.1 Ensure that all overloads of a function are visible from where it is called
- todo

#### 13.1.2 If a member of a set of callable functions includes a universal reference parameter, ensure that one appears in the same position for all other members 
- todo

#### 13.2.1 Do not overload operators with special semantics
- todo, probably not possible without human understanding

#### 13.2.2 Ensure that the return type of an overloaded binary operator matches the built-in counterparts
- todo
- that should be a lot to do, but rather mechanical
- Expression Templates will be very noisy
- Maybe do logical operators as default
- Configurable if Arithmetic operators should be considered as well

#### 13.2.3 Declare binary arithmetic and bitwise operators as non-members
- todo
- operator overload knows if its in a class or nonmember in clang?

#### 13.2.4 When overloading the subscript operator (operator[]) implement both const and non-const versions
- todo
- i think its ez

#### 13.2.5 Implement a minimal set of operators and use them to implement all other related operators
- todo
- heuristic, but i think codereview is necessary

####  14.2.1 Declare template specializations in the same file as the primary template they specialize
- todo

####  14.2.2 Do not explicitly specialize a function template that is overloaded with other templates
- todo

####  14.2.3 Declare extern an explicitly instantiated template 
- todo
- extern templates? Wasn't this a big fail or is something else meant with this?

#### 15.2.1 Do not throw an exception from a destructor
- front end will implement/has implemented, very important

####  15.3.1 Do not access non-static members from a catch handler of constructor/destructor function try block
- todo
- traversing all statements and find out all member acesses

####  15.3.2 Ensure that a program does not result in a call to std::terminate 
- todo
- static analysis?
- terminate: unhandled exception, maybe exception from destructor, exception from `noexcept`-function, stuff with the allocation functions as well

####  16.1.1 Use the preprocessor only for implementing include guards, and including header files with include guards
- todo
- there is something in review or commited already
- refactoring needs that as well, replace MACRO with inline function for example

####  16.1.2 Do not include a path specifier in filenames supplied in #include directives
- todo

####  16.1.3 Match the filename in a #include directive to the one on the filesystem
- todo
- could be done?

####  16.1.4 Use <> brackets for system and standard library headers. Use quotes for all other headers
- todo
- easy or not? system will contain windows headers as well?

####  16.1.5 Include directly the minimum number of headers required for compilation 
- todo
- modularize?
- new possible clang tool: IWYU, Include what you use already exists, google it

#### 17.1.1 Do not use std::vector\<bool>
- in code review, by jonathan

#### 17.2.1 Wrap use of the C Standard Library
- todo

####  17.3.2 Use std::forward to forward universal references
- todo
- get all calls of std::forward on values, not being a universal reference

####  17.3.3 Do not subsequently use the argument to std::forward
- use after move is almost the same, maybe patch there

####  17.3.4 Do not create smart pointers of array type
- todo
- std::make_unique<T[]> works in newer standards

####  17.3.5 Do not create an rvalue reference of std::array 
- todo
- should be done?

####  17.4.1 Use const container calls when result is immediately converted to a const iterator
- interesting

#### 17.5.1 Do not ignore the result of std::remove, std::remove_if or std::unique
- todo
- ez?

#### 18.1.1 Do not use platform specific multi-threading facilities
- todo
- modernize old thread stuff?

####  18.2.1 Use high_integrity::thread in place of std::thread
- todo
- check all decl if its a std::thread?

####  18.2.2 Synchronize access to data shared between threads using a single lock
- todo
- static analyzer

####  18.2.3 Do not share volatile data between threads
- todo

####  18.2.4 Use std::call_once rather than the Double-Checked Locking pattern 
- todo

####  18.3.1 Within the scope of a lock, ensure that no static path results in a lock of the same mutex
- todo
- static analyzer

####  18.3.2 Ensure that order of nesting of locks in a project forms a DAG
- todo
- static analyzer

####  18.3.3 Do not use std::recursive_mutex
- todo
- ez

####  18.3.4 Only use std::unique_lock when std::lock_guard cannot be used
- todo
- maybe one step can be std::unique_lock could be warned always

####  18.3.5 Do not access the members of std::mutex directly
- todo
- ez

####  18.3.6 Do not use relaxed atomics 
- todo
- ez?

#### 18.4.1 Do not use std::condition_variable_any on a std::mutex
- todo
