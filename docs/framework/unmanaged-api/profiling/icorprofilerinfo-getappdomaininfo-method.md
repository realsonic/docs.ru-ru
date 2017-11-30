---
title: "Метод ICorProfilerInfo::GetAppDomainInfo"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetAppDomainInfo
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetAppDomainInfo
helpviewer_keywords:
- ICorProfilerInfo::GetAppDomainInfo method [.NET Framework profiling]
- GetAppDomainInfo method [.NET Framework profiling]
ms.assetid: a6bf5a04-e03e-44f0-917a-96f6a6d3cc96
topic_type: apiref
caps.latest.revision: "23"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: c31d3c61a868bf741213f6e505d91524cc925207
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfogetappdomaininfo-method"></a><span data-ttu-id="59653-102">Метод ICorProfilerInfo::GetAppDomainInfo</span><span class="sxs-lookup"><span data-stu-id="59653-102">ICorProfilerInfo::GetAppDomainInfo Method</span></span>
<span data-ttu-id="59653-103">Принимает идентификатор домена приложения.</span><span class="sxs-lookup"><span data-stu-id="59653-103">Accepts an application domain ID.</span></span> <span data-ttu-id="59653-104">Возвращает имя домена приложения и идентификатор процесса, который его содержит.</span><span class="sxs-lookup"><span data-stu-id="59653-104">Returns an application domain name and the ID of the process that contains it.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="59653-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="59653-105">Syntax</span></span>  
  
```  
HRESULT GetAppDomainInfo(  
    [in]  AppDomainID appDomainId,  
    [in]  ULONG       cchName,  
    [out] ULONG       *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR       szName[] ,  
    [out] ProcessID   *pProcessId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="59653-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="59653-106">Parameters</span></span>  
 `appDomainId`  
 <span data-ttu-id="59653-107">[in] Идентификатор домена приложения.</span><span class="sxs-lookup"><span data-stu-id="59653-107">[in] The ID of the application domain.</span></span>  
  
 `cchName`  
 <span data-ttu-id="59653-108">[in] Длина буфера возврата `szName` в символах.</span><span class="sxs-lookup"><span data-stu-id="59653-108">[in] The length, in characters, of the `szName` return buffer.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="59653-109">[out] Указатель на общую длину имени домена приложения в символах.</span><span class="sxs-lookup"><span data-stu-id="59653-109">[out] A pointer to the total character length of the application domain name.</span></span>  
  
 `szName`  
 <span data-ttu-id="59653-110">[out] Буфер расширенных символов, предоставленный вызывающим объектом.</span><span class="sxs-lookup"><span data-stu-id="59653-110">[out] A caller-provided wide character buffer.</span></span> <span data-ttu-id="59653-111">При возврате метода параметр `szName` будет содержать полное или частичное имя домена приложения.</span><span class="sxs-lookup"><span data-stu-id="59653-111">When the method returns, `szName` will contain the full or partial application domain name.</span></span>  
  
 `pProcessId`  
 <span data-ttu-id="59653-112">[out] Указатель на идентификатор процесса, который содержит этот домен приложения.</span><span class="sxs-lookup"><span data-stu-id="59653-112">[out] A pointer to the ID of the process that contains the application domain.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="59653-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="59653-113">Remarks</span></span>  
 <span data-ttu-id="59653-114">После возврата этого метода необходимо убедиться, что буфер `szName` был достаточно велик, чтобы вместить в себя полное имя домена приложения.</span><span class="sxs-lookup"><span data-stu-id="59653-114">After this method returns, you must verify that the `szName` buffer was large enough to contain the full name of the application domain.</span></span> <span data-ttu-id="59653-115">Для этого сравните значение, на которое указывает параметр `pcchName`, со значением параметра `cchName`.</span><span class="sxs-lookup"><span data-stu-id="59653-115">To do this, compare the value that `pcchName` points to with the value of the `cchName` parameter.</span></span> <span data-ttu-id="59653-116">Если параметр `pcchName` указывает на значение, превышающее значение `cchName`, выделите буфер `szName` большего размера, обновите параметр `cchName`, задав новый, больший размер, и вызовите метод `GetAppDomainInfo` снова.</span><span class="sxs-lookup"><span data-stu-id="59653-116">If `pcchName` points to a value that is larger than `cchName`, allocate a larger `szName` buffer, update `cchName` with the new, larger size, and call `GetAppDomainInfo` again.</span></span>  
  
 <span data-ttu-id="59653-117">Кроме того, сначала можно вызвать метод `GetAppDomainInfo` с буфером `szName` нулевой длины для получения правильного размера буфера.</span><span class="sxs-lookup"><span data-stu-id="59653-117">Alternatively, you can first call `GetAppDomainInfo` with a zero-length `szName` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="59653-118">Затем можно задать размер буфера равным значению, возвращенному в параметре `pcchName`, и вызвать метод `GetAppDomainInfo` снова.</span><span class="sxs-lookup"><span data-stu-id="59653-118">You can then set the buffer size to the value returned in `pcchName` and call `GetAppDomainInfo` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="59653-119">Требования</span><span class="sxs-lookup"><span data-stu-id="59653-119">Requirements</span></span>  
 <span data-ttu-id="59653-120">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="59653-120">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="59653-121">**Заголовок:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="59653-121">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="59653-122">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="59653-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="59653-123">**Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="59653-123">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="59653-124">См. также</span><span class="sxs-lookup"><span data-stu-id="59653-124">See Also</span></span>  
 [<span data-ttu-id="59653-125">ICorProfilerInfo-интерфейс</span><span class="sxs-lookup"><span data-stu-id="59653-125">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [<span data-ttu-id="59653-126">Интерфейсы профилирования</span><span class="sxs-lookup"><span data-stu-id="59653-126">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [<span data-ttu-id="59653-127">Профилирование</span><span class="sxs-lookup"><span data-stu-id="59653-127">Profiling</span></span>](../../../../docs/framework/unmanaged-api/profiling/index.md)