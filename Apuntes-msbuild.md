---
Titulo: "Apuntes msbuild"
---

# Apuntes msbuild

- [Apuntes msbuild](#apuntes-msbuild)
    - [**AUTOMATIZANDO LA COMPILACIÓN CON MSBUILD Y XUNIT**](#automatizando-la-compilación-con-msbuild-y-xunit)
    - [***MSBuild script for compiling all .cs files into a single assembly (DLL or EXE)***](#msbuild-script-for-compiling-all-cs-files-into-a-single-assembly-dll-or-exe)
    - [***Csc (tarea)***](#csc-tarea)
    - [***Tutorial: Crear un archivo de proyecto de MSBuild desde cero***](#tutorial-crear-un-archivo-de-proyecto-de-msbuild-desde-cero)
    - [***Procedimiento Seleccionar los archivos que se van a compilar***](#procedimiento-seleccionar-los-archivos-que-se-van-a-compilar)
    - [***Learn Web Assembly (WASM) In 1 Video***](#learn-web-assembly-wasm-in-1-video)
    - [***Getting Started with the sample***](#getting-started-with-the-sample)
    - [***WebAssembly packager.exe***](#webassembly-packagerexe)
    - [***Uno.Wasm.Bootstrap***](#unowasmbootstrap)
    - [***Introducing Uno WebAssembly Projects and Debugging***](#introducing-uno-webassembly-projects-and-debugging)

### **AUTOMATIZANDO LA COMPILACIÓN CON MSBUILD Y XUNIT**

http://xurxodev.com/automatizando-la-compilacion-con-msbuild-y-xunit/

~~~
<Project
   xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="RestorePackages">
  </Target>

  <Target Name="Rebuild">
  </Target>

  <Target Name="Tests">
  </Target>

</Project>
~~~

~~~
<Project
    DefaultTargets="Default"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <UsingTask
    AssemblyFile="packages\xunit.runner.msbuild.2.1.0\build\portable-net45+win8+wp8+wpa81\xunit.runner.msbuild.dll"
    TaskName="Xunit.Runner.MSBuild.xunit" />

  <ItemGroup>
    <TestAssemblies Include="**\bin\Release\*.test.dll" />
  </ItemGroup>

  <Target Name="Default" DependsOnTargets="RestorePackages;Rebuild;Test">
  </Target>

  <Target Name="RestorePackages">
    <Exec Command="&quot;tools\NuGet.exe&quot; restore &quot;TuSolucion.sln&quot;" />
  </Target>

  <Target Name="Rebuild" >
    <MSBuild Targets="Clean;Rebuild" Projects="TuSolucion.sln" Properties="Configuration=Release"/>

  </Target>

  <Target Name="Test">
    <xunit Assemblies="@(TestAssemblies)" />
  </Target>

</Project>
~~~

___

### ***MSBuild script for compiling all .cs files into a single assembly (DLL or EXE)***

https://blogs.msdn.microsoft.com/dotnetinterop/2008/04/08/msbuild-script-for-compiling-all-cs-files-into-a-single-assembly-dll-or-exe/

~~~
  1 <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"


    2         DefaultTargets="CompileAll"


    3         ToolsVersion="3.5"


    4   >


    5 


    6   <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />


    7   <!-- Import Project="c:\.net3.5\Microsoft.Csharp.targets" /    -->


    8 


    9   <PropertyGroup>


   10     <!-- This AppName thing is the base name of your DLL or EXE -->


   11     <AppName>YourAppNameHere</AppName>


   12   </PropertyGroup>


   13 


   14   <!-- This build file compiles each .cs file into its own exe -->


   15   <PropertyGroup Condition="'$(Configuration)'==''">


   16     <Configuration>Debug</Configuration>


   17     <!-- Default -->


   18   </PropertyGroup>


   19 


   20   <PropertyGroup Condition="'$(Configuration)'=='Debug'">


   21     <Optimize>false</Optimize>


   22     <DebugSymbols>true</DebugSymbols>


   23     <!-- <OutputPath>.\bin</OutputPath>  -->


   24     <OutputPath>.\</OutputPath>


   25     <OutDir>.\</OutDir>


   26     <IntermediateOutputPath>.\</IntermediateOutputPath>


   27   </PropertyGroup>


   28 


   29 


   30   <!-- Specify the inputs by type and file name -->


   31   <ItemGroup>


   32     <CSFile Include="*.cs"/>


   33   </ItemGroup>


   34 


   35 


   36   <!-- specify reference assemblies for all builds in this project -->


   37   <ItemGroup>


   38     <Reference Include="mscorlib" />


   39     <Reference Include="System" />


   40     <Reference Include="System.Core" />


   41     <Reference Include="System.Data" />


   42     <Reference Include="System.Data.Linq" />


   43     <Reference Include="System.ServiceModel" />


   44     <Reference Include="System.ServiceModel.Web" />


   45     <Reference Include="System.Runtime.Serialization" />


   46     <!-- <Reference Include=".\ObjectDumper.dll" /> -->


   47   </ItemGroup>


   48 


   49 


   50   <Target Name="CompileAll"


   51           DependsOnTargets="ResolveAssemblyReferences"


   52     >


   53 


   54     <Message Text="Reference = @(Reference)" />


   55     <Message Text="ReferencePath = @(ReferencePath)" />


   56 


   57 


   58     <!-- Message Text="MS Build Tools path:  $(MSBuildToolsPath)" / -->


   59 


   60     <!-- Run the Visual C# compilation on all the .cs files. -->


   61 


   62     <CSC


   63       Sources="@(CSFile)"


   64       References="@(ReferencePath)"


   65       OutputAssembly="$(OutputPath)\$(AppName).exe"


   66       EmitDebugInformation="$(DebugSymbols)"


   67       TargetType="exe"


   68       Toolpath="$(MSBuildToolsPath)"


   69       Nologo="true"


   70         />


   71   </Target>


   72 


   73   <!-- redefine the Clean target, from the Microsoft.csharp.targets file.  (Last definition wins) -->


   74   <Target Name="Clean">


   75     <Delete Files="$(OutputPath)\$(AppName).exe"/>


   76     <Delete Files="$(OutputPath)\$(AppName).pdb"/>


   77     <Delete Files="%(CSFile.identity)~"/>


   78     <Delete Files="build.xml~"/>


   79   </Target>


   80 


   81 </Project>
~~~

Important line:
~~~
<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
~~~
___

### ***Csc (tarea)***

https://docs.microsoft.com/es-es/visualstudio/msbuild/csc-task?view=vs-2019

### ***Tutorial: Crear un archivo de proyecto de MSBuild desde cero***

https://docs.microsoft.com/es-es/visualstudio/msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch?view=vs-2019

~~~
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <ItemGroup>
    <Compile Include="helloworld.cs" />
  </ItemGroup>
  <Target Name="Build">
    <Csc Sources="@(Compile)"/>  
  </Target>
</Project>
~~~
### ***Procedimiento Seleccionar los archivos que se van a compilar***

https://docs.microsoft.com/es-es/visualstudio/msbuild/how-to-select-the-files-to-build?view=vs-2019

~~~
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Builtdir>built</Builtdir>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="Form1.cs"/>
        <CSFile Include="AssemblyInfo.cs"/>

        <Reference Include="System.dll"/>
        <Reference Include="System.Data.dll"/>
        <Reference Include="System.Drawing.dll"/>
        <Reference Include="System.Windows.Forms.dll"/>
        <Reference Include="System.XML.dll"/>
    </ItemGroup>

    <Target Name="PreBuild">
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>
    </Target>

    <Target Name="Compile" DependsOnTargets="PreBuild">
        <Csc Sources="@(CSFile)"
            References="@(Reference)"
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"
            TargetType="exe" />
    </Target>
</Project>
~~~

___

### ***Learn Web Assembly (WASM) In 1 Video***

https://www.youtube.com/watch?v=LNqicUieSqI&t=50s

Here show how to write and use javasscript code for loading wasm files with vanila js code.

### ***Getting Started with the sample***

https://github.com/mono/mono/blob/master/sdks/wasm/docs/getting-started/sample.md

In this url it is showing how to compile c# code from sdk of webassembly for mono and after that and with dll created,it create wasm files and html scaffolding from packager.exe that belong sdk mono wasm tools

### ***WebAssembly packager.exe***

https://github.com/mono/mono/blob/master/sdks/wasm/docs/packager.md

Explanations about packager.exe tool from sdk webassembly of mono and it gives a full information about how to use this tool on command line prompt.

### ***Uno.Wasm.Bootstrap***

https://github.com/nventive/Uno.Wasm.Bootstrap/blob/master/Readme.md

### ***Introducing Uno WebAssembly Projects and Debugging***

https://hackernoon.com/introducing-uno-webassembly-projects-and-debugging-f360d4776df3

~~~
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netstandard2.0</TargetFramework>
    <WasmHead>true</WasmHead>
    <DefineConstants>__WASM__</DefineConstants>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Uno.UI" Version="1.42.0-dev.395" />
    <DotNetCliToolReference Include="Uno.Wasm.Bootstrap.Cli" Version="1.0.0-dev.112" />
  </ItemGroup>
  ~~~

