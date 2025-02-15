# NEW FEATURES in this fork:

This fork of NuGet2Unity supports an additional option, `-f` (or `--folder`), an absolute or relative path to a folder containing a .nuspec file. The name of the file must match the (required) value of the `-n` (or `--nugetpackage`) option. When `--folder` is supplied, NuGet2Unity will download the dependencies of *the local* .nuspec file, rather than first fetching the package from NuGet. All subsequent dependencies will be fetched from NuGet.

This is useful for bundling NuGet packages for a local, private project, that doesn't exist on NuGet itself.

Example:

```
dotnet run --nugetpackage My.Awesome.Project --folder ../../TopSecretProject
```

The directory structure at `../../TopSecretProject` should be something like this:
```
../../TopSecretProject
└── My.Awesome.Project.nuspec
```

# NuGet2Unity

A .NET Core app to package a NuGet package (and dependencies) as a .UnityPackage for import into a Unity 2018 (or higher) project.
This will build a package that should be compatible with the following Unity player settings
(Player Settings -> Other Settings -> Configuration):

Setting | Value
--------|------
Scripting Runtime Version | .NET 4.x Equivalent
Scripting Backend | Mono or IL2CPP
Api Compatibility Level | .NET Standard 2.0

## Build
It is assumed you have .NET Core 2.1 installed.  If not, you can download from [here](https://www.microsoft.com/net/download/dotnet-core/2.1).  Once installed, from the `src` directory, run the standard `dotnet build` command.

## Usage
Assuming you are in the `src` directory, simply run the standard `dotnet run` command with the following options:

Switch | Description
-------|-------------
-n, --nugetpackage  |  Required. NuGet package to repackage
-f, --folder        |  A path (relative or absolute) to a local C# project that has a .nuspec file. When supplied, this local project will serve as the root instead of fetching a remote NuGet package. If supplied, --version is ignored
-v, --version       |  Version of NuGet package to use
-p, --unityproject  |  Path to the Unity project to include with this package
-m, --includemeta   |  Include .meta files from the Unity project
-o, --outputpath    |  Path to save the .unitypackage
--verbose           |  Maximum verbosity
--skiplinkxml       |  Do not add a link.xml to package
--help              |  Display this help screen.
--version           |  Display version information.

## Example
Let's say you wanted to download and package the latest version of the [WindowsAzure.Storage NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) to a Unity package in the current directory.  Here's what that would look like (note the `--` argument which ensures the switches get passed to the app itself, not the dotnet command:

`dotnet run -- -n WindowsAzure.Storage`

## Packages
Check out our [Sandbox](https://aka.ms/azgamedev) site for some repackaged Azure SDKs that were built using this tool.
