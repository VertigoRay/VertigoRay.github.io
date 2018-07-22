---
layout: post
title: QuserObject
author: VertigoRay
img: //i.imgur.com/OGS4h59.jpg
comments: true
tags:
- PowerShell
- PoSh
- PowerShell Gallery
---
[![Build status](https://ci.appveyor.com/api/projects/status/d88b15ilqgkqgo4e?svg=true)](https://ci.appveyor.com/project/VertigoRay/quserobject)
[![codecov](https://codecov.io/gh/UNT-CAS/QuserObject/branch/master/graph/badge.svg)](https://codecov.io/gh/UNT-CAS/QuserObject)
[![version](https://img.shields.io/powershellgallery/v/QuserObject.svg)](https://www.powershellgallery.com/packages/QuserObject)
[![downloads](https://img.shields.io/powershellgallery/dt/QuserObject.svg?label=downloads)](https://www.powershellgallery.com/packages/QuserObject)

Run `quser.exe` and return a proper PowerShell Object.
I discussed this [on my blog](/2018/04/27/terminal_server_sessions) to enhance [a StackOverflow answer](https://stackoverflow.com/a/49042770/615422).
I ended up making this into a module: [QuserObject](https://www.powershellgallery.com/packages/QuserObject).
The source is on [GitHub](https://github.com/UNT-CAS/QuserObject).

# Quick Setup

1. Install *QuserObject*: `Install-Module QuserObject`.
1. Import *QuserObject*: `Import-Module QuserObject`.
1. Start *QuserObject*: `Get-Quser`.

# Examples

## Quick Example

This will return the `quser.exe` results for the current computer (aka `localhost`).

```powershell
Get-QuserObject
```

## Target a Server

This will return the `quser.exe` results for `ThisServer`.

```powershell
Get-QuserObject -ServerName 'ThisServer'
```

## Target Multiple Servers

This will return the `quser.exe` results for `ThisServer` and `ThatServer`.

```powershell
Get-QuserObject -ServerName 'ThisServer', 'ThatServer'
```

## Pipeline Multiple Servers

This will return the `quser.exe` results for `ThisServer` and `ThatServer`.

```powershell
@('ThisServer', 'ThatServer') | Get-QuserObject
```

## AD Computer

This will return the `quser.exe` results for `ThisServer`.
The value is piped from a `Get-ADComputer` query.

```powershell
Get-ADComputer 'ThisServer' | Get-QuserObject
```

## AD Computer with Different Property

This will return the `quser.exe` results for `ThisServer`.
This value is piped from a `Get-ADComputer` query and using the AD computer `DNSHostName` property instead of the default `Name` property.

```powershell
Get-ADComputer 'ThisServer' | Get-QuserObject -Property 'DNSHostName'
```