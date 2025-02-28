# dotnet-bundle

Command-line interface tools for bundling .NET Core projects into MacOS applications (.app)

### Installation

Install MSBuild task via NuGet package: `HaroohieClub.DotNet.Bundle`

[![NuGet](https://img.shields.io/nuget/v/HaroohieClub.DotNet.Bundle.svg)](https://www.nuget.org/packages/HaroohieClub.DotNet.Bundle/)

```
<PackageReference Include="HaroohieClub.DotNet.Bundle" Version="*" />
```

### Using the tool

```
dotnet msbuild -t:BundleApp -p:RuntimeIdentifier=osx-x64 [-p: ...]
```

### Properties

Define properties to override default bundle values

```
<PropertyGroup>
    <CFBundleName>AppName</CFBundleName> <!-- Also defines .app file name -->
    <CFBundleDisplayName>App Name</CFBundleDisplayName>
    <CFBundleIdentifier>com.example</CFBundleIdentifier>
    <CFBundleVersion>1.0.0</CFBundleVersion>
    <CFBundlePackageType>APPL</CFBundlePackageType>
    <CFBundleSignature>????</CFBundleSignature>
    <CFBundleExecutable>AppName</CFBundleExecutable>
    <CFBundleIconFile>AppName.icns</CFBundleIconFile> <!-- Will be copied from output directory -->
    <NSPrincipalClass>NSApplication</NSPrincipalClass>
    <NSHighResolutionCapable>true</NSHighResolutionCapable>

    <!-- Optional -->
    <NSRequiresAquaSystemAppearance>true</NSRequiresAquaSystemAppearance>
</PropertyGroup>

<ItemGroup>
    <!-- Optional URLTypes.Check TestBundle.csproj for a working example. -->
    <CFBundleURLTypes Include="dummy"> <!-- The name of this file is irrelevant, it's a MSBuild requirement.-->
        <CFBundleURLName>TestApp URL</CFBundleURLName>
        <CFBundleURLSchemes>testappurl;testappurl://</CFBundleURLSchemes> <!-- Note the ";" separator-->
    </CFBundleURLTypes>
    <CFBundleURLTypes Include="dummy">
        <CFBundleURLName>TestApp URL2</CFBundleURLName>
        <CFBundleURLSchemes>test://</CFBundleURLSchemes>
    </CFBundleURLTypes>
</ItemGroup>

<ItemGroup>
    <CFBundleDocumentTypes Include="dummy">
      <CFBundleTypeName>TestFile</CFBundleTypeName>
      <CFBundleTypeIconFile>IconTest.icns</CFBundleTypeIconFile>
      <CFBundleTypeExtensions>test</CFBundleTypeExtensions>
      <CFBundleTypeRole>Editor</CFBundleTypeRole>
    </CFBundleDocumentTypes>
    <CFBundleDocumentTypes Include="dummy">
      <CFBundleTypeName>TestFile2</CFBundleTypeName>
      <CFBundleTypeIconFile>IconTest.icns</CFBundleTypeIconFile>
      <CFBundleTypeExtensions>tst;tst2</CFBundleTypeExtensions>
      <CFBundleTypeRole>Editor</CFBundleTypeRole>
    </CFBundleDocumentTypes>
  </ItemGroup>
```

More info: https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html
