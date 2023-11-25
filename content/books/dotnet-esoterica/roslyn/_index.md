+++
Title = "Roslyn SDK"
Type = "book"
Weight = 100

[menu]
  [menu.dotnet]
    Name = "The Roslyn SDK"
    Identifier = "dotnet.roslyn"
    Parent = "dotnet"
    Weight = 100
+++

The first major section will focus on the Roslyn API. This is the way that we will be interacting with the C# compilation process. While we will mostly be focusing on this from a source generator standpoint at first, the information should be applicable to analyzer and code fixes as well. This is because the Roslyn APIs is more a reflection of the C# language design more than anything. Sure, there are some compiler specific quirks and features. Fundamentally we will learn how to view and understand our own code through the lens of the various compilation stages.

<!--more-->

## Roslyn

Roslyn is the name of the .NET compiler. Roslyn was engineered to be a compiler-as-a-library - it exposes APIs and extension points at almost every phase of the compilation process. This allows for many kinds of tools and utilities to be built that not only understand C#, but use the actual compiler. Compared to regex or parser-only solutions, having the entire compiler stack at your disposal lets you build tools that have not only semantic understanding, but can perform flow analysis and other deeper levels of analysis.

The official [Roslyn SDK Documentation](https://learn.microsoft.com/en-us/dotnet/csharp/roslyn-sdk/) provides a nice overview of Roslyn and the capabilities exposed to you, but it lacks some of the depth that I would have liked to see.