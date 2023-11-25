+++
Title = "Syntax - Methods declarations"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "Methods declarations"
    Identifier = "dotnet.roslyn.syntax.methods"
    Parent = "dotnet.roslyn.syntax"
+++

![BaseMethodDeclaration inheritance](../images/methoddecl-inheritance.svg "Hierarchy")

`BaseMethodDeclarationSyntax` is derived by:
- `ConstructorDeclarationSyntax`
- `ConversionOperatorDeclarationSyntax`
- `DestructorDeclarationSyntax`
- `MethodDeclarationSyntax`
- `OperatorDeclarationSyntax`

All declarations have a `Body`, `ExpressionBody`, `ParameterList`, and a `SemicolonToken`, in addition to `AttributeList` and `Modifiers`.

Constructor declarations also have an `Identifier` and `Initializer`.

Conversion operator declarations also have `CheckedKeyword`, `ExplicitInterfaceSpecifier`,  `ImplicitOrExplicitKeyword`, and `OperatorKeyword`.

Destructor declarations also have a `TildeToken` trivia.

Method declarations also have `ConstraintClauses`, `ExplicitInterfaceSpecifier`, `Identifier`, `ReturnType`, and `TypeParameterList`.

Operator declarations also have `CheckedKeyword`, `ExplicitInterfaceSpecifier`, `OperatorKeyword`, `OperatorToken`, and `ReturnType`.
