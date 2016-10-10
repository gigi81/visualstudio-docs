---
title: "Automation Model"
ms.custom: na
ms.date: 10/10/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ddc192-96ff-46dc-a1fe-df4eb5c62c84
caps.latest.revision: 16
manager: douge
translation.priority.ht: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - ru-ru
  - zh-cn
  - zh-tw
translation.priority.mt: 
  - cs-cz
  - pl-pl
  - pt-br
  - tr-tr
---
# Automation Model
The automation model provides an alternative to VSPackages for extending Visual Studio. Known in earlier versions of Visual Studio as the extensibility model, the automation model is a programming interface that gives you access to the underlying routines that drive the integrated development environment (IDE), and lets you customize, adjust, and automate it.  
  
## VSPackages and Automation  
 The Visual Studio SDK documentation focuses on VSPackages, which offer more development potential than the automation model. For example, you can write code against the objects in the automation model to customize a language, such as Visual Basic. However, you cannot add a new language to the IDE by using the automation model. To add a new language to the environment, you must develop a VSPackage.  
  
 Together, the automation model and the VSPackage model compose a two-pronged approach to extensibility in Visual Studio. Extensibility is the capacity to enhance and extend the functionality of the IDE. Automation refers to user-created code and tools that automate tasks in the existing environment and programmatically drive the IDE. VSPackages, on the other hand, let you add new functionality to the IDE. A VSPackage is a co-creatable object; that is, it has a class factory and makes itself available to the IDE by implementing the interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage?qualifyHint=False>.  
  
 Add-ins and wizards use the automation model to control or extend the functionality of the IDE by using its automation interfaces. Typically, Microsoft includes many add-ins with Visual Studio. You can use add-ins to integrate new commands on the toolbars and menus, to add tool windows, or to automate certain tasks that you perform regularly in Visual Studio.  
  
 As a VSPackage developer, you should contribute to the automation model. For example, if you add a new language to Visual Studio by using the Visual Studio SDK, your language should provide a robust code model that extends the pre-existing one. For more information, see [Contributing to the Automation Model](../Topic/Contributing%20to%20the%20Automation%20Model.md).  
  
## See Also  
 [VSPackages](../Topic/VSPackages.md)   
 [Contributing to the Automation Model](../Topic/Contributing%20to%20the%20Automation%20Model.md)