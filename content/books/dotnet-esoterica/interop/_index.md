+++
Title = "Interoping with native code"
Type = "book"
Weight = 400

[menu]
  [menu.dotnet]
    Name = "Native interop"
    Identifier = "dotnet.interop"
    Parent = "dotnet"
    Weight = 400
+++

Lastly, we'll cover native interoperability in depth. Native interop usually refers to inter-operating to and from C. P/Invoke has traditionally been the mechanism for calling out of managed code and into native. But this is, what I consider, to only be one third of the whole story. Did you know you can call C# code from C code? And now with NativeAOT becoming a first class scenario, doing so has become even easier. Lastly, there's the exploration of `unsafe` code within C#. Despite the name, writing such code does not need to be unsafe. Using it wisely can greatly improve our native interop story to create nice and clean interfaces in both directions.
<!--more-->

- Calling from managed to native
  - P/Invoke
  - DllImport vs LibraryImport
  - Shim DLLs
  - Building and packaging native dependencies
- Calling from native to managed
  - NativeAOT
  - Exporting managed code to C

