---
keywords: Experience Platform;홈;인기 항목;ID;ID;XDM 그래프;ID 서비스;ID 서비스
solution: Experience Platform
title: Identity Service 개요
description: Adobe Experience Platform Identity Service를 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객과 고객의 행동을 더 잘 볼 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 0%

---

# [!DNL Identity Service] 개요

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 이러한 문제는 고객 데이터가 서로 다른 시스템 간에 분산되어 각 개별 고객이 여러 개의 &quot;ID&quot;를 가지는 것처럼 보이는 경우 더욱 어려워집니다.

Adobe Experience Platform Identity Service는 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 포괄적인 보기를 제공하여 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

포함 [!DNL Identity Service], 다음 작업을 수행할 수 있습니다.

- 고객이 각 상호 작용을 통해 일관되고 개인화된 관련 경험을 받도록 합니다.
- 서로 다른 소스의 여러 ID를 결합하고 고객에 대한 포괄적인 보기를 만들 수 있습니다.
- ID 그래프를 활용하여 다양한 ID 네임스페이스를 매핑함으로써 고객이 다양한 채널에서 브랜드와 상호 작용하는 방법을 시각적으로 나타낼 수 있습니다.

## 시작하기

의 세부 사항으로 이동하기 전에 [!DNL Identity Service]주요 용어에 대한 간략한 요약은 다음과 같습니다.

| 용어 | 정의 |
| --- | --- |
| 신원 | ID는 엔티티에 고유한 데이터이며, 일반적으로 개인입니다. 로그인 ID, ECID 또는 충성도 ID와 같은 ID를 &quot;알려진 ID&quot;라고도 합니다. |
| ECID | Experience Cloud ID(ECID)는 Experience Platform 및 Adobe Experience Cloud 애플리케이션에서 사용되는 공유 ID 네임스페이스입니다. ECID는 고객 ID의 기반을 제공하며 장치의 기본 ID와 ID 그래프의 기본 노드로 사용됩니다. 다음을 참조하십시오. [ECID 개요](./ecid.md) 추가 정보. |
| ID 네임스페이스 | ID 네임스페이스는 ID의 컨텍스트 또는 유형을 구분하는 역할을 합니다. 예를 들어 ID는 &quot;name&quot;을 구별합니다<span>@email.com&quot; 을 이메일 주소로 사용하거나 &quot;443522&quot;를 숫자 CRM ID로 사용합니다. ID 네임스페이스는 개별 ID를 조회하고 ID 값에 대한 컨텍스트를 제공하는 데 사용됩니다. 이를 통해 다음 두 가지를 확인할 수 있습니다 [!DNL Profile] 다른 기본 ID를 포함하지만 에 대해 동일한 값을 공유하는 조각 `email` id 네임스페이스, 는 실제로 동일한 개인입니다. 다음을 참조하십시오. [id 네임스페이스 개요](./namespaces.md) 추가 정보. |
| ID 그래프 | ID 그래프는 서로 다른 ID 간의 관계에 대한 맵으로서, 서로 다른 ID가 어떤 고객 ID와 어떻게 결합되는지 시각화하고 더 잘 이해할 수 있습니다. 다음 튜토리얼 참조: [id 그래프 뷰어 사용](./ui/identity-graph-viewer.md) 추가 정보. |
| PII(개인 식별 정보) | PII는 이메일 주소나 전화번호와 같이 고객을 직접 식별할 수 있는 정보입니다. PII 값은 종종 일치시키는 데 사용됩니다. 서로 다른 시스템에 있는 고객의 여러 id. |
| 알 수 없거나 익명의 ID | 알 수 없음 또는 익명 ID는 장치를 사용하는 실제 사용자를 식별하지 않고 장치를 격리하는 표시기입니다. 알 수 없는 익명 ID에는 방문자의 IP 주소 및 쿠키 ID와 같은 정보가 포함됩니다. 알 수 없는 익명 ID는 동작 데이터를 제공할 수 있지만 고객이 PII를 제공할 때까지는 제한됩니다. |

## [!DNL Identity Service]이란 ?

고객은 매일 귀하의 비즈니스와 상호 작용하고 귀하의 브랜드와 지속적으로 성장하는 관계를 수립합니다. 일반적인 고객은 전자 상거래, 로열티 및 헬프 데스크 시스템과 같이 조직의 데이터 인프라 내에 있는 다양한 시스템에서 활동을 수행할 수 있습니다. 동일한 고객이 여러 장치에서도 익명으로 참여할 수 있습니다. [!DNL Identity Service] 을 사용하면 개별 시스템에 분산될 수 있는 관련 데이터를 종합하여 고객에 대한 전체 그림을 그릴 수 있습니다.

브랜드와 소비자의 관계를 보여주는 일상적인 예를 생각해 보십시오.

- Mary는 과거에 몇 가지 주문을 완료한 전자 상거래 사이트의 계정을 보유하고 있습니다. 그녀는 보통 매번 로그인하는 쇼핑에서 개인용 노트북을 사용한다. 그러나 방문 중 한 번 그녀는 자신의 태블릿을 사용하여 샌들을 쇼핑하지만 주문을 하지 않고 로그인하지 않습니다.
- 이때 Mary의 활동은 두 개의 프로필로 표시됩니다.
   - 그녀의 전자 상거래 로그인
   - 디바이스 ID로 식별되는 태블릿 디바이스
- Mary는 나중에 태블릿 세션을 다시 시작하고 뉴스레터를 구독하는 동안 이메일 주소를 제공합니다. 그렇게 하면 스트리밍 수집은 프로필 내의 레코드 데이터로 새 ID를 추가합니다. 그 결과, [!DNL Identity Service] 이제 Mary의 태블릿 장치 활동과 전자 상거래 계정 기록과 관련이 있습니다.
- 다음에 태블릿을 클릭하면 타겟팅된 콘텐츠가 알려지지 않은 쇼핑객이 사용하는 태블릿이 아닌 Mary의 전체 프로필과 내역을 반영할 수 있습니다.

![플랫폼에서 ID 결합](./images/identity-service-stitching.png)

기본적으로, [!DNL Identity Service] 을 사용하면 개별 시스템에 흩어져 있을 수 있는 관련 데이터를 종합하여 고객에 대한 전체 그림을 그릴 수 있습니다. 다음과 같은 ID 관계 [!DNL Identity Service] 는 실시간 고객 프로필에서 정의 및 유지 관리를 활용하여 고객과 브랜드와의 상호 작용을 전체적으로 파악할 수 있도록 합니다. 자세한 내용은 [실시간 고객 프로필 개요](../profile/home.md).

### 사용 사례

예 [!DNL Identity Service] 구현에는 다음이 포함됩니다.

- 통신 회사는 &quot;전화 번호&quot; 값에 의존할 수 있으며, 여기서 전화 번호는 오프라인 및 온라인 데이터 세트에서 관심 있는 동일한 개인을 가리킵니다.
- 익명 방문자의 비율이 높아 소매 업체는 오프라인 데이터 세트의 &quot;이메일 주소&quot; 및 온라인 데이터 세트의 ECID를 사용할 수 있습니다.
- 은행은 지점 거래와 같은 오프라인 데이터 세트의 &quot;계좌 번호&quot;를 선호할 수 있습니다. 대부분의 방문자는 방문 중에 인증되므로 온라인 데이터 세트의 &quot;로그인 ID&quot;에 따라 달라질 수 있습니다.
- 또한 고객은 GUID 또는 기타 범세계적으로 고유한 식별자와 같은 고유한 고유 ID를 가질 수 있습니다.

## ID 네임스페이스 {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="ID 네임스페이스"
>abstract="ID 네임스페이스는 ID의 컨텍스트 또는 유형을 구분하는 역할을 합니다. 예를 들어 ID는 &quot;name&quot;을 구별합니다<span>@email.com&quot; 을 이메일 주소로 사용하거나 &quot;443522&quot;를 숫자 CRM ID로 사용합니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="ID 값"
>abstract="ID 값은 고유한 개인, 조직 또는 에셋을 나타내는 식별자입니다. 값이 나타내는 ID 컨텍스트 또는 유형은 해당 ID 네임스페이스에 의해 정의됩니다. 프로필 조각 간에 레코드 데이터를 일치시킬 때 네임스페이스와 ID 값이 일치해야 함프로필 조각 간에 레코드 데이터를 일치시킬 때 네임스페이스와 ID 값이 일치해야 합니다."
>text="Learn more in documentation"

&quot;ID가 무엇입니까?&quot;라고 묻는 경우 더 이상의 맥락이 없다면, 그들이 유용한 답을 제공하기는 어려울 것이다. 동일한 논리에 의해 ID 값을 나타내는 문자열 값은 시스템 생성 ID이든 이메일 주소이든 간에 문자열 값 컨텍스트(ID 네임스페이스)를 제공하는 한정자와 함께 제공되는 경우에만 완료됩니다.

고객은 온라인 및 오프라인 채널의 조합을 통해 브랜드와 상호 작용할 수 있으므로 이러한 단편화된 상호 작용을 단일 고객 정체성으로 조정하는 방법에 대한 문제가 발생합니다.

여러 디바이스와 채널에서 고객을 이해하려면 각 채널에서 고객을 인식해야 합니다. 플랫폼은 ID 네임스페이스를 사용하여 이를 수행합니다. ID 네임스페이스는 고객 ID에 추가 컨텍스트를 제공하는 데 사용되는 이메일 또는 전화와 같은 식별자입니다. ID 네임스페이스는 개별 ID를 조회하거나 연결하고 ID 값에 대한 컨텍스트를 제공하는 데 사용됩니다. 다음을 참조하십시오. [id 네임스페이스 개요](./namespaces.md) 추가 정보.

## ID 그래프

ID 그래프는 서로 다른 ID 네임스페이스 간의 관계 맵으로, 고객 ID가 어떻게 결합되어 있는지 시각화하고 더 잘 이해할 수 있습니다. 다음 튜토리얼 참조: [id 그래프 뷰어 사용](./ui/identity-graph-viewer.md) 추가 정보.

다음 비디오는 ID 및 ID 그래프에 대한 이해를 돕기 위한 것입니다.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## ID 데이터를에 제공하는 중 [!DNL Identity Service]

이 섹션에서는 다음에 의해 사용되기 전에 Adobe Experience Platform에 제공된 데이터가 처리되는 방식을 다룹니다. [!DNL Identity Service] 각 고객에 대한 id 그래프를 작성하려면

### ID 필드 결정

엔터프라이즈 데이터 수집 전략에 따라 ID로 레이블을 지정하는 데이터 필드에 따라 ID 맵에 포함되는 데이터가 결정됩니다. Adobe Experience Platform의 이점을 최대한 활용하고 가능한 가장 포괄적인 고객 ID를 얻으려면 온라인과 오프라인 데이터를 모두 업로드해야 합니다.

- 온라인 데이터는 사용자 이름 및 이메일 주소와 같이 온라인 상태 및 동작을 설명하는 데이터입니다.

- 오프라인 데이터는 CRM 시스템의 ID와 같이, 온라인 존재와 직접 관련이 없는 데이터를 의미한다. 이러한 유형의 데이터는 ID를 보다 강력하게 만들고 개별 시스템 전반에서 데이터 결합을 지원합니다.

### 추가 ID 네임스페이스 만들기

Experience Platform은 다양한 표준 네임스페이스를 제공하지만 ID를 적절하게 분류하려면 추가 네임스페이스를 만들어야 할 수 있습니다. 자세한 내용은 다음 섹션 을 참조하십시오 [조직의 네임스페이스 보기 및 만들기](./namespaces.md) id 네임스페이스 개요에서 참조하십시오.

>[!NOTE]
>
>ID 네임스페이스는 ID의 한정자입니다. 따라서 네임스페이스가 만들어지면 삭제할 수 없습니다.

### 에 ID 데이터 포함 [!DNL Experience Data Model] (XDM)

표준화된 프레임워크로서 [!DNL Platform] 고객 데이터 구성, [!DNL Experience Data Model] (XDM) 을 사용하면 와 상호 작용하는 Experience Platform 및 기타 서비스에서 데이터를 공유하고 이해할 수 있습니다 [!DNL Platform]. 자세한 내용은 [XDM 시스템 개요](../xdm/home.md).

레코드와 시계열 스키마 모두 ID 데이터를 포함하는 수단을 제공합니다. 데이터가 수집될 때 공통 ID 데이터를 공유하는 것으로 확인되면 ID 그래프는 서로 다른 네임스페이스의 데이터 조각 간에 새로운 관계를 생성합니다.

### XDM 필드를 ID로 표시

유형의 모든 필드 `string` 레코드 또는 시계열 XDM 클래스를 구현하는 스키마에서는 ID 필드로 레이블 지정할 수 있습니다. 따라서 해당 필드에 수집된 모든 데이터는 ID 데이터로 간주됩니다.

>[!NOTE]
>
>배열 및 맵 유형 필드는 지원되지 않으며 ID 필드로 표시하고 레이블 지정할 수 없습니다.

ID 필드를 사용하면 공통 PII 데이터를 공유하는 경우 ID를 연결할 수도 있습니다.
예를 들어 전화번호 필드에 ID 필드로 레이블을 지정하면 [!DNL Identity Service] 는 동일한 전화 번호를 사용하고 있는 것으로 확인된 다른 개인과의 관계를 자동으로 그래프로 표시합니다.

>[!NOTE]
>
>결과 ID의 네임스페이스는 필드에 레이블이 지정될 때 제공됩니다.

### 다음에 대한 데이터 세트 구성 [!DNL Identity Service]

스트리밍 수집 프로세스 중에 [!DNL Identity Service ]레코드 및 시계열 데이터에서 자동으로 id 데이터를 추출합니다. 그러나 데이터를 수집하려면 먼저 다음에 대해 활성화해야 합니다. [!DNL Identity Service]. 다음 튜토리얼 참조:  [api를 사용하여 실시간 고객 프로필 및 ID 서비스에 대한 데이터 세트 구성](../profile/tutorials/dataset-configuration.md) 추가 정보.

### 데이터 수집 대상 [!DNL Identity Service]

[!DNL Identity Service] 은 다음 중 한 방법으로 Experience Platform에 전송된 XDM 호환 데이터를 사용합니다. [일괄 처리 수집](../ingestion/batch-ingestion/overview.md) 또는 [스트리밍 수집](../ingestion/streaming-ingestion/overview.md).

다음 비디오는 ID 서비스에 대한 이해를 돕기 위한 것입니다. 이 비디오는 데이터 필드에 ID로 레이블을 지정하고 ID 데이터를 수집한 다음 데이터가 Adobe Experience Platform ID 서비스 개인 그래프에 적용되었는지 확인하는 방법을 보여 줍니다.

>[!WARNING]
>
>다음 [!DNL Platform] 다음 비디오에 표시된 UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 설명서 를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 데이터 거버넌스

Adobe Experience Platform은 개인 정보를 고려하여 구축되었으며 고객 PII 데이터를 보호하기 위한 데이터 거버넌스 프레임워크를 포함합니다. &quot;이메일&quot; 또는 &quot;전화&quot; 네임스페이스 아래의 ID 데이터는 기본적으로 암호화되지만 중요한 데이터가 지속되기 전에 암호화되도록 하기 위해 수집된 데이터 또는 도착한 데이터에 데이터 사용 레이블을 적용할 수 있습니다 [!DNL Platform]. 자세한 내용은 다음을 참조하십시오. [데이터 거버넌스 개요](../data-governance/home.md).

## 다음 단계

이제 의 주요 개념을 이해하셨군요. [!DNL Identity Service] Experience Platform 내에서 역할과 함께 다음을 사용하여 id 그래프 작업 방법을 배울 수 있습니다. [[!DNL Identity Service API]](./api/getting-started.md).
