---
title: "InvokeDelegate"
ms.custom: na
ms.date: 10/02/2016
ms.prod: .net-framework-4.6
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
caps.latest.revision: 3
manager: erikre
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
# InvokeDelegate
The **InvokeDelegate** designer is used to create and configure an <xref:System.Activities.Statements.InvokeDelegate?qualifyHint=False> activity.  
  
## The InvokeDelegate Activity  
 The <xref:System.Activities.Statements.InvokeDelegate?qualifyHint=False> calls a public delegate.  
  
### Using the InvokeDelegate Activity Designer  
 The **InvokeDelegate** activity designer can be found in the **Primitives** category of the **Toolbox**, which is accessed by clicking the **Toolbox** tab Workflow Designer (Alternatively, select **Toolbar** from the **View** menu, or CRTL+ALT+X.)  
  
 The **InvokeDelegate** activity designer can be dragged from the **Toolbox** and dropped on to the Workflow Designer surface where ever activities are usually placed, such as inside a <xref:System.Activities.Statements.Sequence?qualifyHint=False>. This creates an <xref:System.Activities.Statements.InvokeDelegate?qualifyHint=False> activity with a default <xref:System.Activities.Activity.DisplayName?qualifyHint=False> of InvokeDelegate. The <xref:System.Activities.Activity.DisplayName?qualifyHint=False> can be edited in the header of the **InvokeDelegate** activity designer or in the **DisplayName** box of the property grid.  
  
### The InvokeDelegate Properties  
 The following table shows the <xref:System.Activities.Statements.InvokeDelegate?qualifyHint=False> properties and describes how they are used in the designer. These properties can be edited in property grid and some can be edited on Workflow Designerdesigner surface.  
  
|Property Name|Required|Usage|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName?qualifyHint=False>|False|The friendly name of the <xref:System.Activities.Statements.InvokeDelegate?qualifyHint=False> activity. The default value is InvokeDelegate.<br /><br /> Although the <xref:System.Activities.Activity.DisplayName?qualifyHint=False> is not strictly required, it is a best practice to use one.|  
|<xref:System.Activities.Statements.InvokeDelegate.Delegate?qualifyHint=False>|True|The name of the <xref:System.Activities.Statements.ActivityDelegate?qualifyHint=False> to be called when the activity executes. This property can be edited on designer surface. This is a mandatory property.|  
|<xref:System.Activities.Statements.InvokeMethod.DelegateArguments?qualifyHint=False>|False|The argument collection of the called delegate. The keys are the names of the <xref:System.Activities.Statements.ActivityDelegateParameter?qualifyHint=False> objects on the <xref:System.Activities.Statements.ActivityDelegate?qualifyHint=False> and the values are the arguments whose expressions are evaluated and assigned to the corresponding <xref:System.Activities.Statements.ActivityDelegateParameter?qualifyHint=False> objects. In the property grid, click the ellipses button in the **DelegateArguments** field, it displays the **DelegateArguments** dialog to let you set this property. Click the **Create Argument** field to add the arguments.|  
  
## See Also  
 [How to: Define and consume activity delegates in the Workflow Designer](../WF_Design/How-to--Define-and-consume-activity-delegates-in-the-Workflow-Designer.md)