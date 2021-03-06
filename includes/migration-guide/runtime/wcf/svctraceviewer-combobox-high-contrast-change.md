---
ms.openlocfilehash: cc6d96bd614ff015ae2125c0f1477e18a91a68f7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2020
ms.locfileid: "67802653"
---
### <a name="svctraceviewer-combobox-high-contrast-change"></a>svcTraceViewer ComboBox 고대비 변경

|   |   |
|---|---|
|세부 정보|[Microsoft Service Trace Viewer 도구](~/docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)에서 ComboBox 컨트롤이 특정 고대비 테마에서 올바른 색으로 표시되지 않았습니다. 이 문제는 .NET Framework 4.7.2에서 해결되었습니다. 그러나 .NET Framework SDK의 이전 버전과의 호환성 요구 사항으로 인해, 이 수정 사항은 기본적으로 고객에게 보이지 않습니다. .NET 4.8은 다음 [AppContext 구성 스위치](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)를 svcTraceViewer.exe.config 파일에 추가하여 이 변경 내용을 표시합니다.<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>|
|제안 해결 방법|<ul><li>고대비 동작을 변경하지 않으려는 경우의 변경을 옵트아웃하는 방법은 svcTraceViewer.exe.config 파일에서 다음 섹션을 제거하여 비활성화할 수 있습니다.</li></ul><pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>|
|범위|가장자리|
|Version|4.8|
|형식|런타임|
