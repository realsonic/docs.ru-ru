---
title: Задача 1. Создание нового приложения Windows Presentation Foundation
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 270eaeba-9492-4532-af9f-403ce5c9935b
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: cd21013331e19fa9e18ad7cbee0a7bb07abaf3d2
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="task-1-create-a-new-windows-presentation-foundation-application"></a>Задача 1. Создание нового приложения Windows Presentation Foundation
В этой задаче будет создания пустого приложения Windows Presentation Foundation (WPF), используя шаблон WPF Application Visual Studio и добавить ссылки на соответствующие [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] сборки рабочего процесса.  
  
### <a name="to-create-the-wpf-application-project"></a>Создание проекта приложения WPF  
  
1.  Откройте Visual Studio и на **файл** последовательно выберите пункты **New**, а затем нажмите кнопку **проекта**.  
  
2.  В **новый проект** диалогового окна выберите либо **Visual C#** или **Visual Basic** из **установленные шаблоны** на левой стороне панели поле. Если язык не отображается, разверните узел **другие языки**.  
  
3.  Выберите **Windows** в **установленные шаблоны** области.  
  
4.  Убедитесь, что в верхней области (значение по умолчанию) **.NET Framework 4** был выбранного в раскрывающемся списке, а затем выберите **приложение WPF**.  
  
5.  Задайте имя проекта для **HostingApplication** в нижней части окна.  
  
6.  Задайте имя решения **RehostingTheDesigner**.  
  
7.  Нажмите кнопку **ОК** Создание проекта приложения. Visual Studio создает основной пользовательский Интерфейс WPF для приложения и включает в него соответствующий XAML и файлы кода.  
  
8.  Добавьте ссылки на **WorkflowModel** сборки. Для этого в **обозревателе решений**, щелкните правой кнопкой мыши **HostingApplication** проект и выберите **добавить ссылку**.  
  
9. В **добавить ссылку** диалоговое окно, нажмите кнопку **.NET** удерживайте нажатой клавишу CTRL, выберите следующие сборки и нажмите кнопку **ОК**:  
  
    -   System.Activities  
  
    -   System.Activities.Presentation  
  
    -   System.Activities.Core.Presentation  
  
10. Нажмите кнопку **ОК**.  
  
11. В разделе [задача 2: размещение конструктора рабочих процессов](../../../docs/framework/windows-workflow-foundation/task-2-host-the-workflow-designer.md) чтобы узнать, как разместить полотно конструктора в конструкторе рабочего процесса.  
  
## <a name="see-also"></a>См. также  
 [Отдельное размещение конструктора рабочих процессов](../../../docs/framework/windows-workflow-foundation/rehosting-the-workflow-designer.md)  
 [Задача 2. Размещение конструктора рабочих процессов](../../../docs/framework/windows-workflow-foundation/task-2-host-the-workflow-designer.md)
