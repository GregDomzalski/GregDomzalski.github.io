+++
Title = "Getting started using a playground project"
Type = "book"
Weight = 100

[menu]
  [menu.dotnet]
    Name = "Getting started: SourceGen playground"
    Identifier = "dotnet.sourcegen.getting-started-playground"
    Parent = "dotnet.sourcegen"
    Weight = 100
+++

When learning a new library or API, especially one as complex as source generators, I like to create a small playground project. Here, I have the bare-minimum to play around with all of the features of the library in a context that somewhat resembles what a real project may look like. In this guide, I'll walk you through what you need to do to get started.

## Setting up the project

Let's first start by setting up the solution structure. Since there will be multiple sub-projects, a solution is warranted. We will have the following projects:

1. Generator - This is the library that will actually host our experimental generator(s).
2. TargetCode - The target of the generator. This project consumes the generator and serves as our playground for using it to generate code.
3. TestingHost - This is a project that will allow us to host our generator in the context of a console app that we can step through and debug. This will allow us to test specific behaviors of the Roslyn compilation and generation framework itself.

On my computer, I have all of my source under `~/Source`, and within there I typically have an `Experiments` folder. You do not need to use this exact layout, of course. Run the following commands wherever you want to stick this project. Assume that I'm starting out in my `Experiments` folder.

```powershell
mkdir SourceGenPlayground
cd SourceGenPlayground
dotnet new classlib --framework netstandard2.0 --langVersion latest --name Generator
dotnet new console --framework net8.0 --name TargetCode
dotnet new console --framework net8.0 --name TestingHost
dotnet new sln --name SourceGenPlayground
dotnet sln add **/*.csproj
```

### Generator.csproj

There's a few more things we need to edit in our new `Generator/Generator.csproj` file:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <!-- Unfortunately, netstandard2.0 is required as some IDE hosting processes
         are still .NET Framework 4.x based -->
    <TargetFramework>netstandard2.0</TargetFramework>
    
    <!-- Language settings -->
    <!-- Even though we're stuck on netstandard2.0, we can still try and use the latest features. -->
    <LangVersion>latest</LangVersion>
    <Nullable>enable</Nullable>
    <ImplicitUsings>true</ImplicitUsings>
    
    <!-- Generator settings -->
    <EnforceExtendedAnalyzerRules>true</EnforceExtendedAnalyzerRules>
    <IncludeBuildOutput>false</IncludeBuildOutput>
  </PropertyGroup>

  <ItemGroup>
    <!-- These are the two packages needed for source generation. -->
    <PackageReference Include="Microsoft.CodeAnalysis.Analyzers" Version="3.3.4" PrivateAssets="all" />
    <PackageReference Include="Microsoft.CodeAnalysis.CSharp" Version="4.8.0" PrivateAssets="all" />
  </ItemGroup>

  <!-- This ensures the library will be packaged as a source generator when we use `dotnet pack` -->
  <ItemGroup>
    <None Include="$(OutputPath)\$(AssemblyName).dll" Pack="true"
          PackagePath="analyzers/dotnet/cs" Visible="false" />
  </ItemGroup>
</Project>
```

### TargetCode.csproj

We want our target project to consume the generator so that the generator can actually be run on this project. We can do this the following way:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
    <InvariantGlobalization>true</InvariantGlobalization>
  </PropertyGroup>

  <ItemGroup>
    <!-- In addition to simply referencing the Generator project, we need to treat it
         as an actual generator... which actually the same as we treat analyzers -->
    <ProjectReference Include="..\Generator\Generator.csproj"
                      OutputItemType="Analyzer"
                      ReferenceOutputAssembly="false" />
  </ItemGroup>

</Project>
```

### TestingHost.csproj

Lastly, we want a project that we can host a Roslyn compilation process and host the generator itself. Here's what the csproj should look like:

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net7.0</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
    </PropertyGroup>

    <ItemGroup>
        <!-- These are the two packages needed for source generation. -->
        <PackageReference Include="Microsoft.CodeAnalysis.Analyzers" Version="3.3.4" PrivateAssets="all" />
        <PackageReference Include="Microsoft.CodeAnalysis.CSharp" Version="4.8.0" PrivateAssets="all" />

        <!-- And our source generator itself... -->
        <ProjectReference Include="..\Generator\Generator.csproj" />
    </ItemGroup>

</Project>

```