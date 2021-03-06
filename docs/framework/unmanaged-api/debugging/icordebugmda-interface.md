---
title: ICorDebugMDA 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugMDA
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA
helpviewer_keywords:
- ICorDebugMDA interface [.NET Framework debugging]
ms.assetid: 8ecbb854-295c-4dd4-b9fc-01ebeac46e06
topic_type:
- apiref
ms.openlocfilehash: a147aee1ebba57b86dbbf8a7648456b8d7494936
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76793193"
---
# <a name="icordebugmda-interface"></a>ICorDebugMDA 인터페이스
MDA(관리 디버깅 도우미) 메시지를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetDescription 메서드](icordebugmda-getdescription-method.md)|이 MDA에 대 한 설명을 포함 하는 문자열을 가져옵니다.|  
|[GetFlags 메서드](icordebugmda-getflags-method.md)|이 MDA와 연결 된 플래그를 가져옵니다.|  
|[GetName 메서드](icordebugmda-getname-method.md)|이 MDA의 이름을 포함 하는 문자열을 가져옵니다.|  
|[GetOSThreadId 메서드](icordebugmda-getosthreadid-method.md)|이 MDA가 실행 되 고 있는 운영 체제 스레드 식별자를 가져옵니다.|  
|[GetXML 메서드](icordebugmda-getxml-method.md)|이 MDA와 연결 된 전체 XML 스트림을 가져옵니다.|  
  
## <a name="remarks"></a>주의  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참조

- [디버깅 인터페이스](debugging-interfaces.md)
- [관리 디버깅 도우미를 사용하여 오류 진단](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
