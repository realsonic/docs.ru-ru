---
title: "Метод ICorDebugHeapValue3::GetThreadOwningMonitorLock"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugHeapValue3.GetThreadOwningMonitorLock
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugHeapValue3::GetThreadOwningMonitorLock
helpviewer_keywords:
- GetThreadOwningMonitorLock method [.NET Framework debugging]
- ICorDebugHeapValue3::GetThreadOwningMonitorLock method [.NET Framework debugging]
ms.assetid: e06fc19d-2cf4-4cad-81a3-137a68af8969
topic_type: apiref
caps.latest.revision: "6"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 3571f546f71515a980c5415e568ae85eb0863d42
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugheapvalue3getthreadowningmonitorlock-method"></a><span data-ttu-id="aaa75-102">Метод ICorDebugHeapValue3::GetThreadOwningMonitorLock</span><span class="sxs-lookup"><span data-stu-id="aaa75-102">ICorDebugHeapValue3::GetThreadOwningMonitorLock Method</span></span>
<span data-ttu-id="aaa75-103">Возвращает управляемый поток, который владеет блокировкой монитора на этот объект.</span><span class="sxs-lookup"><span data-stu-id="aaa75-103">Returns the managed thread that owns the monitor lock on this object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="aaa75-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="aaa75-104">Syntax</span></span>  
  
```  
HRESULT GetThreadOwningMonitorLock (  
    [out] ICorDebugThread   **ppThread,  
    [out] DWORD              *pAcquisitionCount  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="aaa75-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="aaa75-105">Parameters</span></span>  
 `ppThread`  
 <span data-ttu-id="aaa75-106">[out] Управляемый поток владеет блокировкой монитора на этот объект.</span><span class="sxs-lookup"><span data-stu-id="aaa75-106">[out] The managed thread that owns the monitor lock on this object.</span></span>  
  
 `pAcquisitionCount`  
 <span data-ttu-id="aaa75-107">[out] Количество раз, этот поток будет необходимо снять блокировку перед возвратом монитором.</span><span class="sxs-lookup"><span data-stu-id="aaa75-107">[out] The number of times this thread would have to release the lock before it returns to being unowned.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="aaa75-108">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="aaa75-108">Return Value</span></span>  
 <span data-ttu-id="aaa75-109">Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.</span><span class="sxs-lookup"><span data-stu-id="aaa75-109">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="aaa75-110">HRESULT</span><span class="sxs-lookup"><span data-stu-id="aaa75-110">HRESULT</span></span>|<span data-ttu-id="aaa75-111">Описание</span><span class="sxs-lookup"><span data-stu-id="aaa75-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="aaa75-112">S_OK</span><span class="sxs-lookup"><span data-stu-id="aaa75-112">S_OK</span></span>|<span data-ttu-id="aaa75-113">Метод завершился успешно.</span><span class="sxs-lookup"><span data-stu-id="aaa75-113">The method completed successfully.</span></span>|  
|<span data-ttu-id="aaa75-114">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="aaa75-114">S_FALSE</span></span>|<span data-ttu-id="aaa75-115">Не управляемый поток владеет блокировкой монитора на этот объект.</span><span class="sxs-lookup"><span data-stu-id="aaa75-115">No managed thread owns the monitor lock on this object.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="aaa75-116">Исключения</span><span class="sxs-lookup"><span data-stu-id="aaa75-116">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="aaa75-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="aaa75-117">Remarks</span></span>  
 <span data-ttu-id="aaa75-118">Если управляемый поток владеет блокировкой монитора на этот объект:</span><span class="sxs-lookup"><span data-stu-id="aaa75-118">If a managed thread owns the monitor lock on this object:</span></span>  
  
-   <span data-ttu-id="aaa75-119">Метод возвращает значение S_OK.</span><span class="sxs-lookup"><span data-stu-id="aaa75-119">The method returns S_OK.</span></span>  
  
-   <span data-ttu-id="aaa75-120">Объект потока действителен до завершения потока.</span><span class="sxs-lookup"><span data-stu-id="aaa75-120">The thread object is valid until the thread exits.</span></span>  
  
 <span data-ttu-id="aaa75-121">Если нет управляемого потока, владеющего блокировкой монитора на этот объект `ppThread` и `pAcquisitionCount` не изменяются, и метод возвращает значение S_FALSE.</span><span class="sxs-lookup"><span data-stu-id="aaa75-121">If no managed thread owns the monitor lock on this object, `ppThread` and `pAcquisitionCount` are unchanged, and the method returns S_FALSE.</span></span>  
  
 <span data-ttu-id="aaa75-122">Если `ppThread` или `pAcquisitionCount` не является допустимым указателем, результат будет неопределенным.</span><span class="sxs-lookup"><span data-stu-id="aaa75-122">If `ppThread` or `pAcquisitionCount` is not a valid pointer, the result is undefined.</span></span>  
  
 <span data-ttu-id="aaa75-123">При возникновении ошибки таким образом, что он не может определить, какие при его наличии, поток владеет блокировкой монитора на этот объект, метод возвращает значение HRESULT, указывающее на сбой.</span><span class="sxs-lookup"><span data-stu-id="aaa75-123">If an error occurs such that it cannot be determined which, if any, thread owns the monitor lock on this object, the method returns an HRESULT that indicates failure.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="aaa75-124">Требования</span><span class="sxs-lookup"><span data-stu-id="aaa75-124">Requirements</span></span>  
 <span data-ttu-id="aaa75-125">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="aaa75-125">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="aaa75-126">**Заголовок:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="aaa75-126">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="aaa75-127">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="aaa75-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="aaa75-128">**Версии платформы .NET framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="aaa75-128">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="aaa75-129">См. также</span><span class="sxs-lookup"><span data-stu-id="aaa75-129">See Also</span></span>  
 [<span data-ttu-id="aaa75-130">Интерфейсы отладки</span><span class="sxs-lookup"><span data-stu-id="aaa75-130">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="aaa75-131">Отладка</span><span class="sxs-lookup"><span data-stu-id="aaa75-131">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)