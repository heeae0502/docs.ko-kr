---
title: ICorDebugProcess2::SetUnmanagedBreakpoint 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetUnmanagedBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint
helpviewer_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint method [.NET Framework debugging]
- SetUnmanagedBreakpoint method [.NET Framework debugging]
ms.assetid: 93829d15-d942-4e2d-b7a4-dfc9d7fb96be
topic_type:
- apiref
ms.openlocfilehash: fb8b8f3e29c141e91587a4d0cdc81cdabccdbc9e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79178644"
---
# <a name="icordebugprocess2setunmanagedbreakpoint-method"></a>ICorDebugProcess2::SetUnmanagedBreakpoint 메서드
지정된 네이티브 이미지 오프셋에서 관리되지 않는 중단점을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetUnmanagedBreakpoint (  
    [in]  CORDB_ADDRESS    address,  
    [in]  ULONG32          bufsize,  
    [out, size_is(bufsize), length_is(*bufLen)]
        BYTE               buffer[],  
    [out] ULONG32          *bufLen  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `address`  
 【인】 기본 `CORDB_ADDRESS` 이미지 오프셋을 지정하는 개체입니다.  
  
 `bufsize`  
 【인】 배열의 크기(바이트)입니다. `buffer`  
  
 `buffer`  
 【아웃】 중단점으로 대체되는 opcode를 포함하는 배열입니다.  
  
 `bufLen`  
 【아웃】 배열에서 반환되는 바이트 수에 `buffer` 대한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 네이티브 이미지 오프셋이 공통 언어 런타임(CLR) 내에 있으면 중단점은 무시됩니다. 이렇게 하면 CLR이 디버거에 의해 중단점을 설정한 대역 외 중단점을 디스패치하지 않도록 할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:**[시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
