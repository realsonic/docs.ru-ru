---
title: "Практическое руководство. Выполнение потокового преобразования крупных XML-документов (C#) | Документы Майкрософт"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 5f16d1f8-5370-4b55-b0c8-e497df163037
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 02919c2e1e76991a3b37533da57b5c3ce4ded3c6
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-perform-streaming-transform-of-large-xml-documents-c"></a>Практическое руководство. Выполнение потокового преобразования крупных XML-документов (C#)
Иногда необходимо преобразовывать большие XML-файлы, при этом приложение должно быть написано так, чтобы используемый им объем памяти был прогнозируемым. Если вставить в XML-дерево очень большой XML-файл, то объем используемой памяти будет пропорциональным размеру файла (то есть чрезмерным). Поэтому следует вместо этого использовать потоки.  
  
 Использование потоков лучше всего уместно в ситуациях, когда требуется обработать исходный документ только один раз, и элементы можно обрабатывать в порядке их следования в документе. Некоторые стандартные операторы запросов, например <xref:System.Linq.Enumerable.OrderBy%2A>, проходят через источник, собирают все данные, сортируют их и выдают первый элемент последовательности. Отметим, что при использовании оператора запроса, который материализует свой источник перед тем, как выдать первый элемент, приложение снова будет использовать большой объем памяти.  
  
 Даже при использовании метода, описанного в разделе [Практическое руководство. Потоковая передача фрагментов XML с доступом к сведениям заголовка](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md), при попытке сборки дерева XML, содержащего преобразованный документ, объем используемой памяти будет слишком большим.  
  
 Существует два основных подхода. Один подход заключается в использовании возможностей отложенной обработки объекта <xref:System.Xml.Linq.XStreamingElement>. Другой — в создании <xref:System.Xml.XmlWriter> и использовании возможностей [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] для записи элементов в <xref:System.Xml.XmlWriter>. В этом разделе рассказывается об обоих подходах.  
  
## <a name="example"></a>Пример  
 Следующий пример основан на примере в разделе [Практическое руководство. Потоковая передача фрагментов XML с доступом к сведениям заголовка (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md).  
  
 В этом примере возможности отложенной обработки объекта <xref:System.Xml.Linq.XStreamingElement> используются для создания выходного потока. Данный пример может преобразовать очень большой документ при незначительном использовании памяти.  
  
 Заметьте, что пользовательская ось (`StreamCustomerItem`) специально написана таким образом, что ожидает документа с элементами `Customer`, `Name` и `Item`, упорядоченными, как в следующем документе Source.xml. Однако более надежная реализации должна предусматривать такую ситуацию, что при проведении синтаксического анализа встретится документ, не прошедший проверку правильности.  
  
 Далее показан исходный документ, Source.xml:  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>   
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null)  
                        {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    XStreamingElement root = new XStreamingElement("Root",  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        )  
    );  
    root.Save("Test.xml");  
    Console.WriteLine(File.ReadAllText("Test.xml"));  
}  
```  
  
 Этот код выводит следующие результаты:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
## <a name="example"></a>Пример  
 Следующий пример также основан на примере в разделе [Практическое руководство. Потоковая передача фрагментов XML с доступом к сведениям заголовка (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md).  
  
 В этом примере используются возможности [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] по записи элементов в <xref:System.Xml.XmlWriter>. Данный пример может преобразовать очень большой документ при незначительном использовании памяти.  
  
 Заметьте, что пользовательская ось (`StreamCustomerItem`) специально написана таким образом, что ожидает документа с элементами `Customer`, `Name` и `Item`, упорядоченными, как в следующем документе Source.xml. Однако при более надежной реализации должна быть либо выполнена проверка правильности исходного документа с помощью XSD, либо проведена подготовка на тот случай, что при проведении синтаксического анализа встретится документ, не прошедший проверку правильности.  
  
 В этом примере используется тот же исходный документ, Source.xml, как и в предыдущем примере этого раздела. Он также выдает точно такие же выходные данные.  
  
 Использование <xref:System.Xml.Linq.XStreamingElement> для потоковой передачи выходных данных XML является предпочтительным по сравнению с записью в <xref:System.Xml.XmlWriter>.  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null) {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    IEnumerable<XElement> srcTree =  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        );  
    XmlWriterSettings xws = new XmlWriterSettings();  
    xws.OmitXmlDeclaration = true;  
    xws.Indent = true;  
    using (XmlWriter xw = XmlWriter.Create("Output.xml", xws)) {  
        xw.WriteStartElement("Root");  
        foreach (XElement el in srcTree)  
            el.WriteTo(xw);  
        xw.WriteEndElement();  
    }  
  
    string str = File.ReadAllText("Output.xml");  
    Console.WriteLine(str);  
}  
```  
  
 Этот код выводит следующие результаты:  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
## <a name="see-also"></a>См. также  
 [Расширенные методы программирования LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)