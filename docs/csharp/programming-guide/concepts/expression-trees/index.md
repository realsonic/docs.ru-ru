---
title: "Деревья выражений (C#) | Документация Майкрософт"
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
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 87195c8936aba485919d6c717fcbfaa1b282bddc
ms.lasthandoff: 03/31/2017

---
# <a name="expression-trees-c"></a>Деревья выражений (C#)
Деревья выражений представляют код в виде древовидной структуры, где каждый узел является выражением, например, вызовом метода или двоичной операцией, такой как `x < y`.  
  
 Вы можете компилировать и выполнять код, представленный деревьями выражений. Это позволяет динамически изменять выполняемый код, выполнять запросы LINQ в различных базах данных и создавать динамические запросы. Дополнительные сведения о деревьях выражений в LINQ см. в разделе [Практическое руководство. Использование деревьев выражений для создания динамических запросов (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md).  
  
 Кроме того, деревья выражений используются в среде выполнения динамического языка (DLR) для обеспечения взаимодействия между динамическими языками и платформой .NET Framework, а также и предоставления разработчикам компиляторов возможности выдавать деревья выражений вместо промежуточного языка Microsoft (MSIL). Дополнительные сведения о DLR см. в разделе [Общие сведения о среде DLR](https://msdn.microsoft.com/library/dd233052).  
  
 Вы можете использовать компилятор C# или Visual Basic для создания дерева выражений на основе анонимного лямбда-выражения или создавать деревья выражений вручную с помощью пространства имен <xref:System.Linq.Expressions>.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>Создание деревьев выражений на основе лямбда-выражений  
 Когда лямбда-выражение присваивается переменной типа <xref:System.Linq.Expressions.Expression%601>, компилятор порождает код для создания дерева выражений, представляющего лямбда-выражение.  
  
 Компилятор C# может создавать деревья выражений только на основе лямбда-выражений (или однострочных лямбда-функций). Они не могут анализировать лямбды операторов (или многострочные лямбды). Дополнительные сведения о лямбда-выражениях на C# см. в разделе [Лямбда-выражения](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 В следующем примере кода демонстрируется способ применения компилятора C# для создания дерева выражений, представляющего лямбда-выражение `num => num < 5`.  
  
```csharp  
Expression<Func<int, bool>> lambda = num => num < 5;  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>Создание деревьев выражений с помощью API-интерфейса  
 Чтобы создавать деревья выражений с помощью API, используйте класс <xref:System.Linq.Expressions.Expression>. Этот класс содержит статические фабричные методы, позволяющие создавать узлы дерева выражения конкретного типа, например <xref:System.Linq.Expressions.ParameterExpression>, который представляет переменную или параметр, или <xref:System.Linq.Expressions.MethodCallExpression>, который представляет вызов метода. В пространстве имен <xref:System.Linq.Expressions> также определены <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression> и другие типы выражений. Эти типы являются производными от абстрактного типа <xref:System.Linq.Expressions.Expression>.  
  
 В следующем примере кода демонстрируется способ создания дерева выражений, представляющего лямбда-выражение `num => num < 5`, с помощью API.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Manually build the expression tree for   
// the lambda expression num => num < 5.  
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");  
ConstantExpression five = Expression.Constant(5, typeof(int));  
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);  
Expression<Func<int, bool>> lambda1 =  
    Expression.Lambda<Func<int, bool>>(  
        numLessThanFive,  
        new ParameterExpression[] { numParam });  
```  
  
 На платформе .NET Framework 4 или более поздней версии API деревьев выражений также поддерживает присваивание и выражения потока управления, такие как циклы, условные блоки и блоки `try-catch`. С помощью API-интерфейса можно создавать деревья выражений, более сложные, чем деревья, создаваемые компилятором C# из лямбда-выражений. В следующем примере показан способ создания дерева выражений, которое вычисляет факториал числа.  
  
```csharp  
// Creating a parameter expression.  
ParameterExpression value = Expression.Parameter(typeof(int), "value");  
  
// Creating an expression to hold a local variable.   
ParameterExpression result = Expression.Parameter(typeof(int), "result");  
  
// Creating a label to jump to from a loop.  
LabelTarget label = Expression.Label(typeof(int));  
  
// Creating a method body.  
BlockExpression block = Expression.Block(  
    // Adding a local variable.  
    new[] { result },  
    // Assigning a constant to a local variable: result = 1  
    Expression.Assign(result, Expression.Constant(1)),  
    // Adding a loop.  
        Expression.Loop(  
    // Adding a conditional block into the loop.  
           Expression.IfThenElse(  
    // Condition: value > 1  
               Expression.GreaterThan(value, Expression.Constant(1)),  
    // If true: result *= value --  
               Expression.MultiplyAssign(result,  
                   Expression.PostDecrementAssign(value)),  
    // If false, exit the loop and go to the label.  
               Expression.Break(label, result)  
           ),  
    // Label to jump to.  
       label  
    )  
);  
  
// Compile and execute an expression tree.  
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);  
  
Console.WriteLine(factorial);  
// Prints 120.  
```

Дополнительные сведения см. в записи блога [Generating Dynamic Methods with Expression Trees in Visual Studio 2010](http://go.microsoft.com/fwlink/p/?LinkId=169513) (Создание динамических методов с использованием деревьев выражений в Visual Studio 2010), которая также применима к более поздним версиям Visual Studio.
  
## <a name="parsing-expression-trees"></a>Синтаксический анализ деревьев выражений  
 В следующем примере кода показано, как дерево выражений, представляющее лямбда-выражение `num => num < 5`, может быть разложено на части.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Create an expression tree.  
Expression<Func<int, bool>> exprTree = num => num < 5;  
  
// Decompose the expression tree.  
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];  
BinaryExpression operation = (BinaryExpression)exprTree.Body;  
ParameterExpression left = (ParameterExpression)operation.Left;  
ConstantExpression right = (ConstantExpression)operation.Right;  
  
Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value);  
  
// This code produces the following output:  
  
// Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>Неизменность деревьев выражений  
 Деревья выражений должны быть неизменными. Это означает, что если требуется изменить дерево выражений, следует создать новое дерево выражений путем копирования существующего и заменить узлы в нем. Для прохода по существующему дереву выражений можно использовать другое дерево выражений (посетитель). Дополнительные сведения см. в разделе [Практическое руководство. Изменение деревьев выражений (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md).  
  
## <a name="compiling-expression-trees"></a>Компиляция деревьев выражений  
 Тип <xref:System.Linq.Expressions.Expression%601> имеет метод <xref:System.Linq.Expressions.Expression%601.Compile%2A>, который компилирует код, представленный деревом выражения, в исполняемый делегат.  
  
 В следующем примере кода показан способ компиляции дерева выражений и выполнения результирующего кода.  
  
```csharp  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 Дополнительные сведения см. в разделе [Практическое руководство. Выполнение деревьев выражений (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Linq.Expressions>   
 [Практическое руководство. Выполнение деревьев выражений (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [Практическое руководство. Изменение деревьев выражений (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)   
 [Лямбда-выражения](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Общие сведения о среде DLR](https://msdn.microsoft.com/library/dd233052)   
 [Основные понятия программирования (C#)](../../../../csharp/programming-guide/concepts/index.md)