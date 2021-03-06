---
title: Использование переменной итератора в лямбда-выражении может привести к неожиданным результатам
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42324
- bc42324
helpviewer_keywords:
- BC42324
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: fb707cd4e09a149d21b70bb0f998a40c7ed58b49
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="using-the-iteration-variable-in-a-lambda-expression-may-have-unexpected-results"></a>Использование переменной итератора в лямбда-выражении может привести к неожиданным результатам
Использование переменной итерации в лямбда-выражение может иметь непредвиденные результаты. Вместо этого создайте локальную переменную в цикле и присвойте ей значение переменной итерации.  
  
 Это предупреждение появляется при использовании переменной итерации цикла, объявленная внутри цикла лямбда-выражение. Например следующий пример приводит к выводу предупреждения.  
  
```vb  
For i As Integer = 1 To 10  
    ' The warning is given for the use of i.  
    Dim exampleFunc As Func(Of Integer) = Function() i  
Next  
```  
  
 В следующем примере показано, которые могут возникнуть непредвиденные результаты.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            array1(i) = Function() i  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
 `For` Цикла создает массив из лямбда-выражений, каждое из которых возвращает значение переменной итерации цикла `i`. Когда лямбда-выражения вычисляются в `For Each` цикла, может ожидать появления 0, 1, 2, 3 и 4, последовательных значений `i` в `For` цикла. Вместо этого вы видите окончательное значение `i` отображаются пять раз:  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 По умолчанию данное сообщение является предупреждением. Дополнительные сведения о скрытии предупреждений или обработке предупреждений как ошибок см. в разделе [Настройка предупреждений в Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Идентификатор ошибки:** BC42324  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
-   Присвоить значение переменной итерации в локальной переменной и используйте локальную переменную в лямбда-выражения.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            Dim j = i  
            array1(i) = Function() j  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
## <a name="see-also"></a>См. также  
 [Лямбда-выражения](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
