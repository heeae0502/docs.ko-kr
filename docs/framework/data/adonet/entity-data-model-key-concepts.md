---
title: 엔터티 데이터 모델의 주요 개념
ms.date: 03/30/2017
ms.assetid: c635a16d-6674-45aa-9344-dcb7df992bab
ms.openlocfilehash: b3a2f8eb9fa5b83eec5ba7c2a56c348d050d1938
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73737825"
---
# <a name="entity-data-model-key-concepts"></a>엔터티 데이터 모델의 주요 개념
EDM (엔터티 데이터 모델)에서는 *엔터티 형식*, *연결 형식*및 *속성*의 세 가지 주요 개념을 사용 하 여 데이터 구조를 설명 합니다. 이는 모든 EDM 구현의 데이터 구조 설명에 가장 중요한 개념입니다.  
  
## <a name="entity-type"></a>엔터티 형식  
 [엔터티 형식은](entity-type.md) 엔터티 데이터 모델를 사용 하 여 데이터의 구조를 설명 하는 기본 구성 요소입니다. 개념적 모델에서 엔터티 형식은 [속성](property.md) 에서 구성 되며 비즈니스 응용 프로그램의 고객 및 주문과 같은 최상위 개념의 구조를 설명 합니다. 컴퓨터 프로그램의 클래스 정의가 클래스 인스턴스의 템플릿인 것과 동일한 방식으로 엔터티 형식은 엔터티의 템플릿입니다. 엔터티는 특정 고객 또는 주문과 같은 특정 개체를 나타냅니다. 각 엔터티에는 [엔터티 집합](entity-set.md)내에 고유한 [엔터티 키](entity-key.md) 가 있어야 합니다.  엔터티 집합은 특정 엔터티 형식 인스턴스의 컬렉션입니다. 엔터티 집합 (및 [연결 집합](association-set.md))은 [엔터티 컨테이너](entity-container.md)에 논리적으로 그룹화 됩니다.  
  
 엔터티 형식에 대해 상속이 지원되므로 한 엔터티 형식에서 다른 엔터티 형식이 파생될 수 있습니다. 자세한 내용은 [엔터티 데이터 모델: 상속](entity-data-model-inheritance.md)을 참조 하세요.  
  
## <a name="association-type"></a>연결 형식  
 연결 [형식](association-type.md) (연결이 라고도 함)은 엔터티 데이터 모델에서 관계를 설명 하는 기본 구성 요소입니다. 개념적 모델에서 연결은 두 엔터티 형식(예: Customer 및 Order) 간의 관계를 나타냅니다. 모든 연결에는 연결에 관련 된 엔터티 형식을 지정 하는 두 개의 [연결 end](association-end.md) 가 있습니다. 또한 각 연결 end는 연결의 해당 끝에 있을 수 있는 엔터티 수를 나타내는 [연결 end 복합성](association-end-multiplicity.md) 을 지정 합니다. 연결 end 복합성은 1 (1), 0 또는 1 (0 ..1) 또는 다 수 (\*) 값을 가질 수 있습니다. 연결의 한 end에 있는 엔터티는 엔터티 형식에서 노출 된 경우 [탐색 속성](navigation-property.md)또는 외래 키를 통해 액세스할 수 있습니다. 자세한 내용은 [외래 키 속성](foreign-key-property.md)을 참조 하세요.  
  
 애플리케이션에서 연결 인스턴스는 특정 연결(예: 고객 인스턴스와 주문 인스턴스 간의 연결)을 나타냅니다. 연결 인스턴스는 [연결 집합](association-set.md)에 논리적으로 그룹화 됩니다. 연결 집합 및 [엔터티 집합](entity-set.md)은 [엔터티 컨테이너](entity-container.md)에 논리적으로 그룹화 됩니다.  
  
## <a name="property"></a>속성  
 [엔터티 형식](entity-type.md) 에는 구조체와 특성을 정의 하는 [속성이](property.md) 포함 되어 있습니다. 예를 들어, Customer 엔터티 형식에는 CustomerId, Name, Address 등의 속성이 있을 수 있습니다.  
  
 개념적 모델의 속성은 컴퓨터 프로그램의 클래스에 정의된 속성과 유사합니다. 클래스의 속성이 클래스의 모양을 정의하고 개체에 대한 정보를 전달하는 것과 동일한 방식으로, 개념적 모델의 속성은 엔터티 형식의 모양을 정의하고 엔터티 형식 인스턴스에 대한 정보를 전달합니다.  
  
 속성에는 기본 데이터(예: 문자열, 정수 또는 부울 값) 또는 구조적 데이터(예: 복합 형식)가 포함될 수 있습니다. 자세한 내용은 [엔터티 데이터 모델: 기본 데이터 형식](entity-data-model-primitive-data-types.md)을 참조 하세요.  
  
## <a name="representations-of-a-conceptual-model"></a>개념적 모델의 표현  
 *개념적 모델* 은 엔터티 및 관계의 일부 데이터 구조에 대 한 특정 표현입니다. 개념적 모델을 나타내는 한 가지 방법은 다이어그램을 사용하는 것입니다. 다음 다이어그램에서는 엔터티 형식 세 개(`Book`, `Publisher` 및 `Author`)와 연결 두 개(`PublishedBy` 및 `WrittenBy`)가 있는 개념적 모델을 나타냅니다.  
  
 ![세 개의 엔터티 형식이 포함 된 개념적 모델을 보여 주는 다이어그램](./media/entity-data-model-key-concepts/conceptual-model-entity-types-associations.gif)  
  
 그러나 이 표현은 모델에 대한 일부 세부 정보의 표시와 관련하여 몇 가지 단점이 있습니다. 예를 들어, 속성 형식과 엔터티 집합 정보가 다이어그램에 표시되지 않습니다. DSL(Domain-Specific Language)을 사용하면 개념적 모델의 세부 정보를 보다 명확하게 표시할 수 있습니다. [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)( *개념 스키마 정의 언어* ) 이라는 XML 기반 DSL을 사용 하 여 개념적 모델을 정의 합니다. 다음은 위의 다이어그램에 표시된 개념적 모델의 CSDL 정의입니다.  
  
 [!code-xml[EDM_Example_Model#EDMExampleCSDL](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#edmexamplecsdl)]  
  
## <a name="see-also"></a>참조

- [엔터티 데이터 모델](entity-data-model.md)
