---
ms.openlocfilehash: 8aae403e3f23d3bfc755140b2ac29d757f10f753
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2020
ms.locfileid: "74451442"
---
### <a name="data-binding-improvement-for-keyedcollection"></a>KeyedCollection에 대한 데이터 바인딩 개선

|   |   |
|---|---|
|세부 정보|원본 개체가 동일한 서명(예: KeyedCollection<xref:System.Windows.Data.Binding>int,TItem&lt;)이 있는 사용자 지정 인덱서를 선언할 때 IList 인덱서가 잘못 사용된 &gt;을 수정했습니다.|
|제안 해결 방법|이전 버전을 대상으로 하는 애플리케이션에서 이 변경의 이점을 활용하려면 .NET Framework 4.8 이상에서 실행해야 하며, 앱 구성 파일의 [ 섹션에 다음과 같은 ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)AppContext 스위치<code>&lt;runtime&gt;</code>를 추가하여 변경 내용을 옵트인하고 <code>false</code>로 설정해야 합니다.<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Data.Binding.IListIndexerHidesCustomIndexer=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|주요함|
|Version|4.8|
|형식|런타임|
