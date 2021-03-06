---
title: ANYELEMENT(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 475a9ad6-8c8d-4f49-9970-af273e5360f1
ms.openlocfilehash: c0f7686f7ff3f6458637b51e29ecafe0c0ccfbc4
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040319"
---
# <a name="anyelement-entity-sql"></a>ANYELEMENT(Entity SQL)
다중값 컬렉션에서 요소를 추출합니다.  
  
## <a name="syntax"></a>구문  
  
```csharp
ANYELEMENT ( expression )  
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 요소를 추출할 컬렉션을 반환하는 유효한 쿼리 식입니다.  
  
## <a name="return-value"></a>반환 값  
 컬렉션의 단일 요소 또는 임의 요소(컬렉션에 여러 요소가 있는 경우)를 반환하거나 컬렉션이 비어 있는 경우 `null`을 반환합니다. `collection` `Collection<T>`형식의 컬렉션인 경우 `ANYELEMENT(collection)` `T`형식의 인스턴스를 생성 하는 유효한 식입니다.  
  
## <a name="remarks"></a>주의  
 ANYELEMENT는 다중값 컬렉션에서 임의의 요소를 추출합니다. 예를 들어, 다음 예제에서는 `Customers`집합에서 singleton 요소를 추출하려고 시도합니다.  
  
```csharp
ANYELEMENT(Customers)  
```  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에서는 ANYELEMENT 연산자를 사용하여 다중값 컬렉션에서 요소를 추출합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1. [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2. 다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#ANYELEMENT](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#anyelement)]  
  
## <a name="see-also"></a>참조

- [엔터티 SQL 참조](entity-sql-reference.md)
- [null 허용 구조적 형식](nullable-structured-types-entity-sql.md)
