---
title: IHostIoCompletionManager::GetMaxThreads 메서드
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.GetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::GetMaxThreads
helpviewer_keywords:
- IHostIoCompletionManager::GetMaxThreads method [.NET Framework hosting]
- GetMaxThreads method, IHostIoCompletionManager interface [.NET Framework hosting]
ms.assetid: e7a6cadc-2433-4472-a701-58891abcde45
topic_type:
- apiref
ms.openlocfilehash: d35fd91f2a28c392176a6dd87bd21baa964ee9a9
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73133810"
---
# <a name="ihostiocompletionmanagergetmaxthreads-method"></a>IHostIoCompletionManager::GetMaxThreads 메서드
호스트가 i/o 요청을 처리 하기 위해 할당할 수 있는 최대 스레드 수를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetMaxThreads (  
    [out] DWORD *pdwMaxIoCompletionThreads  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pdwMaxIoCompletionThreads`  
 제한이 호스트에서 i/o 요청을 처리 하기 위해 할당할 수 있는 스레드 풀의 최대 스레드 수에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|`GetMaxThreads` 성공적으로 반환 되었습니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR (공용 언어 런타임)이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|차단 된 스레드나 파이버에서 대기 하는 동안 이벤트를 취소 했습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL을 반환 하는 경우 프로세스 내에서 더 이상 CLR을 사용할 수 없습니다. 호스팅 메서드에 대 한 후속 호출은 HOST_E_CLRNOTAVAILABLE을 반환 합니다.|  
|E_NOTIMPL|호스트는 `GetMaxThreads`구현을 제공 하지 않습니다.|  
  
## <a name="remarks"></a>주의  
 호스트는 구현, 성능 또는 확장성과 같은 이유로 i/o 요청을 처리 하기 위해 할당할 수 있는 스레드 수에 대 한 배타적 제어를 원할 수 있습니다. 따라서 호스트는 `GetMaxThreads`를 구현 하지 않아도 됩니다. 이 경우 호스트는이 메서드에서 E_NOTIMPL을 반환 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Mscoree.dll  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참조

- [ICLRIoCompletionManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md)
- [IHostIoCompletionManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)
