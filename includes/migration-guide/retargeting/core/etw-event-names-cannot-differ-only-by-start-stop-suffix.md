---
ms.openlocfilehash: 71c81cf188fa4c2300661f10eb87e7ae00e031f6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2020
ms.locfileid: "67804579"
---
### <a name="etw-event-names-cannot-differ-only-by-a-start-or-stop-suffix"></a>ETW 이벤트 이름은 "Start" 또는 "Stop" 접미사만 다를 수 없음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6 및 4.6.1의 경우 두 개의 ETW(Windows용 이벤트 추적) 이벤트 이름이 <xref:System.ArgumentException>Start&quot; 또는 &quot;Stop&quot; 접미사만 다를 때(예: 한 이벤트는 &quot;, 다른 이벤트는 <code>LogUser</code>라고 이름을 지정하는 경우) 런타임에서 <code>LogUserStart</code>을 throw합니다. 이 경우 런타임에서 로깅을 발생할 수 없는 이벤트 소스를 구성할 수 없습니다.|
|제안 해결 방법|예외를 방지하려면 두 이벤트 이름이 &quot;시작&quot; 또는 &quot;중지&quot; 접미사만 다르지 않도록 하세요. 이 요구 사항은 .NET Framework 4.6.2부터 제거됩니다. 런타임은 &quot;시작&quot; 및 &quot;중지&quot; 접미사만 다른 이벤트 이름을 명확하게 할 수 있습니다.|
|범위|가장자리|
|Version|4.6|
|형식|대상 변경|
