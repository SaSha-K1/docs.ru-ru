---
title: Метод ICoreClrDebugTarget::EnumRuntimes
ms.date: 03/30/2017
api_name:
- ICoreClrDebugTarget.EnumRuntimes
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget::EnumRuntimes
helpviewer_keywords:
- remote debugging API [Silverlight]
- ICorClrDebugTarget::EnumRuntimes method [Silverlight debugging]
- EnumRuntimes method, ICoreClrDebugTarget interface [Silverlight debugging]
- Silverlight, remote debugging
ms.assetid: 316df866-442d-40cc-b049-45e8adcb65d1
topic_type:
- apiref
ms.openlocfilehash: 093f49508e8e96a4003f1aab8eed59e2fd196ba9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679277"
---
# <a name="icoreclrdebugtargetenumruntimes-method"></a>Метод ICoreClrDebugTarget::EnumRuntimes

Перечисляет среды CLR в указанном процессе, который выполняется на удаленном компьютере.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT EnumRuntimes (  
      [in] DWORD       dwInternalProcessID,  
      [out] DWORD*     pcRuntimes,  
      [out] CoreClrDebugRuntimeInfo**    ppRuntimes  
    );  
```  
  
## <a name="parameters"></a>Параметры  

 `dwInternalProcessID`  
 [in] Внутренний идентификатор процесса, для которого требуется перечислить среды выполнения. Это будет `m_dwInternalID` из соответствующего [CoreClrDebugProcInfo](coreclrdebugprocinfo-structure.md).  
  
 `pcRuntimes`  
 [out] Число сред выполнения, возвращаемых в `ppRuntimes`. Это значение может быть 0 (ноль).  
  
 `ppRuntimes`  
 заполняет Массив структур [кореклрдебугрунтимеинфо](coreclrdebugruntimeinfo-structure.md) , представляющих среды выполнения, загруженные в удаленном целевом процессе.  
  
## <a name="return-value"></a>Возвращаемое значение  

 S_OK  
 Успешно.  
  
 S_FALSE  
 `dwInternalProcessID` не соответствует ни одному процессу, который выполняется на компьютере, возможно потому, что этот процесс был завершен. `pcRuntimes` и `ppRuntimes` будут иметь значение null.  
  
 E_OUTOFMEMORY  
 Не удается выделить достаточно памяти для `ppRuntimes`.  
  
 E_FAIL (или другие коды возврата E_)  
 Прочие сбои.  
  
## <a name="remarks"></a>Комментарии  

 Чтобы освободить память, выделенную этим методом, вызовите метод [ICoreClrDebugTarget:: FreeMemory](icoreclrdebugtarget-freememory-method.md) .  
  
## <a name="requirements"></a>Требования  

 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** Кореклрремотедебуггингинтерфацес. h  
  
 **Библиотека:** mscordbi_macx86.dll  
  
 **.NET Framework версии:** 3,5 SP1  
  
## <a name="see-also"></a>См. также раздел

- [Интерфейс ICoreClrDebugTarget](icoreclrdebugtarget-interface.md)
