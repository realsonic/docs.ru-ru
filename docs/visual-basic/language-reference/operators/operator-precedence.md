---
title: "Порядок применения операторов в Visual Basic | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "арифметические операторы, приоритет"
  - "ассоциативность операторов"
  - "операторы сравнения, приоритет"
  - "логические операторы, приоритет"
  - "математические операторы"
  - "приоритет операторов"
  - "операторы [Visual Basic], ассоциативность"
  - "операторы [Visual Basic], приоритет"
  - "операторы [Visual Basic], разрешение"
  - "порядок приоритетов"
  - "приоритет, операторов"
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Порядок применения операторов в Visual Basic
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Если одно выражение содержит несколько операций, каждая часть вычисляется и выполняется в соответствии с заранее определенным порядком, называемом *приоритетом операторов*.  
  
## Правила приоритетов  
 Если выражения содержат операторы различных категорий, они вычисляются по следующим правилам:  
  
-   Арифметические операторы и операторы объединения имеют порядок приоритета, описанный далее, их приоритет выше, чем у операторов сравнения, логических и поразрядных.  
  
-   У всех операторов сравнения приоритет одинаковый, и он выше, чем у логических и поразрядных операторов, но ниже, чем у арифметических операторов и операторов объединения.  
  
-   Логические и поразрядные операторы имеют порядок приоритета, описанный далее, их приоритет ниже, чем у арифметических операторов, операторов объединения и сравнения.  
  
-   Операторы с одинаковым приоритетом вычисляются слева направо в том порядке, в каком они стоят в выражении.  
  
## Порядок приоритета  
 Операторы вычисляются в следующем порядке приоритета:  
  
### Подождите оператора  
 Await  
  
### Арифметические операторы и операторы объединения  
 Возведение в степень \(`^`\)  
  
 Унарные плюс и минус \(`+`, `–`\)  
  
 Умножение и деление с плавающей запятой \(`*`, `/`\)  
  
 Целочисленное деление \(`\`\)  
  
 Модульная арифметика \(`Mod`\)  
  
 Сложение и вычитание \(`+`, `–`\)  
  
 Объединение строк \(`&`\)  
  
 Арифметический сдвиг разрядов \(`<<`, `>>`\)  
  
### Операторы сравнения  
 Все операторы сравнения \(`=`, `<>`, `<`, `<=`, `>`, `>=`, `Is`, `IsNot`, `Like`, `TypeOf`... `Is`\)  
  
### Логические и побитовые операторы  
 Отрицание \(`Not`\)  
  
 Конъюнкция \(`And`, `AndAlso`\)  
  
 Включающая дизъюнкция \(`Or`, `OrElse`\)  
  
 Исключающая дизъюнкция \(`Xor`\)  
  
### Комментарии  
 Оператор `=` только оператор сравнения на равенство, не оператор присваивания.  
  
 Оператор объединения строк \(`&&`\) не относится к арифметическим операторам, но имеет такой же приоритет, как у арифметических операторов.  
  
 Операторы `Is` и `IsNot` являются операторами сравнения ссылок объектов.  Они не выполняют сравнение значений двух объектов; они проверяют только ссылаются ли две переменные объекта на один и тот же экземпляр объекта.  
  
## Ассоциативность  
 Когда операторы с одинаковым приоритетом появляются вместе в выражении, например умножение и деление, компилятор вычисляет каждую операцию по порядку слева направо.  Это показано в приведенном ниже примере.  
  
```  
Dim n1 As Integer = 96 / 8 / 4  
Dim n2 As Integer = (96 / 8) / 4  
Dim n3 As Integer = 96 / (8 / 4)  
```  
  
 Для первого выражения вычисляется результат деления 96 \/ 8 \(что в результате дает 12\) и деления 12 \/ 4, что в результате 3.  Так как компилятор вычисляет операции для `n1` слева направо, порядок вычисления при этом такой же, как для `n2`.  И `n1`, и `n2` имеют результат 3.  Напротив `n3` имеет в результате 48, так как скобки принудительно заставляют компилятор сначала вычислить 8 \/ 4.  
  
 Из\-за такого поведения говорится, что операторы являются *лево ассоциативными* в [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
## Переопределение приоритета и ассоциативности  
 Можно использовать скобки для принудительного выполнения некоторых частей выражения раньше других.  Этим можно переопределить порядок приоритетов и левую ассоциативность.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] всегда выполняет операции, заключенные в круглые скобки перед потоками внешней стороны. Однако внутри скобок, он поддерживает обычные приоритет и ассоциативность, если не использовать скобки в скобки.  Это показано в приведенном ниже примере.  
  
```  
Dim a, b, c, d, e, f, g As Double  
a = 8.0  
b = 3.0  
c = 4.0  
d = 2.0  
e = 1.0  
f = a - b + c / d * e  
' The preceding line sets f to 7.0. Because of natural operator   
' precedence and associativity, it is exactly equivalent to the   
' following line.  
f = (a - b) + ((c / d) * e)  
' The following line overrides the natural operator precedence   
' and left associativity.  
g = (a - (b + c)) / (d * e)  
' The preceding line sets g to 0.5.  
```  
  
## См. также  
 [Оператор \=](../../../visual-basic/language-reference/operators/assignment-operator.md)   
 [Оператор Is](../../../visual-basic/language-reference/operators/is-operator.md)   
 [Оператор IsNot](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Оператор Like](../../../visual-basic/language-reference/operators/like-operator.md)   
 [Оператор TypeOf](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [Оператор Await](../../../visual-basic/language-reference/operators/await-operator.md)   
 [Список операторов, сгруппированных по функциональному назначению](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Операторы и выражения](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)