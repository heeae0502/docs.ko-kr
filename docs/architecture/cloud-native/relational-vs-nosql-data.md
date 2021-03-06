---
title: 관계형 대 NoSQL 데이터
description: 클라우드 네이티브 애플리케이션에서 관계형 및 NoSQL 데이터에 대해 알아보기
author: robvet
ms.date: 01/22/2020
ms.openlocfilehash: 04693e30ba3848f1e51f1c69a75be5f18ead4cf1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141421"
---
# <a name="relational-vs-nosql-data"></a>관계형 대 NoSQL 데이터

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

관계형 및 NoSQL은 클라우드 네이티브 앱에서 일반적으로 구현되는 두 가지 유형의 데이터베이스 시스템입니다. 서로 다르게 빌드되고 데이터를 다르게 저장하며 다르게 액세스합니다. 이 섹션에서는 두 가지를 모두 살펴보겠습니다. 이 장의 후반부에서는 *NewSQL*이라는 새로운 데이터베이스 기술을 살펴보겠습니다.

*관계형 데이터베이스는* 수십 년 동안 널리 보급된 기술이었습니다. 그들은 성숙하고 입증되었으며 널리 구현되었습니다. 경쟁 데이터베이스 제품, 툴링 및 전문 지식이 풍부합니다. 관계형 데이터베이스는 관련 데이터 테이블의 저장소를 제공합니다. 이러한 테이블에는 고정 스키마가 있고 SQL(구조화 된 쿼리 언어)을 사용하여 데이터를 관리하고 ACID 보증을 지원합니다.

*SQL 데이터베이스가 없는 데이터베이스는* 고성능 비관계형 데이터 저장소를 참조합니다. 사용 편의성, 확장성, 복원력 및 가용성 특성이 뛰어납니다. NoSQL은 정규화된 데이터의 테이블을 결합하는 대신 비정형 또는 반구조화된 데이터를 키-값 쌍 또는 JSON 문서에 저장합니다. 일반적으로 SQL 데이터베이스가 없는 데이터베이스는 단일 데이터베이스 파티션의 범위를 벗어나는 ACID 보장을 제공하지 않습니다. 두 번째 응답 시간이 필요한 대용량 서비스는 NoSQL 데이터 저장소를 선호합니다.

분산 클라우드 네이티브 시스템에 대한 [NoSQL](https://www.geeksforgeeks.org/introduction-to-nosql/) 기술의 영향은 아무리 강조해도 지나치지 않습니다. 이 공간에서 새로운 데이터 기술이 확산되면 한때 관계형 데이터베이스에만 의존했던 솔루션이 중단되었습니다.

NoSQL 데이터베이스에는 데이터에 액세스하고 관리하기 위한 여러 가지 모델이 포함되어 있으며, 각 모델은 특정 사용 사례에 적합합니다. 그림 5-9는 네 가지 공통 모델을 제공합니다.

![NoSQL 데이터 모델](./media/types-of-nosql-datastores.png)

**그림 5-9**: NoSQL 데이터베이스에 대한 데이터 모델

| 모델 | 특징 |
| :-------- | :-------- |
| 문서 저장소 | 데이터와 메타데이터는 데이터베이스 내부의 JSON 기반 문서에 계층적으로 저장됩니다. |
| 키 밸류 스토어 | NoSQL 데이터베이스 중 가장 간단한 데이터는 키-값 쌍의 컬렉션으로 표시됩니다. |
| 와이드 컬럼 스토어 | 관련 데이터는 단일 열 내에 중첩 키/값 쌍 집합으로 저장됩니다. |
| 그래프 스토어 | 데이터는 노드, 에지 및 데이터 속성으로 그래프 구조에 저장됩니다. |

## <a name="the-cap-theorem"></a>캡 정리

이러한 유형의 데이터베이스 간의 차이점을 이해하는 방법으로 상태를 저장하는 분산 시스템에 적용되는 일련의 원칙인 CAP 정리를 고려하십시오. 도 5-10은 CAP 정리의 세 가지 특성을 나타낸다.

![CAP 원리](./media/cap-theorem.png)

**그림 5-10**. 캡 정리

정리에 따르면 분산 데이터 시스템은 일관성, 가용성 및 파티션 허용 오차 간에 장단점을 제공합니다. 또한 모든 데이터베이스는 세 가지 속성 중 *두 개만* 보장할 수 있습니다.

- *일관성.* 클러스터의 모든 노드는 모든 복제본이 업데이트될 때까지 시스템에서 요청을 차단해야 하는 경우에도 가장 최근 데이터로 응답합니다. 현재 업데이트 중인 항목에 대해 "일관된 시스템"을 쿼리하는 경우 모든 복제본이 성공적으로 업데이트될 때까지 해당 응답을 기다립니다. 그러나 최신 데이터를 받게 됩니다.

- *가용성.* 모든 노드는 해당 응답이 최신 데이터가 아니더라도 즉각적인 응답을 반환합니다. 업데이트되는 항목에 대해 "사용 가능한 시스템"을 쿼리하면 해당 순간에 서비스가 제공할 수 있는 최상의 답변을 얻을 수 있습니다.

- *파티션 허용 오차.* 복제된 데이터 노드가 실패하거나 복제된 다른 데이터 노드와의 연결이 끊어지더라도 시스템이 계속 작동하도록 보장합니다.

관계형 데이터베이스는 일반적으로 일관성과 가용성을 제공하지만 파티션 허용 오차는 제공하지 않습니다. 일반적으로 단일 서버에 프로비전되며 컴퓨터에 더 많은 리소스를 추가하여 수직으로 확장됩니다.

많은 관계형 데이터베이스 시스템은 기본 데이터베이스의 복사본을 다른 보조 서버 인스턴스에 만들 수 있는 기본 제공 복제 기능을 지원합니다. 쓰기 작업은 기본 인스턴스에 대해 만들어지고 각 보조 인스턴스에 복제됩니다. 오류가 발생할 경우 기본 인스턴스가 보조 인스턴스로 장애 조치되어 고가용성을 제공할 수 있습니다. 보조 데이터베이스는 읽기 작업을 배포하는 데 사용할 수도 있습니다. 쓰기 작업은 항상 기본 복제본에 대해 이동하지만 읽기 작업은 시스템 부하를 줄이기 위해 보조 데이터베이스로 라우팅할 수 있습니다.

[샤딩](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-introduction)과 같은 여러 노드에서 데이터를 가로로 분할할 수도 있습니다. 그러나 샤딩은 쉽게 통신할 수 없는 여러 조각에 걸쳐 데이터를 침을 뱉어 운영 오버헤드를 크게 증가시킵니다. 관리비용이 많이 들고 시간이 많이 소요될 수 있습니다. 성능, 테이블 조인 및 참조 무결성에 영향을 미칠 수 있습니다.

데이터 복제본이 "매우 일관된" 관계형 데이터베이스 클러스터에서 네트워크 연결을 끊는 경우 데이터베이스에 쓸 수 없습니다. 시스템은 다른 데이터 복제본에 해당 변경 을 복제할 수 없기 때문에 쓰기 작업을 거부합니다. 트랜잭션이 완료되기 전에 모든 데이터 복제본을 업데이트해야 합니다.

NoSQL 데이터베이스는 일반적으로 고가용성 및 파티션 허용 오차를 지원합니다. 그들은 종종 상품 서버에서 수평으로 확장됩니다. 이 접근 방식은 저렴한 비용으로 지리적 지역 내 및 전체에서 엄청난 가용성을 제공합니다. 이러한 컴퓨터 또는 노드 간에 데이터를 분할하고 복제하여 중복성과 내결함성을 제공합니다. 단점은 일관성입니다. 하나의 NoSQL 노드에서 데이터를 변경하면 다른 노드로 전파하는 데 다소 시간이 걸릴 수 있습니다. 일반적으로 NoSQL 데이터베이스 노드는 표시되는 데이터가 오래되고 아직 업데이트되지 않은 경우에도 쿼리에 대한 즉각적인 응답을 제공합니다.

데이터 복제본이 "가용성이 높은" NoSQL 데이터베이스 클러스터에서 연결이 끊어지는 경우에도 데이터베이스에 대한 쓰기 작업을 완료할 수 있습니다. 데이터베이스 클러스터를 사용하면 쓰기 작업을 허용하고 각 데이터 복제본을 사용할 수 있게 되면 업데이트할 수 있습니다.

이러한 종류의 결과는 ACID 트랜잭션이 지원되지 않는 분산 데이터 시스템의 특성인 최종 일관성이라고 합니다. 데이터 항목의 업데이트와 해당 업데이트를 각 복제노드에 전파하는 데 걸리는 시간 사이에 는 약간의 지연이 있습니다. 정상적인 조건에서는 일반적으로 지연이 짧지만 문제가 발생할 때 증가할 수 있습니다. 예를 들어 미국의 NoSQL 데이터베이스에서 제품 항목을 업데이트하고 유럽의 복제 데이터베이스 노드에서 동일한 데이터 항목을 쿼리하는 경우 어떻게 됩니까? 클러스터가 제품 변경과 함께 유럽 노드를 업데이트할 때까지 이전 제품 정보를 받게 됩니다. 쿼리 결과를 즉시 반환하고 모든 복제본 노드가 업데이트될 때까지 기다리지 않으면 엄청난 규모와 볼륨을 얻을 수 있지만 이전 데이터를 표시할 수 있습니다.

높은 가용성과 대규모 확장성은 종종 강력한 일관성보다 비즈니스에 더 중요합니다. 개발자는 Sagas, CQRS 및 비동기 메시징과 같은 기술과 패턴을 구현하여 최종 일관성을 수용할 수 있습니다.

> 요즘, CAP 정리 제약 조건을 conidering 때주의해야. NewSQL이라는 새로운 유형의 데이터베이스가 등장하여 관계형 데이터베이스 엔진을 확장하여 수평 확장성과 NoSQL 시스템의 확장 가능한 성능을 모두 지원합니다.

## <a name="considerations-for-relational-vs-nosql-systems"></a>관계형 및 NoSQL 시스템에 대한 고려 사항

특정 데이터 요구 사항에 따라 클라우드 네이티브 기반 마이크로 서비스는 관계형, NoSQL 데이터 스토어 또는 둘 다를 구현할 수 있습니다.

|  다음과 같은 경우 NoSQL 데이터 스토어를 고려하십시오. | 다음과 같은 경우 관계형 데이터베이스를 고려하십시오. |
| :-------- | :-------- |
| 대규모 워크로드가 필요한 대용량 워크로드가 있는 경우 | 워크로드 볼륨이 일관되고 중간 규모에서 대규모로 필요합니다. |
| 워크로드에 ACID 보증이 필요하지 않습니다. |  ACID 보증이 필요합니다. |
| 데이터는 동적이며 자주 변경됩니다. | 데이터를 예측 가능하고 고도로 구조화 |
| 관계 없이 데이터를 표현할 수 있습니다. | 데이터는 관계적으로 가장 잘 표현됩니다. |  
| 빠른 쓰기 및 쓰기 안전이 중요하지 않아요. | 쓰기 안전은 필수 사항입니다. |  
| 데이터 검색은 간단하며 평평한 경향이 있습니다. | 복잡한 쿼리 및 보고서로 작업|
| 데이터에는 광범위한 지리적 분포가 필요합니다. | 사용자가 더 중앙 집중화됩니다. |
| 응용 프로그램은 퍼블릭 클라우드와 같은 상용 하드웨어에 배포됩니다. | 응용 프로그램이 대형 고급 하드웨어에 배포됩니다. |
|||

다음 섹션에서는 클라우드 네이티브 데이터를 저장하고 관리하기 위해 Azure 클라우드에서 사용할 수 있는 옵션을 살펴봅니다.

## <a name="database-as-a-service"></a>Database as a Service

시작하려면 Azure 가상 컴퓨터를 프로비전하고 각 서비스에 대해 선택한 데이터베이스를 설치할 수 있습니다. 환경을 완전히 제어할 수 있지만 클라우드 플랫폼의 많은 기본 제공 기능을 포기해야 합니다. 또한 각 서비스에 대한 가상 컴퓨터 및 데이터베이스를 관리해야 합니다. 이 방법은 시간이 많이 걸리고 비용이 많이 들 수 있습니다.

대신 클라우드 네이티브 응용 프로그램은 [DBaaS(서비스)로 데이터베이스로](https://www.stratoscale.com/blog/dbaas/what-is-database-as-a-service/)노출된 데이터 서비스를 선호합니다. 클라우드 공급업체에서 완벽하게 관리되는 이러한 서비스는 기본 제공 보안, 확장성 및 모니터링을 제공합니다. 서비스를 소유하는 대신 [백업 서비스로](./definition.md#backing-services)사용하기만 하면 됩니다. 공급자는 대규모로 리소스를 운영하며 성능 및 유지 관리에 대한 책임을 집니다.

고가용성을 달성하기 위해 클라우드 가용성 영역 및 지역에서 구성할 수 있습니다. 그들은 모두 적시에 용량과 종량제 모델을 지원합니다. Azure는 각각 특정 이점이 있는 다양한 종류의 관리되는 데이터 서비스 옵션을 제공합니다.

먼저 Azure에서 사용할 수 있는 관계형 DBaaS 서비스를 살펴보겠습니다. Microsoft의 주력 SQL Server 데이터베이스를 여러 오픈 소스 옵션과 함께 사용할 수 있습니다. 그런 다음 Azure의 NoSQL 데이터 서비스에 대해 살펴보겠습니다.

## <a name="azure-relational-databases"></a>Azure 관계형 데이터베이스

관계형 데이터가 필요한 클라우드 네이티브 마이크로 서비스의 경우 Azure는 그림 5-11에 표시된 DBaaS(서비스) 서비스로 관리되는 4개의 관계형 데이터베이스를 제공합니다.

![Azure에서 관리되는 관계형 데이터베이스](./media/azure-managed-databases.png)

**그림 5-11**. Azure에서 사용할 수 있는 관리되는 관계형 데이터베이스

이전 그림에서는 추가 비용 없이 주요 기능을 제공하는 공통 DBaaS 인프라에 각 인프라가 어떻게 있는지 알아두어 보살펴 보입니다.

이러한 기능은 많은 수의 데이터베이스를 프로비전하지만 관리할 리소스가 제한된 조직에서 특히 중요합니다.
처리 코어, 메모리 및 기본 저장소의 양을 선택하여 몇 분 만에 Azure 데이터베이스를 프로비전할 수 있습니다. 즉시 데이터베이스를 확장하고 가동 중지 시간이 거의 또는 전혀 없이 리소스를 동적으로 조정할 수 있습니다.

## <a name="azure-sql-database"></a>Azure SQL Database

Microsoft SQL Server에 대한 전문 지식을 갖춘 개발 팀은 [Azure SQL Database를](https://docs.microsoft.com/azure/sql-database/)고려해야 합니다. Microsoft SQL Server 데이터베이스 엔진을 기반으로 하는 DBaaS(서비스형) 완전히 관리되는 관계형 데이터베이스입니다. 이 서비스는 SQL Server의 온-프레미스 버전에 있는 많은 기능을 공유하며 SQL Server 데이터베이스 엔진의 최신 안정 버전을 실행합니다.

클라우드 네이티브 마이크로 서비스와 함께 사용할 수 있는 Azure SQL Database는 세 가지 배포 옵션과 함께 사용할 수 있습니다.

- 단일 데이터베이스는 Azure 클라우드의 Azure [SQL Database 서버에서](https://docs.microsoft.com/azure/sql-database/sql-database-servers) 실행되는 완전히 관리되는 SQL 데이터베이스를 나타냅니다. 데이터베이스는 기본 데이터베이스 서버에 대한 구성 종속성이 없기 때문에 [*포함된*](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) 것으로 간주됩니다.
  
- [관리되는 인스턴스는](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) 온-프레미스 SQL Server와 거의 100% 호환성을 제공하는 Microsoft SQL Server 데이터베이스 엔진의 완전히 관리되는 인스턴스입니다. 이 옵션은 최대 35TB의 더 큰 데이터베이스를 지원하며 더 나은 격리를 위해 [Azure 가상 네트워크에](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 배치됩니다.

- [Azure SQL Database 서버리스는](https://docs.microsoft.com/azure/sql-database/sql-database-serverless) 워크로드 수요에 따라 자동으로 확장되는 단일 데이터베이스의 계산 계층입니다. 초당 사용되는 계산 양에 대해서만 청구됩니다. 이 서비스는 비활성 기간이 산재된 간헐적이고 예측할 수 없는 사용 패턴이 있는 워크로드에 적합합니다. 또한 서버리스 계산 계층은 비활성 기간 동안 데이터베이스를 자동으로 일시 중지하여 저장소 요금만 청구됩니다. 활동이 반환되면 자동으로 다시 시작됩니다.

Azure는 기존의 Microsoft SQL Server 스택 외에도 인기 있는 세 가지 오픈 소스 데이터베이스의 관리되는 버전도 제공합니다.

## <a name="open-source-databases-in-azure"></a>Azure의 오픈 소스 데이터베이스

오픈 소스 관계형 데이터베이스는 클라우드 네이티브 응용 프로그램에 널리 사용되었습니다. 많은 기업들이 상업용 데이터베이스 제품보다 선호하며, 특히 비용 절감을 위해 선호합니다. 많은 개발 팀이 유연성, 커뮤니티 지원 개발 및 도구 및 확장 에코시스템을 누비고 있습니다. 오픈 소스 데이터베이스를 여러 클라우드 공급자에 배포할 수 있어 "공급업체 종속"의 우려를 최소화할 수 있습니다.

개발자는 Azure VM에서 모든 오픈 소스 데이터베이스를 쉽게 자체 호스트할 수 있습니다. 이 접근 방식은 완전한 제어를 제공하는 동시에 데이터베이스와 VM의 관리, 모니터링 및 유지 관리를 위한 후크를 제공합니다.

그러나 Microsoft는 널리 알려진 여러 오픈 소스 데이터베이스를 *완전히 관리되는* DBaaS 서비스로 제공함으로써 Azure를 "개방형 플랫폼"으로 유지하기 위한 노력을 계속하고 있습니다.

### <a name="azure-database-for-mysql"></a>Azure Database for MySQL

[MySQL은](https://en.wikipedia.org/wiki/MySQL) 오픈 소스 관계형 데이터베이스이며 [LAMP 소프트웨어 스택에](https://en.wikipedia.org/wiki/LAMP_(software_bundle))구축된 응용 프로그램의 기둥입니다. 읽기 *무거운* 워크로드에 대 한 널리 선택, 그것은 많은 큰 조직에 의해 사용, 페이스 북을 포함 하 여, 지 저 귀 다, 그리고 유튜브. 커뮤니티 에디션은 무료로 사용할 수 있으며 엔터프라이즈 에디션에서는 라이선스 를 구매해야 합니다. 원래 1995 년에 만든, 제품은 2008 년에 태양 마이크로 시스템에 의해 구입되었다. 오라클은 2010년 썬과 MySQL을 인수했다.

[MySQL용 Azure 데이터베이스는](https://azure.microsoft.com/services/mysql/) 오픈 소스 MySQL Server 엔진을 기반으로 하는 관리되는 관계형 데이터베이스 서비스입니다. 그것은 MySQL 커뮤니티 버전을 사용합니다. Azure MySQL 서버는 서비스의 관리 지점입니다. 온-프레미스 배포에 사용되는 MySQL 서버 엔진과 동일합니다. 엔진은 서버당 단일 데이터베이스 또는 리소스를 공유하는 서버당 여러 데이터베이스를 만들 수 있습니다. 새로운 기술을 배우거나 가상 컴퓨터를 관리할 필요 없이 동일한 오픈 소스 도구를 사용하여 데이터를 계속 관리할 수 있습니다.

### <a name="azure-database-for-mariadb"></a>Azure Database for MariaDB

[마리아DB](https://mariadb.com/) 서버는 또 다른 인기있는 오픈 소스 데이터베이스 서버입니다. 오라클이 MySQL을 소유한 썬 마이크로시스템즈를 인수했을 때 MySQL의 *포크로* 만들어졌습니다. 마리아DB가 오픈 소스로 남아 있도록 하기 위한 것이었습니다. MariaDB는 MySQL의 포크이므로 데이터와 테이블 정의가 호환되며 클라이언트 프로토콜, 구조 및 API가 긴밀하게 관련되어 있습니다.

MariaDB는 강력한 커뮤니티를 가지고 있으며 많은 대기업에서 사용됩니다. 오라클은 MySQL을 지속적으로 유지, 강화 및 지원하지만 MariaDB 재단은 MariaDB를 관리하여 제품 및 문서에 대한 대중의 기여를 허용합니다.

[MariaDB용 Azure 데이터베이스는](https://azure.microsoft.com/services/mariadb/) Azure 클라우드의 서비스로서 완전히 관리되는 관계형 데이터베이스입니다. 이 서비스는 MariaDB 커뮤니티 에디션 서버 엔진을 기반으로 합니다. 예측 가능한 성능과 동적 확장성을 통해 미션 크리티컬 워크로드를 처리할 수 있습니다.

### <a name="azure-database-for-postgresql"></a>Azure Database for PostgreSQL

[PostgreSQL은](https://www.postgresql.org/) 30년 이상의 활발한 개발을 통해 오픈 소스 관계형 데이터베이스입니다. PostgresSQL은 안정성과 데이터 무결성에 대한 강력한 명성을 가지고 있습니다. 특히 복잡한 쿼리와 쓰기가 많은 워크로드의 경우 MySQL보다 풍부하고 SQL을 준수하는 기능이 더 성능이 뛰어난 것으로 간주됩니다. 애플, 레드햇, 후지쯔 등 많은 대기업들이 PostgreSQL을 사용하여 제품을 제작했습니다.

[PostgreSQL용 Azure 데이터베이스는](https://azure.microsoft.com/services/postgresql/) 오픈 소스 Postgres 데이터베이스 엔진을 기반으로 하는 완전히 관리되는 관계형 데이터베이스 서비스입니다. 이 서비스는 C++, Java, 파이썬, 노드,\#C 및 PHP를 포함한 많은 개발 플랫폼을 지원합니다. [명령줄 인터페이스](https://datamigration.microsoft.com/scenario/postgresql-to-azurepostgresql?step=1) 도구 또는 Azure 데이터 마이그레이션 서비스를 사용하여 PostgreSQL 데이터베이스를 마이그레이션할 수 있습니다.

PostgreSQL용 Azure 데이터베이스는 두 가지 배포 옵션으로 사용할 수 있습니다.

- [단일 서버](https://docs.microsoft.com/azure/postgresql/concepts-servers) 배포 옵션은 여러 데이터베이스를 배포할 수 있는 여러 데이터베이스의 중앙 관리 지점입니다. 가격은 코어 및 저장소를 기반으로 서버당 구조화됩니다.

- [하이퍼스케일(Citus) 옵션은](https://azure.microsoft.com/blog/get-high-performance-scaling-for-your-azure-database-workloads-with-hyperscale/) Citus 데이터 기술에 의해 구동됩니다. 수백 개의 노드에서 단일 데이터베이스를 *수평으로 확장하여* 빠른 성능과 확장을 제공함으로써 높은 성능을 구현할 수 있습니다. 이 옵션을 사용하면 엔진이 메모리에 더 많은 데이터를 맞추고, 수백 개의 노드에서 쿼리를 병렬화하고, 데이터를 더 빠르게 인덱싱할 수 있습니다.

## <a name="nosql-data-in-azure"></a>Azure의 NoSQL 데이터

코스모스 DB는 Azure 클라우드에서 완전히 관리되고 전 세계적으로 분산된 NoSQL 데이터베이스 서비스입니다. 코카콜라, 스카이프, 엑손모빌, 리버티 뮤추얼 등 전 세계 많은 대기업에서 채택되었습니다.

전 세계 어디서나 빠른 응답, 고가용성 또는 탄력적 확장성이 필요한 서비스에 필요한 경우 Cosmos DB는 훌륭한 선택입니다. 도 5-12는 코스모스 DB를 나타낸다.

![코스모스 DB 개요](./media/cosmos-db-overview.png)

**그림 5-12**: 코스모스 DB 개요

이전 그림은 Cosmos DB에서 사용할 수 있는 많은 기본 제공 클라우드 네이티브 기능을 제공합니다. 이 섹션에서는 자세히 살펴보겠습니다.

### <a name="global-support"></a>글로벌 지원

클라우드 네이티브 애플리케이션은 종종 전 세계 잠재고객을 가지고 있으며 글로벌 규모가 필요합니다.

Cosmos 데이터베이스를 지역 또는 전 세계에 배포하여 데이터를 사용자에게 가까이 배치하고 응답 시간을 개선하고 대기 시간을 줄일 수 있습니다. 서비스를 일시 중지하거나 다시 배포하지 않고 리전에서 데이터베이스를 추가하거나 제거할 수 있습니다. 배경에서 Cosmos DB는 구성된 각 영역에 데이터를 투명하게 복제합니다.

Cosmos DB는 전역 수준에서 [활성/활성](https://kemptechnologies.com/white-papers/unfog-confusion-active-passive-activeactive-load-balancing/) 클러스터링을 지원하므로 *쓰기 및 읽기를 모두*지원하도록 데이터베이스 영역을 구성할 수 있습니다.

[멀티 마스터](https://docs.microsoft.com/azure/cosmos-db/multi-master-benefits) 프로토콜은 코스모스 DB에서 다음과 같은 기능을 가능하게 하는 중요한 기능입니다.

- 무제한 탄력적 쓰기 및 읽기 확장성.

- 전 세계의 99.999% 읽기 및 쓰기 가용성

- 99번째 백분위에서 10밀리초 미만으로 제공되는 보장된 읽기 및 쓰기

Cosmos DB [다중 호밍 API를](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally)사용하면 마이크로 서비스가 가장 가까운 Azure 지역을 자동으로 인식하고 요청을 보냅니다. 가장 가까운 지역은 구성 변경 없이 Cosmos DB로 식별됩니다. 지역을 사용할 수 없게 되면 다중 호밍 기능은 요청을 가장 가까운 가장 가까운 지역으로 자동으로 라우팅합니다.

### <a name="multi-model-support"></a>다중 모델 지원

모놀리식 응용 프로그램을 클라우드 네이티브 아키텍처로 다시 플랫폼화할 때 개발 팀은 때때로 오픈 소스인 NoSQL 데이터 저장소를 마이그레이션해야 합니다. Cosmos DB는 *멀티 모델* 데이터 플랫폼을 통해 이러한 NoSQL 데이터 스토어에 대한 투자를 보존할 수 있도록 도와드립니다. 그림 5-13은 지원되는 NoSQL [호환성 API를](https://www.wikiwand.com/en/Cosmos_DB)보여 주며 있습니다.

![코스모스 DB 제공업체](./media/cosmos-db-providers.png)

**그림 5-13**: 코스모스 DB 제공업체

개발 팀은 데이터 나 코드를 최소한으로 변경하여 기존 몽고, 그렘린 또는 카산드라 데이터베이스를 Cosmos DB로 마이그레이션할 수 있습니다. 새 앱의 경우 개발 팀은 오픈 소스 옵션 또는 기본 제공 SQL API 모델 중에서 선택할 수 있습니다.

> 내부적으로 Cosmos는 원시 데이터 유형으로 구성된 간단한 구조 체 형식으로 데이터를 저장합니다. 각 요청에 대해 데이터베이스 엔진은 기본 데이터를 선택한 모델 표현으로 변환합니다.

이전 그림 5-13에서는 테이블 [API](https://docs.microsoft.com/azure/cosmos-db/table-introduction) 옵션을 기록합니다. 이 API는 Azure 테이블 저장소의 진화입니다. 둘 다 동일한 기본 테이블 모델을 공유하지만 Cosmos DB 테이블 API는 Azure Storage API에서 사용할 수 없는 프리미엄 향상 기능을 추가합니다. 이러한 기능은 그림 5-4에서 대조적입니다.

![Azure Table API](media/azure-table-api.png)

**그림 5-14**: Azure 테이블 API 공급자

Azure 테이블 저장소를 사용하는 마이크로 서비스는 Cosmos DB 테이블 API로 쉽게 마이그레이션할 수 있습니다. 코드 변경은 필요하지 않습니다.

### <a name="tunable-consistency"></a>조정 가능한 일관성

*관계형 대 NoSQL* 섹션의 앞에서 *데이터 일관성에*대한 주제에 대해 설명했습니다. 데이터 일관성은 데이터의 *무결성을* 나타냅니다. 분산 된 데이터를 가진 클라우드 네이티브 서비스는 복제에 의존 하 고 읽기 일관성, 가용성 및 대기 시간 사이 기본적인 장단점을 만들어야 합니다.

대부분의 분산 데이터베이스를 사용하면 개발자가 강력한 일관성과 최종 일관성이라는 두 가지 일관성 모델 중에서 선택할 수 있습니다. *강력한 일관성은* 데이터 프로그래밍 의 기본입니다. 시스템이 모든 데이터베이스 복사본에서 업데이트가 복제되기를 기다리는 대기 시간이 발생하더라도 쿼리는 항상 최신 데이터를 반환합니다. *최종 일관성을* 위해 구성된 데이터베이스는 해당 데이터가 최신 복사본이 아니더라도 데이터를 즉시 반환합니다. 후자의 옵션을 사용하면 가용성이 높아지고 규모가 커지며 성능이 향상됩니다.

Azure Cosmos DB는 그림 5-15에 표시된 5개의 잘 정의된 [일관성 모델을](https://docs.microsoft.com/azure/cosmos-db/consistency-levels) 제공합니다.

![코스모스 DB 일관성 그래프](./media/cosmos-consistency-level-graph.png)

**그림 5-15**: 코스모스 DB 일관성 수준

 이러한 옵션을 사용하면 데이터의 일관성, 가용성 및 성능을 위해 정확한 선택과 세분화된 장단점을 선택할 수 있습니다. 그림 5-16은 각 레벨을 설명합니다.

![코스모스 DB 일관성 수준](./media/cosmos-db-consistency-levels.png)

**그림 5-16**: 코스모스 DB 일관성 수준 설명

[기사에서 9 공 뒤에 점점: 코스모스 DB 일관성 수준 설명,](https://blog.jeremylikness.com/blog/2018-03-23_getting-behind-the-9ball-cosmosdb-consistency-levels/)마이크로소프트 클라우드 개발자 옹호 제레미 형상 다섯 가지 모델에 대 한 훌륭한 설명을 제공 합니다.

### <a name="partitioning"></a>분할

Azure Cosmos DB는 클라우드 네이티브 서비스의 성능 요구 사항을 충족하도록 데이터베이스를 확장하는 자동 [분할을](https://docs.microsoft.com/azure/cosmos-db/partitioning-overview) 포함합니다.

데이터베이스, 컨테이너 및 항목을 만들어 Cosmos DB 데이터의 데이터를 관리합니다.

컨테이너는 Cosmos DB 데이터베이스에 있으며 항목의 스키마에 없는 그룹화를 나타냅니다. 항목은 컨테이너에 추가하는 데이터입니다. 문서, 행, 노드 또는 가장자리로 표시됩니다. 컨테이너에 추가된 모든 항목은 자동으로 인덱싱됩니다.

컨테이너를 분할하기 위해 항목은 논리 파티션이라는 별개의 하위 집합으로 나뉩니다. 논리 파티션은 컨테이너의 각 항목과 연결된 파티션 키의 값에 따라 채워집니다. 그림 5-18은 파티션 키 값을 기반으로 하는 논리 파티션이 있는 두 개의 컨테이너를 각각 보여 주며, 각각 두 개의 컨테이너를 보여 주며, 이 두 개의 컨테이너를 보여 주며, 각각의 컨테이너를 보여 주며, 이두 가지는 각각이다.

![코스모스 DB 분할 역학](./media/cosmos-db-partitioning.png)

**그림 5-18**: 코스모스 DB 분할 역학

이전 그림에서 각 항목에 '도시' 또는 '공항'의 파티션 키가 포함되는 방식에 유의하십시오. 키는 항목의 논리 파티션을 결정합니다. 도시 코드가 있는 항목은 왼쪽의 컨테이너에 할당되고 공항 코드가 있는 항목은 오른쪽의 컨테이너에 할당됩니다. 파티션 키 값을 ID 값과 결합하면 항목을 고유하게 식별하는 항목 인덱스가 만들어집니다.

내부적으로 Cosmos DB는 컨테이너의 확장성과 성능 요구를 충족하기 위해 물리적 파티션에 [논리 파티션의](https://docs.microsoft.com/azure/cosmos-db/partition-data) 배치를 자동으로 관리합니다. 응용 프로그램 처리량 및 저장소 요구 사항이 증가함에 따라 Azure Cosmos DB는 더 많은 수의 서버에 논리 파티션을 재배포합니다. 재배포 작업은 Cosmos DB에서 관리하며 중단 또는 가동 중지 시간 없이 호출됩니다.

## <a name="newsql-databases"></a>NewSQL 데이터베이스

*NewSQL은* NoSQL의 분산 확장성과 관계형 데이터베이스의 ACID 보증을 결합한 새로운 데이터베이스 기술입니다. NewSQL 데이터베이스는 전체 트랜잭션 지원 및 ACID 규정 준수를 통해 분산 환경에서 대량의 데이터를 처리해야 하는 비즈니스 시스템에 중요합니다. NoSQL 데이터베이스는 대규모 확장성을 제공할 수 있지만 데이터 일관성을 보장하지는 않습니다. 일관성 없는 데이터로 인한 간헐적인 문제는 개발 팀에 부담을 주어주게 될 수 있습니다. 개발자는 일관성 없는 데이터로 인한 문제를 관리하기 위해 마이크로 서비스 코드에 보호 장치를 구성해야 합니다.

클라우드 네이티브 컴퓨팅 재단(CNCF)에는 여러 NewSQL 데이터베이스 프로젝트가 있습니다.

| Project | 특징 |
| :-------- | :-------- |
| 바퀴벌레 DB |전 세계적으로 확장되는 ACID 준수 관계형 데이터베이스입니다. 클러스터에 새 노드를 추가하면 CockroachDB는 인스턴스와 지역 간에 데이터 균형을 조정합니다. 안정성을 보장하기 위해 복제본을 생성, 관리 및 배포합니다. 그것은 오픈 소스이며 자유롭게 사용할 수 있습니다.  |
| 티DB | 하이브리드 트랜잭션 및 분석 처리(HTAP) 워크로드를 지원하는 오픈 소스 데이터베이스입니다. MySQL과 호환되며 수평 확장성, 강력한 일관성 및 고가용성을 제공합니다.  TiDB는 MySQL 서버처럼 작동합니다. 응용 프로그램에 대한 광범위한 코드 변경 없이 기존 MySQL 클라이언트 라이브러리를 계속 사용할 수 있습니다. |
| 유가바이트DB | 고성능 분산 SQL 데이터베이스인 오픈 소스입니다. 낮은 쿼리 대기 시간, 오류에 대한 복원력 및 전역 데이터 배포를 지원합니다. YugabyteDB는 PostgressSQL 호환이며 확장 형 RDBMS 및 인터넷 규모의 OLTP 워크로드를 처리합니다. 이 제품은 또한 NoSQL을 지원하며 카산드라와 호환됩니다. |
|비트 (주) | Vitess는 MySQL 인스턴스의 대규모 클러스터를 배포, 크기 조정 및 관리하기 위한 데이터베이스 솔루션입니다. 공용 또는 프라이빗 클라우드 아키텍처에서 실행할 수 있습니다. 그것은 결합하고 많은 중요한 MySQL 기능과 수직 및 수평 샤딩 지원 기능을 확장합니다. YouTube에서 시작된 Vitess는 2011년부터 모든 YouTube 데이터베이스 트래픽을 제공하고 있습니다. |

이전 그림의 오픈 소스 프로젝트는 클라우드 네이티브 컴퓨팅 재단에서 구할 수 있습니다. 세 가지 제품은 .NET Core 지원을 포함하는 전체 데이터베이스 제품입니다. 다른 Vitess는 MySQL 인스턴스의 큰 클러스터를 가로로 확장하는 데이터베이스 클러스터링 시스템입니다.

NewSQL 데이터베이스의 주요 설계 목표는 플랫폼의 복원력과 확장성을 활용하여 Kubernetes에서 기본적으로 작업하는 것입니다.

NewSQL 데이터베이스는 기본 가상 컴퓨터를 잠시 전에 다시 시작하거나 일정을 변경할 수 있는 임시 클라우드 환경에서 번창하도록 설계되었습니다. 데이터베이스는 데이터 손실이나 가동 중지 시간 없이 노드 오류에서 살아남을 수 있도록 설계되었습니다. 예를 들어 CockroachDB는 클러스터의 노드 에서 데이터의 세 가지 일관된 복제본을 유지 관리하여 컴퓨터 손실을 견딜 수 있습니다.

Kubernetes는 *서비스 구문에서* 클라이언트가 단일 DNS 항목에서 동일한 NewSQL 데이터베이스 프로세스 그룹을 처리하도록 허용합니다. 데이터베이스 인스턴스가 연결된 서비스의 주소에서 데이터베이스 인스턴스를 분리하여 기존 응용 프로그램 인스턴스를 중단하지 않고 확장할 수 있습니다. 지정된 시간에 모든 서비스에 요청을 보내면 항상 동일한 결과가 생성됩니다.

이 시나리오에서는 모든 데이터베이스 인스턴스가 동일합니다. 기본 또는 보조 관계가 없습니다. CockroachDB에서 발견되는 *합의 복제와* 같은 기술을 사용하면 모든 데이터베이스 노드가 모든 요청을 처리할 수 있습니다. 로드 균형 요청을 받는 노드에 필요한 데이터가 로컬로 있으면 즉시 응답합니다. 그렇지 않은 경우 노드는 게이트웨이가 되고 정답을 얻기 위해 요청을 해당 노드로 전달합니다. 클라이언트의 관점에서 모든 데이터베이스 노드는 동일합니다: 백그라운드에서 작동하는 수십 개 또는 수백 개의 노드가 있음에도 불구하고 단일 시스템 시스템의 일관성을 보장하는 단일 *논리* 데이터베이스로 나타납니다.

NewSQL 데이터베이스 뒤에 있는 메커니즘에 대한 자세한 내용은 [DASH: Kubernetes-네이티브 데이터베이스의 네 가지 속성](https://thenewstack.io/dash-four-properties-of-kubernetes-native-databases/) 문서를 참조하십시오.

## <a name="data-migration-to-the-cloud"></a>클라우드로의 데이터 마이그레이션

시간이 많이 소요되는 작업 중 하나는 한 데이터 플랫폼에서 다른 데이터 플랫폼으로 데이터를 마이그레이션하는 것입니다. [Azure 데이터 마이그레이션 서비스는](https://azure.microsoft.com/services/database-migration/) 이러한 노력을 신속하게 하는 데 도움이 될 수 있습니다. 가동 중지 시간을 최소화하면서 여러 외부 데이터베이스 원본의 데이터를 Azure Data 플랫폼으로 마이그레이션할 수 있습니다. 대상 플랫폼에는 다음 서비스가 포함됩니다.

- Azure SQL Database
- Azure Database for MySQL
- Azure Database for MariaDB
- Azure Database for PostgreSQL
- CosmosDB
  
이 서비스는 작거나 큰 마이그레이션을 실행하는 데 필요한 변경 사항을 안내하는 권장 사항을 제공합니다.

>[!div class="step-by-step"]
>[이전](Database-per-microservice.md)
>[다음](azure-caching.md)
