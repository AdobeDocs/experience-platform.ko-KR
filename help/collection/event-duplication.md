---
title: Experience Platform에서 이벤트 복제 처리
description: Adobe Experience Platform에서 이벤트 복제를 처리하는 방법 알아보기
source-git-commit: 89cdb0832009bcee31b4339f021bc5a0ce254752
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Adobe Experience Platform에서의 이벤트 복제 처리

Adobe Experience Platform은 신뢰성을 극대화하는 동시에 증가하는 데이터 볼륨으로 확장할 수 있도록 설계된 고도로 분산된 시스템입니다.

실시간 데이터 수집의 경우 [경험 이벤트](../xdm/classes/experienceevent.md) 다음을 통해 수집됩니다. [에지 네트워크](../edge/home.md#edge-network), 클라이언트측 소스(예: ) [웹 SDK](../edge/home.md) 또는 [Mobile SDK](https://developer.adobe.com/client-sdks/home/), Experience Platform 처리 및 스토리지 계층으로 전달됩니다. 이러한 레이어는 Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko), 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html).

경험 이벤트 손실을 최소화하기 위해 클라이언트 측 SDK와 내부 Experience Platform 전달 서비스에서는 이벤트가 성공적으로 수집되었다는 확인이 필요합니다.

해당 확인이 수신되지 않으면 클라이언트측 SDK 또는 내부 플랫폼 게재 서비스가 다시 시도를 트리거하고 경험 이벤트가 다시 전송됩니다.

이는 일시적인 오류를 처리할 때 사용하는 모범 사례입니다. 그 부작용은 중복 이벤트 도입 가능성이다.

일시적인 오류를 처리하기 위한 모범 사례를 더 잘 이해하려면 다음에서 이 문서를 참조하십시오. [일시적인 고장 처리](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## 이벤트 복제 시나리오 {#scenarios}

이벤트 중복은 다음과 같은 다양한 시나리오에서 발생할 수 있지만, 이에 국한되지는 않습니다.

* 클라이언트측 SDK와 간의 네트워크 관련 문제 [!DNL Edge Network]. 고객과 Edge Network 간의 연결이 공용 인터넷을 통해 이루어지기 때문에 이러한 문제는 인터넷 서비스 공급자 오류, 모바일 신호 손실 또는 기타 네트워크 오류로 인해 발생할 수 있습니다.
* 내부 Experience Platform 자동 확장 이벤트. 간혹 클라우드 인프라 변동성으로 인해 데이터 균형이 재조정될 수 있습니다.

Adobe Experience Platform 데이터 수집 계층은 &quot;최소 한 번 이상&quot; 처리를 지원하도록 설계되었습니다. 따라서 이벤트 중복은 제한적이고 드문 상황에서 발생할 수 있습니다.

&quot;최소 한 번 이상&quot; 처리에 대한 자세한 내용은 다음 문서에서 확인할 수 있습니다 [메시지 게재 보장](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## 이벤트 중복 제거 옵션 {#deduplication}

중복 이벤트에 민감한 비즈니스 시나리오의 경우, Experience Platform은 아래 설명된 것과 같이 다운스트림 스토리지 시스템에서 여러 이벤트 중복 제거 방법을 사용합니다.

* Real-Time CDP 프로필 저장소는 동일한 이벤트가 발생하는 경우 이벤트를 삭제합니다 `_id` 이(가)에 이미 있습니다. [!DNL Profile Store]. 다음에서 설명서를 참조하십시오. [XDM ExperienceEvent 클래스](../xdm/classes/experienceevent.md) 을 참조하십시오.
* Customer Journey Analytics을 사용하면 지표가 값만 비반복적으로 계산하도록 구성할 수 있습니다. 이 작업을 수행하는 방법에 대해 알아보려면 의 설명서를 참조하십시오. [지표 중복 제거 구성 요소 설정](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=ko-KR).
* Experience Platform 쿼리 서비스는 계산에서 전체 행을 제거하거나 행에 있는 데이터 일부만 중복 정보이므로 특정 필드 집합을 무시해야 하는 경우 데이터 중복 제거를 지원합니다. 관련 설명서 보기 [쿼리 서비스의 데이터 중복 제거](../query-service/key-concepts/deduplication.md) 추가 정보.

>[!NOTE]
>
>위에 제시된 사용 사례 외에 이벤트 중복 문제가 발생하는 경우 Adobe 담당자에게 연락하여 사용 사례에 대한 자세한 정보를 제공하십시오.