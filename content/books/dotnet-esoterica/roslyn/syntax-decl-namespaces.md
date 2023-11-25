+++
Title = "Syntax - Namespace declarations"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "Namespace declarations"
    Identifier = "dotnet.roslyn.syntax.namespaces"
    Parent = "dotnet.roslyn.syntax"
+++

![BaseNamespaceDeclarationSyntax inheritance](../images/namespacedecl-inheritance.svg "Hierarchy")

`BaseNamespaceDeclarationSyntax` is derived by:
- `FileScopedNamespaceDeclarationSyntax`
- `NamespaceDeclarationSyntax`

All declarations have `Externs`, `Members`, `Usings`, and `Name`, in addition to `AttributeList` and `Modifiers`, as well as `NamespaceKeyword` trivia.

File-scoped namespace declarations also have a `SemicolonToken` trivia.

Block namespace declarations also have a `CloseBraceToken`, `OpenBraceToken`, and `SemicolonToken` trivia.