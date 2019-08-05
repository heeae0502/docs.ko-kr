---
title: 부분 실패 처리
description: 부분 실패를 정상적으로 처리하는 방법을 알아봅니다. 마이크로 서비스가 완전히 작동하지 않더라도 여전히 일부 유용한 작업을 수행할 수 있습니다.
ms.date: 10/16/2018
ms.openlocfilehash: a667ad2e1456db7b5846023de27d3797dad58731
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674700"
---
# <a name="handle-partial-failure"></a>부분 실패 처리

마이크로 서비스 기반 애플리케이션과 같은 분산 시스템에서는 부분적으로 실패할 위험이 있습니다. 예를 들어, 단일 마이크로 서비스/컨테이너가 실패하거나 짧은 시간 동안 응답하지 못할 수 있으며 단일 VM 또는 서버가 충돌될 수 있습니다. 클라이언트와 서비스는 별도의 프로세스이기 때문에 서비스가 클라이언트의 요청에 적시에 응답하지 못할 수 있습니다. 서비스가 오버로드되고 요청에 매우 느리게 응답하거나, 네트워크 문제로 인해 짧은 시간 동안 액세스하지 못할 수도 있습니다.

예를 들어, eShopOnContainers 샘플 애플리케이션의 주문 세부 정보 페이지를 고려하세요. 사용자가 주문을 제출할 때 순서 마이크로 서비스가 응답하지 않으면 클라이언트 프로세스(MVC 웹 애플리케이션)의 잘못된 구현은 - 예를 들어, 클라이언트 코드가 시간 제한없이 동기 RPC를 사용하는 경우 - 스레드가 응답을 무기한 대기하는 것을 차단합니다. 좋지 않은 사용자 환경을 만드는 것 외에도, 응답이 없는 모든 대기는 스레드를 사용하거나 차단하며, 스레드는 확장성이 뛰어난 애플리케이션에서 매우 중요합니다. 차단된 스레드가 많으면 결국 애플리케이션의 런타임에 스레드가 부족할 수 있습니다. 이 경우 애플리케이션은 그림 8-1과 같이, 부분적으로 응답하지 않는 것이 아니라 전체적으로 응답하지 않을 수 있습니다.

![이전 단락을 설명하는 다이어그램](./media/image1.png)

**그림 8-1**. 서비스 스레드 가용성에 영향을 주는 종속성으로 인해 일부 실패합니다.

대규모 마이크로 서비스 기반 애플리케이션에서 부분 실패는 특히 내부 마이크로 서비스 상호 작용의 대부분이 동기식 HTTP 호출(이것은 안티 패턴으로 간주됨)에 기반하여 증폭될 수 있습니다. 하루에 수백만 건의 수신 호출을 받는 시스템에 대해 생각해 봅니다. 시스템이 동기식 HTTP 호출의 긴 체인을 기반으로 하는 잘못된 디자인을 사용하는 경우, 이러한 수신 호출은 동기 종속성으로 수십 개의 내부 마이크로 서비스에 대한 수백만 건의 발신 호출(1:4 비율로 가정)을 생성할 수 있습니다. 이 상황은 그림 8-2, 특히 종속성 \#3에 나와 있습니다.

![다른 마이크로 서비스의 종속성 체인에 종속된 웹앱 마이크로 서비스에 대한 잘못된 디자인](./media/image2.png)

**그림 8-2**. HTTP 요청의 긴 체인을 특징으로 하는 잘못된 디자인의 영향

모든 종속성 자체에 우수한 가용성이 있더라도 클라우드 기반 분산 시스템에서는 일시적인 실패가 보장됩니다. 이는 실제로 고려해야 할 사항입니다.

내결함성을 보장하는 기술을 디자인하고 구현하지 않으면, 작은 가동 중지 시간이 증폭될 수 있습니다. 예를 들어 가용성이 99.99%인 각각 50개의 종속성은 이 파급 효과 때문에 매월 몇 시간의 가동 중지 시간을 초래합니다. 대용량의 요청을 처리하는 동안 마이크로 서비스 종속성이 실패하면, 실패로 인해 각 서비스의 사용 가능한 모든 요청 스레드가 빠르게 포화되어 전체 애플리케이션이 손상될 수 있습니다.

![부분 실패는 체인 종속성에 의해 심각하게 증폭될 수 있습니다.](./media/image3.png)

**그림 8-3**. 동기식 HTTP 호출의 긴 체인이 있는 마이크로 서비스에 의해 증폭된 부분 실패

이 문제를 최소화하기 위해 이 가이드의 [비동기식 마이크로 서비스 통합 적용 마이크로 서비스의 자율성](../architect-microservice-container-applications/communication-in-microservice-architecture.md#asynchronous-microservice-integration-enforces-microservices-autonomy) 섹션에서는 내부 마이크 서비스 전반에 걸쳐 비동기 통신을 사용하도록 권장하고 있습니다.

또한 부분 실패를 처리하도록 마이크로 서비스 및 클라이언트 애플리케이션을 디자인하는 것이 중요합니다. 즉, 복원력 있는 마이크로 서비스 및 클라이언트 애플리케이션을 빌드해야 합니다.

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](partial-failure-strategies.md)