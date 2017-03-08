# Purpose

This repo is just meant to be able to manage and plan who implements which part
of the high integrity c++ - coding standard in clang-tidy. Would be nice to be
able to reduce duplicate work :)


# Sections overview

Just mention your name on the section you will take care of.


## 0 Introduction

### 0.1 Typographical Conventions
### 0.2 Escalation policy
### 0.3 Base Standard and Policy
### 0.4 Basis of requirements
### 0.5 Rule Enforcement
### 0.6 Deviations
### 0.7 Glossary


## 1 General


### 1.1 Implementation compliance

### 1.2 Redundancy
#### 1.2.1 Ensure that all statements are reachable
#### 1.2.2 Ensure that no expression or sub-expression is redundant 

### 1.3 Deprecated features
#### 1.3.1 Do not use the increment operator (++) on a variable of type bool
- shall be ez

#### 1.3.2 Do not use the register keyword
- should be ez

#### 1.3.3 Do not use the C Standard Library .h headers
- modernize-deprecated-header

#### 1.3.4 Do not use deprecated STL library features
- this would be done with many checkers that can transform as well?

#### 1.3.5 Do not use throw exception specifications
- i saw a check for that in review or sth like that, did not find it right now


## 2 Lexical conventions


### 2.1 Character sets

### 2.2 Trigraph sequences

### 2.3 Comments
#### 2.3.1 Do not use the C comment delimiters /* … */
- preprocessor could do that

#### 2.3.2 Do not comment out code 
- heuristic

### 2.4 Identifiers

### 2.5 Literals
#### 2.5.1 Do not concatenate strings with different encoding prefixes
#### 2.5.2 Do not use octal constants (other than zero)
- should be ez, but unsure for that

#### 2.5.3 Use nullptr for the null pointer constant 
- modernize-use-nullptr


## 3 Basic concepts


### 3.1 Scope

### 3.2 Program and linkage

### 3.3 Storage duration

### 3.4 Object lifetime
#### 3.4.1 Do not return a reference or a pointer to an automatic variable defined within the function
- compiler diagnostic can do this already

#### 3.4.2 Do not assign the address of a variable to a pointer with a greater lifetime
- lifetime analysis? this is CSA area i guess

#### 3.4.3 Use RAII for resources
- this is guideline, many cheks deal with it

### 3.5 Types


## 4 Standard conversions


### 4.1 Array-to-pointer conversion
- cppcoreguidelines-pro-bounds-array-to-pointer-decay

### 4.2 Integral conversions
#### 4.2.1 Ensure that the U suffix is applied to a literal used in a context requiring an unsigned integral expression
#### 4.2.2 Ensure that data loss does not demonstrably occur in an integral expression 

### 4.3 Floating point conversions
- misc-misplaced-widening-cast?

### 4.4 Floating-integral conversions
- misc-misplaced-widening-cast?


## 5 Expressions


### 5.1 Primary expressions

#### 5.1.1 Use symbolic names instead of literal values in code
- code review? is there a way to make some automation on that topic?

#### 5.1.2 Do not rely on the sequence of evaluation within an expression
- order of evaluation, clang diagnostics? UBSan?

#### 5.1.3 Use parentheses in expressions to specify the intent of the expression
#### 5.1.4 Do not capture variables implicitly in a lambda
#### 5.1.5 Include a (possibly empty) parameter list in every lambda expression
#### 5.1.6 Do not code side effects into the right-hand operands of: &&, ||, sizeof, typeid or a function passed to condition_variable::wait 
- start point could be misc-assert-side-effect

### 5.2 Postfix expressions
#### 5.2.1 Ensure that pointer or array access is demonstrably within bounds of a valid object
- cppcoreguidelines-pro-bounds-\*

#### 5.2.2 Ensure that functions do not call themselves, either directly or indirectly
- i dont know, is there a callgraph analysis method?

### 5.3 Unary expressions
#### 5.3.1 Do not apply unary minus to operands of unsigned type
- i think this should be ez

#### 5.3.2 Allocate memory using new and release it using delete
- cppcoreguidelines-no-malloc

#### 5.3.3 Ensure that the form of delete matches the form of new used to allocate the memory 
- static analysis does it already AFAIK

### 5.4 Explicit type conversion
#### 5.4.1 Only use casting forms: static_cast (excl. void*), dynamic_cast or explicit constructor call
- cppcoreguidelines-pro-type-const-cast
- cppcoreguidelines-pro-type-cstyle-cast
- google-explicit-constructor
- google-readability-casting

#### 5.4.2 Do not cast an expression to an enumeration type
#### 5.4.3 Do not convert from a base class to a derived class 

### 5.5 Multiplicative operators

### 5.6 Shift operators

### 5.7 Equality operators
#### 5.7.1 Do not write code that expects floating point calculations to yield exact results
#### 5.7.2 Ensure that a pointer to member that is a virtual function is only compared (==) with nullptr 

### 5.8 Conditional operator


## 6 Statements


### 6.1 Selection statements
#### 6.1.1 Enclose the body of a selection or an iteration statement in a compound statement
- how would that be done?

#### 6.1.2 Explicitly cover all paths through multi-way selection statements
- i think this can be done ez as well, unsure

#### 6.1.3 Ensure that a non-empty case statement block does not fall through to the next label
- should be ez

#### 6.1.4 Ensure that a switch statement has at least two case labels, distinct from the default label 
- should be ez

### 6.2 Iteration statements
#### 6.2.1 Implement a loop that only uses element values as a range-based loop
- modernize-loop-convert

#### 6.2.2 Ensure that a loop has a single loop counter, an optional control variable, and is not degenerate
- hmmm, complicated?

#### 6.2.3 Do not alter a control or counter variable more than once in a loop
- not ez, but visiting the compound stmt could be done, see readability-function-size

#### 6.2.4 Only modify a for loop counter in the for expression 
- should be done ez as well

### 6.3 Jump statements
#### 6.3.1 Ensure that the label(s) for a jump statement or a switch condition appear later, in the same or an enclosing block
- idk, but but that feels like static analysis?

#### 6.3.2 Ensure that execution of a function with a non-void return type ends in a return statement with a value 
- compiler diagnostics!

### 6.4 Declaration statement


## 7 Declarations


### 7.1 Specifiers
#### 7.1.1 Declare each identifier on a separate line in a separate declaration
- there is one already, i did not find it atm

#### 7.1.2 Use const whenever possible
- very valuable to have a checker that will do const correctness with automatic fixing

#### 7.1.3 Do not place type specifiers before non-type specifiers in a declaration

#### 7.1.4 Place CV-qualifiers on the right hand side of the type they apply to
- clang-format area i think

#### 7.1.5 Do not inline large functions
- hm, is this something for readability-function-size

#### 7.1.6 Use class types or typedefs to abstract scalar quantities and standard integer types
- use of uint8 and so on

#### 7.1.7 Use a trailing return type in preference to type disambiguation using typename
- minor check,not so relevant

#### 7.1.8 Use auto id = expr when declaring a variable to have the same type as its initializer function call
- modernize-use-auto

#### 7.1.9 Do not explicitly specify the return type of a lambda
#### 7.1.10 Use static_assert for assertions involving compile time constants 
- misc-static-assert

### 7.2 Enumeration declarations

#### 7.2.1 Use an explicit enumeration base and ensure that it is large enough to store all enumerators
- does the compiler already warn for this?

#### 7.2.2 Initialize none, the first only or all enumerators in an enumeration 
- minor check?

### 7.3 Namespaces
### 7.4 Linkage specifications
#### 7.4.1 Ensure that any objects, functions or types to be used from a single translation unit are defined in an unnamed namespace in the main source file
#### 7.4.2 Ensure that an inline function, a function template, or a type used from multiple translation units is defined in a single header file
#### 7.4.3 Ensure that an object or a function used from multiple translation units is declared in a single header file 

### 7.5 The asm declaration
    - jonathan did it already, in review


## 8 Definitions


### 8.1 Type names

### 8.2 Meaning of declarators
#### 8.2.1 Make parameter names absent or identical in all declarations
    - readability-identifier-naming

#### 8.2.2 Do not declare functions with an excessive number of parameters
    - readability-function-size 

#### 8.2.3 Pass small objects with a trivial copy constructor by value
    - todo

#### 8.2.4 Do not pass std::unique_ptr by const reference 
    - todo


### 8.3 Function definitions
#### 8.3.1 Do not write functions with an excessive McCabe Cyclomatic Complexity
    - readability-function-size

#### 8.3.2 Do not write functions with a high static program path count
    - readability-function-size

#### 8.3.3 Do not use default arguments
    - todo
    - google-default-arguments as a starting point
    
#### 8.3.4 Define =delete functions with parameters of type rvalue reference to const 
    - todo

### 8.4 Initializers
#### 8.4.1 Do not access an invalid object or an object with indeterminate value
    - todo?
    - warning for uninitialized variables should the compiler do
    - access freed memory is CSA, and maybe impossible to determine statically?
    - misc-use-after-move

#### 8.4.2 Ensure that a braced aggregate initializer matches the layout of the aggregate object 
    - todo


## 9 Classes


### 9.1 Member functions
#### 9.1.1 Declare static any member function that does not require this.  Alternatively, declare const any member function that does not modify the externally visible state of the object
    - todo
    - especially the const part is a general issue (automatically mark methods
      const if possible), i think this check is especially valuable

#### 9.1.2 Make default arguments the same or absent when overriding a virtual function
    - i thought dont use default arguments? :D
    - google-default-arguments, not
    - to implement

#### 9.1.3 Do not return non-const handles to class data from const member functions
    - to implement, EZ? and very valuable belonging safety

#### 9.1.4 Do not write member functions which return non-const handles to data less accessible than the member function
    - feels like general version of 9.1.3, should be implemented in the same
      check

#### 9.1.5 Do not introduce virtual functions in a final class 
    - todo

### 9.2 Bit-fields
    - todo


## 10 Derived classes


### 10.1 Multiple base classes
    - todo
    - check for necessaity of a virtual base class

### 10.2 Virtual functions
    - modernize-use-override

### 10.3 Abstract classes
    - todo
    - check inheritence properties

## 11 Member access control


### 11.1 Access specifiers
    - todo
    - EZ, just check for class, and warn for all data members and warn for
      nonprivate ones
    - execption are extern "C" { struct }

### 11.2 Friends
    - todo
    - EZ warn for friends


## 12 Special member functions


### 12.1 Conversions
    - google-explicit-constructor
    - maybe modification, but doesnt seem like it

### 12.2 Destructors
    - todo

### 12.3 Free store
    - misc-new-delete-overloads

### 12.4 Initializing bases and members
#### 12.4.1 Do not use the dynamic type of an object unless the object is fully constructed
    - todo
    - maybe something for undefinedbehavioursanitizer?

#### 12.4.2 Ensure that a constructor initializes explicitly all base classes and non-static data members
    - todo for the baseclasses?
    - cppcoreguidelines-pro-type-member-init

#### 12.4.3 Do not specify both an NSDMI and a member initializer in a constructor for the same non static member
    - todo

#### 12.4.4 Write members in an initialization list in the order in which they are declared
    - i though there is an check for that, cannot find it!
    - maybe todo

#### 12.4.5 Use delegating constructors to reduce code duplication 
    - misc-undelegated-constructor

### 12.5 Copying and moving class objects

#### 12.5.1 Define explicitly =default or =delete implicit special member functions of concrete classes
    - modernize-use-equals-default
    - modernize-use-equals-delete

#### 12.5.2 Define special members =default if the behavior is equivalent
    - handled by the check for 12.5.1

#### 12.5.3 Ensure that a user defined move/copy constructor only moves/copies base and member objects
    - todo

#### 12.5.4 Declare noexcept the move constructor and move assignment operator
    - misc-noexcept-move-constructor

#### 12.5.5 Correctly reset moved-from handles to resources in the move constructor
    - todo?

#### 12.5.6 Use an atomic, non-throwing swap operation to implement the copy and move assignment operators
    - todo

#### 12.5.7 Declare assignment operators with the ref-qualifier &
    - cppcoreguidelines-special-member-functions

#### 12.5.8 Make the copy assignment operator of an abstract class protected or define it =delete 
    - todo


## 13 Overloading


### 13.1 Overload resolution
#### 13.1.1 Ensure that all overloads of a function are visible from where it is called
#### 13.1.2 If a member of a set of callable functions includes a universal reference parameter, ensure that one appears in the same position for all other members 

### 13.2 Overloaded operators
#### 13.2.1 Do not overload operators with special semantics
#### 13.2.2 Ensure that the return type of an overloaded binary operator matches the built-in counterparts
- that should be a lot to do, but rather mechanical

#### 13.2.3 Declare binary arithmetic and bitwise operators as non-members
- operator overload knows if its in a class or nonmember in clang?

#### 13.2.4 When overloading the subscript operator (operator[]) implement both const and non-const versions
- i think its ez

#### 13.2.5 Implement a minimal set of operators and use them to implement all other related operators
- heuritic, but i think codereview is necessary


## 14 Templates

template stuff scares me :)

### 14.1 Template declarations

### 14.2 Template instantiation and specialization
####  14.2.1 Declare template specializations in the same file as the primary template they specialize
####  14.2.2 Do not explicitly specialize a function template that is overloaded with other templates
####  14.2.3 Declare extern an explicitly instantiated template 


## 15 Exception handling


#### 15.1.1 Only use instances of std::exception for exceptions
- this is ez, i want to :)

#### 15.2.1 Do not throw an exception from a destructor
- implemented right now, will go into code review

### 15.3 Handling an exception
####  15.3.1 Do not access non-static members from a catch handler of constructor/destructor function try block
- traversing all statements and find out all member acesses

####  15.3.2 Ensure that a program does not result in a call to std::terminate 
- static analysis?


## 16 Preprocessing


### 16.1 Source file inclusion
####  16.1.1 Use the preprocessor only for implementing include guards, and including header files with include guards
- there is something in review or commited already
- refactoring needs that as well, replace MACRO with inline function for example

####  16.1.2 Do not include a path specifier in filenames supplied in #include directives
####  16.1.3 Match the filename in a #include directive to the one on the filesystem
- could be done?

####  16.1.4 Use <> brackets for system and standard library headers. Use quotes for all other headers
- easy or not? system will contain windows headers as well?

####  16.1.5 Include directly the minimum number of headers required for compilation 
- modularize?


## 17 Standard library


### 17.1 General
    - dont use std::vector<bool> is in code review, by jonathan

### 17.2 The C standard library

### 17.3 General utilities library
####  17.3.1 Do not use std::move on objects declared with const or const & type
- misc-move-const-arg

####  17.3.2 Use std::forward to forward universal references
- can be done?

####  17.3.3 Do not subsequently use the argument to std::forward
- use after move is almost the same

####  17.3.4 Do not create smart pointers of array type
####  17.3.5 Do not create an rvalue reference of std::array 
- should be done?

### 17.4 Containers library
####  17.4.1 Use const container calls when result is immediately converted to a const iterator
- interesting

####  17.4.2 Use API calls that construct objects in place 
- modernize-use-emplace

### 17.5 Algorithms Library


## 18 Concurrency


### 18.1 General

### 18.2 Threads
####  18.2.1 Use high_integrity::thread in place of std::thread
- check all decl if its a std::thread?

####  18.2.2 Synchronize access to data shared between threads using a single lock
- static analysis

####  18.2.3 Do not share volatile data between threads
- forbid volatile in general? :D

####  18.2.4 Use std::call_once rather than the Double-Checked Locking pattern 

### 18.3 Mutual Exclusion
####  18.3.1 Within the scope of a lock, ensure that no static path results in a lock of the same mutex
- static analysis

####  18.3.2 Ensure that order of nesting of locks in a project forms a DAG
- static analysis possible?

####  18.3.3 Do not use std::recursive_mutex
- ez

####  18.3.4 Only use std::unique_lock when std::lock_guard cannot be used
- maybe one step can be std::lock_guard could be warned always

####  18.3.5 Do not access the members of std::mutex directly
- ez?

####  18.3.6 Do not use relaxed atomics 

### 18.4 Condition Variables

