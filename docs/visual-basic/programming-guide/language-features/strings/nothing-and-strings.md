---
title: Nothing и строки в Visual Basic
ms.custom: ''
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- strings [Visual Basic], Nothing
ms.assetid: 261380af-2024-4ecf-823b-43b1034d92cd
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: d7693e712884a500495e4573900e7d9a049c2879
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nothing-and-strings-in-visual-basic"></a>Nothing и строки в Visual Basic
Среда выполнения Visual Basic и [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] оценки `Nothing` по-разному когда дело доходит до строки.  
  
## <a name="visual-basic-runtime-and-the-net-framework"></a>Среда выполнения Visual Basic и .NET Framework  
 Рассмотрим следующий пример.  
  
 [!code-vb[VbVbalrStrings#47](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/nothing-and-strings_1.vb)]  
  
 Среда выполнения Visual Basic обычно расценивает `Nothing` как пустая строка (»»). [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] — Нет, однако и создается исключение при попытке выполнить операцию строки на `Nothing`.  
  
## <a name="see-also"></a>См. также  
 [Знакомство со строками в Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
