---
title: Служба AJAX с использованием HTTP POST
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1ac80f20-ac1c-4ed1-9850-7e49569ff44e
caps.latest.revision: 28
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 1446fadeb249d91f0eb3e65b1155f00090441a5a
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2018
---
# <a name="ajax-service-using-http-post"></a>Служба AJAX с использованием HTTP POST
В этом примере показано, как с помощью [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] создать службу [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] асинхронных скриптов JavaScript и XML (AJAX), использующую HTTP-метод POST. Обращаться к службе AJAX можно с использованием кода JavaScript из клиента на основе веб-браузера. Этот пример основан на [базовой службы AJAX](../../../../docs/framework/wcf/samples/basic-ajax-service.md) образец; единственное различие между двумя образцы является использование HTTP POST, а не HTTP GET.  
  
 Поддержка технологии AJAX в [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] оптимизирована для использования с ASP.NET AJAX с помощью элемента управления `ScriptManager`. Пример использования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] с ASP.NET AJAX, в разделе [примеров Ajax](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md).  
  
> [!NOTE]
>  Процедура настройки и инструкции по построению для данного образца приведены в конце этого раздела.  
  
 Служба в следующем примере является службой [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] без кода, относящегося к AJAX.  
  
 Если <xref:System.ServiceModel.Web.WebInvokeAttribute> при выполнении операции применяется атрибут или <xref:System.ServiceModel.Web.WebGetAttribute> не применяется атрибут, используется HTTP-команда по умолчанию («POST»). Запросы POST строить тяжелее, чем запросы GET, однако они не кэшируются; запросы POST следует использовать для всех операций, в которых нельзя использовать кэширование.  

```csharp
[ServiceContract(Namespace = "PostAjaxService")]  
public interface ICalculator  
{
    [WebInvoke]  
    double Add(double n1, double n2);  
    //Other operations omitted…  
}
```

 Создайте конечную точку AJAX в службе с помощью <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> точно так же, как в образце базовой службы AJAX.  
  
 В отличие от запросов GET вызывать службы POST из браузера нельзя. Например, переход к http://localhost/ServiceModelSamples/service.svc/Add?n1=100&n2=200 приводит к ошибке, поскольку служба POST ожидает `n1` и `n2` параметры, отправляемые в тексте сообщения — в формате JSON —, а не в URL-адрес.  
  
 Клиентская веб-страница PostAjaxClientPage.aspx содержит код ASP.NET для вызова службы, когда пользователь нажимает одну из кнопок операций на странице. Эта служба отвечает таким же образом, как и в [базовой службы AJAX](../../../../docs/framework/wcf/samples/basic-ajax-service.md) примера с помощью запроса GET.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) Чтобы загрузить все [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] образцов. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\PostAjaxService`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Настройка, сборка и выполнение образца  
  
1.  Убедитесь, что инструкции по установке [выполняемая однократно процедура настройки для образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Постройте решение PostAjaxService.sln, как описано в [сборка образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Перейдите к http://localhost/ServiceModelSamples/PostAjaxClientPage.aspx (не открывайте PostAjaxClientPage.aspx в браузере из каталога проекта).  
  
## <a name="see-also"></a>См. также
