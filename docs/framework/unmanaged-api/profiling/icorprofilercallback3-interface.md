---
title: ICorProfilerCallback3 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback3
helpviewer_keywords:
- ICorProfilerCallback3 interface [.NET Framework profiling]
ms.assetid: be83af41-3dec-4c77-8529-9dd6b8042af6
topic_type:
- apiref
ms.openlocfilehash: ad9c5445cbef0be7919570db64b027556d923752
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76865573"
---
# <a name="icorprofilercallback3-interface"></a>ICorProfilerCallback3 인터페이스
CLR (공용 언어 런타임)에서 연결 및 분리 상태 정보를 프로파일러에 전달 하는 데 사용 하는 콜백 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[InitializeForAttach 메서드](icorprofilercallback3-initializeforattach-method.md)|프로파일러가 연결 작업 후 상태를 초기화할 수 있도록 하기 위해 CLR에서 호출 됩니다.|  
|[ProfilerAttachComplete 메서드](icorprofilercallback3-profilerattachcomplete-method.md)|프로파일러가 이제 catch 메서드를 호출할 수 있음을 나타내기 위해 CLR에서 호출 됩니다.|  
|[ProfilerDetachSucceeded 메서드](icorprofilercallback3-profilerdetachsucceeded-method.md)|CLR(공용 언어 런타임)이 프로파일러 DLL을 언로드한다고 프로파일러에 알립니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참조

- [프로파일링 인터페이스](profiling-interfaces.md)
- [ICorProfilerInfo 인터페이스](icorprofilerinfo-interface.md)
- [ICorProfilerCallback2 인터페이스](icorprofilercallback2-interface.md)
- [ICorProfilerCallback4 인터페이스](icorprofilercallback4-interface.md)
