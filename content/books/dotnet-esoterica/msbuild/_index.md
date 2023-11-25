+++
Title = "SDKs - The newer, 'simplified', MSBuild system"
Type = "book"
Weight = 300

[menu]
  [menu.dotnet]
    Name = "MSBuild SDKs"
    Identifier = "dotnet.msbuild"
    Parent = "dotnet"
    Weight = 300
+++

Right now this is the least understood area for me. This section is merely a placeholder for me to do more research into the `Microsoft.NET.SDK` system. I would like to understand how everything works as well as what it will take to author an extended (or from scratch) SDK build system.
<!--more-->

- How the SDK system works
  - MSBuild 101
  - A tour through the stages
  - What's needed to build a project?
  - Hooks and extension points
- Building our own SDK
  - Solving cross platform native build
  - Distributing the SDK on NuGet
  - Creating templates