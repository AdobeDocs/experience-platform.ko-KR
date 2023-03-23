---
keywords: Experience Platform;홈;인기 항목;ID;ID;XDM 그래프;ID 서비스;ID 서비스
solution: Experience Platform
title: ID 서비스 개요
description: Adobe Experience Platform Identity Service를 사용하면 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 해당 행동을 더 잘 볼 수 있으므로 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있습니다.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 7%

---

# [!DNL Identity Service] 개요

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 서로 다른 시스템에서 고객 데이터가 단편화된 경우 각 개별 고객이 여러 &quot;ID&quot;를 보유한 것처럼 보일 때 더욱 어렵습니다.

Adobe Experience Platform Identity 서비스는 장치 및 시스템 전반에서 ID를 결합하여 고객 및 고객 행동에 대한 포괄적인 보기를 제공하여 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있도록 합니다.

사용 [!DNL Identity Service]를 채울 수 있습니다.

- 고객이 각 상호 작용을 통해 일관되고 개인화된 적절한 경험을 받을 수 있도록 합니다.
- 서로 다른 소스에서 여러 ID를 결합하여 고객을 종합적으로 파악합니다.
- ID 그래프를 활용하여 다양한 ID 네임스페이스를 매핑하면 고객이 다양한 채널에서 브랜드와 상호 작용하는 방법을 시각적으로 확인할 수 있습니다.

## 시작하기

세부 사항으로 들어가기 전에 [!DNL Identity Service], 주요 용어에 대한 간단한 요약은 다음과 같습니다.

| 용어 | 정의 |
| --- | --- |
| 신원 | ID는 엔티티에 고유한 데이터(일반적으로 개별 개인)입니다. 로그인 ID, ECID 또는 충성도 ID와 같은 ID를 &quot;알려진 ID&quot;라고도 합니다. |
| ECID | ECID(Experience Cloud ID)는 Experience Platform 및 Adobe Experience Cloud 애플리케이션에서 사용되는 공유 ID 네임스페이스입니다. ECID는 고객 ID의 기반을 제공하며 장치의 기본 ID로 사용되고 ID 그래프의 기본 노드로 사용됩니다. 자세한 내용은 [ECID 개요](./ecid.md) 추가 정보. |
| ID 네임스페이스 | ID 네임스페이스는 ID의 컨텍스트 또는 유형을 구분하는 역할을 합니다. 예를 들어 ID는 “name<span>@email.com”을 이메일 주소로 구분하거나 “443522”를 숫자 CRM ID로 구분합니다. ID 네임스페이스는 개별 ID를 조회하고 ID 값에 대한 컨텍스트를 제공하는 데 사용됩니다. 이를 통해 다음 두 가지 사항을 확인할 수 있습니다 [!DNL Profile] 다른 기본 ID를 포함하지만 동일한 값을 공유하는 조각. `email` id 네임스페이스는 사실상 동일한 개인입니다. 자세한 내용은 [id 네임스페이스 개요](./namespaces.md) 추가 정보. |
| ID 그래프 | ID 그래프는 서로 다른 ID 간의 관계 맵으로, 함께 결합되는 고객 ID와 방법을 시각화하고 더 잘 이해할 수 있도록 해줍니다. 다음에서 자습서를 참조하십시오. [id 그래프 뷰어 사용](./ui/identity-graph-viewer.md) 추가 정보. |
| 개인 식별 정보(PII) | PII는 이메일 주소 또는 전화 번호와 같이 고객을 직접 식별할 수 있는 정보입니다. PII 값은 종종 일치하지 않습니다. 다양한 시스템에서 고객의 여러 ID입니다. |
| 알 수 없음 또는 익명 ID | 알 수 없음 또는 익명 ID는 장치를 사용하여 실제 사람을 식별하지 않고 장치를 분리하는 표시입니다. 알 수 없고 익명의 ID에는 방문자의 IP 주소 및 쿠키 ID와 같은 정보가 포함됩니다. 알 수 없고 익명의 ID가 행동 데이터를 제공할 수 있지만 고객이 PII를 제공할 때까지 제한됩니다. |

## [!DNL Identity Service]이란 ?

매일 고객은 비즈니스 와 상호 작용하고 브랜드와의 지속적인 관계를 구축합니다. 일반적인 고객은 전자 상거래, 충성도, 헬프데스크 시스템과 같이 조직의 데이터 인프라 내에 있는 시스템 수에 관계없이 능동적으로 작업할 수 있습니다. 동일한 고객은 원하는 개수의 장치에서도 익명으로 참여할 수 있습니다. [!DNL Identity Service] 서로 다른 시스템에 분산되어 있을 수 있는 관련 데이터를 집계하여 고객의 전체 상황을 파악할 수 있습니다.

브랜드와의 소비자 관계에 대한 일상적인 예를 생각해 보십시오.

- Mary는 당신의 전자 상거래 사이트에 과거에 몇 개의 주문을 완료한 계정이 있다. 그녀는 보통 개인 노트북을 이용해 쇼핑을 하며 매번 로그인한다. 그러나 방문 중에 태블릿을 사용하여 샌들을 구입하지만 주문을 하지 않고 로그인하지 않는다.
- 이때 Mary의 활동은 두 개의 개별 프로필로 표시됩니다.
   - 그녀의 전자 상거래 로그인
   - 장치 ID로 식별되는 그녀의 태블릿 장치
- Mary는 나중에 태블릿 세션을 다시 시작하고 뉴스레터를 구독하는 동안 이메일 주소를 제공합니다. 스트리밍 수집은 새로운 ID를 프로필 내에 레코드 데이터로 추가합니다. 결과적으로 [!DNL Identity Service] 이제 Mary의 태블릿 장치 활동과 전자 상거래 계정 기록이 있습니다.
- 다음 번 태블릿에서 클릭하면 대상 콘텐츠가 알 수 없는 쇼핑객이 사용하는 태블릿이 아니라 Mary의 전체 프로필 및 내역을 반영할 수 있습니다.

![Platform에서 ID 결합](./images/identity-service-stitching.png)

기본적으로 [!DNL Identity Service] 서로 다른 시스템에 분산되어 있을 수 있는 관련 데이터를 집계하여 고객의 전체 상황을 파악할 수 있습니다. ID는 [!DNL Identity Service] 실시간 고객 프로필에서 정의 및 유지 관리를 활용하여 고객과 브랜드와의 상호 작용을 완벽하게 파악할 수 있습니다. 자세한 내용은 [실시간 고객 프로필 개요](../profile/home.md).

### 사용 사례

예 [!DNL Identity Service] 구현에는 다음이 포함됩니다.

- 한 통신 회사는 &quot;전화 번호&quot; 값에 의존할 수 있는데, 여기서 전화 번호는 오프라인 데이터 세트와 온라인 데이터 세트 모두에서 동일한 개인 정보를 의미합니다.
- 소매 업체는 익명의 방문자가 많기 때문에 오프라인 데이터 세트에서 &quot;이메일 주소&quot;를 사용하고 온라인 데이터 세트에서 ECID를 사용할 수 있습니다.
- 은행은 분기 트랜잭션과 같은 오프라인 데이터 세트에서 &quot;계좌 번호&quot;를 선호할 수 있습니다. 대부분의 방문자는 방문 중에 인증되므로 온라인 데이터 세트의 &quot;로그인 ID&quot;에 따라 달라질 수 있습니다.
- 또한 고객은 GUID 또는 다른 Universally Unique Identifier와 같은 고유한 고유 ID를 가질 수 있습니다.

## ID 네임스페이스 {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="ID 네임스페이스"
>abstract="ID 네임스페이스는 ID의 컨텍스트 또는 유형을 구분하는 역할을 합니다. 예를 들어 ID는 “name<span>@email.com”을 이메일 주소로 구분하거나 “443522”를 숫자 CRM ID로 구분합니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="ID 값"
>abstract="ID 값은 고유 개인, 조직 또는 에셋을 나타내는 식별자입니다. 값이 표시하는 ID의 컨텍스트 또는 유형은 해당 ID 네임스페이스에 의해 정의됩니다. 프로필 조각에서 레코드 데이터를 일치시킬 때 네임스페이스와 ID 값은 일치해야 합니다."
>text="Learn more in documentation"

&quot;신분증이 무엇입니까?&quot;라고 물으셨다면 더 이상의 문맥이 없다면, 그들이 유용한 답을 제공하기가 어려울 것이다. 동일한 논리에서는 시스템 생성 ID이든 이메일 주소이든 ID 값을 나타내는 문자열 값은 문자열 값 컨텍스트를 제공하는 한정자와 함께 제공된 경우에만 완료됩니다. id 네임스페이스입니다.

고객은 온라인 및 오프라인 채널의 조합을 통해 브랜드와 상호 작용할 수 있으므로 단편화된 상호 작용을 단일 고객 ID로 조정하는 방법에 대한 문제가 발생할 수 있습니다.

여러 디바이스와 채널에서 고객을 이해하는 것은 각 채널에서 고객을 인식함으로써 시작됩니다. Platform은 ID 네임스페이스를 사용하여 이러한 작업을 수행합니다. ID 네임스페이스는 고객 ID에 추가 컨텍스트를 제공하는 데 사용되는 이메일 또는 전화와 같은 식별자입니다. ID 네임스페이스는 개별 ID를 조회하거나 연결하고 ID 값에 대한 컨텍스트를 제공하는 데 사용됩니다. 자세한 내용은 [id 네임스페이스 개요](./namespaces.md) 추가 정보.

## ID 그래프

ID 그래프는 서로 다른 ID 네임스페이스 간의 관계 맵으로, 어떤 고객 ID가 함께 결합되는지 및 그 방법을 시각화하고 더 잘 이해할 수 있도록 해줍니다. 다음에서 자습서를 참조하십시오. [id 그래프 뷰어 사용](./ui/identity-graph-viewer.md) 추가 정보.

다음 비디오는 ID 및 ID 그래프에 대한 이해를 지원하기 위한 것입니다.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## ID 데이터를에 제공 [!DNL Identity Service]

이 섹션에서는 Adobe Experience Platform에 제공된 데이터가 [!DNL Identity Service] 각 고객에 대한 id 그래프를 작성하기 위해.

### ID 필드 결정

엔터프라이즈 데이터 수집 전략에 따라 ID로 레이블을 지정하는 데이터 필드는 ID 맵에 포함되는 데이터를 결정합니다. Adobe Experience Platform의 최대 이점과 가장 포괄적인 고객 ID를 얻으려면 온라인 및 오프라인 데이터를 모두 업로드해야 합니다.

- 온라인 데이터는 사용자 이름 및 이메일 주소와 같은 온라인 유무 및 동작을 설명하는 데이터입니다.

- 오프라인 데이터는 CRM 시스템의 ID와 같이 온라인 상태와 직접 관련이 없는 데이터를 참조합니다. 이러한 유형의 데이터는 ID를 더욱 강력하게 만들고 서로 다른 시스템에서 데이터를 통합하도록 지원합니다.

### 추가 ID 네임스페이스 만들기

Experience Platform은 다양한 표준 네임스페이스를 제공하지만 ID를 올바로 분류하기 위해 추가 네임스페이스를 만들어야 할 수 있습니다. 자세한 내용은 [조직의 네임스페이스 보기 및 만들기](./namespaces.md) 를 참조하십시오.

>[!NOTE]
>
>ID 네임스페이스는 ID의 한정자입니다. 따라서 네임스페이스를 만들면 삭제할 수 없습니다.

### 에 ID 데이터 포함 [!DNL Experience Data Model] (XDM)

표준화된 프레임워크로서 [!DNL Platform] 고객 데이터를 정리하고 [!DNL Experience Data Model] (XDM) 을 사용하면 Experience Platform 및 상호 작용하는 기타 서비스 간에 데이터를 공유하고 이해할 수 있습니다 [!DNL Platform]. 자세한 내용은 [XDM 시스템 개요](../xdm/home.md).

레코드와 시계열 스키마는 ID 데이터를 포함하는 방법을 제공합니다. 데이터를 수집하면 ID 그래프가 다른 네임스페이스의 데이터 조각 간에 공통 ID 데이터를 공유하는 것으로 확인되면 새로운 관계를 만듭니다.

### XDM 필드를 ID로 표시

유형의 모든 필드 `string` 레코드 또는 시계열 XDM 클래스를 구현하는 스키마에서는 ID 필드로 레이블이 지정될 수 있습니다. 따라서 해당 필드에 수집된 모든 데이터는 ID 데이터로 간주됩니다.

>[!NOTE]
>
>배열 및 맵 유형 필드는 지원되지 않으며 ID 필드로 표시 및 레이블이 지정할 수 없습니다.

또한 ID 필드가 일반적인 PII 데이터를 공유하는 경우 ID를 연결할 수도 있습니다.
예를 들어, 전화 번호 필드에 ID 필드로 레이블을 지정하면, [!DNL Identity Service] 동일한 전화 번호를 사용하는 다른 사용자와 관계를 자동으로 그래프로 표시합니다.

>[!NOTE]
>
>결과 ID의 네임스페이스는 필드가 레이블이 지정된 시점에 제공됩니다.

### 데이터 집합 구성 [!DNL Identity Service]

스트리밍 수집 프로세스 중에 [!DNL Identity Service ]레코드 및 시계열 데이터에서 id 데이터를 자동으로 추출합니다. 그러나 데이터를 수집하려면 먼저 데이터를 활성화해야 합니다 [!DNL Identity Service]. 다음에서 자습서를 참조하십시오.  [API를 사용하여 실시간 고객 프로필 및 ID 서비스를 위한 데이터 세트 구성](../profile/tutorials/dataset-configuration.md) 추가 정보.

### 데이터를에 수집 [!DNL Identity Service]

[!DNL Identity Service] 는 다음 방법 중 하나로 Experience Platform에 전송되는 XDM 준수 데이터를 사용합니다 [배치 수집](../ingestion/batch-ingestion/overview.md) 또는 [스트리밍 수집](../ingestion/streaming-ingestion/overview.md).

다음 비디오는 ID 서비스에 대한 이해를 지원하기 위한 것입니다. 이 비디오에서는 데이터 필드에 ID로 레이블을 지정하고 ID 데이터를 수집한 다음 데이터가 Adobe Experience Platform Identity 서비스 개인 그래프로 작성되었는지 확인하는 방법을 보여줍니다.

>[!WARNING]
>
>다음 [!DNL Platform] 다음 비디오에 표시된 UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 데이터 거버넌스

Adobe Experience Platform은 개인 정보를 고려하여 구축되었으며 고객 PII 데이터를 보호하기 위한 데이터 거버넌스 프레임워크가 포함되어 있습니다. &quot;email&quot; 또는 &quot;phone&quot; 네임스페이스 아래의 ID 데이터는 기본적으로 암호화되지만, 중요한 데이터가 유지되기 전에 암호화되어 있는지 확인하기 위해 수집되거나 도착하면 데이터 사용 레이블을 데이터에 적용할 수 있습니다 [!DNL Platform]. 자세한 내용은 [데이터 거버넌스 개요](../data-governance/home.md).

## 다음 단계

이제 Adobe Analytics Mobile Apps 또는 Analytics Premium의 [!DNL Identity Service] Experience Platform 내에서 해당 역할을 사용하여 id 그래프를 사용하는 방법을 배울 수 있습니다 [[!DNL Identity Service API]](./api/getting-started.md).
