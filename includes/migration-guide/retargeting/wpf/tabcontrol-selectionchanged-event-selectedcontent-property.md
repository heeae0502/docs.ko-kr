---
ms.openlocfilehash: 923105114c9e8da02c61c842cc02bed1ead3eddc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2020
ms.locfileid: "67858937"
---
### <a name="tabcontrol-selectionchanged-event-and-selectedcontent-property"></a>TabControl SelectionChanged 이벤트 및 SelectedContent 속성

|   |   |
|---|---|
|세부 정보|4\.7.1,.NET Framework부터는 선택 항목이 변경될 때 <xref:System.Windows.Controls.TabControl>이 <xref:System.Windows.Controls.TabControl.SelectedContent> 이벤트를 발생시키기 전에 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 속성 값을 업데이트합니다. .NET Framework 4.7 및 이전 버전에서는 SelectedContent에 대한 업데이트가 이벤트 이후에 발생했습니다.|
|제안 해결 방법|.NET Framework 4.7.1 이상을 대상으로 하는 앱은 애플리케이션 구성 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음을 추가하여 이 변경을 옵트아웃하고 레거시 동작을 사용할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>.NET Framework 4.7 이하를 대상으로 하지만 .NET Framework 4.7.1 이상에서 실행되는 앱은 애플리케이션 .configuration 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음 줄을 추가하여 새 동작을 사용할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|사소함|
|Version|4.7.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.TabControl.SelectedContent?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.Primitives.Selector.SelectionChanged?displayProperty=nameWithType></li></ul>|
