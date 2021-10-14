---
title: "SSH X server on Windows"
date: 2021-10-14
categories:
  - note
tags:
  - powershell
  - x server
toc: true
toc_label: "Outline"
toc_icon: "box-open"
---

## Install VcXsrv

```powershell
scoop install vcxsrv
```

## Setup xLauncher

```powershell
xlaunch.exe
```

![xlaunch-1]({{ site.url }}{{ site.baseurl }}/assets/images/xlauch-1.jpg)
![xlaunch-1]({{ site.url }}{{ site.baseurl }}/assets/images/xlauch-2.jpg)
![xlaunch-1]({{ site.url }}{{ site.baseurl }}/assets/images/xlauch-3.jpg)
![xlaunch-1]({{ site.url }}{{ site.baseurl }}/assets/images/xlauch-4.jpg)

## Add env variable to PowerShell PROFILE

```powershell
# vi $PROFILE, and add below line
$env:DISPLAY='localhost:0.0'
```

## Test out and finish!

```powershell
ssh -Y server
```

```bash
xclock
```
