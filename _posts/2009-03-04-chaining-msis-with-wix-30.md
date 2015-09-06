---
layout: post
title: Chaining MSIs with WiX 3.0
date: 2009-03-04 11:15
author: kal
comments: true
categories: [.NET Development, Installers, WiX]
---
In some deployment scenarios it is not possible to bundle everything into a single installer. This may be because you need to install some third-party software, or because your build process forces you to split a single product across multiple MSIs.

Although there is not much in the WiX documentation about this, it is possible to chain multiple MSI installers in a setup.exe wrapper so that the installers execute one after the other. The key to this is the setupbld.exe command-line tool that comes with the WiX 3.0 installation. Jon Torresdal has written a useful article on <a href="http://blog.torresdal.net/Trackback.aspx?guid=001283d1-5c8e-4b16-b369-7008675e2e72">using setupbld.exe to force elevated privileges for an installer under Vista</a>, and I recommend starting there for an explanation of how to prepare your build to generate setup.exe files. In addition to doing this, setupbld.exe can combine multiple MSI files into a single setup.exe installer. To do this use a command line like:

<code>setupbld.exe -out $(TargetDir)setup.exe -msu FirstInstaller.msi -msu SecondInstaller.msi -setup $(ProjectDir)setup.exe</code>
