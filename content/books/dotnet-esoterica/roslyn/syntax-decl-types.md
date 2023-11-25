+++
Title = "Syntax - Type declarations"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "Type declarations"
    Identifier = "dotnet.roslyn.syntax.types"
    Parent = "dotnet.roslyn.syntax"
+++

I would argue that type declarations are the most important type of declaration syntax to wrap your head around. Types in C# are the fundamental building blocks of the language. Defining classes, structures, enumerations, etc. are what our code bases are all about.

Fundamentally, there are five different kinds of type declarations:

- Interfaces
- Classes
- Structs
- Records
- and, Enums

Enums are treated slightly different, with an extra level of abstraction inserted for the rest of the types. I suppose there were enough missing features of enumerations compared to the rest of the types that it made sense to separate it from them. We'll examine what these differences are in a moment.

![TypePropertyDeclaration inheritance](../images/typedecl-inheritance.svg "Hierarchy")

## Properties of type declarations

When looking at a base type declaration, we have the following properties that are interesting to us:

- `AttributeList` - Any attributes that are adorning this syntax node.
- `BaseList` - the base types that the current declaration inherits or is based on.
- `Identifier` - the token(s) that identify or name the type.
- `Members` - the member syntax contained by this type.
- `Modifiers` - such as `public`, `private`, `static`, `partial`, etc. that apply to the type declaration. Note that not all identifiers apply to all kinds of type declarations. I provide a quick reference table below.

There is of course trivia involved with a type declaration syntax. These are the `OpenBraceToken`, `CloseBraceToken`, and the `SemicolonToken`.

```csharp
[MyAttribute1] // <-- Begin of AttributeList
[MyAttribute2] // <-- End of AttributeList
public partial class TestClass : BaseClass, IInterface
// ^---------^       ^-------^   ^-------------------^
//  Modifiers        Identifier        BaseList
{ // <-- OpenBraceToken
  // (Members go here)
} // <-- CloseBraceToken
```

### Enum declarations

Enum declarations include everything mentioned above, plus the `EnumKeyword` trivia.

```csharp
public enum TestEnum
//     ^--^
//     EnumKeyword
{

}
```

### Base type declarations

Type declarations include everything mentioned above, plus the following:

- `ParameterList` - With the advent of record types and C# 12's primary constructor feature, types like classes and structs can now parameter lists attached to them.
- `TypeParameterList` - This is the list of generic type parameters.
- `ConstraintClauses` - And this is the set of constrains that apply to the generic type parameters.
- `Keyword` - Record types can be either `class` or `struct` types. The extra `keyword` property here can capture this information.

```csharp
public record struct Point<T>(T x, T y) where T : int
//             ^--^        ^   ^----^   ^-----------^
//            Keyword    Type   Param   ConstraintClauses
//                    ParamList  List
```

### Properties

The following table shows which of the properties apply to the given kind of type declaration:


| Property          | Enum               | Class              | Interface          | Record             | Struct             |
| ----------------- | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ |
| AttributeList     | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| BaseList          | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| ConstraintClauses | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Identifier        | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Members           | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Modifiers         | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| ParameterList     | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| TypeParameterList | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |

### Modifiers

While each declaration kind supports modifiers, the set of modifiers may be different. The below table shows the valid modifiers according to the C# language specification:

| Modifier    | Enum               | Class              | Interface          | Record             | Struct             |
| ----------- | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ |
| `new`       | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `public`    | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `protected` | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `internal`  | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `private`   | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `readonly`  | :x:                | :x:                | :x:                | :x:                | :white_check_mark: |
| `ref`       | :x:                | :x:                | :x:                | :x:                | :white_check_mark: |
| `abstract`  | :x:                | :white_check_mark: | :x:                | :white_check_mark: | :x:                |
| `sealed`    | :x:                | :white_check_mark: | :x:                | :white_check_mark: | :x:                |
| `static`    | :x:                | :white_check_mark: | :x:                | :white_check_mark: | :x:                |
| `unsafe`    | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `partial`   | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| `struct`    | :x:                | :x:                | :x:                | :white_check_mark: | :x:                |
| `class`     | :x:                | :x:                | :x:                | :white_check_mark: | :x:                |
