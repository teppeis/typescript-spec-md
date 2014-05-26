# A Grammar

This appendix contains a summary of the grammar found in the main document. As described in section
2.1, the TypeScript grammar is a superset of the grammar defined in the [ECMAScript Language
Specification](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf) (specifically, the ECMA-262 Standard, 5th Edition) and this appendix lists only productions
that are new or modified from the ECMAScript grammar.

## A.1 Types

```text
TypeParameters:
    < TypeParameterList >

TypeParameterList:
    TypeParameter
    TypeParameterList , TypeParameter

TypeParameter:
    Identifier Constraint(opt)

Constraint:
    extends Type

Type:
    PredefinedType
    TypeReference
    TypeQuery
    TypeLiteral

PredefinedType:
    any
    number
    boolean
    string
    void

TypeReference:
    TypeName [no LineTerminator here] TypeArguments(opt)

TypeName:
    Identifier
    ModuleName . Identifier

ModuleName:
    Identifier
    ModuleName . Identifier

TypeArguments:
    < TypeArgumentList >

TypeArgumentList:
    TypeArgument
    TypeArgumentList , TypeArgument

TypeArgument:
    Type

TypeQuery:
    typeof TypeQueryExpression

TypeQueryExpression:
    Identifier
    TypeQueryExpression . IdentifierName

TypeLiteral:
    ObjectType
    ArrayType
    FunctionType
    ConstructorType

ArrayType:
    ElementType [no LineTerminator here] [ ]

ElementType:
    PredefinedType
    TypeReference
    TypeQuery
    ObjectType
    ArrayType

FunctionType:
    TypeParameters(opt) ( ParameterList(opt) ) => Type

ConstructorType:
    new TypeParameters(opt) ( ParameterList(opt) ) => Type

ObjectType:
    { TypeBody(opt) }

TypeBody:
    TypeMemberList ;(opt)

TypeMemberList:
    TypeMember
    TypeMemberList ; TypeMember

TypeMember:
    PropertySignature
    CallSignature
    ConstructSignature
    IndexSignature
    MethodSignature

PropertySignature:
    PropertyName ?(opt) TypeAnnotation(opt)

PropertyName:
    IdentifierName
    StringLiteral
    NumericLiteral

CallSignature:
    TypeParameters(opt) ( ParameterList(opt) ) TypeAnnotation(opt)

ParameterList:
    RequiredParameterList
    OptionalParameterList
    RestParameter
    RequiredParameterList , OptionalParameterList
    RequiredParameterList , RestParameter
    OptionalParameterList , RestParameter
    RequiredParameterList , OptionalParameterList , RestParameter

RequiredParameterList:
    RequiredParameter
    RequiredParameterList , RequiredParameter

RequiredParameter:
    PublicOrPrivate(opt) Identifier TypeAnnotation(opt)
    Identifier : StringLiteral

PublicOrPrivate:
    public
    private

OptionalParameterList:
    OptionalParameter
    OptionalParameterList , OptionalParameter

OptionalParameter:
    PublicOrPrivate(opt) Identifier ? TypeAnnotation(opt)
    PublicOrPrivate(opt) Identifier TypeAnnotation(opt) Initialiser

RestParameter:
    ... Identifier TypeAnnotation(opt)

ConstructSignature:
    new TypeParameters(opt) ( ParameterList(opt) ) TypeAnnotation(opt)

IndexSignature:
    [ Identifier : string ] TypeAnnotation
    [ Identifier : number ] TypeAnnotation

MethodSignature:
    PropertyName ?(opt) CallSignature
```

## A.2 Expressions

```text
PropertyAssignment: ( Modified )
    PropertyName : AssignmentExpression
    PropertyName CallSignature { FunctionBody }
    GetAccessor
    SetAccessor

GetAccessor:
    get PropertyName ( ) TypeAnnotation(opt) { FunctionBody }

SetAccessor:
    set PropertyName ( Identifier TypeAnnotation(opt) ) { FunctionBody }

CallExpression: ( Modified )
    ...
    super ( ArgumentList(opt) )
    super . IdentifierName

FunctionExpression: ( Modified )
    function Identifier(opt) CallSignature { FunctionBody }

AssignmentExpression: ( Modified )
    ...
    ArrowFunctionExpression

ArrowFunctionExpression:
    ArrowFormalParameters => Block
    ArrowFormalParameters => AssignmentExpression

ArrowFormalParameters:
    CallSignature
    Identifier

Arguments: ( Modified )
    TypeArguments(opt) ( ArgumentList(opt) )

UnaryExpression: ( Modified )
    ...
    < Type > UnaryExpression
```

## A.3 Statements

```text
VariableDeclaration: ( Modified )
    Identifier TypeAnnotation(opt) Initialiser(opt)

VariableDeclarationNoIn: ( Modified )
    Identifier TypeAnnotation(opt) InitialiserNoIn(opt)

TypeAnnotation:
    : Type
```

## A.4 Functions

```text
FunctionDeclaration: ( Modified )
    FunctionOverloads(opt) FunctionImplementation

FunctionOverloads:
    FunctionOverload
    FunctionOverloads FunctionOverload

FunctionOverload:
    function Identifier CallSignature ;

FunctionImplementation:
    function Identifier CallSignature { FunctionBody }
```

## A.5 Interfaces

```text
InterfaceDeclaration:
    interface Identifier TypeParameters(opt) InterfaceExtendsClause(opt) ObjectType

InterfaceExtendsClause:
    extends ClassOrInterfaceTypeList

ClassOrInterfaceTypeList:
    ClassOrInterfaceType
    ClassOrInterfaceTypeList , ClassOrInterfaceType

ClassOrInterfaceType:
    TypeReference
```

## A.6 Classes

```text
ClassDeclaration:
    class Identifier TypeParameters(opt) ClassHeritage { ClassBody }

ClassHeritage:
    ClassExtendsClause(opt) ImplementsClause(opt)

ClassExtendsClause:
    extends ClassType

ClassType:
    TypeReference

ImplementsClause:
    implements ClassOrInterfaceTypeList

ClassBody:
    ClassElements(opt)

ClassElements:
    ClassElement
    ClassElements ClassElement

ClassElement:
    ConstructorDeclaration
    PropertyMemberDeclaration
    IndexMemberDeclaration

ConstructorDeclaration:
    ConstructorOverloads(opt) ConstructorImplementation

ConstructorOverloads:
    ConstructorOverload
    ConstructorOverloads ConstructorOverload

ConstructorOverload:
    PublicOrPrivate(opt) constructor ( ParameterList(opt) ) ;

ConstructorImplementation:
    PublicOrPrivate(opt) constructor ( ParameterList(opt) ) { FunctionBody }

PropertyMemberDeclaration:
    MemberVariableDeclaration
    MemberFunctionDeclaration
    MemberAccessorDeclaration

MemberVariableDeclaration:
    PublicOrPrivate(opt) static(opt) PropertyName TypeAnnotation(opt) Initialiser(opt) ;

MemberFunctionDeclaration:
    MemberFunctionOverloads(opt) MemberFunctionImplementation

MemberFunctionOverloads:
    MemberFunctionOverload
    MemberFunctionOverloads MemberFunctionOverload

MemberFunctionOverload:
    PublicOrPrivate(opt) static(opt) PropertyName CallSignature ;

MemberFunctionImplementation:
    PublicOrPrivate(opt) static(opt) PropertyName CallSignature { FunctionBody }

MemberAccessorDeclaration:
    PublicOrPrivate(opt) static(opt) GetAccessor
    PublicOrPrivate(opt) static(opt) SetAccessor

IndexMemberDeclaration:
    IndexSignature ;
```

## A.7 Enums

```text
EnumDeclaration:
    enum Identifier { EnumBody(opt) }

EnumBody:
    ConstantEnumMembers ,(opt)
    ConstantEnumMembers , EnumMemberSections ,(opt)
    EnumMemberSections ,(opt)

ConstantEnumMembers:
    PropertyName
    ConstantEnumMembers , PropertyName

EnumMemberSections:
    EnumMemberSection
    EnumMemberSections , EnumMemberSection

EnumMemberSection:
    ConstantEnumMemberSection
    ComputedEnumMember

ConstantEnumMemberSection:
    PropertyName = NumericLiteral
    PropertyName = NumericLiteral , ConstantEnumMembers

ComputedEnumMember:
    PropertyName = AssignmentExpression

## A.8 Internal Modules

ModuleDeclaration:
    module IdentifierPath { ModuleBody }

IdentifierPath:
    Identifier
    IdentifierPath . Identifier

ModuleBody:
    ModuleElements(opt)

ModuleElements:
    ModuleElement
    ModuleElements ModuleElement

ModuleElement:
    Statement
    export(opt) VariableDeclaration
    export(opt) FunctionDeclaration
    export(opt) ClassDeclaration
    export(opt) InterfaceDeclaration
    export(opt) EnumDeclaration
    export(opt) ModuleDeclaration
    export(opt) ImportDeclaration

ImportDeclaration:
    import Identifier = EntityName ;

EntityName:
    Identifier
    ModuleName . Identifier
```

## A.9 Programs and External Modules

```text
SourceFile:
    ImplementationSourceFile
    DeclarationSourceFile

ImplementationSourceFile:
    ImplementationElements(opt)

ImplementationElements:
    ImplementationElement
    ImplementationElements ImplementationElement

ImplementationElement:
    ModuleElement
    ExportAssignment
    export(opt) ExternalImportDeclaration
    export(opt) AmbientDeclaration

DeclarationSourceFile:
    DeclarationElements(opt)

DeclarationElements:
    DeclarationElement
    DeclarationElements DeclarationElement

DeclarationElement:
    ExportAssignment
    export(opt) InterfaceDeclaration
    export(opt) ImportDeclaration
    export(opt) ExternalImportDeclaration
    export(opt) AmbientDeclaration

ExternalImportDeclaration:
    import Identifier = ExternalModuleReference ;

ExternalModuleReference:
    require ( StringLiteral )

ExportAssignment:
    export = Identifier ;
```

## A.10 Ambients

```text
AmbientDeclaration:
    declare AmbientVariableDeclaration
    declare AmbientFunctionDeclaration
    declare AmbientClassDeclaration
    declare AmbientEnumDeclaration
    declare AmbientModuleDeclaration
    declare AmbientExternalModuleDeclaration

AmbientVariableDeclaration:
    var Identifier TypeAnnotation(opt) ;

AmbientFunctionDeclaration:
    function Identifier CallSignature ;

AmbientClassDeclaration:
    class Identifier TypeParameters(opt) ClassHeritage { AmbientClassBody }

AmbientClassBody:
    AmbientClassBodyElements(opt)

AmbientClassBodyElements:
    AmbientClassBodyElement
    AmbientClassBodyElements AmbientClassBodyElement

AmbientClassBodyElement:
    AmbientConstructorDeclaration
    AmbientPropertyMemberDeclaration
    IndexSignature

AmbientConstructorDeclaration:
    constructor ( ParameterList(opt) ) ;

AmbientPropertyMemberDeclaration:
    PublicOrPrivate(opt) static(opt) PropertyName TypeAnnotation(opt) ;
    PublicOrPrivate(opt) static(opt) PropertyName CallSignature ;

AmbientEnumDeclaration:
    enum Identifier { AmbientEnumBody(opt) }

AmbientEnumBody:
    AmbientEnumMemberList ,(opt)

AmbientEnumMemberList:
    AmbientEnumMember
    AmbientEnumMemberList , AmbientEnumMember

AmbientEnumMember:
    PropertyName
    PropertyName = NumericLiteral

AmbientModuleDeclaration:
    module IdentifierPath { AmbientModuleBody }

AmbientModuleBody:
    AmbientModuleElements(opt)

AmbientModuleElements:
    AmbientModuleElement
    AmbientModuleElements AmbientModuleElement

AmbientModuleElement:
    export(opt) AmbientVariableDeclaration
    export(opt) AmbientFunctionDeclaration
    export(opt) AmbientClassDeclaration
    export(opt) InterfaceDeclaration
    export(opt) AmbientEnumDeclaration
    export(opt) AmbientModuleDeclaration
    export(opt) ImportDeclaration

AmbientExternalModuleDeclaration:
    module StringLiteral { AmbientExternalModuleBody }

AmbientExternalModuleBody:
    AmbientExternalModuleElements(opt)

AmbientExternalModuleElements:
    AmbientExternalModuleElement
    AmbientExternalModuleElements AmbientExternalModuleElement

AmbientExternalModuleElement:
    AmbientModuleElement
    ExportAssignment
    export(opt) ExternalImportDeclaration
```
