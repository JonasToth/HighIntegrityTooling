#### 1.1.1 Ensure that code complies with the 2011 ISO C++ Language Standard
- use --std=c++11 or higher as compiler flag

#### 1.2.1 Ensure that all statements are reachable
- clang-static analyzer - dead-store
- i think there is no dead code check but i felt like there was one

#### 1.3.1 Do not use the increment operator (++) on a variable of type bool
- -Wdeprecated-increment-bool

#### 1.3.2 Do not use the register keyword
- -Wdeprecated-register

#### 1.3.3 Do not use the C Standard Library .h headers
- modernize-deprecated-header

#### 1.3.5 Do not use throw exception specifications
- modernize-use-noexcept

#### 2.1.1 Do not use tab characters in source files
- clang-format

#### 2.2.1 Do not use digraphs or trigraphs
- there is something?
- clang-format?!

#### 2.5.3 Use nullptr for the null pointer constant 
- modernize-use-nullptr

#### 3.2.1 Do not declare functions at block scope
- -Wvexing-parse

#### 3.4.1 Do not return a reference or a pointer to an automatic variable defined within the function
- -Wreturn-stack-address
- clang-analyzer-core.StackAddressEscape

#### 4.1.1 Ensure that a function argument does not undergo an array-to-pointer conversion
- cppcoreguidelines-pro-bounds-array-to-pointer-decay

#### 5.2.1 Ensure that pointer or array access is demonstrably within bounds of a valid object
- cppcoreguidelines-pro-bounds-\*

#### 5.3.2 Allocate memory using new and release it using delete
- cppcoreguidelines-no-malloc
- hicpp-no-malloc

#### 5.3.3 Ensure that the form of delete matches the form of new used to allocate the memory 
- clang-analyzer-cplusplus.NewDelete

#### 5.4.1 Only use casting forms: static_cast (excl. void*), dynamic_cast or explicit constructor call
- cppcoreguidelines-pro-type-const-cast
- cppcoreguidelines-pro-type-cstyle-cast
- google-explicit-constructor
- google-readability-casting

#### 5.5.1 Ensure that the right hand operand of the division or remainder operators is demonstrably non-zero
- clang-analyzer-core.DivideZero

#### 5.6.1 Do not use bitwise operators with signed operands
- hicpp-signed-bitwise

#### 6.1.1 Enclose the body of a selection or an iteration statement in a compound statement
- readability-braces-around-statements
- hicpp-braces-around-statements

#### 6.1.2 Explicitly cover all paths through multi-way selection statements
- -Wswitch
- hicpp-multiway-paths-covered

#### 6.1.3 Ensure that a non-empty case statement block does not fall through to the next label
- -Wimplicit-fallthrough

#### 6.1.4 Ensure that a switch statement has at least two case labels, distinct from the default label 
- hicpp-multiway-paths-covered

#### 6.2.1 Implement a loop that only uses element values as a range-based loop
- modernize-loop-convert

#### 6.3.2 Ensure that execution of a function with a non-void return type ends in a return statement with a value 
- -Wreturn-type

#### 7.1.1 Declare each identifier on a separate line in a separate declaration
- clang-format handles this

#### 7.1.2 Use const whenever possible
- readability-non-const-parameter

#### 7.1.8 Use auto id = expr when declaring a variable to have the same type as its initializer function call
- modernize-use-auto
- hicpp-use-auto

#### 7.1.10 Use static_assert for assertions involving compile time constants 
- misc-static-assert
- hicpp-static-assert

#### 7.5.1 Do not use the asm declaration
- hicpp-no-assembler

#### 8.2.1 Make parameter names absent or identical in all declarations
- readability-identifier-naming
- hicpp-identifier-naming

#### 8.2.2 Do not declare functions with an excessive number of parameters
- readability-function-size 
- hicpp-function-size 

#### 8.3.1 Do not write functions with an excessive McCabe Cyclomatic Complexity
- readability-function-size
- hicpp-function-size

#### 8.3.2 Do not write functions with a high static program path count
- readability-function-size
- hicpp-function-size

#### 8.4.1 Do not access an invalid object or an object with indeterminate value
- warning for uninitialized variables should the compiler do
- access freed memory is CSA, and maybe impossible to determine statically?
- misc-use-after-move

#### 10.2.1 Use the override special identifier when overriding a virtual function
- modernize-use-override
- hicpp-use-override

### 12.1 Conversions
- google-explicit-constructor
- hicpp-explicit-constructor

### 12.3 Free store
- misc-new-delete-overloads
- hicpp-new-delete-overloads

#### 12.4.2 Ensure that a constructor initializes explicitly all base classes and non-static data members
- cppcoreguidelines-pro-type-member-init
- hicpp-member-init

#### 12.4.4 Write members in an initialization list in the order in which they are declared
- clang-diagnostic-reorder

#### 12.4.5 Use delegating constructors to reduce code duplication 
- misc-undelegated-constructor
- hicpp-undelegated-constructor

#### 12.5.1 Define explicitly =default or =delete implicit special member functions of concrete classes
- modernize-use-equals-default
- modernize-use-equals-delete
- hicpp-use-equals-default
- hicpp-use-equals-delete

#### 12.5.2 Define special members =default if the behavior is equivalent
- handled by the check for 12.5.1

#### 12.5.4 Declare noexcept the move constructor and move assignment operator
- misc-noexcept-move-constructor
- hicpp-noexcept-move-constructor

#### 12.5.7 Declare assignment operators with the ref-qualifier &
- cppcoreguidelines-special-member-functions
- hicpp-special-member-functions

#### 14.1.1 Use variadic templates rather than an ellipsis
- cppcoreguidelines-pro-type-vararg
- hicpp-vararg

#### 15.1.1 Only use instances of std::exception for exceptions
- hicpp-exception-baseclass

####  17.3.1 Do not use std::move on objects declared with const or const & type
- misc-move-const-arg
- hicpp-move-const-arg

####  17.3.3 Do not subsequently use the argument to std::forward
- use after move is almost the same

####  17.4.2 Use API calls that construct objects in place 
- modernize-use-emplace
- hicpp-use-emplace
