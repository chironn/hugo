---
title: "Publish .NetCore"
author: "Chiron"
tags: ["Theme", "Hugo"]
categories: [".NetCore"]
date: 2018-09-20T20:37:18+08:00
draft: false
---
## Preparations

NET Core开发要求:

Visual Studio 2017

.NET Core 2.0 SDK

一个基于.Net Core2.0开发平台的项目:

可以新创建一个.NET Core控制台项目

也可以将原有项目迁移至.net core开发平台

## Method

Portable applications（便携应用）：

需要目标主机安装有.NET Core的运行时，对比现在的情况就是需要机器安装.NET Framework。

Self-contained application（自宿主应用）：

这种方式会将运行时与程序共同打包，也就意味着目标机器不需要装.NET Core运行时（这种方式是将Core CLR打包进去）。

备注：

由于自宿主应用方式需要编辑“project.json”文件，但是在.net core1.1之后，微软又回归了.csproj文件。所以目前采用的是便携应用。

## Operation

使用（CLI）命令行发布

```
##运行“CMD”（命令提示符），定位到项目路径。
##使用发布命令 “dotnet Publish -c release”  发布完成，可以去“release”目录中“netcoreapp2.1”文件夹下找到“publish”文件夹。
##备注：
$ -f, --framework [FID]
##指定运行框架，如：netcoreapp2.1，net45，net451等，具体  由“project.json”中的“framework”节点指定。
$ -r, --runtime [RID]
##指定应用程序运行时（自宿主应用），这种方式将会把指定平台的Core CLR打包进去。
##格式：[os].[version]-[arch]
##例子：win7-x64、win7-x86、win10-x64、win10-x86、rhel.7.0-x64、ubuntu.14.04-x64、osx.10.10-x64等。
$ -b, --build-base-path [DIR]
##指定输出路径根。
$ -o, –output
##指定具体的输出路径,会与“-b”命令配合。
##默认路径：
$ Portable applications：./bin/[configuration]/[framework]//app
$ Self-contained application：./bin/[configuration]/[framework]/[runtime]/app
$ --version-suffix [VERSION_SUFFIX]
##替换在“project.json”文件中依赖包版本号中的*。
$ -c, --configuration [Debug|Release]
##发布配置，默认为：Debug。
```

使用Visual Studio发布

```
右键发布，可选参数请参考上面的备注内容
```