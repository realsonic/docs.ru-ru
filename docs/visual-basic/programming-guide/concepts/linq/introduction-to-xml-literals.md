---
title: Общие сведения об XML-литералов в Visual Basic2
ms.custom: ''
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 94fc0e03-978e-4c08-ab6c-0dc3c1e64f10
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 112c1d898c3cdf14b52d843dee8f5a51002be858
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="introduction-to-xml-literals-in-visual-basic"></a>Знакомство с литералами XML в Visual Basic
Этот раздел содержит сведения о создании XML-деревьев в Visual Basic.  
  
 Сведения об использовании результатов запросов LINQ как содержимого XML-дерева см. в разделе [функциональное сборка (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
 Дополнительные сведения о XML-литералов в Visual Basic см. в разделе [Общие сведения о LINQ to XML в Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md).  
  
## <a name="creating-xml-trees"></a>Создание деревьев XML  
 В следующем примере показано, как создать объект <xref:System.Xml.Linq.XElement>. В этом случае дерево `contacts`:  
  
```vb  
Dim contacts As XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone>206-555-0144</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
### <a name="creating-an-xelement-with-simple-content"></a>Создание объекта XElement с простым содержимым  
 Следующим образом можно создать объект <xref:System.Xml.Linq.XElement> с простым содержимым.  
  
```vb  
Dim n as XElement = <Customer>Adventure Works</Customer>  
Console.WriteLine(n)   
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
### <a name="creating-an-empty-element"></a>Создание пустого элемента  
 Следующим образом можно создать пустой объект <xref:System.Xml.Linq.XElement>:  
  
```vb  
Dim n As XElement = <Customer/>  
Console.WriteLine(n)  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Customer />  
```  
  
### <a name="using-embedded-expressions"></a>Использование внедренных выражений  
 Важной характеристикой XML-литералов является использование внедренных выражений. Внедренные выражения позволяют вычислять выражения и вставлять результаты вычисления в XML-дерево. Если результат выражения имеет тип объекта <xref:System.Xml.Linq.XElement>, элемент вставляется в дерево. Если результат выражения имеет тип объекта <xref:System.Xml.Linq.XAttribute>, атрибут вставляется в дерево. Элементы и атрибуты можно вставлять в дерево, только если они допустимы.  
  
 Важно отметить, что только простое выражение может входить во внедренное выражение. Можно внедрять несколько инструкций. Если выражение выходит за пределы одной строки, нужно использовать знак объединения строк.  
  
 Если использовать внедренное выражение для добавления существующих узлов (включая элементы) и атрибутов в новое XML-дерево и если существующие узлы уже имеют родителей, узлы копируются. Скопированные узлы присоединяются к новому XML-дереву. Если существующие узлы не имеют родителей, узлы просто присоединяются к новому XML-дереву. Это демонстрирует последний пример из данного раздела.  
  
 В следующем примере используется внедренное выражение для вставки элементов в дерево:  
  
```vb  
xmlTree1 As XElement = _  
    <Root>  
        <Child>Contents</Child>  
    </Root>  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child> %>  
    </Root>  
Console.WriteLine(xmlTree2)  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Root>  
  <Child>Contents</Child>  
</Root>  
```  
  
### <a name="using-embedded-expressions-for-content"></a>Использование внедренных выражений в содержимом  
 Можно использовать внедренное выражение для создания содержимого элемента:  
  
```vb  
Dim str As String  
str = "Some content"  
Dim root As XElement = <Root><%= str %></Root>  
Console.WriteLine(root)  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Root>Some content</Root>  
```  
  
### <a name="using-a-linq-query-in-an-embedded-expression"></a>Использование запросов LINQ во внедренном выражении  
 Можно использовать результаты запросов LINQ для создания содержимого элемента:  
  
```vb  
Dim arr As Integer() = {1, 2, 3}  
  
Dim n As XElement = _  
    <Root>  
        <%= From i In arr Select <Child><%= i %></Child> %>  
    </Root>  
  
Console.WriteLine(n)  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Child>3</Child>  
</Root>  
```  
  
### <a name="using-embedded-expressions-for-node-names"></a>Использование внедренных выражений для создания имен узлов  
 Можно также использовать внедренные выражения для вычисления имен атрибутов, значений атрибутов, имен элементов и значений элементов:  
  
```vb  
Dim eleName As String = "ele"  
Dim attName As String = "att"  
Dim attValue As String = "aValue"  
Dim eleValue As String = "eValue"  
Dim n As XElement = _  
    <Root <%= attName %>=<%= attValue %>>  
        <<%= eleName %>>  
            <%= eleValue %>  
        </>  
    </Root>  
Console.WriteLine(n)  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Root att="aValue">  
  <ele>eValue</ele>  
</Root>  
```  
  
### <a name="cloning-vs-attaching"></a>Сравнение клонирования и  присоединения  
 Как уже было сказано, если использовать внедренное выражение для добавления существующих узлов (включая элементы) и атрибутов в новое XML-дерево и если существующие узлы уже имеют родителей, узлы копируются и присоединяются к новому XML-дереву. Если существующие узлы не имеют родителей, узлы просто присоединяются к новому XML-дереву.  
  
```vb  
' Create a tree with a child element.  
Dim xmlTree1 As XElement = _  
    <Root>  
        <Child1>1</Child1>  
    </Root>  
  
' Create an element that is not parented.  
Dim child2 As XElement = <Child2>2</Child2>  
  
' Create a tree and add Child1 and Child2 to it.  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child1>(0) %>  
        <%= child2 %>  
    </Root>  
  
' Compare Child1 identity.  
Console.WriteLine("Child1 was {0}", _  
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _  
    "attached", "cloned"))  
  
' Compare Child2 identity.  
Console.WriteLine("Child2 was {0}", _  
    IIf(child2 Is xmlTree2.Element("Child2"), _  
    "attached", "cloned"))  
```  
  
 В этом примере выводятся следующие данные:  
  
```  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>См. также  
 [Создание деревьев XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
