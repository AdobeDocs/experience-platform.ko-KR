---
solution: Experience Platform
title: Edge 네트워크와 허브 비교
description: Adobe Experience Platform에서 사용할 수 있는 다양한 처리 경로에 대해 알아봅니다.
exl-id: 3e9c63d2-c798-44b4-870d-bf1551f29690
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 3%

---

# Edge 네트워크와 허브 비교

Adobe Experience Platform은 고객 경험을 주도하는 완벽한 솔루션을 구축하고 관리하기 위해 시장에서 가장 강력하고 유연하며 개방적인 시스템입니다. Experience Platform을 사용하여 모든 시스템의 고객 데이터와 콘텐츠를 중앙 집중화 및 표준화하고 데이터 과학 및 시스템 학습을 적용하여 풍부한 개인별 경험의 디자인과 전달을 획기적으로 향상시킬 수 있습니다. 따라서 Experience Platform에는 데이터를 처리하는 여러 가지 방법이 있으므로 데이터를 가능한 한 가장 적합한 방법으로 평가할 수 있습니다.

## 서버 유형

Experience Platform에서 데이터는 일괄 처리 및 스트리밍 워크플로우를 위한 Adobe Experience Platform 허브와 실시간 경험을 위한 Edge Network의 두 가지 경로로 처리될 수 있습니다.

### Adobe Experience Platform 허브

허브는 중앙에 위치하며 Adobe Experience Platform에서 수집된 모든 내역 데이터 및 풍부한 프로필 컨텍스트를 포함하는 기본 데이터 센터입니다. 이를 통해 보다 강력하고 완전한 데이터를 다운스트림 서비스로 보내고 받을 수 있습니다. 따라서 데이터의 **전체**&#x200B;가 더 중요한 시나리오에서는 허브를 사용해야 합니다.

허브에서 사용할 수 있는 서비스에는 다음이 포함됩니다.

- 배치 세분화
- 스트리밍 세분화
- 프로필
- 대상
- ID 그래프
- Data Distiller - 쿼리 서비스
- Source 커넥터

### Experience Platform Edge Network

Edge Network은 물리적으로 다른 지리적 위치에 더 가깝게 위치한 서버입니다. 이러한 데이터 센터는 SDK 확장 및 Edge Network API를 통해 수집된 모든 데이터를 처리합니다. Edge Network에 있는 유일한 데이터는 개인화에 필요한 대상 멤버십, 프로필 ID 및 속성입니다.

Edge Network을 사용하면 최종 사용자와 가까운 위치에 있으므로 고객에게 데이터를 보다 빠르게 보내고 받을 수 있습니다. 또한 Edge Network을 사용하여 이벤트 전달 요청 및 태그 관리 요청을 처리할 수 있습니다. 하지만 Edge Network은 **동작** 데이터만 처리합니다. 따라서 Edge Network은 데이터의 **속도**&#x200B;가 더 중요한 시나리오에서 사용해야 합니다.

Edge Network에서 사용할 수 있는 서비스는 다음과 같습니다.

- 에지 세분화
- Edge 프로필
- Edge 대상
- 데이터 수집
- SDK 확장

## 위치

다음 섹션에는 Hub와 Edge Network의 위치가 나열됩니다.

![허브 서버와 Edge Network 서버의 다른 위치를 나열하는 다이어그램입니다.](./images/servers/platform-server-locations.png)

**허브**

- VA7(버지니아, 미국)
- NLD2(네덜란드)
- AUS5(오스트레일리아)
- CAN2(캐나다)
- GBR9(영국)
- IND1(인도)

**Edge Network**

- OR2(오레곤, 미국)
- VA6(버지니아, 미국)
- IRL1(아일랜드)
- IND1(인도)
- SGP3(싱가포르)
- AUS3(오스트레일리아)
- JPN3(일본)

사용 가능한 서버 위치에 대한 자세한 내용은 [멀티 클라우드 개요](./multi-cloud.md#available-cloud-regions)를 참조하십시오.

## 다음 단계

이 개요를 읽고 나면 이제 Adobe Experience Platform 허브와 Adobe Experience Platform Edge Network의 처리 데이터 간의 차이점을 이해할 수 있습니다.

## 부록

다음 섹션에서는 Adobe Experience Platform에서 데이터를 처리하는 방법에 대한 보충 정보를 나열합니다.

### 자주 묻는 질문

다음 섹션에서는 허브 및 Edge Network에 대해 자주 묻는 질문들을 나열합니다.

#### 허브에 가장 적합한 시나리오는 무엇입니까?

허브는 데이터의 **철저함**&#x200B;이 더 중요한 시나리오에서 가장 적합합니다. 예를 들어 장바구니를 포기한 모든 고객을 타겟팅하는 마케팅 캠페인을 만들려고 한다고 가정해 보겠습니다. 이 사용 사례에서는 배치 세분화를 사용하여 포기한 장바구니 사용자와 일치하는 대상을 만들고 배치 대상으로 내보낼 수 있습니다.

#### Edge Network에 가장 적합한 시나리오는 무엇입니까?

Edge Network은 데이터의 **속도**&#x200B;가 더 중요한 시나리오에 가장 적합합니다. 예를 들어 장바구니에 제품을 넣어 사이트를 탐색하는 고객을 타겟팅하기 위해 제한된 플래시 세일을 만들어야 한다고 가정해 보겠습니다. 이 사용 사례에서는 엣지 세그멘테이션을 사용하여 바로 타겟팅하고 &quot;Flash Sale&quot;이 포함된 장바구니에 제품이 있는 사용자에게 개인화된 알림을 보낼 수 있습니다.

#### 허브에서 Edge Network으로 이동하는 데이터는 무엇입니까?

Edge에서 실시간 경험을 전달하는 데 필요한 데이터만 허브에서 Edge Network으로 로드됩니다. 이 데이터는 일관성을 유지하기 위해 허브에서 Edge Network으로 자동으로 전송되며 최대 14일 동안만 유지됩니다. 그러나 이는 데이터가 허브의 데이터와 완벽하게 동기화된 상태로 유지됨을 의미하므로 **그렇지**&#x200B;합니다. 그 결과 허브와 Edge Network 간 사용 가능한 데이터에 차이가 발생할 수 있습니다.
