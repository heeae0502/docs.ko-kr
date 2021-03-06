---
title: F# 스타일 가이드
description: '좋은 F # 코드의 다섯 가지 원칙을 알아보십시오.'
ms.date: 12/10/2018
ms.openlocfilehash: 9f47257626e04b09b546de2ae315d48d791678be
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401114"
---
# <a name="f-style-guide"></a>F# 스타일 가이드

다음 문서에서는 F# 코드 서식 지정에 대한 지침과 언어 기능에 대한 국소 지침 및 사용 방법에 대해 설명합니다.

이 지침은 다양한 프로그래머 그룹이 있는 대규모 코드베이스에서 F#을 사용하여 공식화되었습니다. 이 지침은 일반적으로 F#을 성공적으로 사용하게 되며 시간에 따라 프로그램에 대한 요구 사항이 변경될 때 불만을 최소화합니다.

## <a name="five-principles-of-good-f-code"></a>좋은 F # 코드의 다섯 가지 원칙

특히 시간이 지남에 따라 변경되는 시스템에서 는 F# 코드를 작성할 때마다 다음 원칙을 염두에 두어야 합니다. 추가 기사의 모든 지침은 이 다섯 가지 사항에서 비롯됩니다.

1. **좋은 F # 코드는 간결하고 표현력이 뛰어나며 컴포지블합니다.**

    F#에는 적은 코드 줄로 작업을 표현하고 일반 기능을 다시 사용할 수 있는 많은 기능이 있습니다. F# 코어 라이브러리에는 일반적인 데이터 컬렉션 작업에 유용한 형식과 함수도 많이 포함되어 있습니다. 사용자 고유의 함수와 F# 코어 라이브러리(또는 기타 라이브러리)의 컴포지션은 일상적인 관용F# 프로그래밍의 일부입니다. 일반적으로 적은 코드 줄에서 문제에 대한 해결책을 표현할 수 있다면 다른 개발자(또는 미래의 자체)는 감사하게 될 것입니다. 또한 FSharp.Core, F#가 실행되는 [광대 한 .NET 라이브러리](../../../api/index.md) 또는 사소한 작업을 수행해야 할 때 [NuGet에서](https://www.nuget.org/) 타사 패키지를 사용하는 것이 좋습니다.

2. **좋은 F # 코드는 상호 운용 가능**

    상호 운용은 다른 언어로 코드를 사용하는 것을 포함하여 여러 형태를 취할 수 있습니다. 다른 호출자가 상호 운용하는 코드의 경계는 호출자가 F#에 있더라도 올바르게 작동하기 위해 중요한 부분입니다. F#을 작성할 때는 C#과 같은 다른 언어에서 다른 코드를 작성하는 경우를 포함하여 다른 코드가 작성하는 코드에 어떻게 호출되는지 항상 고려해야 합니다. [F# 구성 요소 디자인 지침은](component-design-guidelines.md) 상호 운용성을 자세히 설명합니다.

3. **좋은 F # 코드는 객체 방향이 아닌 객체 프로그래밍을 사용합니다.**

    F#은 [클래스,](../language-reference/classes.md)인터페이스, [액세스 수정자,](../language-reference/access-control.md) [추상 클래스](../language-reference/abstract-classes.md)등을 포함하여 .NET의 [개체를](../language-reference/interfaces.md)사용하여 프로그래밍하는 데 전폭적인 지원을 제공합니다. 컨텍스트를 인식해야 하는 함수와 같이 더 복잡한 함수 코드의 경우 개체는 함수가 할 수 없는 방식으로 컨텍스트 정보를 쉽게 캡슐화할 수 있습니다. [선택적 매개 변수](../language-reference/members/methods.md#optional-arguments) 및 [과부하를](../language-reference/members/methods.md#overloaded-methods) 주의 깊게 사용하면 호출자에게 이 기능을 더 쉽게 사용할 수 있습니다.

4. **좋은 F # 코드는 돌연변이를 노출하지 않고 잘 수행됩니다.**

    고성능 코드를 작성하려면 돌연변이를 사용해야 한다는 것은 비밀이 아닙니다. 결국 컴퓨터가 작동하는 방식입니다. 이러한 코드는 종종 오류가 발생하기 쉽고 올바르게 이해하기가 어렵습니다. 호출자에게 돌연변이를 노출하지 마십시오. 대신 성능이 중요한 경우 [돌연변이 기반 구현을 숨기는 기능 인터페이스를 빌드합니다.](conventions.md#performance)

5. **좋은 F # 코드는 툴 수 있습니다**

    도구는 대규모 코드베이스에서 작업하는 데 매우 유용하며 F# 언어 툴링에서 보다 효과적으로 사용할 수 있도록 F# 코드를 작성할 수 있습니다. 한 가지 예는 중간 값을 디버거로 검사할 수 있도록 포인트 프리 프로그래밍 스타일로 과도하게 수행하지 않도록 하는 것입니다. 또 다른 예는 편집기의 도구 설명이 호출 사이트에 해당 주석을 표시할 수 있도록 구문 설명을 설명하는 [XML 설명서](../language-reference/xml-documentation.md) 주석을 사용하는 것입니다. 다른 프로그래머가 도구를 사용하여 코드를 읽고, 탐색하고, 디버깅하고, 조작하는 방법을 항상 생각해 보십시오.

## <a name="next-steps"></a>다음 단계

[F# 코드 서식 지정 지침은](formatting.md) 읽기 쉽도록 코드를 포맷하는 방법에 대한 지침을 제공합니다.

[F# 코딩 규칙은](conventions.md) 더 큰 F# 코드베이스의 장기적인 유지 관리에 도움이 되는 F# 프로그래밍 숙어에 대한 지침을 제공합니다.

[F# 구성 요소 디자인 지침은](component-design-guidelines.md) 라이브러리와 같은 F# 구성 요소를 작성하기 위한 지침을 제공합니다.
