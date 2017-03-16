---
title: "Практическое руководство. Доступ к объектам взаимодействия Office с помощью функций языка Visual C# (Руководство по программированию на C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "dynamic [C#], программирование для Office"
  - "именованные и необязательные аргументы [C#], программирование для Office"
  - "именованные аргументы [C#], программирование для Office"
  - "программирование для Office [C#]"
  - "необязательные аргументы [C#], программирование для Office"
  - "необязательные параметры [C#], программирование для Office"
ms.assetid: 041b25c2-3512-4e0f-a4ea-ceb2999e4d5e
caps.latest.revision: 33
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 33
---
# Практическое руководство. Доступ к объектам взаимодействия Office с помощью функций языка Visual C# (Руководство по программированию на C#)
В Visual C\# 2010 появились новые функции, упрощающие доступ к объектам API Office.  К новым функциям относятся именованные и необязательные аргументы, новый тип `dynamic`, а также возможность передавать аргументы ссылочным параметрам в методах COM, как если бы они были параметрами значений.  
  
 В этом разделе с использованием новых функций будет написан код, который создает и отображает лист Microsoft Office Excel.  После этого будет написан код для добавления документа Office Word, который содержит значок, ссылающийся на лист Excel.  
  
 Для выполнения данного пошагового руководства на компьютере должны быть установлены Microsoft Office Excel 2007 и Microsoft Office Word 2007 или более поздние версии продуктов.  
  
 Если используется операционная система, более ранняя, чем [!INCLUDE[windowsver](../../../csharp/programming-guide/interop/includes/windowsver-md.md)], убедитесь, что установлена платформа [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)].  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Создание нового проекта консольного приложения  
  
1.  Запустите Visual Studio.  
  
2.  В меню **Файл** выберите пункт **Создать**, а затем команду **Проект**.  Откроется диалоговое окно **Новый проект**.  
  
3.  В области **Установленные шаблоны** разверните узел **Visual C\#** и выберите **Windows**.  
  
4.  В верхней части диалогового окна **Новый проект** должен быть выбран вариант **.NET Framework 4** \(или более поздняя версия\) выбран в качестве требуемой версии платформы.  
  
5.  В области **Шаблоны** щелкните **Консольное приложение**.  
  
6.  Введите имя проекта в поле **Имя**.  
  
7.  Нажмите кнопку **ОК**.  
  
     В **обозревателе решений** появится новый проект.  
  
### Добавление ссылок  
  
1.  В **обозревателе решений** щелкните имя проекта правой кнопкой мыши и выберите **Добавить ссылку**.  Откроется диалоговое окно **Добавление ссылки**.  
  
2.  На странице **Сборки** в списке **Имя компонента** выберите **Microsoft.Office.Interop.WordComponent Name**, а затем, удерживая нажатой клавишу CTRL, выберите **Microsoft.Office.Interop.Excel**.  Если сборки отсутствуют, может потребоваться проверить, что они установлены и отображаются \(см. раздел [Практическое руководство. Установка основных сборок взаимодействия Microsoft Office](../Topic/How%20to:%20Install%20Office%20Primary%20Interop%20Assemblies.md)\).  
  
3.  Нажмите кнопку **ОК**.  
  
### Добавление необходимых директив using  
  
1.  В **обозревателя решений** щелкните правой кнопкой мыши файл **Program.cs** и выберите пункт **Просмотреть код**.  
  
2.  В начало файла кода добавьте следующие директивы `using`.  
  
     [!code-cs[csProgGuideOfficeHowTo#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_1.cs)]  
  
### Создание списка банковских счетов  
  
1.  Вставьте следующее определение классов в файл **Program.cs** в класс `Program`.  
  
     [!code-cs[csProgGuideOfficeHowTo#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_2.cs)]  
  
2.  Чтобы создать список `bankAccounts`, содержащий два счета, добавьте в метод `Main` следующий код.  
  
     [!code-cs[csProgGuideOfficeHowTo#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_3.cs)]  
  
### Объявление метода, экспортирующего сведения о счетах в Excel  
  
1.  Чтобы настроить лист Excel, добавьте в класс `Program` следующий метод.  
  
     У метода [Add](http://go.microsoft.com/fwlink/?LinkId=210910) есть необязательный параметр для указания конкретного шаблона.  Необязательные параметры, впервые появившиеся в [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)], позволяют опускать аргумент для таких параметров, если требуется использовать значение параметра по умолчанию.  Поскольку в следующем коде никакой аргумент не передается, в методе `Add` используется шаблон по умолчанию и создается новая книга.  В эквивалентном операторе в более ранних версиях C\# необходимо было использовать аргумент\-местозаполнитель `ExcelApp.Workbooks.Add(Type.Missing)`.  
  
     [!code-cs[csProgGuideOfficeHowTo#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_4.cs)]  
  
2.  Добавьте в конец метода `DisplayInExcel` следующий код.  Этот код вставляет значения в первые два столбца первой строки листа.  
  
     [!code-cs[csProgGuideOfficeHowTo#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_5.cs)]  
  
3.  Добавьте в конец метода `DisplayInExcel` следующий код.  Цикл `foreach` помещает сведения из списка счетов в первые два столбца последовательных строк листа.  
  
     [!code-cs[csProgGuideOfficeHowTo#7](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_6.cs)]  
  
4.  Добавьте в конец метода `DisplayInExcel` следующий код, чтобы ширина столбца изменялась в соответствии с содержимым.  
  
     [!code-cs[csProgGuideOfficeHowTo#13](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_7.cs)]  
  
     В более ранних версиях C\# требовалось явное приведение типов для этих операций, поскольку `ExcelApp.Columns[1]` возвращает тип `Object`, а метод `AutoFit` является методом Excel [Range](http://go.microsoft.com/fwlink/?LinkId=210911).  Приведение показано в следующих строках.  
  
     [!code-cs[csProgGuideOfficeHowTo#14](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_8.cs)]  
  
     В [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] и более поздних версиях возвращаемое значение `Object` преобразуется в `dynamic` автоматически, если ссылка на сборку задана с помощью параметра компилятора [\/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md) или, что эквивалентно, если свойство Excel **Внедрить типы взаимодействия** имеет значение true.  True является значением по умолчанию для этого свойства.  
  
### Запуск проекта  
  
1.  Добавьте в конец метода `Main` следующую строку.  
  
     [!code-cs[csProgGuideOfficeHowTo#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_9.cs)]  
  
2.  Нажмите клавиши CTRL\+F5.  
  
     Появится книга Excel, содержащая данные о двух счетах.  
  
### Добавление документа Word  
  
1.  Чтобы продемонстрировать дополнительные способы, совершенствующие программирование для Office в [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] и более поздних версиях, следующий код открывает приложение Word и создает значок со ссылкой на лист Excel.  
  
     Вставьте метод `CreateIconInWordDoc`, указанный далее в этом шаге, в класс `Program`.  В методе `CreateIconInWordDoc` используются именованные и необязательные аргументы, чтобы упростить вызовы методов [Add](http://go.microsoft.com/fwlink/?LinkId=210937) и [PasteSpecial](http://go.microsoft.com/fwlink/?LinkId=147099).  Этих вызовах используются две новые возможности, появившиеся в [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] которые упрощают вызовы методов COM, имеющих ссылочные параметры.  Во\-первых, аргументы можно передать в ссылочные параметры, как если бы они были параметрами значений.  Это значит, что значения можно передавать напрямую без создания переменной для каждого ссылочного параметра.  Компилятор создает временные переменные для хранения значений аргументов и уничтожает эти переменные после завершения вызываемого метода.  Во\-вторых, ключевое слово `ref` в списке аргументов можно опустить.  
  
     У метода `Add` имеется четыре ссылочных параметра, все из которых являются необязательными.  В [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] или более поздних версиях можно опустить аргументы для любого или для всех параметров, если требуется использовать значения по умолчанию.  В [!INCLUDE[csharp_orcas_long](../../../csharp/programming-guide/interop/includes/csharp-orcas-long-md.md)] и более ранних версиях необходимо было указывать аргумент для каждого из параметров, и этот аргумент должен был быть переменной, поскольку параметры являются ссылочными.  
  
     Метод `PasteSpecial` вставляет содержимое буфера обмена.  У метода имеется семь ссылочных параметров, все из которых являются необязательными.  Следующий код задает аргументы для двух из них: `Link` для создания ссылки на исходное содержимое буфера и `DisplayAsIcon` для отображение ссылки в виде значка.  В [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] можно использовать именованные аргументы для этих двух параметров и опустить остальные аргументы.  Хотя эти параметры являются ссылочными, использовать ключевое слово `ref` или создавать переменные для передачи аргументов не требуется.  Значения можно передать напрямую.  В [!INCLUDE[csharp_orcas_long](../../../csharp/programming-guide/interop/includes/csharp-orcas-long-md.md)] и более ранних версиях необходимо было передавать аргумент в виде переменной для каждого ссылочного параметра.  
  
     [!code-cs[csProgGuideOfficeHowTo#9](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_10.cs)]  
  
     В [!INCLUDE[csharp_orcas_long](../../../csharp/programming-guide/interop/includes/csharp-orcas-long-md.md)] и более ранних версиях приходилось использовать следующий более сложный синтаксис.  
  
     [!code-cs[csProgGuideOfficeHowTo#10](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_11.cs)]  
  
2.  Добавьте в конец метода `Main` следующую инструкцию.  
  
     [!code-cs[csProgGuideOfficeHowTo#11](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_12.cs)]  
  
3.  Добавьте в конец метода `DisplayInExcel` следующую инструкцию.  Метод `Copy` добавляет лист в буфер обмена.  
  
     [!code-cs[csProgGuideOfficeHowTo#12](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_13.cs)]  
  
4.  Нажмите клавиши CTRL\+F5.  
  
     Появится документ Word, содержащий значок.  Дважды щелкните значок, чтобы отобразить лист на переднем плане.  
  
### Задание свойства "Внедрить типы взаимодействия"  
  
1.  При вызове типа COM, который не требует во время выполнения основной сборки взаимодействия \(PIA\), можно использовать дополнительные усовершенствования.  Избавление от зависимостей от PIA приводит к независимости версий и делает развертывание более простым.  Дополнительные сведения о преимуществах программирования без основных сборок взаимодействия см. в разделе [Пошаговое руководство. Внедрение данных о типах из управляемых сборок](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
     Кроме того, писать программы стало проще, поскольку типы, принимаемые и возвращаемые методами COM, можно представить с помощью типа `dynamic` вместо типа `Object`.  Переменные типа `dynamic` не вычисляются до времени выполнения, что позволяет обходиться без явного приведения.  Для получения дополнительной информации см. [Использование типа dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md).  
  
     В [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] внедрение сведений о типах вместо использования сборок PIA является поведением по умолчанию.  За счет этого несколько приведенных выше примеров становятся проще, поскольку явное приведение не требуется.  Например, объявление `worksheet` в методе `DisplayInExcel` записывается как `Excel._Worksheet workSheet = excelApp.ActiveSheet`, а не как `Excel._Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet`.  Для вызовов `AutoFit` в рамках одного метода также требовалось бы явное приведение без поведения по умолчанию, поскольку `ExcelApp.Columns[1]` возвращает тип `Object`, а `AutoFit` является методом Excel.  Приведение показано в следующем примере.  
  
     [!code-cs[csProgGuideOfficeHowTo#14](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_8.cs)]  
  
2.  Чтобы изменить поведение по умолчанию и использовать сборки PIA вместо внедрения сведений о типе, разверните узел **Ссылки** в **обозревателе решений** и выберите **Microsoft.Office.Interop.Excel** или **Microsoft.Office.Interop.Word**.  
  
3.  Если окно **Свойства** не отображается, нажмите клавишу **F4**.  
  
4.  В списке свойств найдите свойство **Внедрить типы взаимодействия** и измените его значение на **False**.  Либо можно выполнить компиляцию через командную строку с использованием параметра компилятора [\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) вместо [\/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md).  
  
### Дополнительное форматирование таблицы  
  
1.  Замените два вызова `AutoFit` в методе `DisplayInExcel` следующей инструкцией.  
  
     [!code-cs[csProgGuideOfficeHowTo#15](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_14.cs)]  
  
     У метода [AutoFormat](http://go.microsoft.com/fwlink/?LinkId=210948) имеется семь параметров значений, все из которых являются необязательными.  Именованные и необязательные аргументы позволяют задать аргументы для всех параметров, их части или ни для одного параметра.  В приведенной выше инструкции аргумент задается только для одного из параметров, `Format`.  Поскольку `Format` является первым параметром в списке, имя параметра указывать не требуется.  Однако инструкция может быть проще для понимания, если указать имя параметра, как показано в следующем фрагменте кода.  
  
     [!code-cs[csProgGuideOfficeHowTo#16](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_15.cs)]  
  
2.  Нажмите сочетание клавиш CTRL \+ F5, чтобы увидеть результат.  Другие форматы представлены в перечислении [XlRangeAutoFormat](http://go.microsoft.com/fwlink/?LinkId=210967).  
  
3.  Сравните инструкцию в шаге 1 со следующим кодом, в котором показаны аргументы, необходимые в [!INCLUDE[csharp_orcas_long](../../../csharp/programming-guide/interop/includes/csharp-orcas-long-md.md)] или более ранней версии.  
  
     [!code-cs[csProgGuideOfficeHowTo#17](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_16.cs)]  
  
## Пример  
 Ниже приведен полный пример кода.  
  
 [!code-cs[csProgGuideOfficeHowTo#18](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_17.cs)]  
  
## См. также  
 <xref:System.Type.Missing?displayProperty=fullName>   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Использование типа dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Именованные и необязательные аргументы](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [Практическое руководство. Использование именованных и необязательных аргументов в программировании приложений Office](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)