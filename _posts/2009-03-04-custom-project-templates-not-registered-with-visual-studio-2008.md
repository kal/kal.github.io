---
layout: post
title: Custom Project Templates Not Registered with Visual Studio 2008
date: 2009-03-04 09:00
author: kal
comments: true
categories: [.NET Development, Installers, VS2008 SDK, WiX]
---
At the moment I'm in the middle of updating the NetworkedPlanet NPCL Schema Editor so that it works with Visual Studio 2008, a task that sets new standards for the word 'frustrating'. Anyway, having got my whine out of the way, I did find the fix for something which no amount of Googling revealed and I'm writing it up here in the hope that it might save some other poor soul from a bruised forehead.

One of the key steps in deploying a Visual Studio package is writing all of the correct package registration details into the target machine's registry. For my deployment I wanted to use the WiX toolset to create my installer. According to <a href="http://msdn.microsoft.com/en-us/library/bb707481.aspx">this MSDN article</a>, you can use the tool regpkg.exe in the Visual Studio SDK to generate a .wxs file that contains the necessary WiX magic to get all of the package registration entries written by the installer. Its then just a question of writing the rest of the installer to put files in the right place, include the .wxs file with the right sort of invocation and off you go.

On testing the deployment on a clean Visual Studio installation I found that the project template I had created to allow users to choose to create an NPCL project didn't show up in the New Project dialog box. I could see that my Project Package was properly registered with Visual Studio on the target machine (as proof of which I could see it displayed in the list of registered extensions in the Help &gt; About dialog box). I could also see that the project template was installed into the Common7IDEProjectTemplates directory as expected.

After much cursing, rebuilding, redeploying and retesting I finally went back to first principles and decided to compare my package registration key by key with another project package extension that I knew worked - in this case the WiX installation. What I found was interesting. This is the code generated for my project package's template registration by regpgk.exe:

<code xml:space="preserve">
&lt;Registry Root="HKLM" Key="SoftwareMicrosoftVisualStudio9.0NewProjectTemplatesTemplateDirs{41a84a7e-462c-4a74-9559-3c2568001dc2}/1"&gt;
&lt;Registry Name="SortPriority" Value="100" Type="integer" /&gt;
&lt;Registry Name="TemplatesDir" Value="[$ComponentPath].NullPath" Type="string" /&gt;
&lt;/Registry&gt;
</code>

And here, for comparison is the Wix registration

<code>&lt;RegistryKey Key="NewProjectTemplatesTemplateDirs$(var.WixVsPackageGuid)" Action="createAndRemoveOnUninstall"&gt;
&lt;RegistryKey Key="/1"&gt;
&lt;RegistryValue Value="WiX" Type="string" /&gt;
&lt;RegistryValue Name="SortPriority" Value="30" Type="integer" /&gt;
&lt;RegistryValue Name="TemplatesDir" Value="[VsProjectTemplatesWixDir$(var.VsVersion)]" Type="string" /&gt;</code><code>
&lt;/RegistryKey&gt;
&lt;/RegistryKey&gt;
</code>

The key difference is that the generated registration doesn't set the default value for the /1 registry key. It appears that this default key value is actually the label for the project type that is displayed in the New Project dialog box, but the regpkg.exe tool doesn't generate a &lt;Registry&gt; tag to set its value. In the WiX schema there appear to be multiple ways to do this, and I found the syntax below worked for me:

<code>&lt;Registry Root="HKLM" Key="SoftwareMicrosoftVisualStudio9.0NewProjectTemplatesTemplateDirs{41a84a7e-462c-4a74-9559-3c2568001dc2}/1" Type="string" Value="NPCL"&gt;
&lt;Registry Name="SortPriority" Value="100" Type="integer" /&gt;
&lt;Registry Name="TemplatesDir" Value="[ptNPCL]" Type="string" /&gt;
&lt;/Registry&gt;</code>

As an aside, the regpkg.exe generates a .wxs file that uses the schema supported by WiX 2.0. I'm using WiX 3.0 for my installer, and it reports these &lt;Registry&gt; elements as deprecated. However, it does work and I can now get on with finishing off my installer.

I hope that this tip saves some one the hours that I will never get back again ;-)
