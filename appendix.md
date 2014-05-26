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
    Identifier Constraintopt

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
    TypeName [no LineTerminator here] TypeArgumentsopt

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
    TypeParametersopt ( ParameterListopt ) => Type

ConstructorType:
    new TypeParametersopt ( ParameterListopt ) => Type

ObjectType:
    { TypeBodyopt }

TypeBody:
    TypeMemberList ;opt

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
    PropertyName ?opt TypeAnnotationopt

PropertyName:
    IdentifierName
    StringLiteral
    NumericLiteral

CallSignature:
    TypeParametersopt ( ParameterListopt ) TypeAnnotationopt

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
    PublicOrPrivateopt Identifier TypeAnnotationopt
    Identifier : StringLiteral

PublicOrPrivate:
    public
    private

OptionalParameterList:
    OptionalParameter
    OptionalParameterList , OptionalParameter

OptionalParameter:
    PublicOrPrivateopt Identifier ? TypeAnnotationopt
    PublicOrPrivateopt Identifier TypeAnnotationopt Initialiser

RestParameter:
    ... Identifier TypeAnnotationopt

ConstructSignature:
    new TypeParametersopt ( ParameterListopt ) TypeAnnotationopt

IndexSignature:
    [ Identifier : string ] TypeAnnotation
    [ Identifier : number ] TypeAnnotation

MethodSignature:
    PropertyName ?opt CallSignature
```

## A.2 Expressions

```text
PropertyAssignment: ( Modified )
    PropertyName : AssignmentExpression
    PropertyName CallSignature { FunctionBody }
    GetAccessor
    SetAccessor

GetAccessor:
    get PropertyName ( ) TypeAnnotationopt { FunctionBody }

SetAccessor:
    set PropertyName ( Identifier TypeAnnotationopt ) { FunctionBody }

CallExpression: ( Modified )
    ...
    super ( ArgumentListopt )
    super . IdentifierName

FunctionExpression: ( Modified )
    function Identifieropt CallSignature { FunctionBody }

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
    TypeArgumentsopt ( ArgumentListopt )

UnaryExpression: ( Modified )
    ...
    < Type > UnaryExpression
```

## A.3 Statements

```text
VariableDeclaration: ( Modified )
    Identifier TypeAnnotationopt Initialiseropt

VariableDeclarationNoIn: ( Modified )
    Identifier TypeAnnotationopt InitialiserNoInopt

TypeAnnotation:
    : Type
```

## A.4 Functions

```text
FunctionDeclaration: ( Modified )
    FunctionOverloadsopt FunctionImplementation

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
    interface Identifier TypeParametersopt InterfaceExtendsClauseopt ObjectType

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
    class Identifier TypeParametersopt ClassHeritage { ClassBody }

ClassHeritage:
    ClassExtendsClauseopt ImplementsClauseopt

ClassExtendsClause:
    extends ClassType

ClassType:
    TypeReference

ImplementsClause:
    implements ClassOrInterfaceTypeList

ClassBody:
    ClassElementsopt

ClassElements:
    ClassElement
    ClassElements ClassElement

ClassElement:
    ConstructorDeclaration
    PropertyMemberDeclaration
    IndexMemberDeclaration

ConstructorDeclaration:
    ConstructorOverloadsopt ConstructorImplementation

ConstructorOverloads:
    ConstructorOverload
    ConstructorOverloads ConstructorOverload

ConstructorOverload:
    PublicOrPrivateopt constructor ( ParameterListopt ) ;

ConstructorImplementation:
    PublicOrPrivateopt constructor ( ParameterListopt ) { FunctionBody }

PropertyMemberDeclaration:
    MemberVariableDeclaration
    MemberFunctionDeclaration
    MemberAccessorDeclaration

MemberVariableDeclaration:
    PublicOrPrivateopt staticopt PropertyName TypeAnnotationopt Initialiseropt ;

MemberFunctionDeclaration:
    MemberFunctionOverloadsopt MemberFunctionImplementation

MemberFunctionOverloads:
    MemberFunctionOverload
    MemberFunctionOverloads MemberFunctionOverload

MemberFunctionOverload:
    PublicOrPrivateopt staticopt PropertyName CallSignature ;

MemberFunctionImplementation:
    PublicOrPrivateopt staticopt PropertyName CallSignature { FunctionBody }

MemberAccessorDeclaration:
    PublicOrPrivateopt staticopt GetAccessor
    PublicOrPrivateopt staticopt SetAccessor

IndexMemberDeclaration:
    IndexSignature ;
```

## A.7 Enums

```text
EnumDeclaration:
    enum Identifier { EnumBodyopt }

EnumBody:
    ConstantEnumMembers ,opt
    ConstantEnumMembers , EnumMemberSections ,opt
    EnumMemberSections ,opt

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
    ModuleElementsopt

ModuleElements:
    ModuleElement
    ModuleElements ModuleElement

ModuleElement:
    Statement
    exportopt VariableDeclaration
    exportopt FunctionDeclaration
    exportopt ClassDeclaration
    exportopt InterfaceDeclaration
    exportopt EnumDeclaration
    exportopt ModuleDeclaration
    exportopt ImportDeclaration

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
    ImplementationElementsopt

ImplementationElements:
    ImplementationElement
    ImplementationElements ImplementationElement

ImplementationElement:
    ModuleElement
    ExportAssignment
    exportopt ExternalImportDeclaration
    exportopt AmbientDeclaration

DeclarationSourceFile:
    DeclarationElementsopt

DeclarationElements:
    DeclarationElement
    DeclarationElements DeclarationElement

DeclarationElement:
    ExportAssignment
    exportopt InterfaceDeclaration
    exportopt ImportDeclaration
    exportopt ExternalImportDeclaration
    exportopt AmbientDeclaration

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
    var Identifier TypeAnnotationopt ;

AmbientFunctionDeclaration:
    function Identifier CallSignature ;

AmbientClassDeclaration:
    class Identifier TypeParametersopt ClassHeritage { AmbientClassBody }

AmbientClassBody:
    AmbientClassBodyElementsopt

AmbientClassBodyElements:
    AmbientClassBodyElement
    AmbientClassBodyElements AmbientClassBodyElement

AmbientClassBodyElement:
    AmbientConstructorDeclaration
    AmbientPropertyMemberDeclaration
    IndexSignature

AmbientConstructorDeclaration:
    constructor ( ParameterListopt ) ;

AmbientPropertyMemberDeclaration:
    PublicOrPrivateopt staticopt PropertyName TypeAnnotationopt ;
    PublicOrPrivateopt staticopt PropertyName CallSignature ;

AmbientEnumDeclaration:
    enum Identifier { AmbientEnumBodyopt }

AmbientEnumBody:
    AmbientEnumMemberList ,opt

AmbientEnumMemberList:
    AmbientEnumMember
    AmbientEnumMemberList , AmbientEnumMember

AmbientEnumMember:
    PropertyName
    PropertyName = NumericLiteral

AmbientModuleDeclaration:
    module IdentifierPath { AmbientModuleBody }

AmbientModuleBody:
    AmbientModuleElementsopt

AmbientModuleElements:
    AmbientModuleElement
    AmbientModuleElements AmbientModuleElement

AmbientModuleElement:
    exportopt AmbientVariableDeclaration
    exportopt AmbientFunctionDeclaration
    exportopt AmbientClassDeclaration
    exportopt InterfaceDeclaration
    exportopt AmbientEnumDeclaration
    exportopt AmbientModuleDeclaration
    exportopt ImportDeclaration

AmbientExternalModuleDeclaration:
    module StringLiteral { AmbientExternalModuleBody }

AmbientExternalModuleBody:
    AmbientExternalModuleElementsopt

AmbientExternalModuleElements:
    AmbientExternalModuleElement
    AmbientExternalModuleElements AmbientExternalModuleElement

AmbientExternalModuleElement:
    AmbientModuleElement
    ExportAssignment
    exportopt ExternalImportDeclaration
```
