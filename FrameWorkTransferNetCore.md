---
title: "Get the .Net FrameWork Project into .Net Core"
author: "Chiron"
tags: ["Theme", "Hugo"]
categories: [".NetCore"]
date: 2018-09-20T20:27:39+08:00
draft: false
---
## Introduction
在迁移.net core的过程中，第一步就是要把.net framework 工程的目标框架改为.net core2.1（最新框架版本）

以下是查阅到最简便的一种方式，采用通过编辑.csproj文件，强制把工程迁移到.net core下：

## Operation
通过VS2017打开.net framework 解决方案，卸载指定的项目后，打开.csproj文件

移除两个标签为import的引用

移除 Release、Debug编译的配置信息

```
$ <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
$ <PlatformTarget>AnyCPU</PlatformTarget>
$ <DebugSymbols>true</DebugSymbols>
$ <DebugType>full</DebugType>
$ <Optimize>false</Optimize>
$ <OutputPath>bin\Debug\</OutputPath>
$ <DefineConstants>DEBUG;TRACE</DefineConstants>
$ <ErrorReport>prompt</ErrorReport>
$ <WarningLevel>4</WarningLevel>
$ </PropertyGroup>
$ <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
$ <PlatformTarget>AnyCPU</PlatformTarget>
$ <DebugType>pdbonly</DebugType>
$ <Optimize>true</Optimize>
$ <OutputPath>bin\Release\</OutputPath>
$ <DefineConstants>TRACE</DefineConstants>
$ <ErrorReport>prompt</ErrorReport>
$ <WarningLevel>4</WarningLevel>
$ </PropertyGroup>
```

修改 Project节点属性

```
$ <Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
##替换为
$ <Project Sdk="Microsoft.NET.Sdk">
```

移除TargetFrameworkVersion信息
```
##增加信息:
$ <TargetFramework>netcoreapp2.1</TargetFramework>
```

重新加载项目

在已经加载的 .net core项目上，继续编辑csproj文件

移除文件列表信息

```
$ <ItemGroup>
$ <Compile Include="Entity\FromIncomBufferEntity.cs" />
$ <Compile Include="Entity\FromInComEntity.cs" />
$ <Compile Include="Logic\DownloadLogic.cs" />
$ <Compile Include="Logic\UploadLogic.cs" />
$ <Compile Include="MainService.cs" />
$ <Compile Include="Parse\FromInComDownEntityParse.cs" />
$ <Compile Include="Parse\FromInComUPEntityParse.cs" />
$ <Compile Include="Program.cs" />
$ <Compile Include="Properties\AssemblyInfo.cs" />
$ <Compile Include="Protocol\ProtocolParseDownload.cs" />
$ <Compile Include="Protocol\ProtocolParseUpload.cs" />
$ </ItemGroup>
$ <ItemGroup>
$ <None Include="App.config" />
$ <None Include="IniFiles\communicateQueue.config">
$ <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
$ </None>
$ <None Include="packages.config" />
$ </ItemGroup>
```

移除AssemblyInfo.cs文件

移除.net framework工程中隐藏的文件。因为.net core 工程不支持排除文件，所以在完成上述迁移后，原来隐藏的文件会自动添加到工程中，对这些垃圾文件，请识别后，手工删除即可。

重新添加nuget包引用。.net framework 对nuget包的引用信息是存储到packages.config中的。此文件已经在.net core中移除。请根据packages.config信息，在项目中重新添加nuget引用。引用信息将会自动添加到csproj文件中。

编译工程

## Tips
备注

1.注意关于涉及控制台样式设计部分的代码。

2.注意关于设计路径设置部分的代码。


