---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼트 서비스;세그먼트;세그먼트;세그먼트;세그먼트
solution: Experience Platform
title: 세그먼테이션 서비스 개요
topic-legacy: overview
description: Adobe Experience Platform 세그멘테이션 서비스 및 플랫폼 생태계에서 수행하는 역할에 대해 알아봅니다.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# [!DNL Segmentation Service] 개요

Adobe Experience Platform [!DNL Segmentation Service] 는 세그먼트를 작성하고 사용자의 세그먼트를 생성할 수 있도록 해주는 사용자 인터페이스 및 RESTful API를 제공합니다 [!DNL Real-Time Customer Profile] 데이터. 이러한 세그먼트는 중앙에서 구성 및 관리됩니다 [!DNL Platform], 그리고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

이 문서에서는 [!DNL Segmentation Service] Adobe Experience Platform에서 수행하는 역할입니다.

## 시작하기 [!DNL Segmentation Service]

이 문서 전체에서 사용되는 다음과 같은 주요 용어를 이해하는 것이 중요합니다.

- **세그먼테이션**: 큰 개인 그룹(예: 고객, 잠재 고객, 사용자 또는 조직)을 유사한 트레이트를 공유하고 마케팅 전략과 유사하게 응답하는 작은 그룹으로 분할합니다.
- **세그먼트 정의**: 타겟 대상의 주요 특성 또는 동작을 설명하는 데 사용되는 규칙 세트입니다. 개념화된 경우 세그먼트 정의에 요약된 규칙은 세그먼트에 대한 자격을 부여하는 대상 구성원을 결정하는 데 사용됩니다.
- **Audience**: 세그먼트 정의 기준을 충족하는 결과 프로필 집합입니다.

## 세그먼테이션 작동 방식

세그먼테이션은 마케팅 가능한 사람 그룹을 고객 기반과 구분하기 위해 프로필 저장소의 프로필 하위 집합에 의해 공유되는 특정 속성 또는 동작을 정의하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서 지난 30일 이내에 운동화 구매를 검색했지만 구매를 완료하지 않은 모든 사용자의 청중을 원할 수 있습니다.

세그먼트가 개념적으로 정의되면, [!DNL Experience Platform]. 일반적으로 세그먼트는 마케팅 부서에서 데이터 분석가와 협력하여 만드는 것을 선호하지만 마케팅 전문가 또는 대상 전문가가 작성합니다. 전송 중인 데이터를 검토할 때 [!DNL Platform], 데이터 분석가는 세그먼트의 규칙 또는 조건을 작성하는 데 사용할 필드 및 값을 선택하여 세그먼트 정의를 작성합니다. 이 작업은 UI 또는 API를 사용하여 수행됩니다.

## 세그먼트 만들기

API를 사용하여 만들었는지 또는 [!DNL Segment Builder], 세그먼트는 궁극적으로 [!DNL Profile Query Language] (PQL). 여기서 기준에 맞는 프로필을 검색하기 위해 빌드된 언어로 개념적 세그먼트 정의를 설명합니다. 자세한 내용은 [PQL 개요](./pql/overview.md).

에서 세그먼트를 만들고 사용하는 방법을 배우려면 [!DNL Segment Builder] (UI 구현 [!DNL Segmentation Service]). 자세한 내용은 [세그먼트 빌더 안내서](./ui/overview.md).

API를 사용하여 세그먼트 정의 작성에 대한 자세한 내용은 [api를 사용하여 대상 세그먼트 만들기](./tutorials/create-a-segment.md).

>[!NOTE]
>
>스키마가 확장되는 경우 이후의 모든 업로드는 그에 따라 새로 추가된 필드를 업데이트해야 합니다. 사용자 지정에 대한 자세한 정보 [!DNL Experience Data Model] (XDM), [스키마 편집기 자습서](../xdm/tutorials/create-schema-ui.md).
>
>또한 데이터 세트에서 경험 이벤트 만료 값이 활성화된 경우 생성된 세그먼트의 멤버십에 영향을 줄 수 있습니다. 다음 안내서를 읽어 주십시오 [경험 이벤트 만료](../profile/event-expirations.md) 이 기능이 세그멘테이션에 어떻게 영향을 줄 수 있는지에 대해 자세히 알아보십시오.

## 세그먼트 평가 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="평가 방법"
>abstract="Platform은 현재 세 가지 세그먼트 평가 방법을 지원합니다. 스트리밍 세그멘테이션, 배치 세그멘테이션 및 에지 세그먼테이션."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="스트리밍 평가"
>abstract="스트리밍 세그먼테이션은 사용자 활동에 대한 응답으로 세그먼트를 업데이트하는 지속적인 데이터 선택 프로세스입니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="스트리밍 세그먼테이션을 통해 거의 실시간으로 이벤트 평가"

Platform은 현재 세 가지 세그먼트 평가 방법을 지원합니다. 스트리밍 세그멘테이션, 배치 세그멘테이션 및 에지 세그먼테이션.

### 스트리밍 세그멘테이션 {#streaming}

스트리밍 세그먼테이션은 사용자 활동에 대한 응답으로 세그먼트를 업데이트하는 지속적인 데이터 선택 프로세스입니다. 세그먼트가 만들어지고 저장되면, 들어오는 데이터에 대해 세그먼트 정의가 적용됩니다. [!DNL Real-Time Customer Profile]. 세그먼트 추가 및 제거는 정기적으로 처리되므로 타겟 대상이 적절하도록 합니다.

스트리밍 세그멘테이션에 대한 자세한 내용은 [스트리밍 세그멘테이션 설명서](./api/streaming-segmentation.md).

### 일괄 세분화 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="일괄 평가"
>abstract="일괄 처리 세그먼테이션은 진행 중인 데이터 선택 프로세스의 대안으로서, 세그먼트 정의를 통해 모든 프로필 데이터를 한 번에 이동하여 해당 대상을 생성합니다. 세그먼트가 만들어지면 저장되고 저장되므로 사용할 수 있도록 내보낼 수 있습니다."

일괄 처리 세그먼테이션은 진행 중인 데이터 선택 프로세스의 대안으로서, 세그먼트 정의를 통해 모든 프로필 데이터를 한 번에 이동하여 해당 대상을 생성합니다. 세그먼트가 만들어지면 저장되고 저장되므로 사용할 수 있도록 내보낼 수 있습니다.

배치 세그먼트는 24시간 간격으로 자동 평가됩니다. 요청 시 배치 세그먼트를 평가하려면 세그먼트 작업을 사용할 수 있습니다. 세그먼트 작업에 대한 자세한 내용은 [세그먼트 작업 설명서](./api/segment-jobs.md).

### 에지 세그멘테이션 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="에지 평가"
>abstract="Edge 세그멘테이션은 Experience Edge에서 즉시 세그먼트를 평가하여 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Edge Segmentation UI 안내서"

Edge 세그멘테이션은 즉시 Platform의 세그먼트를 평가하는 기능입니다 [Experience Edge에서](../edge/home.md), 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

Edge Segmentation에 대한 자세한 내용은 [API 설명서](./api/edge-segmentation.md) 또는 [UI 설명서](./ui/edge-segmentation.md).

## 세그먼테이션 결과 액세스

내보낸 세그먼트에 액세스하는 방법에 대해 알아보려면 [세그먼트 평가 자습서](./tutorials/evaluate-a-segment.md).

## 세그먼트 메타데이터

세그먼트 메타데이터를 사용하면 세그먼트를 다시 사용하고/또는 결합할 때 손쉽게 색인을 생성할 수 있습니다.

세그먼트 작성(API 또는 [!DNL Segment Builder])을 사용하려면 세그먼트 이름과 병합 정책을 정의해야 합니다.

### 세그먼트 이름

새 세그먼트를 만들 때는 세그먼트 이름을 제공해야 합니다. 세그먼트 이름은 [!DNL Segmentation Service]. 따라서 세그먼트 이름은 수사적, 간결한 및 고유해야 합니다.

>[!NOTE]
>
>세그먼트를 계획할 때 세그먼트를 다른 세그먼트에서 참조하고 세그먼트와 결합할 수 있습니다. 이름을 선택할 때 세그먼트에 재사용 가능한 부분이 포함될 수 있는 가능성을 고려하십시오.

### 병합 정책

병합 정책은 [!DNL Profile] 를 입력하여 특정 조건에서 데이터의 우선 순위가 지정되고 통합 보기에 결합되는 방법을 결정합니다.
병합 정책이 정의되지 않으면 기본값이 됩니다 [!DNL Platform] 병합 정책이 사용됩니다. 조직 고유의 병합 정책을 사용하는 것이 나을 경우 고유한 병합 정책을 만들어 조직의 기본값으로 표시할 수 있습니다.

병합 정책에 대한 자세한 내용은 [정책 병합 안내서](../profile/api/merge-policies.md).

>[!NOTE]
>
>대상 크기 추정은 조직의 기본 프로필 병합 정책을 기반으로 합니다.

### 기타 세그먼트 메타데이터

세그먼트 이름 및 병합 정책 외에도 [!DNL Segment Builder] 세그먼트 정의의 목적을 요약할 수 있는 추가 &quot;세그먼트 설명&quot; 메타데이터 필드를 제공합니다.

## 고급 세분화 기능

세그먼트를 결합하여 대상을 지속적으로 생성하도록 구성할 수 있습니다 [스트리밍 데이터 수집](../ingestion/streaming-ingestion/overview.md) 다음 고급 세분화 기능을 사용할 수 있습니다.
- [순차적 세그먼테이션](#sequential)
- [동적 세분화](#dynamic)
- [다중 엔티티 세그먼테이션](#multi-entity)

이러한 고급 기능은 다음 섹션에서 자세히 설명합니다.

## 순차적 세그먼테이션 {#sequential}

표준 사용자 여정은 자연에서 순차적 것입니다. Adobe Experience Platform에서는 이벤트가 발생할 때 여정 시퀀스를 캡처하므로 이 세그먼트를 반영하도록 순서가 지정된 일련의 세그먼트를 정의할 수 있습니다. 에서 시각적 이벤트 타임라인을 사용하여 이벤트를 원하는 순서로 배열할 수 있습니다 [!DNL Segment Builder].

순차적 세그먼테이션이 필요한 고객 여정의 예는 제품 보기 > 제품 추가 > 체크아웃 > 구매 없음입니다.

## 동적 세분화 {#dynamic}

동적 세그멘테이션은 마케팅 캠페인을 위해 세그먼트를 작성할 때 일반적으로 발생하는 확장성 문제를 해결합니다.

가능한 모든 사용 사례를 명시적으로 및 반복적으로 캡처해야 하는 정적 세그먼테이션과 달리, 동적 세그멘테이션은 변수를 사용하여 규칙 논리를 만들고 관계를 동적으로 나타냅니다.

### 사용 사례: 홈 상태 외부에서 구입한 고객 찾기

이러한 고급 세분화 기능의 가치를 이해하려면 마케팅 담당자와 협력하여 홈 상태 외부에서 구입한 고객을 식별하십시오.

**문제**

정적 세그먼테이션을 사용하려면 홈 상태와 같지 않은 구매 이벤트를 필터링하기 전에 고유한 홈 상태 특성을 사용하여 개별 세그먼트를 정의해야 합니다. 이 유형의 노골적인 세그먼트는 &quot;나는 그들의 구매의 주가 유타가 아닌 유타에서 온 사람들을 찾고 있다.&quot;라고 읽힐 것이다. 이 방법을 사용하여 대상을 만들려면 총 50개의 세그먼트에 대해 미국 주마다 하나의 세그먼트를 정의해야 합니다.

규모에 따라 필연적으로 발생하는 여러 세그먼트 조합의 결과, 정적 세그먼테이션에 필요한 수동 프로세스는 시간이 많이 걸리며 전체 효율성을 감소합니다.

**솔루션**

구매 상태 속성에 변수를 할당하면 동적 세그먼트가 &quot;구매 상태가 고객의 홈 상태와 같지 않은 구매 찾기&quot;로 단순화됩니다. 그런 다음 50개의 정적 세그먼트를 단일 동적 세그먼트로 통합할 수 있습니다.

## 다중 엔티티 세그먼테이션 {#multi-entity}

고급 다중 엔티티 세그먼테이션 기능을 사용하여 다음을 확장할 수 있습니다 [!DNL Real-Time Customer Profile] 제품, 저장소 또는 기타 비개인을 기반으로 하는 &quot;차원&quot; 엔티티라고도 하는 추가 데이터가 있는 데이터. 결과적으로 [!DNL Segmentation Service] 세그먼트 정의 중에 추가 필드에 액세스할 수 있습니다. [!DNL Profile] 데이터 저장소. 다중 엔티티 세그먼테이션은 고유한 비즈니스 요구 사항과 관련된 데이터를 기반으로 대상을 식별할 때 유연성을 제공합니다. 사용 사례 및 워크플로우 등 자세한 내용은 [다중 엔티티 세그먼테이션 안내서](multi-entity-segmentation.md).

## [!DNL Segmentation Service] 데이터 유형

[!DNL Segmentation Service] 에서는 다양한 기본 및 복잡한 데이터 유형을 지원합니다. 지원되는 데이터 유형 목록을 포함한 자세한 정보는 [지원되는 데이터 유형 안내서](./data-types.md).

## 다음 단계

[!DNL Segmentation Service] 에서 세그먼트를 작성할 통합 워크플로우를 제공합니다. [!DNL Real-Time Customer Profile] 데이터. 요약하면 다음과 같습니다.

- [!DNL Segmentation] 은 프로필 저장소에서 프로필 하위 집합을 정의하는 프로세스를 통해 원하는 마케팅 그룹의 동작이나 속성을 규명할 수 있습니다. [!DNL Segmentation Service] 이 프로세스를 가능하게 합니다.
- 세그먼트를 계획할 때는 세그먼트를 다른 세그먼트에서 참조하고 세그먼트와 결합할 수 있다는 점에 유의하십시오.
- 세그먼트는 프로필 데이터, 관련 시계열 데이터 또는 둘 다에 기반한 규칙으로 작성할 수 있습니다.
- 세그먼트를 온디맨드 또는 지속적으로 평가할 수 있습니다. 온디맨드로 평가되면 모든 프로필 데이터가 세그먼트 정의를 한 번에 통과합니다. 지속적으로 평가되면 데이터가 입력되는 대로 세그먼트 정의를 통해 스트리밍됩니다 [!DNL Platform].

UI에서 세그먼트를 정의하는 방법을 알려면 [세그먼트 빌더 안내서](./ui/overview.md). API를 사용하여 세그먼트 정의 작성에 대한 자세한 내용은 [api를 사용하여 세그먼트 만들기](./tutorials/create-a-segment.md).
