---
title: ICLRStrongName::StrongNameGetPublicKey 메서드
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameGetPublicKey
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameGetPublicKey
helpviewer_keywords:
- StrongNameGetPublicKey method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameGetPublicKey method [.NET Framework hosting]
ms.assetid: a31dcaa9-a404-4c1d-8cc7-081827c52935
topic_type:
- apiref
ms.openlocfilehash: cb96c7e17627205db0573e56fc8c2a29e7717434
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181932"
---
# <a name="iclrstrongnamestrongnamegetpublickey-method"></a>ICLRStrongName::StrongNameGetPublicKey 메서드
공개/개인 키 쌍에서 공개 키를 가져옵니다. 키 쌍은 CSP(암호화 서비스 공급자) 내에서 키 컨테이너 이름으로 또는 원시 바이트 컬렉션으로 제공될 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT StrongNameGetPublicKey (
    [in]  LPCWSTR   szKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szKeyContainer`  
 【인】 공개/개인 키 쌍을 포함하는 키 컨테이너의 이름입니다. null인 `pbKeyBlob` 경우 `szKeyContainer` CSP 내에서 유효한 컨테이너를 지정해야 합니다. 이 경우 [ICLRStrongName::StrongNameGetPublicKey](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetpublickey-method.md) 메서드는 컨테이너에 저장된 키 쌍에서 공개 키를 추출합니다.  
  
 null이 아닌 경우 `pbKeyBlob` 키 쌍은 키 이진 큰 개체(BLOB)에 포함되는 것으로 가정합니다.  
  
 키는 1024비트 Rivest-Shamir-Adleman(RSA) 서명 키여야 합니다. 현재 다른 유형의 키는 지원되지 않습니다.  
  
 `pbKeyBlob`  
 【인】 공용/개인 키 쌍에 대한 포인터입니다. 이 쌍은 Win32 `CryptExportKey` 함수에서 만든 형식입니다. null인 경우 `pbKeyBlob` 지정한 `szKeyContainer` 키 컨테이너는 키 쌍을 포함하는 것으로 가정합니다.  
  
 `cbKeyBlob`  
 【인】 의 크기(바이트)입니다. `pbKeyBlob`  
  
 `ppbPublicKeyBlob`  
 【아웃】 반환된 공개 키 BLOB입니다. 매개 `ppbPublicKeyBlob` 변수는 공통 언어 런타임에 의해 할당되고 호출자에게 반환됩니다. 호출자는 [ICLRStrongName::StrongNameFreeBuffer](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) 메서드를 사용하여 메모리를 해제해야 합니다.  
  
 `pcbPublicKeyBlob`  
 【아웃】 반환된 공개 키 BLOB의 크기입니다.  
  
## <a name="return-value"></a>Return Value  
 `S_OK`메서드가 성공적으로 완료된 경우 그렇지 않으면 실패를 나타내는 HRESULT 값입니다(목록의 [공통 HRESULT 값](/windows/win32/seccrypto/common-hresult-values) 참조).  
  
## <a name="remarks"></a>설명  
 공개 키는 [PublicKeyBlob](../../../../docs/framework/unmanaged-api/strong-naming/publickeyblob-structure.md) 구조에 포함되어 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:**[시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** 메타호스트  
  
 **라이브러리:** MSCorEE.dll의 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [StrongNameTokenFromPublicKey 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [PublicKeyBlob 구조체](../../../../docs/framework/unmanaged-api/strong-naming/publickeyblob-structure.md)
- [ICLRStrongName 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
