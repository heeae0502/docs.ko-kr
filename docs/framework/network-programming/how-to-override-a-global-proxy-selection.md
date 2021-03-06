---
title: '방법: 전역 프록시 선택 재정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0da481a9-b414-4230-beb0-e3ceba882fe5
ms.openlocfilehash: 44845fb67aac4ff9ab9dda8cf4934153c8c4f23c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2020
ms.locfileid: "71048266"
---
# <a name="how-to-override-a-global-proxy-selection"></a>방법: 전역 프록시 선택 재정의
이 예제에서는 글로벌 프록시 선택을 포트 80의 **라는 프록시 서버로 재정의하는** WebRequest`www.contoso.com`를 `alternateproxy`에 보냅니다.  
  
## <a name="example"></a>예제  
  
```csharp  
WebRequest req = WebRequest.Create("http://www.contoso.com/");  
req.Proxy = new WebProxy("http://alternateproxy:80/");  
```  
  
```vb  
Dim req As WebRequest = WebRequest.Create("http://www.contoso.com/")  
req.Proxy = New WebProxy("http://alternateproxy:80/")  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- [System.Net`using` 네임스페이스에 대한 ](../../csharp/language-reference/keywords/using-directive.md) **지시문**  
  
## <a name="see-also"></a>참고 항목

- [애플리케이션 프로토콜 사용](using-application-protocols.md)
- [프록시를 통해 인터넷 액세스](accessing-the-internet-through-a-proxy.md)
