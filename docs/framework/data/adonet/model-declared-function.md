---
title: "объявляемая моделью функция"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 37c6b04fbea69f62aaf7bc148ee04ace5a5a349c
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="model-declared-function"></a>объявляемая моделью функция
Объект *объявляемая моделью функция* — функция, которая объявлена в концептуальной модели, но не определена в концептуальной модели. Функция может быть определена в среде размещения или хранения. Например, объявляемая моделью функция может быть сопоставлена функции, определенной в базе данных, экспонируя таким образом функцию в концептуальной модели на стороне сервера.  
  
 Объявление объявляемой моделью функции содержит следующую информацию.  
  
-   Имя функции. (Обязательный атрибут).  
  
-   Тип возвращаемого значения. (Необязательный параметр).  
  
    > [!NOTE]
    >  Если возвращаемое значение не задано, возвращаемого значения не будет.  
  
-   Сведения о параметрах, включая имя и тип параметров. (Необязательный параметр).  
  
## <a name="example"></a>Пример  
 [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) использует доменный язык (DSL), называемый языком определения концептуальной схемы ([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)) для определения концептуальных моделей. В языке CSDL, имеет одну реализацию объявляемая моделью функция [импорт функции](http://msdn.microsoft.com/library/125704ae-56c7-4233-80b7-389a10f3a65d). Далее на языке CSDL определяется контейнер сущностей с определением импорта функции. Обратите внимание, что тип возвращаемого значения для функции отсутствует, поскольку тип возвращаемого значения не задан.  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## <a name="see-also"></a>См. также  
 [Основные понятия модели EDM](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)  
 [Сущностная модель данных](../../../../docs/framework/data/adonet/entity-data-model.md)
