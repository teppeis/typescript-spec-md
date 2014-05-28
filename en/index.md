TypeScript Language Specification
====

Version 1.0

April, 2014

Microsoft is making this Specification available under the Open Web Foundation Final Specification
Agreement Version 1.0 ("OWF 1.0") as of October 1, 2012. The OWF 1.0 is available at
http://www.openwebfoundation.org/legal/the-owf-1-0-agreements/owfa-1-0.

TypeScript is a trademark of Microsoft Corporation.

## Table of Contents

* [1 Introduction](./ch01.md)
    * 1.1 Ambient Declarations
    * 1.2 Function Types
    * 1.3 Object Types
    * 1.4 Structural Subtyping
    * 1.5 Contextual Typing
    * 1.6 Classes
    * 1.7 Enum Types
    * 1.8 Overloading on String Parameters
    * 1.9 Generic Types and Functions
    * 1.10 Modules
* [2 Basic Concepts](./ch02.md)
    * 2.1 Grammar Conventions
    * 2.2 Namespaces and Named Types
    * 2.3 Declarations
    * 2.4 Scopes
* [3 Types](./ch03.md)
    * 3.1 The Any Type
    * 3.2 Primitive Types
        * 3.2.1 The Number Type
        * 3.2.2 The Boolean Type
        * 3.2.3 The String Type
        * 3.2.4 The Void Type
        * 3.2.5 The Null Type
        * 3.2.6 The Undefined Type
        * 3.2.7 Enum Types
        * 3.2.8 String Literal Types
    * 3.3 Object Types
        * 3.3.1 Named Type References
        * 3.3.2 Array Types
        * 3.3.3 Anonymous Types
        * 3.3.4 Members
    * 3.4 Type Parameters
        * 3.4.1 Type Parameter Lists
        * 3.4.2 Type Argument Lists
    * 3.5 Named Types
        * 3.5.1 Instance Types
    * 3.6 Specifying Types
        * 3.6.1 Predefined Types
        * 3.6.2 Type References
        * 3.6.3 Type Queries
        * 3.6.4 Type Literals
    * 3.7 Object Type Literals
        * 3.7.1 Property Signatures
        * 3.7.2 Call Signatures
        * 3.7.3 Construct Signatures
        * 3.7.4 Index Signatures
        * 3.7.5 Method Signatures
    * 3.8 Type Relationships
        * 3.8.1 Apparent Type
        * 3.8.2 Type and Member Identity
        * 3.8.3 Subtypes and Supertypes
        * 3.8.4 Assignment Compatibility
        * 3.8.5 Contextual Signature Instantiation
        * 3.8.6 Type Inference
        * 3.8.7 Recursive Types
    * 3.9 Widened Types
    * 3.10 Best Common Type
* [4 Expressions](./ch04.md)
    * 4.1 Values and References
    * 4.2 The this Keyword
    * 4.3 Identifiers
    * 4.4 Literals
    * 4.5 Object Literals
    * 4.6 Array Literals
    * 4.7 Parentheses
    * 4.8 The super Keyword
        * 4.8.1 Super Calls
        * 4.8.2 Super Property Access
    * 4.9 Function Expressions
        * 4.9.1 Standard Function Expressions
        * 4.9.2 Arrow Function Expressions
        * 4.9.3 Contextually Typed Function Expressions
    * 4.10 Property Access
    * 4.11 The new Operator
    * 4.12 Function Calls
        * 4.12.1 Overload Resolution
        * 4.12.2 Type Argument Inference
        * 4.12.3 Grammar Ambiguities
    * 4.13 Type Assertions
    * 4.14 Unary Operators
        * 4.14.1 The ++ and -- operators
        * 4.14.2 The +, -, and ~ operators
        * 4.14.3 The ! operator
        * 4.14.4 The delete Operator
        * 4.14.5 The void Operator
        * 4.14.6 The typeof Operator
    * 4.15 Binary Operators
        * 4.15.1 The *, /, %, -, <<, >>, >>>, &, ^, and | operators
        * 4.15.2 The + operator
        * 4.15.3 The <, >, <=, >=, ==, !=, ===, and !== operators
        * 4.15.4 The instanceof operator
        * 4.15.5 The in operator
        * 4.15.6 The && operator
        * 4.15.7 The || operator
    * 4.16 The Conditional Operator
    * 4.17 Assignment Operators
    * 4.18 The Comma Operator
    * 4.19 Contextually Typed Expressions
* [5 Statements](./ch05.md)
    * 5.1 Variable Statements
    * 5.2 If, Do, and While Statements
    * 5.3 For Statements
    * 5.4 For-In Statements
    * 5.5 Continue Statements
    * 5.6 Break Statements
    * 5.7 Return Statements
    * 5.8 With Statements
    * 5.9 Switch Statements
    * 5.10 Throw Statements
    * 5.11 Try Statements
* [6 Functions](./ch06.md)
    * 6.1 Function Declarations
    * 6.2 Function Overloads
    * 6.3 Function Implementations
    * 6.4 Generic Functions
    * 6.5 Code Generation
* [7 Interfaces](./ch07.md)
    * 7.1 Interface Declarations
    * 7.2 Declaration Merging
    * 7.3 Interfaces Extending Classes
    * 7.4 Dynamic Type Checks
* [8 Classes](./ch08.md)
    * 8.1 Class Declarations
        * 8.1.1 Class Heritage Specification
        * 8.1.2 Class Body
    * 8.2 Members
        * 8.2.1 Instance and Static Members
        * 8.2.2 Accessibility
        * 8.2.3 Inheritance and Overriding
        * 8.2.4 Class Types
        * 8.2.5 Constructor Function Types
    * 8.3 Constructor Declarations
        * 8.3.1 Constructor Parameters
        * 8.3.2 Super Calls
        * 8.3.3 Automatic Constructors
    * 8.4 Property Member Declarations
        * 8.4.1 Member Variable Declarations
        * 8.4.2 Member Function Declarations
        * 8.4.3 Member Accessor Declarations
    * 8.5 Index Member Declarations
    * 8.6 Code Generation
        * 8.6.1 Classes Without Extends Clauses
        * 8.6.2 Classes With Extends Clauses
* [9 Enums](./ch09.md)
    * 9.1 Enum Declarations
    * 9.2 Enum Members
    * 9.3 Declaration Merging
    * 9.4 Code Generation
* [10 Internal Modules](./ch10.md)
    * 10.1 Module Declarations
    * 10.2 Module Body
    * 10.3 Import Declarations
    * 10.4 Export Declarations
    * 10.5 Declaration Merging
    * 10.6 Code Generation
* [11 Source Files and External Modules](./ch11.md)
    * 11.1 Source Files
        * 11.1.1 Source Files Dependencies
    * 11.2 External Modules
        * 11.2.1 External Module Names
        * 11.2.2 External Import Declarations
        * 11.2.3 Export Declarations
        * 11.2.4 Export Assignments
        * 11.2.5 CommonJS Modules
        * 11.2.6 AMD Modules
* [12 Ambients](./ch12.md)
    * 12.1 Ambient Declarations
        * 12.1.1 Ambient Variable Declarations
        * 12.1.2 Ambient Function Declarations
        * 12.1.3 Ambient Class Declarations
        * 12.1.4 Ambient Enum Declarations
        * 12.1.5 Ambient Module Declarations
        * 12.1.6 Ambient External Module Declarations
* [A Grammar](./appendix.md)
    * A.1 Types
    * A.2 Expressions
    * A.3 Statements
    * A.4 Functions
    * A.5 Interfaces
    * A.6 Classes
    * A.7 Enums
    * A.8 Internal Modules
    * A.9 Programs and External Modules
    * A.10 Ambients
