---
title: ICorRuntimeHost::NextDomain 메서드
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.NextDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::NextDomain
helpviewer_keywords:
- ICorRuntimeHost::NextDomain method [.NET Framework hosting]
- NextDomain method [.NET Framework hosting]
ms.assetid: fe07a05b-f6d6-44b5-ab01-b9a6eb15c350
topic_type:
- apiref
ms.openlocfilehash: 36eacedfb83c1248fc252091872bcfeecdbcd874
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73139503"
---
# <a name="icorruntimehostnextdomain-method"></a>ICorRuntimeHost::NextDomain 메서드
열거형의 다음 도메인에 대 한 인터페이스 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT NextDomain (  
    [in] HCORENUM hEnum,  
    [out] void** pAppDomain  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `hEnum`  
 진행 [Enumdomains](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-enumdomains-method.md)호출을 통해 가져온 열거자입니다.  
  
 `pAppDomain`  
 제한이 열거형의 다음 도메인을 나타내는 <xref:System._AppDomain?displayProperty=nameWithType> 형식에 대 한 인터페이스 포인터 이거나, 더 이상 도메인이 없는 경우 null입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|작업에 성공 했습니다.|  
|S_FALSE|작업을 완료 하지 못했거나 열거에 도메인이 더 이상 없습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL을 반환 하는 경우 프로세스에서 CLR (공용 언어 런타임)을 더 이상 사용할 수 없습니다. 모든 호스팅 Api에 대 한 후속 호출은 HOST_E_CLRNOTAVAILABLE을 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Mscoree.dll  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** 1.0, 1.1  
  
## <a name="see-also"></a>참조

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [ICorRuntimeHost 인터페이스](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)
