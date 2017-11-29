---
title: "Функция NextMethod (Справочник по неуправляемым API)"
description: "Функция NextMethod получает следующий метод в перечислении."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: NextMethod
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: NextMethod
helpviewer_keywords: NextMethod function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: d9b14424bb914be3ba127670e1b6490f79854d6e
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="nextmethod-function"></a><span data-ttu-id="56c1d-103">Функция NextMethod</span><span class="sxs-lookup"><span data-stu-id="56c1d-103">NextMethod function</span></span>
<span data-ttu-id="56c1d-104">Извлекает следующий метод в перечисление, которое начинается с вызова [BeginMethodEnumeration](beginmethodenumeration.md).</span><span class="sxs-lookup"><span data-stu-id="56c1d-104">Retrieves the next method in an enumeration that begins with a call to [BeginMethodEnumeration](beginmethodenumeration.md).</span></span>  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="56c1d-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="56c1d-105">Syntax</span></span>  
  
```  
HRESULT NextMethod (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature   
); 
```  

## <a name="parameters"></a><span data-ttu-id="56c1d-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="56c1d-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="56c1d-107">[in] Этот параметр не используется.</span><span class="sxs-lookup"><span data-stu-id="56c1d-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="56c1d-108">[in] Указатель на [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) экземпляра.</span><span class="sxs-lookup"><span data-stu-id="56c1d-108">[in] A pointer to an [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) instance.</span></span>

`lFlags`  
<span data-ttu-id="56c1d-109">[in] Зарезервировано.</span><span class="sxs-lookup"><span data-stu-id="56c1d-109">[in] Reserved.</span></span> <span data-ttu-id="56c1d-110">Этот параметр должен быть 0.</span><span class="sxs-lookup"><span data-stu-id="56c1d-110">This parameter must be 0.</span></span>

`pName`  
<span data-ttu-id="56c1d-111">[out] Указатель, который указывает на `null` до вызова метода.</span><span class="sxs-lookup"><span data-stu-id="56c1d-111">[out] A pointer that points to `null` prior to the call.</span></span> <span data-ttu-id="56c1d-112">Когда функция возвращает, новый адрес `BSTR` , содержащий имя метода.</span><span class="sxs-lookup"><span data-stu-id="56c1d-112">When the function returns, the address of a new `BSTR` that contains the method name.</span></span> 

`ppSignatureIn`  
<span data-ttu-id="56c1d-113">[out] Указатель, получающий указатель [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) , содержащий `in` параметры для метода.</span><span class="sxs-lookup"><span data-stu-id="56c1d-113">[out] A pointer that receives a pointer to an [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) that contains the `in` parameters for the method.</span></span> 

`ppSignatureOut`  
<span data-ttu-id="56c1d-114">[out] Указатель, получающий указатель [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) , содержащий `out` параметры для метода.</span><span class="sxs-lookup"><span data-stu-id="56c1d-114">[out] A pointer that receives a pointer to an [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) that contains the `out` parameters for the method.</span></span> 

## <a name="return-value"></a><span data-ttu-id="56c1d-115">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="56c1d-115">Return value</span></span>

<span data-ttu-id="56c1d-116">Следующие значения, возвращаемые этой функцией, определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде:</span><span class="sxs-lookup"><span data-stu-id="56c1d-116">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="56c1d-117">Константа</span><span class="sxs-lookup"><span data-stu-id="56c1d-117">Constant</span></span>  |<span data-ttu-id="56c1d-118">Значение</span><span class="sxs-lookup"><span data-stu-id="56c1d-118">Value</span></span>  |<span data-ttu-id="56c1d-119">Описание</span><span class="sxs-lookup"><span data-stu-id="56c1d-119">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | <span data-ttu-id="56c1d-120">0x8004101d</span><span class="sxs-lookup"><span data-stu-id="56c1d-120">0x8004101d</span></span> | <span data-ttu-id="56c1d-121">Был не вызов [ `BeginEnumeration` ](beginenumeration.md) функции.</span><span class="sxs-lookup"><span data-stu-id="56c1d-121">There was no call to the [`BeginEnumeration`](beginenumeration.md) function.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="56c1d-122">0</span><span class="sxs-lookup"><span data-stu-id="56c1d-122">0</span></span> | <span data-ttu-id="56c1d-123">Успешный вызов функции.</span><span class="sxs-lookup"><span data-stu-id="56c1d-123">The function call was successful.</span></span>  |
| `WBEM_S_NO_MORE_DATA` | <span data-ttu-id="56c1d-124">0x40005</span><span class="sxs-lookup"><span data-stu-id="56c1d-124">0x40005</span></span> | <span data-ttu-id="56c1d-125">Нет дополнительных свойств в перечислении.</span><span class="sxs-lookup"><span data-stu-id="56c1d-125">There are no more properties in the enumeration.</span></span> |
  
## <a name="remarks"></a><span data-ttu-id="56c1d-126">Примечания</span><span class="sxs-lookup"><span data-stu-id="56c1d-126">Remarks</span></span>

<span data-ttu-id="56c1d-127">Эта функция создает оболочку для вызова [IWbemClassObject::NextMethod](https://msdn.microsoft.com/library/aa391454(v=vs.85).aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="56c1d-127">This function wraps a call to the [IWbemClassObject::NextMethod](https://msdn.microsoft.com/library/aa391454(v=vs.85).aspx) method.</span></span>

<span data-ttu-id="56c1d-128">Вызывающий объект начинается последовательность перечисления путем вызова метода [BeginMethodEnumeration](beginmethodenumeration.md) функции, а затем вызывает функцию [NextMethod] до возврата функции `WBEM_S_NO_MORE_DATA`.</span><span class="sxs-lookup"><span data-stu-id="56c1d-128">The caller begins the enumeration sequence by calling the [BeginMethodEnumeration](beginmethodenumeration.md) function, and then calls the [NextMethod] function until the function returns `WBEM_S_NO_MORE_DATA`.</span></span> <span data-ttu-id="56c1d-129">При необходимости, вызывающий объект завершения последовательности путем вызова [EndMethodEnumeration](endmethodenumeration.md).</span><span class="sxs-lookup"><span data-stu-id="56c1d-129">Optionally, the caller finishes the sequence by calling [EndMethodEnumeration](endmethodenumeration.md).</span></span> <span data-ttu-id="56c1d-130">Вызывающий объект может завершить перечисление раньше путем вызова [EndMethodEnumeration](endmethodenumeration.md) в любое время.</span><span class="sxs-lookup"><span data-stu-id="56c1d-130">The caller may terminate the enumeration early by calling [EndMethodEnumeration](endmethodenumeration.md) at any time.</span></span>

## <a name="example"></a><span data-ttu-id="56c1d-131">Пример</span><span class="sxs-lookup"><span data-stu-id="56c1d-131">Example</span></span>

<span data-ttu-id="56c1d-132">Пример C++ см. в разделе [IWbemClassObject::NextMethod](https://msdn.microsoft.com/library/aa391454(v=vs.85).aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="56c1d-132">For a C++ example, see the [IWbemClassObject::NextMethod](https://msdn.microsoft.com/library/aa391454(v=vs.85).aspx) method.</span></span>

## <a name="requirements"></a><span data-ttu-id="56c1d-133">Требования</span><span class="sxs-lookup"><span data-stu-id="56c1d-133">Requirements</span></span>  
 <span data-ttu-id="56c1d-134">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="56c1d-134">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="56c1d-135">**Заголовок:** WMINet_Utils.idl</span><span class="sxs-lookup"><span data-stu-id="56c1d-135">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="56c1d-136">**Версии платформы .NET framework:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="56c1d-136">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="56c1d-137">См. также</span><span class="sxs-lookup"><span data-stu-id="56c1d-137">See also</span></span>  
[<span data-ttu-id="56c1d-138">WMI и счетчиков производительности (Справочник по неуправляемым API)</span><span class="sxs-lookup"><span data-stu-id="56c1d-138">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)