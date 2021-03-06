---
title: Очереди и надежные сеансы
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7e794d03-141c-45ed-b6b1-6c0e104c1464
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: dbbaa432f7f1e137fc6cbd47ecd8e24d9eab97c3
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2018
---
# <a name="queues-and-reliable-sessions"></a>Очереди и надежные сеансы
Очереди и надежные сеансы - функции [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], реализующие надежный обмен сообщениями. В подразделах данного раздела рассматриваются функции надежного обмена сообщениями [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Надежный обмен сообщениями - это надежная передача сообщений от надежного источника сообщений (называемого источником) в надежное назначение сообщений (называемое назначением).  
  
 Надежный обмен сообщениями имеет следующие ключевые аспекты:  
  
-   Гарантии передачи сообщений, отправленных из источника в назначение, вне зависимости от сбоев передачи сообщений или транспортных сбоев.  
  
-   Отделение источника от назначения, благодаря чему любые сбои и восстановления источника и назначения происходят независимо, и обеспечивается надежность доставки сообщения даже при недоступности источника или назначения.  
  
 Надежность обмена сообщениями часто обеспечивается ценой высокой задержки. Задержкой называется время, затрачиваемое на доставку сообщения от источника в назначение. В [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] предусмотрены следующие типы надежного обмена сообщениями:  
  
-   [Надежные сеансы](../../../../docs/framework/wcf/feature-details/reliable-sessions.md), которое обеспечивает надежной передачи без ценой высокой задержки  
  
-   [Очереди в WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md), которые обеспечивают надежную передачу и разделение между источником и назначением.  
  
## <a name="reliable-sessions"></a>Надежные сеансы  
 Надежные сеансы обеспечивают надежную сквозную доставку сообщений между источником и назначением с помощью протокола WS-ReliableMessaging, вне зависимости от количества и типа посредников между конечными точками обмена сообщениями (источником и назначением). В него входят любые транспортные посредники, не использующие протокол SOAP (например, прокси-серверы HTTP), и посредники, использующие этот протокол (например, мосты и маршрутизаторы на базе SOAP), необходимые для продвижения сообщений между конечными точками. Надежные сеансы используют окно передачи в памяти для маскировки сбоев на уровне сообщений SOAP и повторной установки соединений при транспортных сбоях.  
  
 Надежные сеансы обеспечивают надежную передачу сообщений с низкой задержкой. Они обеспечивают доставку сообщений протокола SOAP через любые прокси или маршрутизаторы подобно тому, как протокол TCP обеспечивает доставку пакетов через IP-мосты. Дополнительные сведения о надежных сеансов см. в разделе [надежные сеансы](../../../../docs/framework/wcf/feature-details/reliable-sessions.md).  
  
### <a name="queues"></a>Очереди  
 Очереди в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] обеспечивают надежную передачу сообщений и отделение источника от назначения (ценой высокой задержки). Взаимодействие через очереди в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] построено на основе MSMQ.  
  
 MSMQ поставляется как дополнительный компонент Windows и выполняется как служба NT. MSMQ помещает передаваемые сообщения в очередь передачи от имени источника и доставляет их в целевую очередь. Целевая очередь принимает сообщения от имени назначения для дальнейшей доставки в назначения, запрашиваемые для этих сообщений. Диспетчеры очередей MSMQ реализуют надежный протокол передачи сообщений, благодаря которому сообщения не могут быть потеряны при передаче. Протокол может быть собственным или основанным на SOAP, как, например, протокол SRMP.  
  
 Разделение в сочетании с надежностью передачи сообщений между очередями обеспечивает надежную передачу данных между слабо связанными приложениями. В отличие от технологии надежных сеансов, не требуется, чтобы источник и назначение выполнялись одновременно. Таким образом, однозначно возможны сценарии, в которых запросы фактически используются как механизм контроля нагрузки при несоответствии интенсивности создания сообщений источником и их потребления назначением. Дополнительные сведения об очередях см. в разделе [очереди в WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md).  
  
## <a name="see-also"></a>См. также  
 [Очереди в WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)  
 [Очереди в WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)  
 [Надежные сеансы](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)  
 [Общие сведения о надежных сеансах](../../../../docs/framework/wcf/feature-details/reliable-sessions-overview.md)
