---
layout: post
title: MVC4 List view template error: Column Attribute is an ambiguous reference
date: 2012-11-07 10:59
author: kal
comments: true
categories: [.NET Development]
---
I came across this problem when trying to create a strongly-typed MVC4 view using the List scaffolding template in Visual Studio 2010. When trying to add the view, an error is generated that reports:

c:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\ItemTemplates\CSharp\Web\MVC 4\CodeTemplates\AddView\CSHTML\List.tt(206,35): error CS0104: Compiling transformation: 'ColumnAttribute' is an ambiguous reference between 'System.ComponentModel.DataAnnotations.ColumnAttribute' and 'System.Data.Linq.Mapping.ColumnAttribute'

The fix for this is to locate that .TT file (c:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\ItemTemplates\CSharp\Web\MVC 4\CodeTemplates\AddView\CSHTML\List.tt) and on line 206 change

var column = attribute as ColumnAttribute;

to

var column = attribute as System.Data.Linq.Mapping.ColumnAttribute;

Strangely, this error doesn't occur in a VS2012 installation so it must have got fixed at some point but even after reinstalling MVC4 into VS2010 the error still came up.

Hopefully this post will help someone else find the fix !

Edit: This problem seems to also affect the Create.tt template (on line 122), the Delete.tt template (line 174), the Details template (line 179) and the Edit template (line 229) - the same fix works in all cases.
