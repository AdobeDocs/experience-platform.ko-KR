---
solution: Experience Platform
title: 세그먼테이션 서비스 개요
description: Adobe Experience Platform 세분화 서비스 및 플랫폼 생태계에서 수행하는 역할에 대해 알아봅니다.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: f981b26a468a1d5ab9931a9cce59b176cd0fd9b3
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 13%

---

# [!DNL Segmentation Service] 개요

Adobe Experience Platform [!DNL Segmentation Service]에서는 [!DNL Real-Time Customer Profile] 데이터의 세그먼트 정의나 다른 소스를 통해 대상자를 만들 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

이 문서에서는 [!DNL Segmentation Service] 및 Adobe Experience Platform에서 수행하는 역할에 대한 개요를 제공합니다.

## [!DNL Segmentation Service] 시작하기

이 문서 전체에서 사용되는 다음 주요 용어를 이해해야 합니다.

- **대상**: 유사한 비헤이비어 및/또는 특성을 공유하는 사람들의 컬렉션입니다. 이 사람 컬렉션은 Adobe Experience Platform에서 세그먼트 정의(플랫폼 생성 대상)를 사용하여 생성하거나 외부 소스(외부 생성 대상)에서 생성할 수 있습니다.
- **세그먼트 정의**: Adobe Experience Platform에서 대상 대상의 주요 특성 또는 동작을 설명하는 데 사용하는 규칙 집합입니다.
- **세그먼트**: 프로필을 대상자로 분리하는 작업입니다.

## 세그먼테이션 작동 방식

세그먼테이션은 프로필 하위 집합이 공유하는 특정 속성 또는 동작을 프로필 스토어와 정의하여 마케팅 가능한 사용자 그룹과 고객 기반을 구분하는 프로세스입니다. 예를 들어 &quot;운동화 구입하는 것을 잊었습니까?&quot;라는 이메일 캠페인에서 지난 30일 내에 운동화를 찾았지만 구입을 완료하지 않은 모든 사용자를 대상으로 할 수 있습니다.

대상자가 개념적으로 정의되면 [!DNL Experience Platform]에 작성됩니다. 일반적으로 대상자는 마케터 또는 대상 전문가가 구축하지만, 일부 조직에서는 마케팅 부서가 데이터 분석가와 공동 작업을 통해 대상자를 생성하는 것을 선호합니다. [!DNL Platform]&#x200B;(으)로 전송되는 데이터를 검토할 때 데이터 분석가는 대상자의 규칙이나 조건을 작성하는 데 사용할 필드와 값을 선택하여 세그먼트 정의를 만들거나 대상 구성을 사용하여 대상을 구성하여 두 가지 방법으로 대상을 만들 수 있습니다.

## 대상자 만들기

대상자는 Adobe Experience Platform에서 대상자로 직접 구성 또는 플랫폼에서 파생된 세그먼트 정의를 통한 두 가지 방식으로 생성할 수 있습니다.

### 대상자 구성

플랫폼에서 대상을 직접 작성할 때 대상 작성을 사용할 수 있습니다. 대상 구성을 사용하여 대상을 만드는 방법에 대해 알아보려면 [대상 구성 가이드](./ui/audience-composition.md)를 참조하십시오.

### 세그먼트 정의

API를 사용하여 생성하든 [!DNL Segment Builder]을(를) 사용하여 생성하든 세그먼트 정의는 궁극적으로 [!DNL Profile Query Language]&#x200B;(PQL)을 사용하여 정의됩니다. 여기에서 개념 세그먼트 정의가 기준을 충족하는 프로필을 검색하도록 빌드된 언어로 설명됩니다. 자세한 내용은 [PQL 개요](./pql/overview.md)를 참조하세요.

[!DNL Segment Builder]&#x200B;([!DNL Segmentation Service]의 UI 구현)에서 세그먼트를 만들고 사용하는 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](./ui/segment-builder.md)를 참조하세요.

API를 사용하여 세그먼트 정의를 작성하는 방법에 대한 자세한 내용은 [API를 사용하여 세그먼트 정의 만들기](./tutorials/create-a-segment.md)에 대한 자습서를 참조하십시오.

>[!NOTE]
>
>스키마가 확장되는 경우 모든 향후 업로드는 그에 따라 새로 추가된 필드를 업데이트해야 합니다. [!DNL Experience Data Model]&#x200B;(XDM) 사용자 지정에 대한 자세한 내용은 [스키마 편집기 튜토리얼](../xdm/tutorials/create-schema-ui.md)을(를) 참조하십시오.
>
>또한 데이터 세트에서 경험 이벤트 만료 값이 활성화되면 생성된 세그먼트 정의의 멤버십에 영향을 줄 수 있습니다. 이 기능이 세분화에 미치는 영향에 대한 자세한 내용은 [경험 이벤트 만료](../profile/event-expirations.md)에 대한 안내서를 참조하십시오.

### 페더레이션된 대상자 구성 {#fac}

대상 구성 및 세그먼트 정의 외에 Adobe Federated Audience Composition을 사용하여 기본 데이터를 복사하지 않고 Enterprise 데이터 세트에서 새 대상을 작성하고 이러한 대상을 Adobe Experience Platform Audience Portal에 저장할 수 있습니다. Enterprise Data Warehouse에서 페더레이션된 구성된 대상 데이터를 활용하여 Adobe Experience Platform의 기존 대상을 강화할 수도 있습니다. [Federated Audience Composition](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/home)에 대한 안내서를 읽어 보십시오.

## 대상자 평가 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="평가 방법"
>abstract="현재 Platform은 대상자를 평가하는 세 가지 방식(스트리밍 세분화, 배치 세분화, 에지 세분화)을 지원합니다."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="스트리밍 평가"
>abstract="스트리밍 세분화는 사용자 활동에 대응하여 대상자를 업데이트하는 진행형 데이터 선택 프로세스입니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/streaming-segmentation.html" text="스트리밍 세분화를 통해 거의 실시간으로 이벤트 평가"

현재 Platform은 대상자를 평가하는 세 가지 방식(스트리밍 세분화, 배치 세분화, 에지 세분화)을 지원합니다.

### 스트리밍 세분화 {#streaming}

스트리밍 세분화는 사용자 활동에 대응하여 대상자를 업데이트하는 진행형 데이터 선택 프로세스입니다. 대상을 빌드하고 저장하면 [!DNL Real-Time Customer Profile]&#x200B;(으)로 들어오는 데이터에 대해 세그먼트 정의가 적용됩니다. 대상에 대한 추가 및 제거는 정기적으로 처리되므로 대상 대상의 관련성이 유지됩니다.

스트리밍 세분화에 대한 자세한 내용은 [스트리밍 세분화 설명서](./methods/streaming-segmentation.md)를 참조하세요.

### 배치 세분화 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="배치 평가"
>abstract="진행 중인 데이터 선택 프로세스를 사용하는 대신 배치 세분화는 세그먼트 정의를 통해 한 번에 모든 프로필 데이터를 이동하여 해당 대상자를 생성합니다. 대상자가 생성되면 저장되므로 이를 사용하기 위해 내보낼 수 있습니다."

진행 중인 데이터 선택 프로세스를 사용하는 대신 배치 세분화는 세그먼트 정의를 통해 한 번에 모든 프로필 데이터를 이동하여 해당 대상자를 생성합니다. 만든 후에는 사용하기 위해 내보낼 수 있도록 결과 대상자가 저장되고 저장됩니다.

배치 대상은 24시간마다 자동으로 평가됩니다. 배치 대상을 온디맨드로 평가하려면 세그먼트 작업을 사용할 수 있습니다. 세그먼트 작업에 대한 자세한 내용은 [세그먼트 작업 설명서](./api/segment-jobs.md)를 참조하세요.

### 에지 세분화 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="에지 평가"
>abstract="에지 세분화는 Edge Network에서 Platform의 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지의 개인화 사용 사례를 활성화하는 기능입니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/edge-segmentation.html" text="에지 세분화 안내서"

Edge 세그멘테이션은 Edge Network](../landing/edge-and-hub-comparison.md)에서 플랫폼의 세그먼트를 즉시 [평가하는 기능으로, 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

Edge 세그멘테이션에 대한 자세한 내용은 [API 설명서](./methods/edge-segmentation.md) 또는 [UI 설명서](./methods/edge-segmentation.md)를 참조하십시오.

## 세그먼테이션 결과 액세스

내보낸 대상자에 액세스하는 방법에 대한 자세한 내용은 [세그먼트 정의 평가 튜토리얼](./tutorials/evaluate-a-segment.md)을 참조하세요.

## 세그먼트 정의 메타데이터

세그먼트 정의 메타데이터는 대상을 재사용 및/또는 결합할 이벤트에서 색인을 용이하게 합니다.

API 또는 [!DNL Segment Builder]을(를) 통해 세그먼트 정의를 작성하려면 이름 및 병합 정책을 정의해야 합니다.

### 세그먼트 정의 이름

새 세그먼트 정의를 생성할 때 이름을 제공해야 합니다. 세그먼트 정의 이름은 [!DNL Segmentation Service]에서 빌드한 컬렉션 중 특정 세그먼트 정의를 식별하는 데 사용됩니다. 따라서 세그먼트 정의 이름은 설명적이고 간결하며 고유해야 합니다.

>[!NOTE]
>
>세그먼트 정의를 계획할 때 세그먼트 정의는 다른 세그먼트 정의에서 참조하고 와 결합할 수 있습니다. 이름을 선택할 때 세그먼트 정의에 재사용 가능한 부분이 포함될 수 있는 가능성을 고려하십시오.

### 병합 정책

병합 정책은 특정 조건에서 데이터의 우선 순위를 지정하고 통합 보기에 결합하는 방법을 결정하기 위해 [!DNL Profile]에서 사용하는 규칙입니다.

병합 정책이 정의되지 않으면 기본 [!DNL Platform] 병합 정책이 사용됩니다. 조직 고유의 병합 정책을 사용하려는 경우 자체 정책을 만들어 조직의 기본값으로 표시할 수 있습니다.

병합 정책에 대한 자세한 내용은 [병합 정책 안내서](../profile/api/merge-policies.md)를 참조하십시오.

>[!NOTE]
>
>대상 크기의 추정은 조직의 기본 프로필 병합 정책을 기반으로 합니다.

### 기타 세그먼트 정의 메타데이터

[!DNL Segment Builder]은(는) 이름 및 병합 정책 외에도 세그먼트 정의의 목적을 요약할 수 있는 추가 설명 메타데이터 필드를 제공합니다.

## 고급 세그먼테이션 기능

[스트리밍 데이터 수집](../ingestion/streaming-ingestion/overview.md)을(를) 다음 고급 세분화 기능과 결합하여 지속적으로 대상을 생성하도록 세그먼트 정의를 구성할 수 있습니다.
- [순차적인 세분화](#sequential)
- [동적 세분화](#dynamic)
- [다중 엔티티 세그멘테이션](#multi-entity)

이러한 고급 기능에 대해서는 다음 섹션에서 자세히 설명합니다.

### 순차적인 세분화 {#sequential}

표준 사용자 여정은 기본적으로 순차적입니다. Adobe Experience Platform에서는 이 여정을 반영할 순서가 지정된 일련의 대상을 정의하여 이벤트가 발생할 때 일련의 이벤트를 캡처할 수 있습니다. [!DNL Segment Builder]의 시각적 이벤트 타임라인을 사용하여 이벤트를 원하는 순서로 정렬할 수 있습니다.

순차적인 세분화가 필요한 고객 여정의 예로는 제품 보기 > 제품 추가 > 체크아웃 > 구매 안 함 이 있습니다.

### 동적 세분화 {#dynamic}

동적 세그먼테이션은 마케터가 마케팅 캠페인용 대상자를 구축할 때 일반적으로 직면한 확장성 문제를 해결합니다.

가능한 모든 사용 사례를 명시적 및 반복적으로 캡처해야 하는 정적 세그먼테이션과 달리, 동적 세그먼테이션은 변수를 사용하여 규칙 논리를 구축하고 관계를 동적으로 표현합니다.

이 고급 세분화 기능의 가치를 설명하기 위해 데이터 설계자가 마케터와 협력하여 집 밖에서 구입한 고객을 식별하는 것을 고려하십시오.

정적 세그먼테이션을 사용하려면 홈 상태와 같지 않은 구매 이벤트에 대해 필터링하기 전에 고유한 홈 상태 속성으로 개별 세그먼트를 정의해야 합니다. 이 유형에 대한 명시적 세그먼트 정의에는 &quot;구매 상태가 유타가 아닌 유타에서 온 사람을 찾고 있습니다.&quot;라고 표시됩니다. 이 방법을 사용하여 대상을 만들려면 총 50개의 세그먼트에 대해 모든 미국 주에 대해 하나의 세그먼트 정의를 정의해야 합니다.

크기를 조정할 때 필연적으로 발생하는 다양한 세그먼트 정의 조합의 결과, 정적 세그먼테이션에 필요한 수동 프로세스는 시간이 더 많이 소요되어 전체 효율성을 감소시킵니다.

변수를 구매 상태 속성에 할당하면 동적 세그먼트 정의가 &quot;해당 구매의 상태가 고객의 홈 상태와 같지 않은 구매를 찾을 수 있습니다.&quot;로 단순화됩니다. 그런 다음 50개의 정적 세그먼트를 하나의 동적 세그먼트 정의로 통합할 수 있습니다.

### 다중 엔티티 세그멘테이션 {#multi-entity}

고급 다중 엔터티 세분화 기능을 사용하면 제품, 스토어 또는 &quot;차원&quot; 엔터티라고도 하는 기타 비사용자를 기반으로 하는 추가 데이터로 [!DNL Real-Time Customer Profile] 데이터를 확장할 수 있습니다. 따라서 [!DNL Segmentation Service]은(는) [!DNL Profile] 데이터 저장소의 기본인 것처럼 세그먼트 정의 중에 추가 필드에 액세스할 수 있습니다. 다중 엔티티 세그먼테이션은 고유한 비즈니스 요구 사항과 관련된 데이터를 기반으로 대상자를 식별할 때 유연성을 제공합니다. 사용 사례 및 워크플로와 같은 자세한 내용은 [다중 엔터티 세분화 가이드](./tutorials/multi-entity-segmentation.md)를 참조하세요.

## [!DNL Segmentation Service] 데이터 형식

[!DNL Segmentation Service]은(는) 다양한 기본 데이터 형식과 복잡한 데이터 형식을 지원합니다. 지원되는 데이터 형식 목록을 포함한 자세한 정보는 [지원되는 데이터 형식 안내서](./data-types.md)에서 찾을 수 있습니다.

## 다음 단계

[!DNL Segmentation Service]은(는) [!DNL Real-Time Customer Profile] 데이터에서 대상을 빌드하는 통합 워크플로우를 제공합니다.

세분화 서비스 UI 사용에 대한 자세한 내용은 [세분화 서비스 UI 개요](./ui/overview.md)를 참조하십시오.

UI에서 대상을 구성하는 방법을 알아보려면 [대상 구성 안내서](./ui/audience-composition.md)를 읽어 보십시오. UI에서 세그먼트 정의를 정의하는 방법은 [세그먼트 빌더 안내서](./ui/overview.md)를 참조하세요. API를 사용하여 세그먼트 정의를 작성하는 방법에 대한 자세한 내용은 [API를 사용하여 세그먼트 정의 만들기](./tutorials/create-a-segment.md)에 대한 자습서를 참조하십시오.
