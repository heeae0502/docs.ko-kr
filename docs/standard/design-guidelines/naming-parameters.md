---
title: 매개 변수 이름 지정
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
ms.openlocfilehash: ebe2e2db4b109057bf576d4e18cfe511c657707e
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76743836"
---
# <a name="naming-parameters"></a>매개 변수 이름 지정
시각적 디자인 도구에서 Intellisense 및 클래스 검색 기능을 제공 하는 경우 매개 변수가 설명서 및 디자이너에 표시 되기 때문에 가독성을 명확 하 게 이해 하는 것은 매개 변수 이름에 대 한 지침을 따르는 것이 중요 합니다.

 ✔️ 매개 변수 이름에 camelCasing를 사용 합니다.

 ✔️ 설명 매개 변수 이름을 사용 합니다.

 매개 변수의 형식이 아닌 매개 변수의 의미에 따라 이름을 사용 하는 것이 좋습니다 ✔️.

### <a name="naming-operator-overload-parameters"></a>명명 연산자 오버 로드 매개 변수
 매개 변수에 의미가 없으면 이항 연산자 오버 로드 매개 변수 이름에 대해 `left` 및 `right`를 사용 ✔️ 합니다.

 매개 변수에 의미가 없는 경우 단항 연산자 오버 로드 매개 변수 이름에 대해 `value`을 사용 ✔️ 합니다.

 연산자 오버 로드 매개 변수에 대 한 의미 있는 이름을 고려 ✔️ 합니다. 이렇게 하면 중요 한 값이 추가 됩니다.

 ❌ 연산자 오버 로드 매개 변수 이름에 약어 또는 숫자 인덱스를 사용 하지 않습니다.

 *2005, 2009 Microsoft Corporation © 부분입니다. All rights reserved.*

 *Pearson Education, Inc의 동의로 재인쇄. 출처: [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 작성자: Krzysztof Cwalina 및 Brad Abrams, 출판 정보: Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*

## <a name="see-also"></a>참고 항목

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)
