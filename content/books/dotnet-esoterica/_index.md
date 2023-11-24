+++
Title = ".NET Esoterica"
Type = "book"
Layout = "cover"

[menu]
  [menu.dotnet]
    Name = ".NET Esoterica"
    Weight = 0
+++

.NET Esoterica is a living book. It serves as the lost documentation and reference manuals that I wish I had when I began my journey learning some of the more esoteric features and extension points of .NET. Everything in here focuses on the latest .NET technologies - so .NET 7+, not .NET Framework. The only time .NET Framework topics will be covered is when our goal is to target .NET Standard 2.0 (in the case of Source Generators) or we are aiming to create a library that is compatible with the widest audience possible.

<!--more-->

Granted, I am still learning new things about these topics every day. Hence, a living book. Contents subject to change.

Topics:

- Roslyn syntax and symbol APIs
  - Syntax overview
    - Declarations
    - The rest
  - The semantic model (Symbol API)
- Source generators
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
- The SDK-based project system
  - How the SDK system works
    - MSBuild 101
    - A tour through the stages
    - What's needed to build a project?
    - Hooks and extension points
  - Building our own SDK
    - Solving cross platform native build
    - Distributing the SDK on NuGet
    - Creating templates
- Native interop
  - Calling from managed to native
    - P/Invoke
    - DllImport vs LibraryImport
    - Shim DLLs
    - Building and packaging native dependencies
  - Calling from native to managed
    - NativeAOT
    - Exporting managed code to C
