---
ms.openlocfilehash: 975edd1bda507b46da353db788d9730560f9b573
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2020
ms.locfileid: "65632100"
---
> [!NOTE]
> .NET Core 2.0 SDK부터 복원을 수행해야 하는 모든 명령(예: [, `dotnet restore` 및 ](~/docs/core/tools/dotnet-restore.md))에서 암시적으로 실행되므로 `dotnet new``dotnet build``dotnet run`를 실행할 필요가 없습니다.
> [Azure DevOps Services의 연속 통합 빌드](https://docs.microsoft.com/azure/devops/build-release/apps/aspnet/build-aspnet-core)와 같이 명시적 복원을 수행하는 것이 올바른 특정 시나리오 또는 복원이 발생하는 시간을 명시적으로 제어해야 하는 빌드 시스템에서는 여전히 유효한 명령입니다.
