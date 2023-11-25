+++
Title = "Source generators - .NET meta-programming"
Type = "book"
Weight = 200

[menu]
  [menu.dotnet]
    Name = "Source generators"
    Identifier = "dotnet.sourcegen"
    Parent = "dotnet"
    Weight = 200
+++

This is where I'm currently spending a lot of time doing research. Source generators are an extremely powerful tool in the .NET ecosystem. It takes meta-programming to the next level by allowing us to extend the compiler itself. While it doesn't necessarily allow us to do things like add new language features and keywords, it still allows us to do a lot. We can remove a large amount of boiler plate code from our code bases. Things that would have been infeasible otherwise are now within our grasp. And now, with some new features in .NET 8 / C# 12 - namely "interceptors" - we have even more power and flexibility.
<!--more-->

- Anatomy of a source generator
- Working backwards: Emitting code
- Defining the model
- Building the pipeline
- Testing a source generator
  - Unit testing
  - Integration testing through snapshot testing
- Packaging the source generator
- Reference
  - Syntax providers
  - Source sinks
  - Transformation pipelines
  - Performance and caching