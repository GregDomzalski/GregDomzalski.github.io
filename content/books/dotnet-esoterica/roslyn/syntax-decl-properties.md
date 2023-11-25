+++
Title = "Syntax - Property declarations"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "Property declarations"
    Identifier = "dotnet.roslyn.syntax.properties"
    Parent = "dotnet.roslyn.syntax"
+++

![BasePropertyDeclaration inheritance](../images/propdecl-inheritance.svg "Hierarchy")

`BasePropertyDeclarationSyntax` is derived by:
- `EventDeclarationSyntax`
- `IndexerDeclarationSyntax`
- `PropertyDeclarationSyntax`

All declarations have an `AccessorList`, `ExplicitInterfaceSpecifier`, and `Type` in addition to `AttributeList` and `Modifiers`.

Event declarations have an `EventKeyword`, `Identifier`, and `SemiColonToken`.

Indexer declarations have an `ExpressionBody`, `ParameterList`, as well as `Semicolon`, `SemicolonToken`, and `ThisKeyword` trivia.

Property declarations have an `ExpressionBody`, `Identifier`, and `Initializer`, as well as `Semicolon` and `SemicolonToken` trivia.
