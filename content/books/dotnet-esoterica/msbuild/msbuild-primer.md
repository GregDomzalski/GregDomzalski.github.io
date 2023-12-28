+++
Title = "MSBuild primer - for developers"
Type = "book"

[menu]
  [menu.dotnet]
    Name = "MSBuild primer"
    Identifier = "dotnet.msbuild.primer"
    Parent = "dotnet.msbuild"
    Weight = 10
+++

MSBuild is a programming language. Its form just happens to be XML. But it's a programming language alright. Complete with variables, types, conditions, functions, and more. In this section, we'll take a look at MSBuild under that context: how can we use it to make programs?

# Basic syntax

An MSBuild file is an XML file. It follows a relatively simple schema, which we'll take a look at now. While the 

## File structure

Every file uses the `<project>` tag as its root element. While not strictly required, it's good practice to include the `xmlns` attribute when declaring a stand-alone MSBuild file. Comments are also supported, as is expected with any XML derived language.

```xml
<!-- This is a sample MSBuild file -->
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

</Project>
```

Files are always discussed in the context of a "project". I won't be using that term consistently throughout the documentation - only when it's explicitly needed. MSBuild files typically have the file extension `props` or `targets`, depending on the intended use and import location of the file. (More on this later.)

Like other languages, you're able to break down your files into many sub-files. These can then be included, or "imported" in MSBuild terminology, into your project file. This is done with the `<Import />` element. Imports must be declared within the top-level `Project` node, and cannot exist inside of any other tags.

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Import Project="path/to/file.props" />
    <Import Project="path/to/other.targets" />
</Project>
```

## Variables

MSBuild supports declaring variables. Variables are essentially treated as a key-value store. While there are some limited scoping rules within MSBuild, most of what you will see declared belongs to a single global scope.

Values are assigned to keys in the order in which the files are evaluated. If a key is seen more than once (barring any other conditions) its value will be updated to the latest value evaluated. For example:

```xml
<!-- File: a.props -->
<Project>
    <PropertyGroup>
        <MyVariable>foo</MyVariable>
    </PropertyGroup>

    <Import Project="b.props" />
    <!-- My variable is now set to bar for the remainder of this file. -->
</Project>

<!-- File: b.props -->
<Project>
    <PropertyGroup>
        <MyVariable>bar</MyVariable> <!-- My variable is now set to bar -->
    </PropertyGroup>
</Project>
```

There are two kinds of values that can be stored using MSBuild: scalar (single) values, and collections of dictionaries.

### Scalar key / value pairs

#### Defining key / value pairs

Storing a scalar value is one of the most basic actions you can take in MSBuild. We saw the syntax for this already in the previous section. These kinds of variables are defined in `<PropertyGroup>` elements.

A property group does nothing more than to say that you are about to define some key value pairs. You may have as many or as few property group sections within your file as you need. The values defined in each section don't necessarily need to have any relation to each other, but generally it is good practice to keep like things together.

If you do group related values together, you have two options. You can of course use an XML comment to leave a note about what's contained within that property group. Or, you can use the `Label` attribute of the property group element. It seems like comments are used more widely within the official project system files, but a label can be useful as well:

```xml
<!-- This property group does XYZ -->
<PropertyGroup Label="XYZ related properties">
    <!-- A bunch of keys and values -->
</PropertyGroup>
```

Any undefined key will have a default value of `''` or the empty string. This is also treated as a `false` value.

#### Usage

Values are not strongly typed. Generally, everything is treated as a string - but values can be coerced to behave like numbers and booleans as well.

You can refer to values using the `$()` substitution syntax. For example, if you wanted to create a version property out of smaller pieces, you could do the following:

```xml
<PropertyGroup>
    <MajorVersion>1</MajorVersion>
    <MinorVersion>5</MinorVersion>
    <PatchVersion>3</PatchVersion>

    <!-- Construct a Version variable based on the values contained within the major/minor/patch versions. -->
    <Version>$(MajorVersion).$(MinorVersion).$(PatchVersion)</Version>
    <!-- Version will be set to "1.5.3" -->
</PropertyGroup>
```

### Collections and dictionaries

#### Defining collections (and dictionaries)

In addition to `PropertyGroup` sections, there are `ItemGroup` sections as well. These can be considered to both be collections of things (items), of which these items may or may not have additional properties (metadata) attached.

The most common scenario for using item groups is referring to files (such as what to compile) or to dependencies (such as what projects or packages to reference).

Here's an example:

```xml
<ItemGroup>
    <CompileItems Include="**/*.cs" />

    <PackageReference Include="Foo" Version="1.5.3" />
    <PackageReference Include="Bar" Version="5.0.0" />
</ItemGroup>
```

This example illustrates quite a few different ideas.

1. The element name, `CompileItems` and `PackageReference` in this example, acts as the name of a _particular_ dictionary.
2. The value of the `Include` attribute acts as the key (or set of keys) _within_ the dictionary.
3. File paths are treated special in item groups. The `**`, `*`, and `?` wildcards are all supported.
4. You can specify an item more than once so long as the key in `Include` is unique. This has an additive effect to the collection.
5. You can have additional metadata in the form of attributes or child elements. In this example `Version` is extra metadata associated with each of the PackageReference entries.

#### Referring to a collection

Similar to a scalar property value, you can access collections. Instead of using `$()` you will use `@()`. This will return a semi-colon separated list of the keys for that particular collection.

Using the above example: `@(PackageReference)` will return `Foo;Bar`.

You can change the separator that is returned by specifying it as the second argument to the `@()` like this: `@(PackageReference, '%0A%0D')` will return a value with each key on its own line. `%##` is the ASCII escape syntax for MSBuild. `0A` and `0D` correspond to `\r\n`.

Metadata can be accessed using the `%()` syntax. For example, `%(PackageReference.Version)` will return the version information for each entry in the collection.

