---
title: 값 또는 참조로 인수 전달
ms.date: 07/20/2015
helpviewer_keywords:
- ByRef keyword [Visual Basic], passing arguments by reference
- Visual Basic code, procedures
- passing arguments [Visual Basic], by value or by reference
- ByVal keyword [Visual Basic], passing arguments by value
- arguments [Visual Basic], passing by value or by reference
- argument passing [Visual Basic], by value or by reference
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
ms.openlocfilehash: 28e59753a35ab67b15fbc549df5bb8a3489aba5a
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352601"
---
# <a name="passing-arguments-by-value-and-by-reference-visual-basic"></a>값 및 참조로 인수 전달(Visual Basic)
Visual Basic에서 인수를 *값* 또는 *참조로*프로시저에 전달할 수 있습니다. 이를 *전달 메커니즘*이라고 하며 프로시저에서 호출 코드의 인수 내부 프로그래밍 요소를 수정할 수 있는지 여부를 결정 합니다. 프로시저 선언은 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 또는 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 키워드를 지정 하 여 각 매개 변수에 대 한 전달 메커니즘을 결정 합니다.  
  
## <a name="distinctions"></a>기준을  
 프로시저에 인수를 전달할 때 서로 상호 작용 하는 여러 가지 차이점에 주의 해야 합니다.  
  
- 기본 프로그래밍 요소를 수정할 수 있는지 여부를 지정 합니다.  
  
- 인수 자체를 수정할 수 있는지 여부를 지정 합니다.  
  
- 인수가 값 또는 참조로 전달 되는지 여부  
  
- 인수 데이터 형식이 값 형식 인지 또는 참조 형식 인지 여부  
  
 자세한 내용은 [수정 가능 및 수정할](./differences-between-modifiable-and-nonmodifiable-arguments.md) 가능성이 [없는 인수와 인수를 값으로 전달할 때와 참조로 전달할](./differences-between-passing-an-argument-by-value-and-by-reference.md)때의 차이점을 참조 하세요.  
  
## <a name="choice-of-passing-mechanism"></a>전달 메커니즘 선택  
 각 인수에 대해 전달 메커니즘을 신중 하 게 선택 해야 합니다.  
  
- **보호**. 두 전달 메커니즘 중에서 하나를 선택 하는 경우 가장 중요 한 기준은 변경 하는 호출 변수를 노출 하는 것입니다. 인수 `ByRef` 전달의 이점은 프로시저에서 해당 인수를 통해 호출 코드에 값을 반환할 수 있다는 것입니다. `ByVal` 인수를 전달 하는 이점은 프로시저에 의해 변수가 변경 되지 않도록 보호 하는 것입니다.  
  
- **성능**. 전달 메커니즘이 코드의 성능에 영향을 줄 수 있지만 차이점은 일반적으로 중요 하지 않습니다. 한 가지 예외는 `ByVal`전달 되는 값 형식입니다. 이 경우 Visual Basic은 인수의 전체 데이터 내용을 복사 합니다. 따라서 구조체와 같은 많은 값 형식의 경우 `ByRef`전달 하는 것이 더 효율적일 수 있습니다.  
  
     참조 형식의 경우에는 데이터에 대 한 포인터만 복사 됩니다 (32 비트 플랫폼에서는 4 바이트, 64 비트 플랫폼에서는 8 바이트). 따라서 저하를 사용 하지 않고 `String` 또는 `Object` 형식의 인수를 값으로 전달할 수 있습니다.  
  
## <a name="determination-of-the-passing-mechanism"></a>전달 메커니즘의 결정  
 프로시저 선언은 각 매개 변수에 대 한 전달 메커니즘을 지정 합니다. 호출 코드는 `ByVal` 메커니즘을 재정의할 수 없습니다.  
  
 `ByRef`를 사용 하 여 매개 변수를 선언 하는 경우 호출 코드는 호출에서 인수 이름을 괄호로 묶어 `ByVal` 메커니즘을 강제로 적용할 수 있습니다. 자세한 내용은 [방법: 인수를 값으로 전달](./how-to-force-an-argument-to-be-passed-by-value.md)하는 방법을 참조 하세요.  
  
 Visual Basic의 기본값은 인수를 값으로 전달 하는 것입니다.  
  
## <a name="when-to-pass-an-argument-by-value"></a>값으로 인수를 전달 하는 경우  
  
- 인수의 내부 호출 코드 요소가 수정할 수 없는 요소인 경우 해당 하는 매개 변수를 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)로 선언 합니다. 수정할 수 없는 요소의 값을 변경할 수 있는 코드는 없습니다.  
  
- 기본 요소를 수정할 수 있지만 프로시저에서 해당 값을 변경할 수 없도록 하려면 `ByVal`매개 변수를 선언 합니다. 호출 코드만 값으로 전달 되는 수정 가능한 요소의 값을 변경할 수 있습니다.  
  
## <a name="when-to-pass-an-argument-by-reference"></a>인수를 참조로 전달 하는 경우  
  
- 프로시저에서 호출 코드의 기본 요소를 변경 해야 하는 경우 해당 매개 변수 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)를 선언 합니다.  
  
- 코드를 올바르게 실행 하는 경우 호출 코드에서 기본 요소를 변경 하는 절차에 따라 `ByRef`매개 변수를 선언 합니다. 값으로 전달 하거나 호출 하는 코드가 인수를 괄호로 묶어 `ByRef` 전달 하는 메커니즘을 재정의 하는 경우 프로시저 호출이 예기치 않은 결과를 생성할 수 있습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 인수를 값으로 전달 하는 경우와 참조로 인수를 전달 하는 경우를 보여 줍니다. 프로시저 `Calculate`에 `ByVal` 및 `ByRef` 매개 변수가 모두 있습니다. 이자율을 지정 하 고, `rate`하 고, `debt`금액의 합계를 제공 하는 경우 절차의 작업은 `debt`의 원래 값에 이자율을 적용 한 결과 `debt`에 대 한 새 값을 계산 하는 것입니다. `debt`는 `ByRef` 매개 변수 이므로 새 합계는 `debt`에 해당 하는 호출 코드의 인수 값에 반영 됩니다. `Calculate`에서 값을 변경 하면 안 되기 때문에 매개 변수 `rate` `ByVal` 매개 변수입니다.  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbcnProcedures#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class2.vb#74)]  
  
## <a name="see-also"></a>참고 항목

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [방법: 프로시저 인수의 값 변경](./how-to-change-the-value-of-a-procedure-argument.md)
- [방법: 값 변경에 대해 프로시저 인수 보호](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [방법: 인수가 값으로 전달되도록 설정](./how-to-force-an-argument-to-be-passed-by-value.md)
- [위치 및 이름으로 인수 전달](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
