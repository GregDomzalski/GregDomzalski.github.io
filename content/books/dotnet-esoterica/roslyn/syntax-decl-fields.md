+++
Title = "Syntax - Field declarations"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "Field declarations"
    Identifier = "dotnet.roslyn.syntax.fields"
    Parent = "dotnet.roslyn.syntax"
+++

![BaseFieldDeclaration inheritance](../images/fielddecl-inheritance.svg "Hierarchy")

`BaseFieldDeclarationSyntax` is derived by:
- `EventFieldDeclarationSyntax`
- `FieldDeclarationSyntax`

All declarations have a `Declaration` with `SemicolonToken` trivia, in addition to `AttributeList` and `Modifiers`.

Event fields also have an `EventKeyword` trivia.

Field declarations have no additional attributes or trivia.
