---
title: .NET Core 런타임 및 SDK 제거
description: 이 문서에서는 현재 설치된 .NET Core 런타임 및 SDK 버전을 확인하는 방법 및 Windows, Mac 및 Linux에서 제거하는 방법을 설명합니다.
ms.date: 12/17/2019
author: billwagner
ms.author: wiwagn
ms.custom: updateeachrelease
ms.openlocfilehash: 71c11825981c6259a779e1ac8f947a41618e922d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79397850"
---
# <a name="how-to-remove-the-net-core-runtime-and-sdk"></a>.NET Core 런타임 및 SDK를 제거하는 방법

시간이 지남에 따라 .NET Core 런타임 및 SDK의 업데이트된 버전을 설치할 때 머신에서 .NET Core의 오래된 버전을 제거합니다. 이전 버전의 런타임을 제거하면 [.NET Core 버전 선택](selection.md)의 문서에서 설명한 대로 공유 프레임워크 애플리케이션을 실행하기 위해 선택한 런타임이 변경될 수 있습니다.

## <a name="should-i-remove-a-version"></a>버전을 제거해야 하나요?

[.NET Core 버전 선택](selection.md) 동작 및 .NET Core의 런타임 호환성을 업데이트하여 이전 버전을 안전하게 제거할 수 있습니다. .NET Core 런타임 업데이트는 1.x 및 2.x와 같은 주 버전 '대역' 내에서 호환됩니다. 또한 .NET Core SDK의 최신 릴리스는 호환 가능한 방식으로 이전 버전의 런타임을 대상으로 하는 애플리케이션을 빌드하는 기능을 일반적으로 유지합니다.

일반적으로 애플리케이션에 필요한 최신 SDK 및 런타임의 최신 패치 버전만 있으면 됩니다. 이전 SDK 또는 런타임 버전을 유지하는 인스턴스에는 **project.json** 기반 애플리케이션 유지 관리가 포함됩니다. 애플리케이션에 이전 SDK 또는 런타임에 대한 특정 이유가 없는 경우 이전 버전을 안전하게 제거할 수 있습니다.

## <a name="determine-what-is-installed"></a>설치된 버전 확인

.NET Core 2.1부터 .NET CLI에는 머신에 설치된 SDK 및 런타임 버전을 나열하는 데 사용할 수 있는 옵션이 있습니다.  [`dotnet --list-sdks`](../tools/dotnet.md#options)를 사용하여 머신에 설치된 SDK의 목록을 확인합니다. [`dotnet --list-runtimes`](../tools/dotnet.md#options)을 사용하여 머신에 설치된 런타임의 목록을 확인합니다. 다음 텍스트는 Windows, macOS 또는 Linux의 일반적인 출력을 보여 줍니다.

<!-- markdownlint-disable MD025 -->

# <a name="windows"></a>[Windows](#tab/windows)

다음 명령을 실행합니다.

```dotnetcli
dotnet --list-sdks
```

그러면 다음과 같은 출력이 표시됩니다.

```console
2.1.200-preview-007474 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007480 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007509 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007570 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007576 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007587 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007589 [C:\Program Files\dotnet\sdk]
2.1.200 [C:\Program Files\dotnet\sdk]
2.1.201 [C:\Program Files\dotnet\sdk]
2.1.202 [C:\Program Files\dotnet\sdk]
2.1.300-preview2-008533 [C:\Program Files\dotnet\sdk]
2.1.300 [C:\Program Files\dotnet\sdk]
2.1.400-preview-009063 [C:\Program Files\dotnet\sdk]
2.1.400-preview-009088 [C:\Program Files\dotnet\sdk]
2.1.400-preview-009171 [C:\Program Files\dotnet\sdk]
```

그리고 다음 명령을 실행합니다.

```dotnetcli
dotnet --list-runtimes
```

그러면 다음과 같은 출력이 표시됩니다.

```console
Microsoft.AspNetCore.All 2.1.0-preview2-final [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.0 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.1 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.2 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.0-preview2-final [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.0 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.1 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.2 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.0.6 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.7 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.9 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0-preview2-26406-04 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.1 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.2 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
```

# <a name="linux"></a>[Linux](#tab/linux)

다음 명령을 실행합니다.

```dotnetcli
dotnet --list-sdks
```

그러면 다음과 같은 출력이 표시됩니다.

```console
1.0.1 [/usr/share/dotnet/sdk]
1.0.4 [/usr/share/dotnet/sdk]
2.0.0-preview1-005977 [/usr/share/dotnet/sdk]
2.0.0-preview2-006497 [/usr/share/dotnet/sdk]
2.0.0 [/usr/share/dotnet/sdk]
2.1.4 [/usr/share/dotnet/sdk]
2.1.300-preview2-008530 [/usr/share/dotnet/sdk]
2.1.300 [/usr/share/dotnet/sdk]
2.1.301 [/usr/share/dotnet/sdk]
```

그리고 다음 명령을 실행합니다.

```dotnetcli
dotnet --list-runtimes
```

그러면 다음과 같은 출력이 표시됩니다.

```console
Microsoft.AspNetCore.All 2.1.0-preview2-final [/usr/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.0 [/usr/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.1 [/usr/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.0-preview2-final [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.0 [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.1 [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 1.0.4 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.0.5 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.1 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.2 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview1-002111-00 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview2-25407-01 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.5 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0-preview2-26406-04 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.1 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
```

# <a name="macos"></a>[macOS](#tab/macos)

다음 명령을 실행합니다.

```dotnetcli
dotnet --list-sdks
```

그러면 다음과 같은 출력이 표시됩니다.

```console
1.0.1 [/usr/local/share/dotnet/sdk]
1.0.4 [/usr/local/share/dotnet/sdk]
2.0.0-preview1-005977 [/usr/local/share/dotnet/sdk]
2.0.0-preview2-006497 [/usr/local/share/dotnet/sdk]
2.0.0 [/usr/local/share/dotnet/sdk]
2.1.4 [/usr/local/share/dotnet/sdk]
2.1.300-preview2-008530 [/usr/local/share/dotnet/sdk]
2.1.300 [/usr/local/share/dotnet/sdk]
2.1.301 [/usr/local/share/dotnet/sdk]
```

그리고 다음 명령을 실행합니다.

```dotnetcli
dotnet --list-runtimes
```

그러면 다음과 같은 출력이 표시됩니다.

```console
Microsoft.AspNetCore.All 2.1.0-preview2-final [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.1 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.0-preview2-final [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.1 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 1.0.4 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.0.5 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.1 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.2 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview1-002111-00 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview2-25407-01 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.5 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0-preview2-26406-04 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.1 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
```

---

## <a name="uninstall-net-core"></a>.NET Core 제거

# <a name="windows"></a>[Windows](#tab/windows)

.NET core는 Windows **프로그램 추가/제거** 대화 상자를 사용하여 .NET Core 런타임 및 SDK의 버전을 제거합니다. 다음 그림에서는 여러 버전의 .NET 런타임 및 SDK가 설치된 **프로그램 추가/제거** 대화 상자를 보여 줍니다.

![.NET Core 제거를 위한 프로그램 추가/제거](./media/remove-runtime-sdk-versions/programs-and-features.png)

머신에서 제거할 버전을 선택하고 **제거**를 클릭합니다.

# <a name="linux"></a>[Linux](#tab/linux)

Linux에서 .NET Core(SDK 또는 런타임)를 제거하는 옵션이 더 있습니다. .NET Core를 제거하는 가장 좋은 방법은 .NET Core 설치에 사용한 작업을 미러링하는 것입니다. 세부 정보는 선택한 배포 및 설치 방법에 따라 다릅니다.

> [!IMPORTANT]
> Red Hat 설치의 경우 .NET Core 설치 및 제거에 대한 정보는 [Red Hat 시작 가이드](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel)를 참조하세요.

.NET Core 2.1부터 패키지 관리자를 사용하여 업그레이드할 때 .NET Core SDK를 제거할 필요가 없습니다. 패키지 관리자 `update` 또는 `refresh` 명령은 최신 버전을 성공적으로 설치하면 이전 버전을 자동으로 제거합니다.

패키지 관리자를 사용하여 .NET Core를 설치한 경우 동일한 패키지 관리자를 사용하여 .NET SDK 또는 런타임을 제거합니다. .NET core 설치는 가장 인기 있는 패키지 관리자를 지원합니다. 환경의 정확한 구문은 배포의 패키지 관리자에 대한 설명서를 참조하세요.

- [apt-get(8)](https://linux.die.net/man/8/apt-get)은 Debian 기반 시스템(Ubuntu 포함)에서 사용됩니다.
- [yum(8)](https://linux.die.net/man/8/yum)은 Fedora, CentOS 및 Oracle Linux에서 사용됩니다.
- [zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain))는 openSUSE 및 SLES(SUSE Linux Enterprise 시스템)에서 사용됩니다.
- [dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html)는 Fedora에서 사용됩니다.

대부분의 경우 패키지를 제거하는 명령은 `remove`입니다.

대부분의 패키지 관리자에 대한 .NET Core SDK 설치의 패키지 이름은 `dotnet-sdk`이며, 그 뒤에 버전 번호가 옵니다. .NET Core SDK의 버전 2.1.300 및 런타임의 버전 `2.1`부터는 주 및 부 버전 번호만 필요합니다. 예를 들어 .NET Core SDK 버전 2.1.300은 `dotnet-sdk-2.1` 패키지로 참조할 수 있습니다. 이전 버전에는 전체 버전 문자열이 필요합니다. 예를 들어 .NET Core SDK의 버전 2.1.200에는 `dotnet-sdk-2.1.200`이 필요합니다.

SDK가 아닌 런타임만 설치한 머신의 경우, 패키지 이름은 .NET Core 런타임의 경우에는 `dotnet-runtime-<version>`이고 전체 런타임 스택의 경우에는 `aspnetcore-runtime-<version>`입니다.

2\.0 이전의 .NET Core 설치는 패키지 관리자를 사용하여 SDK를 제거할 때 호스트 애플리케이션을 제거하지 않았습니다. `apt-get`을 사용하는 명령은 다음과 같습니다.

```bash
apt-get remove dotnet-host
```

`dotnet-host`에 연결된 버전이 없습니다.

tarball을 사용하여 설치한 경우 수동 메서드를 사용하여 .NET Core를 제거해야 합니다.

해당 버전을 포함하는 디렉터리를 제거하여 SDK와 런타임을 별도로 제거합니다. 예는 들어 1.0.1 SDK 및 런타임을 제거하려면 다음 bash 명령을 사용합니다.

```bash
sudo rm -rf /usr/share/dotnet/sdk/1.0.1
sudo rm -rf /usr/share/dotnet/shared/Microsoft.NETCore.App/1.0.1
sudo rm -rf /usr/share/dotnet/shared/Microsoft.AspNetCore.App/1.0.1
sudo rm -rf /usr/share/dotnet/host/fxr/1.0.1
```

SDK 및 런타임에 대한 부모 디렉터리는 이전 표에 표시된 것처럼 `dotnet --list-sdks` 및 `dotnet --list-runtimes` 명령의 출력에 나열됩니다.

# <a name="macos"></a>[macOS](#tab/macos)

Mac에서는 해당 버전을 포함하는 디렉터리를 제거하여 SDK와 런타임을 별도로 제거해야 합니다. 예는 들어 1.0.1 SDK 및 런타임을 제거하려면 다음 bash 명령을 사용합니다.

```bash
sudo rm -rf /usr/local/share/dotnet/sdk/1.0.1
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/1.0.1
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/1.0.1
sudo rm -rf /usr/local/share/dotnet/host/fxr/1.0.1
```

SDK 및 런타임에 대한 부모 디렉터리는 이전 표에 표시된 것처럼 `dotnet --list-sdks` 및 `dotnet --list-runtimes` 명령의 출력에 나열됩니다.

---

## <a name="net-core-uninstall-tool"></a>.NET Core 제거 도구

[.NET Core 제거 도구](../additional-tools/uninstall-tool.md)(`dotnet-core-uninstall`)를 사용하면 시스템에서 .NET Core SDK 및 런타임을 제거할 수 있습니다. 제거해야 하는 버전을 지정할 수 있는 옵션 컬렉션이 제공됩니다.

## <a name="visual-studio-dependency-on-net-core-sdk-versions"></a>.NET Core SDK 버전에 대한 Visual Studio 종속성

Visual Studio 2019 버전 16.3 이전에는 Visual Studio 설치 관리자가 독립 실행형 .NET Core SDK 설치 관리자를 호출했습니다. 따라서 SDK 버전은 Windows **프로그램 추가/제거** 대화 상자에 표시됩니다. 독립 실행형 설치 관리자를 사용하여 Visual Studio에서 설치한 .NET Core SDK를 제거하면 Visual Studio가 중단될 수 있습니다. SDK를 제거한 후 Visual Studio에서 문제가 발생하는 경우 해당 특정 버전의 Visual Studio에서 복구를 실행합니다. 다음 표에서는 .NET Core SDK 버전에 대한 몇 가지 Visual Studio 종속성을 보여줍니다.

| Visual Studio 버전 | .NET Core SDK 버전 |
| -- | -- |
| Visual Studio 2019 버전 16.2 | .NET Core SDK 2.2.4xx, 2.1.8xx |
| Visual Studio 2019 버전 16.1 | .NET Core SDK 2.2.3xx, 2.1.7xx |
| Visual Studio 2019 버전 16.0 | .NET Core SDK 2.2.2xx, 2.1.6xx |
| Visual Studio 2017 버전 15.9 | .NET Core SDK 2.2.1xx, 2.1.5xx |
| Visual Studio 2017 버전 15.8 | .NET Core SDK 2.1.4xx |

Visual Studio 2019 버전 16.3부터 Visual Studio는 .NET Core SDK의 자체 복사본을 담당합니다. 그런 이유로 **프로그램 추가/제거** 대화 상자에 해당 SDK 버전이 더 이상 표시되지 않습니다.

## <a name="remove-the-nuget-fallback-folder"></a>NuGet 대체 폴더 제거

.NET Core 3.0 SDK 이전에 .NET Core SDK 설치 관리자는 *NuGetFallbackFolder*를 사용하여 NuGet 패키지의 캐시를 저장했습니다. 이 캐시는 `dotnet restore`나 `dotnet build /t:Restore` 같은 작업 중에 사용되었습니다. `NuGetFallbackFolder`는 Windows의 *C:\Program Files\dotnet\sdk* 그리고 macOS의 */usr/local/share/dotnet/sdk*에 있습니다.

다음 경우에는 이 폴더를 제거하고자 할 수 있습니다.

* .NET Core 3.0 SDK 이후 버전을 사용하여 개발 중인 경우.
* 3\.0 이전의 .NET Core SDK 버전을 사용하여 개발 중인 경우, 온라인으로 작업할 수 있으며 한 번 더 느려질 수 있습니다.

NuGet 대체 폴더를 제거하고자 하는 경우 삭제할 수 있지만 관리자 권한이 필요합니다.

*dotnet* 폴더는 삭제하지 않는 것이 좋습니다. 이렇게 하면 이전에 설치한 모든 전역 도구가 제거됩니다. 또한 Windows에서

- Visual Studio 2019 버전 16.3 이상 버전의 호환성이 손상됩니다. **복구**를 실행하여 복구할 수 있습니다.
- **프로그램 추가/제거** 대화 상자에 .NET Core SDK 항목이 있는 경우 분리됩니다.
