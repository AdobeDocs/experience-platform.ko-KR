---
title: ID 서비스 및 실시간 고객 프로필
description: ID 서비스와 실시간 고객 프로필 간의 관계에 대해 알아봅니다
hide: true
hidefromtoc: true
badge: Alpha
source-git-commit: 03e4cd440f8627ad837a31e1c017d0b824cafb04
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# ID 서비스와 실시간 고객 프로필 간의 관계 이해

>[!IMPORTANT]
>
>* ID 그래프 연결 규칙이 현재 Alpha 중입니다. 기능 및 설명서는 변경될 수 있습니다.
>
>* 이 페이지에서는 병합 정책이 ID 그래프를 사용한다고 가정합니다. 실시간 고객 프로필의 병합 정책에 대한 자세한 내용은 [병합 정책 및 id 결합](../../profile/merge-policies/overview.md#identity-stitching).

ID 서비스와 실시간 고객 프로필을 함께 사용할 수 있지만, Adobe Experience Platform의 두 가지 기능은 기본적으로 동일하지 않습니다.

* ID 서비스를 사용하여 개별 고객의 서로 다른 ID를 통합하는 ID 그래프를 생성하고 유지 관리할 수 있습니다.
* Real-Time Customer Profile을 사용하여 서로 다른 프로필 조각을 모으고 병합 프로필을 만들 수 있습니다. 이 프로세스에는 ID 그래프를 사용해야 합니다.

이 문서에서는 ID 서비스와 실시간 고객 프로필 간의 유사성, 차이점 및 관계에 대해 간략히 설명합니다.

## ID 서비스와 실시간 고객 프로필 비교

ID 서비스와 실시간 고객 프로필 간의 주요 차이점은 다음과 같습니다.

| | ID 서비스 | 실시간 고객 프로필 |
| --- | --- |--- |
| **용도** | <ul><li>ID 서비스를 사용하여 ID 그래프를 만들고 관리할 수 있습니다.</li></ul> | 실시간 고객 프로필을 사용하여 다음을 수행할 수 있습니다. <ul><li>고객 프로필에 대한 360도 보기를 만듭니다.</li><li>프로필 보기 및 관리</li><li>세그먼트를 만들어 대상자를 만듭니다.</li></ul> |
| **입력** | <ul><li>ID 서비스를 사용하려면 ID로 표시된 필드가 두 개 이상 있는 레코드 데이터나 시계열 이벤트를 수집해야 합니다. ID로 표시한 필드는 ID 서비스에 수집됩니다.</li></ul> | **프로필을 병합하려면 다음을 제공해야 합니다.**: <ul><li>프로필 조각: 고유한 기본 ID와 주어진 데이터 세트 내의 해당 ID에 대한 해당 레코드 또는 이벤트 데이터를 나타냅니다.</li><li>ID 그래프: 프로필은 주어진 고객 프로필에 대한 ID 그래프를 참조하여 동일한 기본 ID를 가진 모든 프로필 조각을 식별합니다.</li></ul> **세그먼트 자격의 경우 다음을 제공해야 합니다.**: <ul><li>병합 프로필: 병합 프로필은 서로 다른 프로필 조각 및 ID가 하나의 포괄적인 보기로 수집되는 고객에 대한 단일 보기입니다.</li></ul> |
| **프로세스** | <ul><li>두 개 이상의 ID를 수집했으면 Identity Service가 이러한 ID를 함께 연결합니다.</li></ul> | <ul><li>Real-Time Customer Profile은 해당 ID 그래프를 참조하면서 프로필 조각을 병합합니다.</li><li>세분화 기준을 기반으로 세그먼트에 프로필 자격 부여</li></ul> |
| **출력** | <ul><li>그 결과 개인과 관련된 ID 세트인 ID 그래프가 만들어집니다.</li></ul> | <ul><li>그 결과 지정된 고객에 대한 단일하고 포괄적인 보기인 병합된 프로필이 됩니다.</li><li>세그먼트 멤버십이 정의된 프로필</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## 병합된 프로필은 어떻게 만들어집니까?

병합 프로필을 만드는 프로세스를 더 잘 이해하려면 아래 단계를 참조하십시오.

* 먼저 실시간 고객 프로필은 ID 그래프를 참조하고 모든 ID를 검색합니다.
* 그런 다음 프로필은 각 ID와 관련된 모든 프로필 조각을 검색합니다.
* 성공하면 Profile than은 기존의 모든 이벤트와 속성을 병합합니다.
   * 필요한 경우 우선 순위 규칙을 적용하여 사용할 속성 또는 이벤트를 결정합니다

![ID 서비스 및 프로필 병합의 작동 방식을 자세히 설명하는 순서도입니다.](../images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### 필드를 정체성으로 표시하는 것은 무엇을 의미합니까?

필드를 ID로 표시하거나 지정하는 것은 Experience Platform이 특정 필드를 ID 서비스로 수집하는 지침입니다. 이렇게 지정하면 프로필 조각을 실시간 고객 프로필에 병합할 수 있습니다. ID와 연결된 프로필 조각이 없는 경우 ID로 지정하지 마십시오.

#### 기본 및 보조 ID 이해

필드를 ID로 표시하면 기본 또는 보조 ID로 정의할 수 있습니다. 기본 및 보조 ID는 실시간 고객 프로필의 일부입니다.

* 기본 ID(경우에 따라 &quot;기본 키&quot;라고도 함)는 프로필 조각이 저장된 ID입니다.
* 지정된 데이터 행에 ID가 하나만 있는 경우 해당 단일 ID가 기본 ID로 지정됩니다.
* 2개 이상의 ID가 있는 경우 1개는 1차 ID로 지정되고 나머지 ID는 2차 ID로 지정됩니다.

ID 서비스는 ID로 지정된 필드만 수집합니다. ID 서비스는 ID가 기본 ID인지 보조 ID인지에 대한 정보를 저장하지 않습니다.

## 다음 단계

ID 그래프 연결 규칙에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [ID 그래프 연결 규칙 개요](./overview.md)
* [ID 그래프 연결 규칙을 구성하기 위한 예제 시나리오](./example-scenarios.md)
* [ID 연결 논리](./identity-linking-logic.md)