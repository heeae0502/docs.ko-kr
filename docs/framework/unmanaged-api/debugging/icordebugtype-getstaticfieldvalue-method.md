---
title: ICorDebugType::GetStaticFieldValue 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetStaticFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 62eb5d55-53ee-4fb3-8d47-7b6c96808f9e
topic_type:
- apiref
ms.openlocfilehash: 37bf5abf66b613d8432af84c7d73aff60e9127cb
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76791269"
---
# <a name="icordebugtypegetstaticfieldvalue-method"></a>ICorDebugType::GetStaticFieldValue 메서드
지정 된 스택 프레임에서 지정 된 필드 토큰이 참조 하는 정적 필드의 값을 포함 하는 ICorDebugValue 개체에 대 한 인터페이스 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef        fieldDef,  
    [in]  ICorDebugFrame    *pFrame,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fieldDef`  
 진행 정적 필드를 지정 하는 `mdFieldDef` 토큰입니다.  
  
 `pFrame`  
 진행 스택 프레임을 나타내는 ICorDebugFrame에 대 한 포인터입니다.  
  
 `ppValue`  
 제한이 정적 필드의 값을 포함 하는 `ICorDebugValue`의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>주의  
 [ICorDebugType:: GetType](icordebugtype-gettype-method.md) 메서드에 표시 된 대로 형식이 ELEMENT_TYPE_CLASS 또는 ELEMENT_TYPE_VALUETYPE 인 경우에만 `GetStaticFieldValue` 메서드를 사용할 수 있습니다.  
  
 제네릭이 아닌 형식의 경우 `GetStaticFieldValue`에서 수행 하는 작업은 [ICorDebugType:: GetClass](icordebugtype-getclass-method.md)에서 반환 하는 ICorDebugClass 개체에 대해 [ICorDebugClass:: GetStaticFieldValue](icordebugclass-getstaticfieldvalue-method.md) 를 호출 하는 것과 동일 합니다.  
  
 제네릭 형식의 경우 정적 필드 값은 특정 인스턴스화를 기준으로 합니다. 또한 정적 필드가 스레드, 컨텍스트 또는 응용 프로그램 도메인에 대 한 상대 값일 수 있는 경우 스택 프레임은 디버거가 적절 한 값을 결정 하는 데 도움이 됩니다.  
  
## <a name="remarks"></a>주의  
 `ICorDebugType::GetType`에 대 한 호출에서 ELEMENT_TYPE_CLASS 또는 ELEMENT_TYPE_VALUETYPE 값을 반환 하는 경우에만 `GetStaticFieldValue`을 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
