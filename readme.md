# MultiTargeting AutoCAD .NET Plugin to NET 4.8 and NET 8.0

This application implements a command called `ellipsejig`. It will help you 
create an ellipse from scratch by doing a jig. The user is first asked to
enter the ellipse major axis followed by ellipse minor axis. 

To use JigSample.dll:

1. Start AutoCAD and open a new drawing.
2. Type netload and select JigSample.dll from the `\bin\x64\ACAD2024` subfolder for AutoCAD 2024 and `\bin\x64\ACAD2025`
3. Execute the ellipsejig command, defined by JigSample.dll.

Please add the References `acdbmgd.dll`,`accoremgd.dll` and `acmgd.dll` from your ObjectARX SDK  directory for respective configuration before trying to build this project.

The Project structure to accomodate multi frameworks.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <AssemblyName>JigSample</AssemblyName>
    <OutputType>Library</OutputType>
    <RootNamespace>JigSample</RootNamespace>
    <TargetFramework>net8.0-windows</TargetFramework>
    <GenerateAssemblyInfo>False</GenerateAssemblyInfo>
	<Platforms>x64</Platforms>
    <Configurations>ACAD2024;ACAD2025</Configurations>
	<BaseOutputPath>bin</BaseOutputPath>    
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)' == 'ACAD2025'">
    <TargetFramework>net8.0-windows</TargetFramework>
      <!-- uncomment to use Forms or WPF-->
      <!--<UseWindowsForms>true</UseWindowsForms>
      <UseWPF>true</UseWPF>-->
	<AssemblySearchPaths>D:\ArxSdks\Arx2025\inc\;$(AssemblySearchPaths)</AssemblySearchPaths>	
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)' == 'ACAD2024'">
    <TargetFramework>net48</TargetFramework>
	<AssemblySearchPaths>D:\ArxSdks\Arx2024\inc\;$(AssemblySearchPaths)</AssemblySearchPaths>
  </PropertyGroup>
    <ItemGroup Condition="'$(Configuration)' == 'ACAD2025'">
        <FrameworkReference Include="Microsoft.WindowsDesktop.App"/>
    </ItemGroup>
  <ItemGroup>
    <Reference Include="AcDbMgd">
      <Private>False</Private>
    </Reference>
    <Reference Include="acmgd">
      <Private>False</Private>
    </Reference>
    <Reference Include="accoremgd">
      <Private>False</Private>
    </Reference>
  </ItemGroup>
</Project>
```

#### Steps To Build

```bashag-0-1i1mltncuag-1-1i1mltncu
git clone
cd EllipseJig
```

- To build AutoCAD 2024 plugin
  
  ```bash
  dotnet build Ellipsejig.csproj -c ACAD2024 -a x64
  ```

- To build AutoCAD 2025 plugin
  
  ```bash
  dotnet build Ellipsejig.csproj -c ACAD2025 -a x64
  ```

Or, you build through Visual Studio UI.

After cloning the project, open the EllipseJig project in Visual Studio 2022, make the ACAD2024 or ACAD2025 configuration as default to build respective version projects.





## Written by

Madhukar Moogala [APS](https://aps.autodesk.com) , [@Galakar](https://x.com/Galakar)