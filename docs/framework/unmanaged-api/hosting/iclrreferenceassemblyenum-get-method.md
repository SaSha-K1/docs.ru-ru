---
title: Метод ICLRReferenceAssemblyEnum::Get
ms.date: 03/30/2017
api_name:
- ICLRReferenceAssemblyEnum.Get
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRReferenceAssemblyEnum::Get
helpviewer_keywords:
- ICLRReferenceAssemblyEnum::Get method [.NET Framework hosting]
- Get method, ICLRReferenceAssemblyEnum interface [.NET Framework hosting]
ms.assetid: f21c1612-9c5d-4abc-a337-577086d29c17
topic_type:
- apiref
ms.openlocfilehash: 3968adf418fcea847ee2be5a412385d041a53544
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728914"
---
# <a name="iclrreferenceassemblyenumget-method"></a>Метод ICLRReferenceAssemblyEnum::Get

Возвращает удостоверение сборки по заданному индексу.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT Get (  
    [in] DWORD dwIndex,  
    [out, size_is(*pcchBufferSize)] LPWSTR pwzBuffer,  
    [in, out] DWORD *pcchBufferSize  
);  
```  
  
## <a name="parameters"></a>Параметры  

 `dwIndex`  
 окне Отсчитываемый от нуля индекс возвращаемого удостоверения сборки.  
  
 `pwzBuffer`  
 заполняет Буфер, содержащий данные удостоверения сборки.  
  
 `pcchBufferSize`  
 [вход, выход] Размер `pwzBuffer` буфера.  
  
## <a name="return-value"></a>Возвращаемое значение  
  
|HRESULT|Описание:|  
|-------------|-----------------|  
|S_OK|`Get` успешно возвращено.|  
|ERROR_INSUFFICIENT_BUFFER|`pwzBuffer` слишком мал.|  
|ERROR_NO_MORE_ITEMS|Перечисление не содержит больше элементов.|  
|HOST_E_CLRNOTAVAILABLE|Среда CLR не была загружена в процесс, или среда CLR находится в состоянии, в котором она не может выполнить управляемый код или успешно обработать вызов.|  
|HOST_E_TIMEOUT|Время ожидания вызова истекло.|  
|HOST_E_NOT_OWNER|Вызывающий объект не владеет блокировкой.|  
|HOST_E_ABANDONED|Событие было отменено, пока заблокированный поток или волокно ожидают его.|  
|E_FAIL|Произошла неизвестная фатальная ошибка. Если метод возвращает E_FAIL, среда CLR больше не может использоваться в процессе. Последующие вызовы методов размещения возвращают HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Комментарии  

 `Get` обычно вызывается дважды. Первый вызов предоставляет значение NULL для `pwzBuffer` , а устанавливает `pcchBufferSize` в качестве размера, соответствующего `pwzBuffer` . Второй вызов предоставляет соответствующий размер `pwzBuffer` и содержит канонические данные удостоверений сборки после завершения.  
  
## <a name="requirements"></a>Требования  

 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** MSCorEE. h  
  
 **Библиотека:** Включается в качестве ресурса в MSCorEE.dll  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Интерфейс ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)
- [Интерфейс ICLRReferenceAssemblyEnum](iclrreferenceassemblyenum-interface.md)
