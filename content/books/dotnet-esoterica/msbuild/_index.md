+++
Title = "MSBuild SDKs"
Type = "book"
Weight = 300

[menu]
  [menu.dotnet]
    Name = "MSBuild SDKs"
    Identifier = "dotnet.msbuild"
    Parent = "dotnet"
    Weight = 300
+++

MSBuild can be quite intimidating at first. At least, it was for me. The [SDK-style projects](https://learn.microsoft.com/en-us/dotnet/core/project-sdk/overview) used by .NET today greatly simplifies creating projects, but it pushes even more of the build system into a black box. The goal of this section is to open that box and look inside. To understand not just MSBuild, but the "SDK" projects built on top of them.
<!--more-->

- MSBuild primer for developers
- A tour through the stages
- How the SDK system works
  - Anatomy of an SDK
  - What makes up the Microsoft.NET.SDK?
  - What's needed to build a project?
  - Hooks and extension points
- Building our own SDK
  - Solving cross platform native build
  - Distributing the SDK on NuGet
  - Creating templates