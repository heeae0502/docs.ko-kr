---
title: ICorDebugMDA::GetDescription 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugMDA.GetDescription
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA::GetDescription
helpviewer_keywords:
- GetDescription method [.NET Framework debugging]
- ICorDebugMDA::GetDescription method [.NET Framework debugging]
ms.assetid: 01d1b481-ca67-4712-8744-d342ec0df639
topic_type:
- apiref
ms.openlocfilehash: e3744cbfa08de30c53f15c457034b50e2fc5d283
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76793244"
---
# <a name="icordebugmdagetdescription-method"></a>ICorDebugMDA::GetDescription 메서드
[ICorDebugMDA](icordebugmda-interface.md)로 표시 된 MDA (관리 디버깅 도우미)에 대 한 설명을 포함 하는 문자열을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetDescription (  
    [in] ULONG32   cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
        WCHAR      szName[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cchName`  
 진행 설명을 저장 하는 문자열 버퍼의 크기입니다.  
  
 `pcchName`  
 제한이 문자열 버퍼에서 반환 된 바이트 수에 대 한 포인터입니다.  
  
 `szName`  
 제한이 MDA에 대 한 설명을 포함 하는 문자열 버퍼입니다.  
  
## <a name="remarks"></a>주의  
 문자열의 길이는 0 일 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참조

- [ICorDebugMDA 인터페이스](icordebugmda-interface.md)
- [관리 디버깅 도우미를 사용하여 오류 진단](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
