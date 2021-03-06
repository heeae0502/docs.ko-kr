---
title: 보안
ms.date: 03/30/2017
helpviewer_keywords:
- XAML files [WPF], sandbox behavior
- browser-hosted application security [WPF]
- application security [WPF]
- navigation security [WPF]
- loose XAML files [WPF], sandbox behavior
- WPF security [WPF]
- WebBrowser control [WPF], security
- feature controls [WPF], security
- XBAP security [WPF]
- Internet Explorer security settings [WPF]
ms.assetid: ee1baea0-3611-4e36-9ad6-fcd5205376fb
ms.openlocfilehash: e0a56dcbf8d151fcb0d4f6271ecba15c0ff955a4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174617"
---
# <a name="security-wpf"></a>보안(WPF)
<a name="introduction"></a>WPF(Windows 프레젠테이션 파운데이션) 독립 실행형 및 브라우저 호스팅 응용 프로그램을 개발할 때는 보안 모델을 고려해야 합니다. WPF 독립 실행형 응용 프로그램은 무제한 권한(CAS**FullTrust** 권한 집합)으로 실행되며, Windows 설치 관리자(.msi), XCopy 또는 ClickOnce를 사용하여 배포되었는지 여부입니다. ClickOnce를 포함한 부분 신뢰, 독립 실행형 WPF 애플리케이션 배포가 지원되지 않습니다. 그러나 완전 신뢰 호스트 응용 프로그램은 .NET <xref:System.AppDomain> Framework 추가 기능 모델을 사용하여 부분 신뢰를 만들 수 있습니다. 자세한 내용은 [WPF 추가 기능 개요를](./app-development/wpf-add-ins-overview.md)참조하십시오.  
  
 WPF 브라우저 호스팅 응용 프로그램은 Windows Internet Explorer 또는 Firefox에서 호스팅하며 XAML 브라우저 응용 [!INCLUDE[TLA#tla_xaml](../../../includes/tlasharptla-xaml-md.md)] 프로그램(XBAPs) [WPF XAML Browser Applications Overview](./app-development/wpf-xaml-browser-applications-overview.md)또는 느슨한 문서일 수 있습니다.  
  
 WPF 브라우저에서 호스팅되는 응용 프로그램은 기본적으로 기본 CAS**인터넷** 영역 사용 권한 집합으로 제한되는 부분 신뢰 보안 샌드박스 내에서 실행됩니다. 이렇게 하면 일반적인 웹 응용 프로그램이 격리될 것으로 예상되는 것과 동일한 방식으로 WPF 브라우저 호스팅 응용 프로그램을 클라이언트 컴퓨터에서 격리할 수 있습니다. XBAP는 배포 URL 및 클라이언트의 보안 구성의 보안 영역에 따라 권한을 완전 신뢰까지 높일 수 있습니다. 자세한 내용은 [WPF 부분 신뢰 보안](wpf-partial-trust-security.md)을 참조하세요.  
  
 이 항목에서는 WPF(Windows 프레젠테이션 Foundation) 독립 실행형 및 브라우저 호스팅 응용 프로그램에 대한 보안 모델에 대해 설명합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
- [안전한 탐색](#SafeTopLevelNavigation)  
  
- [웹 브라우징 소프트웨어 보안 설정](#InternetExplorerSecuritySettings)  
  
- [WebBrowser 컨트롤 및 기능 컨트롤](#webbrowser_control_and_feature_controls)  
  
- [부분적으로 신뢰할 수 있는 클라이언트 애플리케이션에 대한 APTCA 어셈블리를 사용하지 않도록 설정](#APTCA)  
  
- [XAML 사용 완화 파일에 대한 샌드박스 동작](#LooseContentSandboxing)  
  
- [보안을 승격하는 WPF 애플리케이션 개발을 위한 리소스](#BestPractices)  
  
<a name="SafeTopLevelNavigation"></a>
## <a name="safe-navigation"></a>안전한 탐색  
 XBAPs의 경우 WPF는 응용 프로그램과 브라우저의 두 가지 유형의 탐색을 구분합니다.  
  
 *애플리케이션 탐색*은 브라우저에서 호스트되는 애플리케이션 내의 콘텐츠 항목 간을 탐색합니다. *브라우저 탐색*은 브라우저 자체의 콘텐츠 및 위치 URL을 변경하는 탐색입니다. 응용 프로그램 탐색(일반적으로 XAML)과 브라우저 탐색(일반적으로 HTML) 간의 관계는 다음 그림에 나와 있습니다.
  
 ![응용 프로그램 탐색과 브라우저 탐색 간의 관계입니다.](./media/security-wpf/application-browser-navigation-relationship.png)  
  
 XBAP가 탐색하기에 안전한 것으로 간주되는 콘텐츠 유형은 주로 응용 프로그램 탐색 또는 브라우저 탐색이 사용되는지 여부에 따라 결정됩니다.  
  
<a name="Application_Navigation_Security"></a>
### <a name="application-navigation-security"></a>애플리케이션 탐색 보안  
 응용 프로그램 탐색은 다음 네 가지 유형의 콘텐츠를 지원하는 pack URI로 식별할 수 있는 경우 안전한 것으로 간주됩니다.  
  
|콘텐츠 형식|Description|URI 예제|  
|------------------|-----------------|-----------------|  
|리소스|**리소스의**빌드 유형이 있는 프로젝트에 추가되는 파일 .|`pack://application:,,,/MyResourceFile.xaml`|  
|콘텐츠|**콘텐츠의**빌드 유형이 있는 프로젝트에 추가되는 파일 .|`pack://application:,,,/MyContentFile.xaml`|  
|원래 사이트|없음의 빌드 유형이 있는 프로젝트에 **None**추가되는 파일입니다.|`pack://siteoforigin:,,,/MySiteOfOriginFile.xaml`|  
|애플리케이션 코드|컴파일된 코드 숨김이 있는 XAML 리소스.<br /><br /> 또는<br /><br /> **페이지**의 빌드 유형이 있는 프로젝트에 추가되는 XAML 파일 .|`pack://application:,,,/MyResourceFile` `.xaml`|  
  
> [!NOTE]
> 응용 프로그램 데이터 파일 및 팩 URI에 대한 자세한 내용은 [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일을](./app-development/wpf-application-resource-content-and-data-files.md)참조하십시오.  
  
 이러한 콘텐츠 형식의 파일은 사용자 또는 프로그래밍 방식으로 탐색할 수 있습니다.  
  
- **사용자 탐색**. 사용자는 요소를 클릭하여 탐색합니다. <xref:System.Windows.Documents.Hyperlink>  
  
- **프로그래밍 방식 탐색**. 응용 프로그램은 예를 들어 속성을 설정하여 사용자를 <xref:System.Windows.Navigation.NavigationWindow.Source%2A?displayProperty=nameWithType> 포함하지 않고 탐색합니다.  
  
<a name="Browser_Navigation_Security"></a>
### <a name="browser-navigation-security"></a>브라우저 탐색 보안  
 브라우저 탐색은 다음 조건에서만 안전한 것으로 간주됩니다.  
  
- **사용자 탐색**. 사용자는 중첩된 <xref:System.Windows.Documents.Hyperlink> 가 아닌 main <xref:System.Windows.Navigation.NavigationWindow>내에 있는 요소를 클릭하여 <xref:System.Windows.Controls.Frame>탐색합니다.  
  
- **영역**. 탐색 대상 콘텐츠는 인터넷 또는 로컬 인트라넷에 있습니다.  
  
- **프로토콜**. 사용 중인 프로토콜은 **http**, **https**, **파일**또는 **mailto**입니다.  
  
 XBAP가 이러한 조건을 준수하지 않는 방식으로 콘텐츠로 이동하려고 하면 <xref:System.Security.SecurityException> a가 throw됩니다.  
  
<a name="InternetExplorerSecuritySettings"></a>
## <a name="web-browsing-software-security-settings"></a>웹 브라우징 소프트웨어 보안 설정  
 컴퓨터의 보안 설정은 웹 브라우징 소프트웨어 권한이 부여된 액세스 권한을 결정합니다. 웹 브라우징 소프트웨어에는 인터넷 익스플로러 및 PresentationHost.exe를 포함하여 [WinINet](/windows/win32/wininet/portal) 또는 [UrlMon](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa767916(v=vs.85)) API를 사용하는 모든 응용 프로그램 또는 구성 요소가 포함됩니다.  
  
 Internet Explorer는 다음을 포함하여 Internet Explorer에서 실행하거나 실행할 수 있는 기능을 구성할 수 있는 메커니즘을 제공합니다.  
  
- .NET 프레임워크 기반 구성 요소  
  
- ActiveX 컨트롤 및 플러그인  
  
- 다운로드  
  
- 스크립팅  
  
- 사용자 인증  
  
 이러한 방식으로 보호할 수 있는 기능 모음은 **인터넷,** **인트라넷,** **신뢰할 수 있는 사이트**및 제한된 **사이트** 영역에 대해 영역별로 구성됩니다. 다음 단계는 보안 설정을 구성하는 방법을 설명합니다.  
  
1. **제어판**을 엽니다.  
  
2. **네트워크 및 인터넷을** 클릭한 다음 인터넷 옵션을 **클릭합니다.**  
  
     인터넷 옵션 대화 상자가 나타납니다.  
  
3. **보안** 탭에서 영역을 선택하여 보안 설정을 구성합니다.  
  
4. 사용자 지정 수준 버튼을 **클릭합니다.**  
  
     **보안 설정** 대화 상자가 나타나고 선택한 영역에 대한 보안 설정을 구성할 수 있습니다.  
  
     ![보안 설정 대화 상자를 보여 주는 스크린샷입니다.](./media/security-wpf/windows-presentation-foundation-security-settings.png)  
  
> [!NOTE]
> Internet Explorer에서 인터넷 옵션 대화 상자에 액세스할 수도 있습니다. **도구를** 클릭한 다음 **인터넷 옵션을 클릭합니다.**  
  
 Windows 인터넷 익스플로러 7부터 .NET Framework를 위한 다음 보안 설정이 포함되어 있습니다.  
  
- **느슨한 XAML**. Internet Explorer가 파일로 탐색하고 파일을 느슨하게 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 할 수 있는지 여부를 제어합니다. (설정, 해제 및 확인 옵션).  
  
- **XAML 브라우저 애플리케이션**. Internet Explorer에서 XBAP로 이동하여 실행할 수 있는지 여부를 제어합니다. (설정, 해제 및 확인 옵션).  
  
 기본적으로 이러한 설정은 **모두 인터넷,** **로컬 인트라넷**및 **신뢰할 수 있는 사이트** 영역에 대해 활성화되고 제한된 **사이트** 영역에 대해 비활성화됩니다.  
  
<a name="Security_Settings_for_IE6_and_Below"></a>
### <a name="security-related-wpf-registry-settings"></a>보안 관련 WPF 레지스트리 설정  
 인터넷 옵션을 통해 사용할 수 있는 보안 설정 외에 다음 레지스트리 값은 선택적으로 다양한 보안 관련 WPF 기능을 차단하는 데 사용할 수 있습니다. 해당 값은 다음 키에서 정의됩니다.  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\Windows Presentation Foundation\Features`  
  
 다음 표에서는 설정할 수 있는 값을 보여 줍니다.  
  
|값 이름|값 형식|값 데이터|  
|----------------|----------------|----------------|  
|XBAPDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
|LooseXamlDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
|WebBrowserDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
|MediaAudioDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
|MediaImageDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
|MediaVideoDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
|ScriptInteropDisallow|REG_DWORD|1은 허용되지 않으며 0은 허용됩니다.|  
  
<a name="webbrowser_control_and_feature_controls"></a>
## <a name="webbrowser-control-and-feature-controls"></a>WebBrowser 컨트롤 및 기능 컨트롤  
 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤을 사용하여 웹 콘텐츠를 호스팅할 수 있습니다. WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤은 기본 웹 브라우저 ActiveX 컨트롤을 래핑합니다. WPF는 신뢰할 수 없는 웹 콘텐츠를 호스트하기 위해 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤을 사용할 때 응용 프로그램 보안을 위한 몇 가지 지원을 제공합니다. 그러나 일부 보안 기능은 <xref:System.Windows.Controls.WebBrowser> 컨트롤을 사용하는 응용 프로그램에서 직접 적용해야 합니다. WebBrowser ActiveX 컨트롤에 대한 자세한 내용은 [웹 브라우저 제어 개요 및 자습서를](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752041(v=vs.85))참조하십시오.  
  
> [!NOTE]
> 이 섹션은 HTML <xref:System.Windows.Controls.Frame> 콘텐츠로 이동하는 <xref:System.Windows.Controls.WebBrowser> 데 를 사용하기 때문에 컨트롤에도 적용됩니다.  
  
 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤이 신뢰할 수 없는 웹 콘텐츠를 호스트하는 데 사용되는 <xref:System.AppDomain> 경우 응용 프로그램은 부분 트러스트를 사용하여 응용 프로그램 코드를 악의적인 HTML 스크립트 코드로부터 격리해야 합니다. 응용 프로그램이 <xref:System.Windows.Controls.WebBrowser.InvokeScript%2A> 메서드 및 <xref:System.Windows.Controls.WebBrowser.ObjectForScripting%2A> 속성을 사용하여 호스팅된 스크립트와 상호 작용하는 경우 특히 그렇습니다. 자세한 내용은 [WPF 추가 기능 개요를](./app-development/wpf-add-ins-overview.md)참조하십시오.  
  
 응용 프로그램에서 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤을 사용하는 경우 보안을 강화하고 공격을 완화하는 또 다른 방법은 Internet Explorer 기능 컨트롤을 사용하도록 설정하는 것입니다. 기능 컨트롤은 관리자와 개발자가 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤이 래핑하는 WebBrowser ActiveX 컨트롤을 호스팅하는 인터넷 익스플로러 및 응용 프로그램의 기능을 구성할 수 있도록 하는 Internet Explorer에 추가된 기능입니다. 기능 컨트롤은 [CoInternetSetFeatureEnabled](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537168(v=vs.85)) 기능을 사용하거나 레지스트리의 값을 변경하여 구성할 수 있습니다. 피처 컨트롤에 대한 자세한 내용은 기능 컨트롤 및 [인터넷 기능 컨트롤](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/general-info/ee330720(v=vs.85)) [소개를](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537184(v=vs.85)) 참조하십시오.  
  
 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤을 사용하는 독립 실행형 WPF 응용 프로그램을 개발하는 경우 WPF는 응용 프로그램에 대해 다음 기능 컨트롤을 자동으로 활성화합니다.  
  
|기능 컨트롤|  
|---------------------|  
|FEATURE_MIME_HANDLING|  
|FEATURE_MIME_SNIFFING|  
|FEATURE_OBJECT_CACHING|  
|FEATURE_SAFE_BINDTOOBJECT|  
|FEATURE_WINDOW_RESTRICTIONS|  
|FEATURE_ZONE_ELEVATION|  
|FEATURE_RESTRICT_FILEDOWNLOAD|  
|FEATURE_RESTRICT_ACTIVEXINSTALL|  
|FEATURE_ADDON_MANAGEMENT|  
|FEATURE_HTTP_USERNAME_PASSWORD_DISABLE|  
|FEATURE_SECURITYBAND|  
|FEATURE_UNC_SAVEDFILECHECK|  
|FEATURE_VALIDATE_NAVIGATE_URL|  
|FEATURE_DISABLE_TELNET_PROTOCOL|  
|FEATURE_WEBOC_POPUPMANAGEMENT|  
|FEATURE_DISABLE_LEGACY_COMPRESSION|  
|FEATURE_SSLUX|  
  
 이러한 기능 컨트롤은 조건에 상관 없이 사용되므로 이 컨트롤로 인해 완전 신뢰 애플리케이션가 손상될 수 있습니다. 이 경우 특정 애플리케이션 및 호스팅하는 콘텐츠에 대한 보안 위험이 없다면, 해당 기능 컨트롤을 비활성화할 수 있습니다.  
  
 기능 컨트롤은 WebBrowser ActiveX 개체를 인스턴스화하는 프로세스에 의해 적용됩니다. 따라서 신뢰할 수 없는 콘텐츠를 탐색할 수 있는 독립 실행형 애플리케이션을 만드는 경우, 추가 기능 컨트롤 사용을 심각하게 고려해야 합니다.  
  
> [!NOTE]
> 이 권장 사항은 MSHTML 및 SHDOCVW 호스트 보안을 위한 일반 권장 사항을 기반으로 합니다. 자세한 내용은 [MSHTML 호스트 보안 FAQ: II 파트 I](https://msrc-blog.microsoft.com/2009/04/02/the-mshtml-host-security-faq-part-i-of-ii/) 및 [MSHTML 호스트 보안 FAQ: II 의 파트 II를](https://msrc-blog.microsoft.com/2009/04/03/the-mshtml-host-security-faq-part-ii-of-ii/)참조하십시오.  
  
 실행 파일의 경우, 레지스트리 값을 1로 설정하여 다음 기능 컨트롤을 사용하도록 설정하는 것이 좋습니다.  
  
|기능 컨트롤|  
|---------------------|  
|FEATURE_ACTIVEX_REPURPOSEDETECTION|  
|FEATURE_BLOCK_LMZ_IMG|  
|FEATURE_BLOCK_LMZ_OBJECT|  
|FEATURE_BLOCK_LMZ_SCRIPT|  
|FEATURE_RESTRICT_RES_TO_LMZ|  
|FEATURE_RESTRICT_ABOUT_PROTOCOL_IE7|  
|FEATURE_SHOW_APP_PROTOCOL_WARN_DIALOG|  
|FEATURE_LOCALMACHINE_LOCKDOWN|  
|FEATURE_FORCE_ADDR_AND_STATUS|  
|FEATURE_RESTRICTED_ZONE_WHEN_FILE_NOT_FOUND|  
  
 실행 파일의 경우, 레지스트리 값을 0으로 설정하여 다음 기능 컨트롤을 사용하지 않도록 설정하는 것이 좋습니다.  
  
|기능 컨트롤|  
|---------------------|  
|FEATURE_ENABLE_SCRIPT_PASTE_URLACTION_IF_PROMPT|  
  
 Windows 인터넷 익스플로러에서 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤을 포함하는 부분 신뢰 XAML 브라우저 응용 프로그램(XBAP)을 실행하는 경우 WPF는 인터넷 익스플로러 프로세스의 주소 공간에서 WebBrowser ActiveX 컨트롤을 호스팅합니다. WebBrowser ActiveX 컨트롤은 인터넷 익스플로러 프로세스에서 호스팅되므로 Internet Explorer에 대한 모든 기능 컨트롤도 WebBrowser ActiveX 컨트롤에 대해 활성화됩니다.  
  
 또한 Internet Explorer에서 실행하는 XBAP는 일반 독립 실행형 애플리케이션보다 추가된 보안 수준이 제공됩니다. 이 추가 보안은 인터넷 익스플로러, 따라서 WebBrowser ActiveX 컨트롤, 기본적으로 Windows Vista 및 Windows 7에서 보호 모드에서 실행 하기 때문에. 보호 모드에 대한 자세한 내용은 [보호 모드 인터넷 익스플로러에서 이해 및 작업](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/)작업을 참조하십시오.  
  
> [!NOTE]
> 파이어 폭스에서 WPF <xref:System.Windows.Controls.WebBrowser> 컨트롤을 포함 하는 XBAP를 실행 하려고 하는 <xref:System.Security.SecurityException> 경우, 인터넷 영역에 있는 동안, 던져집니다. 이는 WPF 보안 정책에 의한 것입니다.  
  
<a name="APTCA"></a>
## <a name="disabling-aptca-assemblies-for-partially-trusted-client-applications"></a>부분적으로 신뢰할 수 있는 클라이언트 애플리케이션에 대한 APTCA 어셈블리를 사용하지 않도록 설정  
 관리되는 어셈블리가 GAC(전역 어셈블리 캐시)에 설치되면 사용자가 설치할 수 있는 명시적 권한을 제공해야 하므로 완전히 신뢰할 수 있습니다. 완전히 신뢰할 수 있기 때문에 완전히 신뢰할 수 있는 관리 클라이언트 애플리케이션에서 사용할 수 있습니다. 부분적으로 신뢰할 수 있는 응용 프로그램을 사용할 수 있도록 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 하려면 APTCA(APTCA)로 표시해야 합니다. 부분 신뢰로 실행하기에 안전한 것으로 테스트된 어셈블리만 이 특성으로 표시되어야 합니다.  
  
 그러나 APTCA 어셈블리가 GAC에 설치한 후 보안 결함을 나타낼 수 있습니다. 보안 결함이 발견되면 어셈블리 게시자는 기존 설치에서 문제를 해결하는 보안 업데이트를 생성할 수 있으며, 문제가 발견된 후 발생할 수 있는 설치를 방지할 수 있습니다. 업데이트에 대한 한 가지 옵션은 어셈블리를 제거하는 것이지만 어셈블리를 사용하는 완전히 신뢰할 수 있는 다른 클라이언트 애플리케이션이 중단될 수 있습니다.  
  
 WPF는 APTCA 어셈블리를 제거하지 않고 부분적으로 신뢰할 수 있는 XBAP에 대해 APTCA 어셈블리를 비활성화할 수 있는 메커니즘을 제공합니다.  
  
 APTCA 어셈블리를 사용하지 않도록 설정하려면 특수한 레지스트리 키를 만들어야 합니다.  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\policy\APTCA\<AssemblyFullName>, FileVersion=<AssemblyFileVersion>`  
  
 이에 대한 예는 다음과 같습니다.  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\policy\APTCA\aptcagac, Version=1.0.0.0, Culture=neutral, PublicKeyToken=215e3ac809a0fea7, FileVersion=1.0.0.0`  
  
 이 키는 APTCA 어셈블리에 대한 항목을 설정합니다. 어셈블리를 사용할지를 지정하는 이 키에서 값을 만들 수도 있습니다. 다음은 값의 세부 정보입니다.  
  
- 값 이름: **APTCA_FLAG**.  
  
- 값 유형: **REG_DWORD**.  
  
- 값 데이터: **1을** 사용하지 않도록 설정합니다. **0을** 활성화합니다.  
  
 어셈블리를 부분적으로 신뢰할 수 있는 클라이언트 애플리케이션에 사용하지 않도록 설정해야 하는 경우, 레지스트리 키와 값을 만드는 업데이트를 작성할 수 있습니다.  
  
> [!NOTE]
> Core .NET Framework 어셈블리는 관리되는 응용 프로그램을 실행하는 데 필요하기 때문에 이러한 방식으로 사용하지 않도록 설정하면 영향을 받지 않습니다. APTCA 어셈블리를 사용하지 않도록 설정하는 것에 대한 지원은 기본적으로 타사 애플리케이션을 대상으로 합니다.  
  
<a name="LooseContentSandboxing"></a>
## <a name="sandbox-behavior-for-loose-xaml-files"></a>느슨한 XAML 파일에 대한 샌드박스 동작  
 느슨한 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 파일은 코드 숨결, 이벤트 처리기 또는 응용 프로그램 별 어셈블리에 의존하지 않는 태그 전용 XAML 파일입니다. 느슨한 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 파일이 브라우저에서 직접 탐색되면 기본 인터넷 영역 사용 권한 집합에 따라 보안 샌드박스에 로드됩니다.  
  
 그러나 느슨한 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 파일이 독립 실행형 응용 프로그램 <xref:System.Windows.Navigation.NavigationWindow> 또는 <xref:System.Windows.Controls.Frame> 독립 실행형 응용 프로그램에서 탐색될 때 보안 동작이 다릅니다.  
  
 두 경우 모두 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 호스트 응용 프로그램의 사용 권한을 상속하기 위해 탐색되는 느슨한 파일입니다. 그러나 이 동작은 보안 관점에서 바람직하지 않을 수 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 있으며, 특히 신뢰할 수 없거나 알 수 없는 엔터티에서 느슨한 파일이 생성된 경우 는 그렇지 않을 수 있습니다. 이러한 유형의 콘텐츠를 *외부 콘텐츠라고* <xref:System.Windows.Controls.Frame> 하며 <xref:System.Windows.Navigation.NavigationWindow> 탐색할 때 격리되도록 구성할 수 있습니다. 격리는 다음에 대한 예제와 <xref:System.Windows.Controls.Frame> <xref:System.Windows.Navigation.NavigationWindow>같이 **SandboxExternalContent** 속성을 true로 설정하여 수행됩니다.  
  
 [!code-xaml[SecurityOverviewSnippets#FrameMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/SecurityOverviewSnippets/CS/Window2.xaml#framemarkup)]  
  
 [!code-xaml[SecurityOverviewSnippets#NavigationWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/SecurityOverviewSnippets/CS/Window1.xaml#navigationwindowmarkup)]  
  
 이 설정을 통해 외부 콘텐츠가 애플리케이션을 호스팅하는 프로세스와 별개인 프로세스로 로드됩니다. 이 프로세스는 효과적으로 호스팅 애플리케이션과 클라이언트 컴퓨터에서 격리되어 기본 인터넷 영역 권한 집합으로 제한됩니다.  
  
> [!NOTE]
> 프레젠테이션 호스트 프로세스와 관련된 <xref:System.Windows.Navigation.NavigationWindow> WPF 브라우저 호스팅 인프라를 기반으로 독립 <xref:System.Windows.Controls.Frame> 실행형 응용 프로그램에서 느슨한 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 파일로 탐색하는 것이 구현되더라도 콘텐츠가 Windows Vista 및 Windows 7의 Internet Explorer에서 직접 로드될 때보다 보안 수준이 약간 적습니다(여전히 PresentationHost를 통해 있음). 웹 브라우저를 사용하는 독립 실행형 WPF 애플리케이션은 Internet Explorer의 추가 보호 모드 보안 기능을 제공하지 않습니다.  
  
<a name="BestPractices"></a>
## <a name="resources-for-developing-wpf-applications-that-promote-security"></a>보안을 승격하는 WPF 애플리케이션 개발을 위한 리소스  
 다음은 보안을 촉진하는 WPF 응용 프로그램을 개발하는 데 도움이 되는 몇 가지 추가 리소스입니다.  
  
|영역|리소스|  
|----------|--------------|  
|관리 코드|[애플리케이션에 대한 패턴 및 사례 보안 지침](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))|  
|CAS|[코드 액세스 보안](../misc/code-access-security.md)|  
|ClickOnce|[클릭원스 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)|  
|WPF|[WPF 부분 신뢰 보안](wpf-partial-trust-security.md)|  
  
## <a name="see-also"></a>참고 항목

- [WPF 부분 신뢰 보안](wpf-partial-trust-security.md)
- [WPF 보안 전략 - 플랫폼 보안](wpf-security-strategy-platform-security.md)
- [WPF 보안 전략 - 보안 엔지니어링](wpf-security-strategy-security-engineering.md)
- [애플리케이션에 대한 패턴 및 사례 보안 지침](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))
- [코드 액세스 보안](../misc/code-access-security.md)
- [클릭원스 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)
- [XAML 개요(WPF)](../../desktop-wpf/fundamentals/xaml.md)
