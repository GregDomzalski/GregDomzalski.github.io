+++
Title = "The semantic model"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "The semantic model"
    Identifier = "dotnet.roslyn.semantics"
    Parent = "dotnet.roslyn"
    Weight = 20
+++

One might think that there would be a 1:1 relationship between the syntax (especially the declarations) and the symbols that are produced. But this is not the case.

Semantic meaning it built from the context of one or more syntax nodes. Meaning might even come from completely different syntax trees - as is the case with partial types.

Here is a rough mapping of declaration syntax to symbol types:

| DeclarationSyntax              | Symbol types                                                   |
| ------------------------------ | -------------------------------------------------------------- |
| BaseNamespaceDeclarationSyntax | INamespaceSymbol, INamespaceOrTypeSymbol                       |
| EventFieldDeclarationSyntax    | IEventSymbol, ISymbol                                          |
| FieldDeclarationSyntax         | IFieldSymbol, ISymbol                                          |
| BaseMethodDeclarationSyntax    | IMethodSyntax, ISymbol                                         |
| BasePropertyDeclarationSyntax  | IPropertySymbol, ISymbol                                       |
| BaseTypeDeclarationSyntax      | INamedTypeSymbol, INamespaceOrTypeSymbol, ITypeSymbol, ISymbol |

