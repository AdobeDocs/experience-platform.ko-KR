---
keywords: Experience Platform;home;popular topics;identity;Identity;XDM graphs;identity service;Identity service
solution: Experience Platform
title: Adobe Experience Platform ID 서비스
topic: overview
description: Adobe Experience Platform ID 서비스를 사용하면 다양한 디바이스와 시스템에 ID를 연결함으로써 고객 행동과 고객의 행동을 보다 정확하게 파악할 수 있으므로 효과적이고 개인화된 경험을 실시간으로 전달할 수 있습니다.
translation-type: tm+mt
source-git-commit: af7eab0599b17be55d5a4c129f7ebaeba91333bc
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 0%

---


# [!DNL Identity Service]개요

고객의 기대에 부응하는 디지털 경험을 전달하려면 고객을 완벽하게 이해해야 합니다. 고객 데이터가 서로 다른 시스템에서 분열되어 각각의 개별 고객이 여러 개의 &quot;ID&quot;를 갖는 것처럼 보일 경우 이러한 문제는 더욱 복잡해집니다. Adobe Experience Platform [!DNL Identity Service] 는 다양한 디바이스와 시스템에 ID를 연결함으로써 효과적이고 개인화된 디지털 경험을 실시간으로 전달할 수 있도록 함으로써 고객 및 고객의 행동을 보다 정확하게 파악할 수 있도록 지원합니다.

## [!DNL Identity Service] 이해 

고객은 매일 기업과 교류하고 브랜드와의 지속적인 관계를 형성합니다. 일반적인 고객은 e커머스, 충성도, 헬프데스크 시스템 등 조직의 데이터 인프라 내에 있는 다양한 시스템에서 활성 상태일 수 있습니다. 이러한 고객은 모든 디바이스에서 익명으로 참여할 수 있습니다. [!DNL Identity Service] 서로 다른 시스템에서 격리될 수 있는 관련 데이터를 집계하여 고객의 전체 상황을 파악할 수 있습니다.

브랜드와의 소비자 관계에 대한 일상적인 예를 살펴보십시오.

Mary는 과거 몇 번의 주문을 완료한 e커머스 사이트에 계정을 가지고 있다. 그녀는 보통 개인 노트북을 이용해 쇼핑하고, 매번 로그인한다. 그러나 그는 샌들을 사기 위해 태블릿을 사용하지만 주문을 하지 않고 로그인하지 않는다.

이때 Mary의 활동은 두 개의 개별 프로필로 나타납니다.디바이스 ID로 확인되는 e커머스 로그인 및 태블릿 디바이스

Mary는 나중에 자신의 뉴스레터를 구독하는 동안 태블릿 세션을 다시 시작하고 이메일 주소를 제공합니다. 이렇게 하면 스트리밍 통합 기능이 새로운 ID를 프로필 내 레코드 데이터로 추가합니다. 그 결과, [!DNL Identity Service] 이제 Mary의 태블릿 장치 활동과 전자 상거래 계정 내역이 관련되어 있습니다.

태블릿에서 다음 클릭까지 타겟팅된 컨텐츠는 알려지지 않은 쇼핑객이 사용하는 태블릿이 아니라 매리의 전체 프로필과 역사를 반영할 수 있습니다.

정의 및 유지 관리하는 ID 관계는 고객에 대한 완벽한 사진과 브랜드와의 상호 작용 [!DNL Identity Service] [!DNL Real-time Customer Profile] 을 만드는 데 이용됩니다. 자세한 내용은 [실시간 고객 프로필 개요를 참조하십시오](../profile/home.md).

### ID

ID는 엔티티, 일반적으로 개별 개인에 고유한 데이터입니다. 로그인 ID, ECID 또는 충성도 ID와 같은 ID를 알려진 ID라고 합니다.

이메일 주소 및 전화 번호와 같은 PII는 고객을 직접 식별하는 데 사용됩니다. 그 결과, PII는 여러 시스템에서 고객의 여러 ID와 일치시키는 데 사용됩니다.

디바이스의 실제 사용자를 식별하지 않고 알 수 없거나 익명 ID가 분리됩니다. 이 카테고리에는 방문자의 IP 주소 및 쿠키 ID와 같은 정보가 포함됩니다. 알 수 없는 ID를 사용하여 장치에서 행동 데이터를 수집할 수 있지만, 장치 또는 미디어에 이러한 ID를 연결하는 것은 고객이 여행 중에 PII를 제공할 때까지 제한됩니다.

아래 이미지에서 보듯이, 알려진 ID와 익명 ID는 [ID 그래프의](#identity-graphs)중요한 구성 요소로서 이 문서의 후반부에서 설명합니다.

![플랫폼에서 ID 연결](./images/identity-service-stitching.png)

구현의 예는 다음과 [!DNL Identity Service] 같습니다.

- 통신 회사는 &quot;전화 번호&quot; 값에 의존할 수 있는데, 여기서 전화 번호는 오프라인 데이터 세트와 온라인 데이터 세트 모두에서 동일한 관심 있는 개인을 의미합니다.
- 소매 회사는 익명의 방문자의 높은 비율로 인해 오프라인 데이터 세트에서 &quot;이메일 주소&quot;를 사용하고 온라인 데이터 세트에서 ECID를 사용할 수 있습니다.
- 은행은 지점 거래와 같은 오프라인 데이터 세트에서 &quot;계좌 번호&quot;를 선호할 수 있습니다. 대부분의 방문자가 방문 중에 인증되기 때문에 온라인 데이터 세트의 &quot;로그인 ID&quot;에 의존할 수 있습니다.
- 또한 고객은 GUID 또는 기타 범용 고유 식별자와 같은 고유한 재산 ID를 가질 수 있습니다.

### ID 데이터

어떤 사람에게 &quot;신분증이 무엇입니까?&quot;라고 물으면 더 이상의 문맥이 없다면, 그들이 유용한 답을 제공하는 것은 어려울 것이다. 동일한 논리로, 시스템 생성 ID인지 이메일 주소인지 ID 값을 나타내는 문자열 값은 문자열 값 컨텍스트를 제공하는 한정자와 함께 제공되는 경우에만 완료됩니다.id 네임스페이스입니다.

## ID 네임스페이스 및 ID 그래프

고객은 온라인 및 오프라인 채널을 함께 사용하여 브랜드와 상호 작용할 수 있으므로 세분화된 상호 작용을 단일 고객 ID로 조정하는 방법을 고민할 수 있습니다.

[!DNL Experience Platform] 다음 두 가지 개념을 통해 이 문제를 해결합니다. [id 네임스페이스](#identity-namespaces) 및 [ID 그래프](#identity-graphs).

다음 비디오는 ID 및 ID 그래프에 대한 이해를 지원하기 위한 것입니다. 다음 비디오에서는 ID 수집, ID 그래프 및 API의 세 가지 기능을 다룹니다. 또한 개인 ID 그래프를 구성하는 데 결정적 및 확률적 알고리즘이 어떻게 사용되는지 설명하고, 개인 ID 그래프, Adobe Experience Platform ID 서비스 Co-Op 그래프 및 타사 그래프의 역할에 대해 설명합니다.

>[!IMPORTANT]
>
> 확률적 개인 그래프가 아직 개발 중에 있으며 나중에 발표되도록 설정됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### ID 네임스페이스

웹, 모바일 애플리케이션, 콜센터 또는 스토어를 비롯한 다양한 채널에서 고객이 브랜드와 인터랙션하는 경우 채널 전반에서 고객의 활동을 관찰하고 추적할 수 없는 경우 고객을 파악하고 서비스를 제공하는 것이 어려울 수 있습니다.

다양한 디바이스와 채널에서 고객을 이해하면 각 채널에서 고객을 인식하게 됩니다. Adobe Experience Platform은 ID 네임스페이스를 사용하여 이를 달성합니다.
ID 네임스페이스는 데이터가 시작되는 컨텍스트를 제공하는 데 사용되는 장치 ID 또는 이메일 ID와 같은 식별자입니다. ID 네임스페이스는 개별 ID를 조회하거나 연결하는 데 사용되며 ID 값에 대한 컨텍스트를 제공하여 데이터 충돌을 방지합니다. 예를 들어, ID &quot;123456&quot;은 전자 상거래 시스템의 한 사람과 도움말 데스크 시스템의 다른 사람을 나타낼 수 있습니다. 자세한 내용은 [ID 네임스페이스 개요를 참조하십시오](./namespaces.md).

### ID 그래프

ID 그래프는 서로 다른 ID 네임스페이스 간의 관계를 보여주는 지도로, 고객이 다양한 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여줍니다.

모든 고객 ID 그래프는 고객 활동에 대한 대응으로 거의 실시간으로 종합적으로 관리 및 업데이트됩니다 [!DNL Identity Service] .

[!DNL Identity Service] 조직만이 볼 수 있고 데이터를 기반으로 하여 개인 그래프라고 하는 ID 그래프를 관리합니다. [!DNL Identity Service] 인제스트된 데이터 레코드에 둘 이상의 ID가 포함되어 있는 경우 개인 그래프를 늘려 검색된 ID 간의 관계를 추가합니다.

ID 데이터를 제공하고 레이블을 지정할 때 고려해야 할 잠재적 유형의 예로, &quot;직장 전화&quot;와 같은 전화 번호를 사용하면 ID 그래프에 의도한 것보다 더 많은 관계를 만들 수 있습니다. 많은 직원들이 동일한 번호로 직장에서 사용하고 있으며, 그 &quot;가정&quot; 및 &quot;모바일&quot;은 관계를 최대한 정확하게 유지하기 위해 더 나은 서비스를 제공한다는 사실을 알게 될 것입니다.

자세한 내용은 ID 그래프 뷰어 [액세스에 대한 자습서를 참조하십시오.](./ui/identity-graph-viewer.md)

## ID 데이터 제공 [!DNL Identity Service]

이 섹션에서는 각 고객에 대한 ID 그래프를 작성하기 위해 Adobe Experience Platform에 제공된 데이터 [!DNL Identity Service] 가 사용되기 전에 처리되는 방법에 대해 설명합니다.

### ID 필드 결정

기업 데이터 수집 전략에 따라 ID로 레이블을 지정하는 데이터 필드는 ID 맵에 포함된 데이터를 결정합니다. Adobe Experience Platform의 최대 이점과 가장 포괄적인 고객 ID를 얻으려면 온라인 및 오프라인 데이터를 모두 업로드해야 합니다.

- 온라인 데이터는 사용자 이름 및 이메일 주소와 같은 온라인 상태 및 행동을 설명하는 데이터입니다.

- 오프라인 데이터는 CRM 시스템의 ID와 같이 온라인 비즈니스와 직접 관련이 없는 데이터를 나타냅니다. 이러한 유형의 데이터는 ID를 더욱 견고하게 만들고 서로 다른 시스템에서 데이터 결합을 지원합니다.

### 추가 ID 네임스페이스 만들기

다양한 표준 네임스페이스를 [!DNL Experience Platform] 제공하지만 ID를 제대로 분류하려면 추가 네임스페이스를 만들어야 할 수 있습니다. 자세한 내용은 ID 네임스페이스 개요에서 조직의 [](./namespaces.md) 네임스페이스 보기 및 만들기에 대한 섹션을 참조하십시오.

>[!NOTE]
>
>ID 네임스페이스는 ID의 한정자입니다. 따라서 네임스페이스를 만들면 이를 삭제할 수 없습니다.

### ID 데이터 포함 [!DNL Experience Data Model] (XDM)

XDM( [!DNL Platform] Customization Framework)은 고객 데이터 [!DNL Experience Data Model] 를 구성하는 표준화된 프레임워크로서, 상호 작용하는 [!DNL Experience Platform] 기타 서비스와 다양한 서비스에서 데이터를 공유 및 이해할 수 있도록 [!DNL Platform]해줍니다. 자세한 내용은 [XDM 시스템 개요를 참조하십시오](../xdm/home.md).

레코드 및 시간 시리즈 스키마 모두 ID 데이터를 포함하는 방법을 제공합니다. 데이터가 수집되면 ID 그래프는 여러 네임스페이스의 데이터 조각 간에 일반적인 ID 데이터를 공유하는 것으로 확인되면 새로운 관계를 만듭니다.

### XDM 필드를 ID로 표시

레코드 또는 시간 시리즈 XDM 클래스 `string` 를 구현하는 스키마의 모든 유형 필드는 ID 필드로 레이블이 지정될 수 있습니다. 따라서 해당 필드에 수집되는 모든 데이터는 ID 데이터로 간주됩니다.

ID 필드는 ID가 공통 PII 데이터를 공유하는 경우 ID의 연결을 허용합니다.
예를 들어, 전화 번호 필드에 ID 필드로 레이블을 지정하면 동일한 전화 번호를 사용하는 것으로 확인된 다른 개인과의 관계를 자동으로 그래프로 표시합니다. [!DNL Identity Service]

>[!NOTE]
>
>결과 ID의 네임스페이스는 필드 레이블이 지정된 시간에 제공됩니다.

### 데이터 세트 구성 [!DNL Identity Service]

스트리밍 수집 프로세스 동안 레코드 및 시간 시리즈 데이터에서 ID 데이터를 [!DNL Identity Service ]자동으로 추출합니다. 하지만 데이터를 수집하려면 먼저 데이터를 활성화해야 합니다 [!DNL Identity Service]. 자세한 내용은 API를 [사용하여 실시간 고객 프로필 및 ID 서비스용 데이터 세트 구성에 대한](../profile/tutorials/dataset-configuration.md) 자습서를 참조하십시오.

### 데이터 인제스트 [!DNL Identity Service]

[!DNL Identity Service] 일괄 처리 [!DNL Experience Platform] 또는 [스트리밍 수집](../ingestion/batch-ingestion/overview.md) 방식으로 전송된 XDM 호환 데이터를 [사용합니다](../ingestion/streaming-ingestion/overview.md).

다음 비디오는 ID 서비스에 대한 귀하의 이해를 지원하기 위한 것입니다. 이 비디오에서는 데이터 필드에 ID로 레이블을 지정하고 ID 데이터를 인제스트한 다음 데이터가 Adobe Experience Platform ID 서비스 비공개 그래프로 작성되었는지 확인하는 방법을 보여줍니다.

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 데이터 거버넌스

Adobe Experience Platform은 개인 정보를 고려하여 구축되었으며 고객 PII 데이터를 보호하기 위한 데이터 거버넌스 프레임워크를 포함하고 있습니다. &quot;email&quot; 또는 &quot;phone&quot; 네임스페이스의 ID 데이터는 기본적으로 암호화되지만 중요한 데이터가 지속되기 전에 암호화되도록 하기 위해 데이터 사용 레이블을 인제스트되거나 데이터가 도착하면 데이터에 적용할 수 있습니다 [!DNL Platform]. 자세한 내용은 [데이터 거버넌스 개요를 참조하십시오](../data-governance/home.md).

## 다음 단계

이제 핵심 개념 [!DNL Identity Service] 과 그 역할 [!DNL Experience Platform]을 이해했으므로 ID 그래프를 사용하여 작업하는 방법을 배울 수 있습니다 [[!DNL Identity Service API]](./api/getting-started.md).
