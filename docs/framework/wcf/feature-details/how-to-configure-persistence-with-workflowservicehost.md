---
title: Как настроить сохраняемость с помощью WorkflowServiceHost
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: de177180dc22fc3236924da691cf9b1f594519ce
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2018
---
# <a name="how-to-configure-persistence-with-workflowservicehost"></a>Как настроить сохраняемость с помощью WorkflowServiceHost
В данном разделе описывается способ настройки функции хранилища экземпляров рабочих процессов SQL для включения сохраняемости рабочих процессов, размещенных в <xref:System.ServiceModel.Activities.WorkflowServiceHost>, с помощью файла конфигурации. Перед использованием возможности хранилища экземпляров рабочих процессов SQL необходимо создать базу данных SQL, которая используется для хранения экземпляров рабочих процессов. Дополнительные сведения см. в разделе [как: включить сохраняемость SQL для рабочих процессов и служб рабочих процессов](../../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-configuration"></a>Настройка хранилища экземпляров рабочих процессов SQL в конфигурации  
  
1.  Свойства хранилища экземпляров рабочих процессов SQL можно настроить с помощью объекта <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> - поведения службы, позволяющего менять параметры с помощью конфигурации XML. В следующем примере конфигурации показано, как настроить хранилище экземпляров рабочих процессов SQL с помощью элемента поведения <`sqlWorkflowInstanceStore`> в файле конфигурации.  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore   
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"   
                 runnableInstancesDetectionPeriod="00:00:05">  
            <sqlWorkflowInstanceStore/>  
        </behavior>  
    </serviceBehaviors>  
    ```  
  
     Дополнительные сведения о том, как настроить хранилище экземпляров рабочих процессов SQL см. в разделе [как: включить сохраняемость SQL для рабочих процессов и служб рабочих процессов](../../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md). Дополнительные сведения об отдельных параметрах для <`sqlWorkflowInstanceStore`> элемент поведения в разделе [хранилище экземпляров рабочих процессов SQL](../../../../docs/framework/windows-workflow-foundation/sql-workflow-instance-store.md). Фабрика приложений Windows Server имеет собственное хранилище сохраняемости. Дополнительные сведения см. в разделе [Windows Server App Fabric сохраняемости](http://go.microsoft.com/fwlink/?LinkId=193121).  
  
    > [!NOTE]
    >  В предыдущем примере конфигурации используется упрощенная конфигурация. Дополнительные сведения см. в разделе [упрощенной конфигурации](../../../../docs/framework/wcf/simplified-configuration.md)  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-code"></a>Настройка хранилища экземпляров рабочих процессов SQL в коде  
  
1.  Свойства хранилища экземпляров рабочих процессов SQL можно настроить с помощью объекта <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>, определяющего поведение службы, позволяющее менять параметры с помощью кода. В следующем примере показано, как настроить хранилище экземпляров рабочих процессов SQL с помощью элемента поведения <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> в коде.  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     Дополнительные сведения о том, как настроить хранилище экземпляров рабочих процессов SQL см. в разделе [как: включить сохраняемость SQL для рабочих процессов и служб рабочих процессов](../../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md). Дополнительные сведения об отдельных параметрах для <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> элемента поведения в разделе [хранилище экземпляров рабочих процессов SQL](../../../../docs/framework/windows-workflow-foundation/sql-workflow-instance-store.md). Фабрика приложений Windows Server имеет собственное хранилище сохраняемости. Дополнительные сведения см. в разделе [Windows Server App Fabric сохраняемости](http://go.microsoft.com/fwlink/?LinkId=193121).  
  
    > [!NOTE]
    >  В предыдущем примере конфигурации используется упрощенная конфигурация. Дополнительные сведения см. в разделе [упрощенной конфигурации](../../../../docs/framework/wcf/simplified-configuration.md)  
  
     Пример того, как для программной настройки сохраняемости см [как: Включение сохраняемости для рабочих процессов и служб рабочих процессов](../../../../docs/framework/windows-workflow-foundation/how-to-enable-persistence-for-workflows-and-workflow-services.md).  
  
## <a name="see-also"></a>См. также  
 [Службы рабочих процессов](../../../../docs/framework/wcf/feature-details/workflow-services.md)  
 [Сохраняемость рабочих процессов](../../../../docs/framework/windows-workflow-foundation/workflow-persistence.md)  
 [Windows Server App Fabric сохраняемости](http://go.microsoft.com/fwlink/?LinkId=193121)
