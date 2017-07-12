---
title: "Инструкции по размещению в службах IIS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 959a21c8-9d9d-4757-b255-4e57793ae9d6
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Инструкции по размещению в службах IIS
Для выполнения примеров, размещаемых в службах IIS, следует убедиться, что службы IIS правильно установлены и запущены.  
  
### Установка служб IIS версии 7.5 в Windows Server 2008 R2  
  
1.  В **Диспетчере сервера** выберите **Роли**. В окне **Сводка по ролям** нажмите кнопку **Добавить роли**.  
  
2.  Нажмите кнопку **Далее** для отображения диалогового окна **Выбор ролей сервера**.  
  
3.  Выберите **Сервер приложений** в списке **Роли** и дважды нажмите кнопку **Далее**, чтобы отобразить диалоговое окно **Выбор служб ролей** для роли "Сервер приложений".  
  
4.  Установите флажок **Веб\-сервер \(IIS\)**.  Если будет предложено установить дополнительные службы и компоненты ролей, нажмите кнопку **Добавить необходимые компоненты**.  Дважды нажмите кнопку **Далее**, чтобы отобразить диалоговое окно **Выбор служб ролей** для роли "Веб\-сервер \(IIS\)".  
  
5.  Разверните узел **Средства управления**, а затем разверните узел **Совместимость управления IIS 6**.  Выберите пункт **Службы сценариев IIS 6**.  При запросе установки дополнительных служб и компонентов роли щелкните **Добавить требуемые службы роли**.  Нажмите кнопку **Далее**.  
  
6.  Если элементы выбраны правильно, нажмите кнопку **Установить**.  
  
7.  После завершения установки нажмите кнопку **Закрыть**.  
  
### Установка служб IIS версии 7.5 в Windows 7  
  
1.  Нажмите кнопку **Пуск**, затем щелкните **Панель управления**.  
  
2.  Откройте группу **Программы**.  
  
3.  В группе **Программы и компоненты** выберите пункт **Включение или отключение компонентов Windows**.  
  
4.  Откроется диалоговое окно **Контроль учетных записей**.  Нажмите кнопку **Продолжить**.  
  
5.  Отображается диалоговое окно **Компоненты Windows**.  Разверните элемент **Службы IIS**.  
  
6.  Разверните элемент **Службы Интернета**.  
  
7.  Разверните элемент **Компоненты разработки приложений**.  
  
8.  Убедитесь, что выбраны следующие элементы.  
  
    1.  **Расширяемость .NET**  
  
    2.  **ASP.NET**  
  
    3.  **Расширения ISAPI**  
  
    4.  **Фильтры ISAPI**  
  
9. В элементе **Службы Интернета** разверните элемент **Основные возможности HTTP**.  
  
10. Убедитесь, что выбран параметр **Статическое содержимое**.  
  
11. В элементе **Службы Интернета** разверните элемент **Безопасность**.  
  
12. Убедитесь, что выбран параметр **Проверка подлинности Windows**.  
  
13. В каталоге **Службы IIS** разверните элемент **Средства управления веб\-узлом**, а затем выберите **Консоль управления IIS**.  
  
14. Разверните элемент **Совместимость управления IIS 6**, а затем выберите элемент **Службы сценариев IIS 6**.  
  
15. В каталоге **Службы IIS** разверните элемент **Microsoft .NET Framework 3.5.1**, а затем выберите **Активация Windows Communication Foundation по HTTP**.  
  
16. Нажмите кнопку **ОК**.  
  
### Установка служб IIS версии 7.0 в Windows Server 2008  
  
1.  В **Диспетчере сервера** выберите **Роли.** В окне **Сводка по ролям** нажмите кнопку **Добавить роли**.  
  
2.  Нажмите кнопку **Далее** для отображения диалогового окна **Выбор ролей сервера**.  
  
3.  Выберите **Сервер приложений** в списке **Роли** и дважды нажмите кнопку **Далее**, чтобы отобразить диалоговое окно **Выбор служб ролей** для роли "Сервер приложений".  
  
4.  Установите флажок **Веб\-сервер \(IIS\)**.  Если будет предложено установить дополнительные службы и компоненты ролей, нажмите кнопку **Добавить необходимые компоненты**.  Дважды нажмите кнопку **Далее**, чтобы отобразить диалоговое окно **Выбор служб ролей** для роли "Веб\-сервер \(IIS\)".  
  
5.  Разверните узел **Средства управления**, а затем разверните узел **Совместимость управления IIS 6**.  Выберите пункт **Службы сценариев IIS 6**.  При запросе установки дополнительных служб и компонентов роли щелкните **Добавить требуемые службы роли**.  Нажмите кнопку **Далее**.  
  
6.  Если элементы выбраны правильно, нажмите кнопку **Установить**.  
  
7.  После завершения установки нажмите кнопку **Закрыть**.  
  
### Установка служб IIS версии 7.0 в Windows Vista  
  
1.  Нажмите кнопку Пуск, а затем щелкните «Панель управления».  
  
2.  Выберите группу **Программы**.  
  
3.  В группе **Программы и компоненты** выберите пункт **Включение или отключение компонентов Windows**.  
  
4.  Откроется диалоговое окно **Контроль учетных записей**.  Нажмите кнопку **Продолжить**.  
  
5.  Отображается диалоговое окно **Компоненты Windows**.  Разверните элемент **Службы IIS**.  
  
6.  Разверните элемент **Службы Интернета**.  
  
7.  Разверните элемент **Компоненты разработки приложений**.  
  
8.  Убедитесь, что выбраны следующие элементы.  
  
    1.  **Расширяемость .NET**  
  
    2.  **ASP.NET**  
  
    3.  **Расширения ISAPI**  
  
    4.  **Фильтры ISAPI**  
  
9. Разверните элемент **Средства управления веб\-узлом**, а затем выберите **Консоль управления IIS**.  
  
10. В элементе **Службы Интернета** разверните элемент **Основные возможности HTTP**.  
  
11. Убедитесь, что выбран параметр **Статическое содержимое**.  
  
12. В элементе **Службы Интернета** разверните элемент **Безопасность**.  
  
13. Убедитесь, что выбран параметр **Проверка подлинности Windows**.  
  
14. Разверните элемент **Совместимость управления IIS 6**, а затем выберите элемент **Службы сценариев IIS 6**.  
  
15. Разверните элемент **Microsoft .NET Framework 3.0**, затем выберите **Активация Windows Communication Foundation по HTTP**.  
  
16. Нажмите кнопку **ОК**.  
  
### Установка служб IIS версии 6.0 в Windows Server 2003  
  
1.  В окне **Управление данным сервером** щелкните **Добавить или удалить роль** и нажмите кнопку **Далее**.  
  
2.  Выберите **Сервер приложений \(IIS, ASP.NET\)** в списке **Роль сервера** и нажмите кнопку **Далее**.  
  
3.  Установите флажок **Включить ASP.NET** и нажмите кнопку **Далее**.  
  
4.  Если элементы выбраны правильно, нажмите кнопку Далее.  
  
### Установка служб IIS версии 5.1 в Windows XP с установленными пакетами обновления 2 и 3 \(SP2 и SP3\)  
  
1.  В панели управления щелкните значок **Установка и удаление программ**.  
  
2.  В диалоговом окне **Установка и удаление программ** выберите **Установка и удаление компонентов Windows**.  
  
3.  В диалоговом окне **Мастер компонентов Windows** установите флажок **Службы IIS** и нажмите кнопку **Далее**.  
  
4.  При отображении диалогового окна **Требуемые файлы** вставьте диск установки операционной системы, выберите папку i386 и нажмите кнопку **ОК**.  
  
5.  После завершения установки нажмите кнопку **Готово**.  
  
6.  Закройте диалоговое окно **Установка и удаление программ**, затем закройте **Панель управления**.  
  
### Проверка установки служб IIS и ASP.NET  
  
1.  Сохраните HTML\-файл, указанный в конце данного раздела, в корневом каталоге \\InetPub\\wwwroot и назовите его Default.aspx.  
  
2.  Откройте окно браузера.  
  
3.  Введите `http://localhost/Default.aspx` в поле адреса и нажмите клавишу ВВОД.  
  
4.  Должна появиться веб\-страница с текстом "Здравствуй, мир\!".  
  
> [!NOTE]
>  При каждой установке новой версии [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] необходимо повторно регистрировать aspnet\_isapi как расширение веб\-службы для IIS.  Чтобы сделать это, выполните команду `aspnet_regiis –I –enable`.  
  
## Пример кода  
  
```  
<html>  
   <body>  
       <form >  
           <h3> Hello World  
           </h3>  
       </form>  
   </body>  
</html>  
```