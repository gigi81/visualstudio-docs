---
title: "CA1725: Parameter names should match base declaration"
ms.custom: na
ms.date: 10/03/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - vs-devops-test
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
caps.latest.revision: 11
manager: douge
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# CA1725: Parameter names should match base declaration
|||  
|-|-|  
|TypeName|ParameterNamesShouldMatchBaseDeclaration|  
|CheckId|CA1725|  
|Category|Microsoft.Naming|  
|Breaking Change|Breaking|  
  
## Cause  
 The name of a parameter in an externally visible method override does not match the name of the parameter in the base declaration of the method, or the name of the parameter in the interface declaration of the method.  
  
## Rule Description  
 Consistent naming of parameters in an override hierarchy increases the usability of the method overrides. A parameter name in a derived method that differs from the name in the base declaration can cause confusion about whether the method is an override of the base method or a new overload of the method.  
  
## How to Fix Violations  
 To fix a violation of this rule, rename the parameter to match the base declaration. The fix is a breaking change for COM visible methods.  
  
## When to Suppress Warnings  
 Do not suppress a warning from this rule except for COM visible methods in libraries that have previously shipped.