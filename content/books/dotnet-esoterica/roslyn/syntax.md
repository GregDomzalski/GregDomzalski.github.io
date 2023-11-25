+++
Title = "Understanding C#'s syntax"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "Understanding syntax"
    Identifier = "dotnet.roslyn.syntax"
    Parent = "dotnet.roslyn"
    Weight = 10
+++

C#'s syntax is quite expansive. But there's one particular subset that is relatively self-contained. This subset is also quite interesting when writing source generators as they're often used to find trees to work on, and used to build up the things we're generating.

This, of course, is the *declaration syntax*.

Something is declared whenever we are introducing a name into a compilation unit. For example, creating a new class using the familiar `public class Foo` is a `ClassDeclarationSyntax`. Note that I said you will see a declaration syntax whenever the name is introduced to a compilation unit (think, a single `*.cs` file). This means that you may actually see more than one declaration syntax for the same underlying type. Example: partial classes will have class declaration syntax for each file the class spans.

In this section, we'll go through the various types of declarations that you'll encounter when working with a C# syntax tree.

## Declarations

The best way to understand the various types of declaration syntaxes is to simply walk through the inheritance hierarchy using your IDE of course and/or the Microsoft documentation. The problem I did run into is understanding the properties, methods, and things I could do to abstract these different declarations. What is shared? What may look shared but really has different constraints based on the type of syntax?

These are my notes based on what I've found through a combination of reading the public Roslyn SDK documentation, reading the C# language specification, and of course reading the Roslyn source code itself.

Let's start with the bottom of the declaration syntax hierarchy. This is `MemberDeclarationSyntax`. Why "member declaration"? Two reasons: First, this matches the [grammar](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/basic-concepts#73-declarations) in the C# specification. Second, types are members of namespaces... but even namespaces are members of other namespaces. The special case being the `global::` namespace. But for the purposes of syntax, it is the same as all other namespaces.

![MemberDeclarationSyntax inheritance](../images/memberdecl-inheritance.svg "Hierarchy")

`MemberDeclarationSyntax` is derived by:
- `BaseFieldDeclarationSyntax`
- `BaseMethodDeclarationSyntax`
- `BaseNamespaceDeclarationSyntax`
- `BasePropertyDeclarationSyntax`
- `BaseTypeDeclarationSyntax`

### Components of the base member declaration

Not much is here. Only two properties: `AttributeList` and `Modifiers`.

`AttributeList`s are the attributes attached to the member. For example:

```csharp
[MyAttribute]
[MyAttributeWithParams("foo", bar = "baz")]
public class TestClass
{

}
```

While a `namespace` declaration technically has an attribute list attached to it, these attributes are treated as module-level attributes.

Similar with modifiers, the modifiers attached to a `MemberDeclarationSyntax` representing a namespace is kind of special. Namespaces are implicitly `public`. But the author cannot actually change, add, or remove any other modifiers. And indeed, with `modifier`, the list of acceptable options depend on the type of the declaration. We'll show later, syntax by syntax, which `modifier` applies to what `syntax`.
