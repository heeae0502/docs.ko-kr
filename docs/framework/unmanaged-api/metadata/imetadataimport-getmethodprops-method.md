---
title: IMetaDataImport::GetMethodProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMethodProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMethodProps
helpviewer_keywords:
- GetMethodProps method [.NET Framework metadata]
- IMetaDataImport::GetMethodProps method [.NET Framework metadata]
ms.assetid: e0667ef7-1d31-4c89-a2d3-d426f023f8d2
topic_type:
- apiref
ms.openlocfilehash: 4a258ce9121a287929ca5bc39c480f1ca2596e78
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74437468"
---
# <a name="imetadataimportgetmethodprops-method"></a>IMetaDataImport::GetMethodProps 메서드
지정한 MethodDef 토큰이 참조하는 메서드와 연결된 메타데이터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetMethodProps (  
    [in]  mdMethodDef         mb,  
    [out] mdTypeDef           *pClass,  
    [out] LPWSTR              szMethod,  
    [in]  ULONG               cchMethod,  
    [out] ULONG               *pchMethod,  
    [out] DWORD               *pdwAttr,  
    [out] PCCOR_SIGNATURE     *ppvSigBlob,  
    [out] ULONG               *pcbSigBlob,  
    [out] ULONG               *pulCodeRVA,  
    [out] DWORD               *pdwImplFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `mb`  
 진행 메타 데이터를 반환할 메서드를 나타내는 MethodDef 토큰입니다.  
  
 `pClass`  
 제한이 메서드를 구현 하는 형식을 나타내는 TypeDef 토큰에 대 한 포인터입니다.  
  
 `szMethod`  
 제한이 메서드의 이름이 있는 버퍼에 대 한 포인터입니다.  
  
 `cchMethod`  
 진행 요청 된 `szMethod`크기입니다.  
  
 `pchMethod`  
 제한이 `szMethod`의 와이드 문자 크기에 대 한 포인터 이거나, 잘림 인 경우 메서드 이름에 있는 와이드 문자의 실제 수입니다.  
  
 `pdwAttr`  
 제한이 메서드와 연결 된 플래그에 대 한 포인터입니다.  
  
 `ppvSigBlob`  
 제한이 메서드의 이진 메타 데이터 서명에 대 한 포인터입니다.  
  
 `pcbSigBlob`  
 제한이 `ppvSigBlob`의 크기 (바이트)에 대 한 포인터입니다.  
  
 `pulCodeRVA`  
 제한이 메서드의 상대 가상 주소에 대 한 포인터입니다.  
  
 `pdwImplFlags`  
 제한이 메서드에 대 한 구현 플래그에 대 한 포인터입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Cor  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
