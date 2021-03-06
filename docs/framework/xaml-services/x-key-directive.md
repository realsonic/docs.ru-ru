---
title: Директива x:Key
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- xKey
- Key
- x:Key
helpviewer_keywords:
- x:Key attribute [XAML Services]
- Key attribute in XAML [XAML Services]
- XAML [XAML Services], x:Key attribute
ms.assetid: 1985cd45-f197-42d5-b75e-886add64b248
caps.latest.revision: 25
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: f28ed1e4077a48016ddd8d9b5eeb45d6ba25d8e5
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="xkey-directive"></a>Директива x:Key
Однозначно определяет элементы, которые создаются и ссылки в словаре, определенные в XAML. Добавление `x:Key` значение элемента объекта XAML является наиболее распространенным способом для идентификации ресурса в словаре ресурсов, например в WPF <xref:System.Windows.ResourceDictionary>.  
  
## <a name="xaml-attribute-usage"></a>Использование атрибута XAML  
  
```  
<object x:Key="stringKeyValue".../>  
-or-  
<object x:Key="{markupExtensionUsage}".../>  
```  
  
## <a name="xaml-attribute-usage-wpf-specific"></a>Использование атрибута XAML (характерные для WPF)  
  
```  
<object.Resources>  
  <object x:Key="stringKeyValue".../>  
</object.Resources>  
-or-  
<object.Resources>  
  <object x:Key="{markupExtensionUsage}".../>  
</object.Resources>  
```  
  
## <a name="xaml-values"></a>Значения XAML  
  
|||  
|-|-|  
|`stringKeyValue`|Текстовая строка для использования в качестве ключа. Строка текста должна соответствовать [Грамматика XamlName](../../../docs/framework/xaml-services/xamlname-grammar.md).|  
|`markupExtensionUsage`|В разделители расширения разметки {}, использование расширения разметки, которое предоставляет объект для использования в качестве ключа. См. заметки.|  
  
## <a name="remarks"></a>Примечания  
 `x:Key` поддерживает концепцию словарь ресурсов XAML. XAML как языка не определен реализацию словаря ресурсов, которые требуются для конкретных платформ пользовательского интерфейса. Дополнительные сведения о реализации словари ресурсов XAML в WPF см. в разделе [ресурсов XAML](../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 В XAML 2006 и WPF `x:Key` должно быть указано как атрибут. Нестроковые ключи по-прежнему можно использовать, но это требует использования расширения разметки для обеспечения нестроковые значения в виде атрибутов. При использовании XAML 2009, `x:Key` может быть указан как элемент, чтобы явным образом поддерживают словари, различаемых по типы объектов, отличных от строки без необходимости промежуточного расширения разметки. В разделе «XAML 2009» этого раздела. В оставшейся части раздел «примечания» относятся к реализации XAML 2006 г.  
  
 Значение атрибута `x:Key` может быть любая строка, определен в [Грамматика XamlName](../../../docs/framework/xaml-services/xamlname-grammar.md) или объект, вычисленный с помощью расширения разметки. Пример из WPF. в разделе «Примечания об использовании WPF».  
  
 Дочерние элементы родительского элемента, который является <xref:System.Collections.IDictionary> реализация должна содержать обычно `x:Key` атрибут, указывающий уникальности значения ключа в пределах этого словаря. Платформы могут реализовать псевдонимы ключевых свойств для замены `x:Key` с определенными типами; типы, которые определяют такие свойства должен быть помечен атрибутом <xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>.  
  
 Код эквивалентно указанию `x:Key` — это ключ, используемый для базового <xref:System.Collections.IDictionary>. Например `x:Key` , применяемый в разметке для ресурсов в WPF эквивалентно значению `key` параметр <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> при добавлении ресурса в WPF <xref:System.Windows.ResourceDictionary> в коде.  
  
## <a name="wpf-usage-notes"></a>Примечания об использовании WPF  
 Объект, дочерних объектов родительского <xref:System.Collections.IDictionary> реализации, например WPF <xref:System.Windows.ResourceDictionary>, обычно необходимо включить `x:Key` атрибут и значение ключа должно быть уникальным в пределах этого словаря. Существует два важных исключения:  
  
-   Некоторые типы WPF объявляют неявный ключ для использования словаря. Например <xref:System.Windows.Style> с <xref:System.Windows.Style.TargetType%2A>, или <xref:System.Windows.DataTemplate> с <xref:System.Windows.DataTemplate.DataType%2A>, могут находиться в <xref:System.Windows.ResourceDictionary> и использовать неявный ключ.  
  
-   WPF поддерживает концепцию словарь объединенных ресурсов. Ключи могут совместно использоваться объединенных словарей и общего ключа поведение может осуществляться с использованием <xref:System.Windows.FrameworkContentElement.FindResource%2A>. Подробнее см. в разделе [Объединенные словари ресурсов](../../../docs/framework/wpf/advanced/merged-resource-dictionaries.md).  
  
 В общей WPF XAML реализацию и приложение модели уникальность ключа не проверяется компилятором разметки XAML. Вместо этого отсутствует или неуникальным `x:Key` значения привести к ошибкам синтаксического анализа XAML во время загрузки. Однако обработка словарей для WPF для Visual Studio можно часто Обратите внимание такие ошибки на этапе разработки.  
  
 Обратите внимание, что в приведенном синтаксисе <xref:System.Windows.ResourceDictionary> объекта неявно в том, как процессор WPF XAML создает коллекцию для заполнения <xref:System.Windows.FrameworkElement.Resources%2A> коллекции. Объект <xref:System.Windows.ResourceDictionary> явно не указан обычно как элемент в разметке, несмотря на то, что в некоторых случаях бывает, если хотите, чтобы для ясности (было бы элемент объекта коллекции между <xref:System.Windows.FrameworkElement.Resources%2A> свойства элементов и элементов, заполнение словарь). Сведения о том, почему объект коллекции почти всегда является неявным элементом в разметке см. в разделе [XAML Syntax In Detail](../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 В реализации XAML в WPF, определяется обработка для ключей словаря ресурсов <xref:System.Windows.ResourceKey> абстрактного класса. Тем не менее процессор WPF XAML создает различные типы базовых расширений для ключей в зависимости от их применения. Например, ключ для <xref:System.Windows.DataTemplate> или любой производный класс обрабатывается отдельно и выводятся различные <xref:System.Windows.DataTemplateKey> объекта.  
  
 Ключи и имена используют различные директивы и языковые элементы (`x:Key` и `x:Name`) в базовом определении XAML. Ключи и имена также используются в различных ситуациях определением WPF и приложением этих концепций. Дополнительные сведения см. в разделе [области имен XAML WPF](../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md).  
  
 Как уже говорилось ранее, значение ключа может предоставляться через расширения разметки и может принимать строковое значение. Примером WPF является ситуация, что значение `x:Key` может быть[ComponentResourceKey](../../../docs/framework/wpf/advanced/componentresourcekey-markup-extension.md). Некоторые элементы управления предоставляют ключ стиля такого типа для пользовательского ресурса стиля, которые влияют частью внешнего вида и поведения элемента управления без полной замены стиля. Примером такого ключа является <xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A>.  
  
 Функция объединенного словаря WPF ряд дополнительных вопросов для поведения поиска ключа и уникальности. Подробнее см. в разделе [Объединенные словари ресурсов](../../../docs/framework/wpf/advanced/merged-resource-dictionaries.md).  
  
## <a name="xaml-2009"></a>XAML 2009  
 XAML 2009 ослабляет используемые ограничение, `x:Key` всегда предоставляется в виде атрибутов.  
  
 В WPF можно использовать возможности XAML 2009, но только для кода XAML, который не является компилированной разметки. Скомпилированный с разметкой XAML и форма BAML кода XAML в настоящее время не поддерживают ключевые слова и компоненты XAML 2009.  
  
 В XAML 2009 г. можно указать `x:Key` элементы следующим образом:  
  
### <a name="xaml-element-usage-xaml-2009-only"></a>Использование элемента XAML (только для XAML 2009)  
  
```  
<object>  
  <x:Key>  
keyObject  
  </x:Key>  
...  
</object>  
```  
  
### <a name="xaml-values"></a>Значения XAML  
  
|||  
|-|-|  
|`keyObject`|Элемент Object для объекта, который используется в качестве ключа для данного `object` в специализированном словаре.|  
  
-   Контейнер/родитель для этого типа используйте здесь не показан. `object` должно быть дочерним элементом элемента объекта, который представляет реализацию специализированного словаря. `keyObject` должен быть экземпляр объекта (или значением типа значения), подходит в качестве ключа для этой конкретной реализации специализированного словаря.  
  
-   WPF не реализует словари, это требование. Ключи объектов – это более Общая функция языка XAML, возможно полезная для определенных сценариев настраиваемых словарей, когда желательно создание словаря в XAML. Для функций WPF, таких как неявные стили, использующие ключи нестроковых ресурсов существуют другие методы установки или указания ключей, поэтому использование ключа объекта не является обязательным.  
  
-   *keyObject* также может быть использование расширения разметки в форме элемента объекта, а не непосредственным экземпляром объекта.  
  
## <a name="silverlight-usage-notes"></a>Примечания об использовании Silverlight  
 `x:Key` для Silverlight задокументирован отдельно. Дополнительные сведения см. в разделе [пространства имен XAML (x:) Языковые возможности (Silverlight)](http://go.microsoft.com/fwlink/?LinkId=199081).  
  
## <a name="see-also"></a>См. также  
 [Ресурсы XAML](../../../docs/framework/wpf/advanced/xaml-resources.md)  
 [Ресурсы и код](../../../docs/framework/wpf/advanced/resources-and-code.md)  
 [Расширение разметки StaticResource](../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)
