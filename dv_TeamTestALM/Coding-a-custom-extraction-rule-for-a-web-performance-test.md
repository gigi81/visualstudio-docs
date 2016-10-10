---
title: "Coding a custom extraction rule for a web performance test"
ms.custom: na
ms.date: 10/03/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bcc5712-6cc6-4f59-8933-6e8078318c45
caps.latest.revision: 50
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
# Coding a custom extraction rule for a web performance test
You can create your own extraction rules. To do this, you derive your own rules from an extraction rule class. Extraction rules derive from the <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule?qualifyHint=False> base class.  
  
 Visual Studio Enterprise provides some predefined extraction rules. For more information, see [Using Validation and Extraction Rules in Web Performance Tests](../Topic/Using%20Validation%20and%20Extraction%20Rules%20in%20Web%20Performance%20Tests.md).  
  
> [!NOTE]
>  You can also create custom validation rules. For more information, see [Create custom code and plug-ins for load tests](../dv_TeamTestALM/Create-custom-code-and-plug-ins-for-load-tests.md).  
  
 **Requirements**  
  
-   Visual Studio Enterprise  
  
### To create a custom extraction rule  
  
1.  Open a Test Project that contains a Web performance test.  
  
2.  (Optional) Create a separate Class library project in which to store your extraction rule.  
  
    > [!IMPORTANT]
    >  You can create the class in the same project that your tests are in. However, if you want to reuse the rule, it is better to create a separate Class library project in which to store your rule. If you create a separate project, you must complete the optional steps in this procedure.  
  
3.  (Optional) In the Class library project, add a reference to the Microsoft.VisualStudio.QualityTools.WebTestFramework dll.  
  
4.  Create a class that derives from the <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule?qualifyHint=False> class. Implement the <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract?qualifyHint=False> and <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.RuleName?qualifyHint=False> members.  
  
5.  (Optional) Build the new Class library project.  
  
6.  (Optional) In the Test Project, add a reference to the Class library project that contains the custom extraction rule.  
  
7.  In the Test Project, open a Web performance test in the **Web Performance Test Editor**.  
  
8.  To add the custom extraction rule, right-click a Web performance test request and select **Add Extraction Rule**.  
  
     The **Add Extraction Rule** dialog box appears. You will see your custom validation rule in the **Select a rule** list, together with the predefined validation rules. Select your custom extraction rule and then choose **OK**.  
  
9. Run your Web performance test.  
  
## Example  
 The following code shows an implementation of a custom extraction rule. This extraction rule extracts the value from a specified input field. Use this example as a starting point for your own custom extraction rules.  
  
```c#  
using System;  
using System.Collections.Generic;  
using Microsoft.VisualStudio.TestTools.WebTesting;  
using System.Globalization;  
  
namespace ClassLibrary2  
{  
    //-------------------------------------------------------------------------  
    // This class creates a custom extraction rule named "Custom Extract Input"  
    // The user of the rule specifies the name of an input field, and the  
    // rule attempts to extract the value of that input field.  
    //-------------------------------------------------------------------------  
    public class CustomExtractInput : ExtractionRule  
    {  
        /// Specify a name for use in the user interface.  
        /// The user sees this name in the Add Extraction dialog box.  
        //---------------------------------------------------------------------  
        public override string RuleName  
        {  
            get { return "Custom Extract Input"; }  
        }  
  
        /// Specify a description for use in the user interface.  
        /// The user sees this description in the Add Extraction dialog box.  
        //---------------------------------------------------------------------  
        public override string RuleDescription  
        {  
            get { return "Extracts the value from a specified input field"; }  
        }  
  
        // The name of the desired input field  
        private string NameValue;  
        public string Name  
        {  
            get { return NameValue; }  
            set { NameValue = value; }  
        }  
  
        // The Extract method.  The parameter e contains the web performance test context.  
        //---------------------------------------------------------------------  
        public override void Extract(object sender, ExtractionEventArgs e)  
        {  
            if (e.Response.HtmlDocument != null)  
            {  
                foreach (HtmlTag tag in e.Response.HtmlDocument.GetFilteredHtmlTags(new string[] { "input" }))  
                {  
                    if (String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase))  
                    {  
                        string formFieldValue = tag.GetAttributeValueAsString("value");  
                        if (formFieldValue == null)  
                        {  
                            formFieldValue = String.Empty;  
                        }  
  
                        // add the extracted value to the web performance test context  
                        e.WebTest.Context.Add(this.ContextParameterName, formFieldValue);  
                        e.Success = true;  
                        return;  
                    }  
                }  
            }  
            // If the extraction fails, set the error text that the user sees  
            e.Success = false;  
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name);  
        }  
    }  
}  
```  
  
```vb#  
Imports System  
Imports System.Collections.Generic  
Imports Microsoft.VisualStudio.TestTools.WebTesting  
Imports System.Globalization  
  
Namespace ClassLibrary2  
  
    '-------------------------------------------------------------------------  
    ' This class creates a custom extraction rule named "Custom Extract Input"  
    ' The user of the rule specifies the name of an input field, and the  
    ' rule attempts to extract the value of that input field.  
    '-------------------------------------------------------------------------  
    Public Class CustomExtractInput  
        Inherits ExtractionRule  
  
        ' Specify a name for use in the user interface.  
        ' The user sees this name in the Add Extraction dialog box.  
        '---------------------------------------------------------------------  
        Public Overrides ReadOnly Property RuleName() As String  
            Get  
                Return "Custom Extract Input"  
            End Get  
        End Property  
  
        ' Specify a description for use in the user interface.  
        ' The user sees this description in the Add Extraction dialog box.  
        '---------------------------------------------------------------------  
        Public Overrides ReadOnly Property RuleDescription() As String  
            Get  
                Return "Extracts the value from a specified input field"  
            End Get  
        End Property  
  
        ' The name of the desired input field  
        Private NameValue As String  
        Public Property Name() As String  
            Get  
                Return NameValue  
            End Get  
            Set(ByVal value As String)  
                NameValue = value  
            End Set  
        End Property  
  
        ' The Extract method.  The parameter e contains the web performance test context.  
        '---------------------------------------------------------------------  
        Public Overrides Sub Extract(ByVal sender As Object, ByVal e As ExtractionEventArgs)  
  
            If Not e.Response.HtmlDocument Is Nothing Then  
  
                For Each tag As HtmlTag In e.Response.HtmlDocument.GetFilteredHtmlTags(New String() {"input"})  
  
                    If String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase) Then  
  
                        Dim formFieldValue As String = tag.GetAttributeValueAsString("value")  
                        If formFieldValue Is Nothing Then  
  
                            formFieldValue = String.Empty  
                        End If  
  
                        ' add the extracted value to the web performance test context  
                        e.WebTest.Context.Add(Me.ContextParameterName, formFieldValue)  
                        e.Success = True  
                        Return  
                    End If  
                Next  
            End If  
            ' If the extraction fails, set the error text that the user sees  
            e.Success = False  
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name)  
        End Sub  
    End Class  
end namespace  
```  
  
 The <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract?qualifyHint=False> method contains the core functionality of an extraction rule. The <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract?qualifyHint=False> method in the previous example takes an <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionEventArgs?qualifyHint=False> that provides the response generated by the request this extraction rule covers. The response contains an <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument?qualifyHint=False> which contains all the tags in the response. Input tags are filtered out of the <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument?qualifyHint=False>. Each input tag is examined for an attribute called `name` whose value equals the user supplied value of the `Name` property. If a tag with this matching attribute is found, an attempt is made to extract a value that is contained by the `value` attribute, if a value attribute exists. If it exists, the name and value of the tag are extracted and added to the web performance test context. The extraction rule passes.  
  
## See Also  
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractAttributeValue?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractFormField?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHttpHeader?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractRegularExpression?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractText?qualifyHint=False>   
 <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHiddenFields?qualifyHint=False>   
 [Using Validation and Extraction Rules in Web Performance Tests](../Topic/Using%20Validation%20and%20Extraction%20Rules%20in%20Web%20Performance%20Tests.md)   
 [How to: Add an Extraction Rule to a Web Performance Test](../Topic/How%20to:%20Add%20an%20Extraction%20Rule%20to%20a%20Web%20Performance%20Test.md)   
 [Adding validation and extraction rules to a web performance test](../Topic/Adding%20validation%20and%20extraction%20rules%20to%20a%20web%20performance%20test.md)   
 [Coding a custom validation rule for a web performance test](../dv_TeamTestALM/Coding-a-custom-validation-rule-for-a-web-performance-test.md)