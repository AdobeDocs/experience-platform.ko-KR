---
title: Adobe Experience Platform의 AI Assistant 개요
description: AI Assistant, 그 뉘앙스와 사용 사례 및 이를 사용하여 Adobe Experience Platform 및 Real-time Customer Data Platform을 사용하여 워크플로를 신속하게 하는 방법에 대해 알아봅니다.
source-git-commit: dd3a7d07c0c78d76c552affef892d5e5c0f0bfb5
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 0%

---

# Adobe Experience Platform의 AI 지원

Adobe Experience Platform의 AI Assistant에 대해 알아보려면 이 문서를 참조하십시오.

Adobe Experience Platform의 AI Assistant는 Adobe 애플리케이션에서 워크플로를 가속화하는 데 사용할 수 있는 대화형 경험입니다. AI Assistant를 사용하여 제품 지식을 보다 잘 이해하고, 문제를 해결하거나, 정보를 검색하고, 운영 통찰력을 찾을 수 있습니다. AI Assistant는 Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer 및 Customer Journey Analytics을 지원합니다.

>[!IMPORTANT]
>
>* 동의해야 합니다. [사용자 계약](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) 먼저 AI Assistant를 사용할 수 있습니다. 사용자 계약에는 공개 베타 계약도 포함되어 있습니다. 추가 AI Assistant 기능이 Beta 용량으로 롤아웃될 때 이를 사용할 수 있도록 합니다.

![처음 사용자 경험이 트리거된 AI Assistant 인터페이스입니다.](./images/blank.png)

## AI Assistant 이해 {#understanding-ai-assistant}

AI Assistant는 데이터베이스에 질의한 다음 데이터베이스의 데이터를 사람이 읽을 수 있는 답변으로 변환하여 제출된 질문에 응답합니다.

기본 데이터의 이러한 내부 표현은 **[!DNL Knowledge Graph]** - 주어진 질문에 대한 개념, 데이터 및 메타데이터의 포괄적인 웹.

다음 [!DNL Knowledge Graph] 는 쿼리가 제출될 때마다 참조되는 하위 그래프로 구성됩니다.

* 고객 운영 통찰력.
* 다양한 메타 스토어에서 고객 운영 통찰력.
* Experience League 설명서입니다.

AI Assistant를 쿼리하기 전에 고려해야 할 두 가지 유형의 질문이 있습니다.

### 제품 지식 {#product-knowledge}

제품 지식은 Experience League 설명서에 기반을 둔 개념과 주제를 의미합니다. 제품 지식 질문은 다음 하위 그룹에 추가로 지정할 수 있습니다.

| 제품 지식 | 예시 |
| --- | --- |
| 뾰족한 학습 | <ul><li>ID와 기본 또는 외래 키 간의 차이점은 무엇입니까?</li><li>프로필 풍부성은 어떻게 계산됩니까?</li></ul> |
| 검색 열기 | <ul><li>이 데이터 세트를 내보내려면 어떻게 해야 합니까?</li><li>의료 서비스 고객을 위한 스키마가 있습니까?</li></ul> |
| 문제 해결 | <ul><li>프로필에 대해 Adobe 소유의 스키마를 켤 수 없는 이유는 무엇입니까?</li><li>세그먼트를 삭제할 수 없는 이유</li></ul> |

{style="table-layout:auto"}

### Operational insights {#operational-insights}

>[!IMPORTANT]
>
>Operational Insights 답변은 Beta 버전입니다. 에 액세스할 수 있는 모든 사용자 **Operational Insights 보기** 권한은 operational insights 응답에 액세스할 수 있습니다.

운영 인사이트는 카운트, 조회 및 계보 영향을 포함하여 AI 비서가 메타 데이터 개체(속성, 대상, 데이터 흐름, 데이터 세트, 대상, 여정, 스키마 및 소스)에 대해 생성하는 답변을 말합니다. 샌드박스 내의 데이터는 보지 않습니다.

* 보유한 데이터 세트는 몇 개입니까?
* 사용된 적이 없는 스키마 속성 수는 몇 개입니까?
* 활성화된 대상은 무엇입니까?

다음 도메인에서 운영 통찰력에 대해 AI Assistant에 질문할 수 있습니다.

* 속성
* 대상자
* 데이터 흐름
* 데이터 세트
* 대상 _(계정에 대한 질문과 데이터 흐름에 대한 일부 질문은 현재 답변할 수 없습니다.)_
* 여정
* 스키마 _(필드 그룹에 대한 질문에 지금은 답변할 수 없습니다.)_
* 소스 _(현재 계정에 대한 질문에 답변할 수 없습니다.)_

운영 통찰력 질문에 대한 답변이 UI의 현재 상태를 반영하지 않을 수 있습니다. 이러한 질문을 뒷받침하는 데이터는 24시간마다 한 번씩 업데이트됩니다. 예를 들어 사용자가 낮에 Real-Time CDP에서 수행하는 변경 사항은 밤에 데이터 스토어와 동기화된 다음 아침에 사용자 질문에 대해 사용할 수 있게 됩니다. 객체와 관련된 특정 데이터를 조회하려면 샌드박스에 로그인해야 합니다.

### 기능 범위 {#feature-scope}

현재 AI Assistant의 범위는 다음과 같습니다.

* [제품 지식](./home.md#product-knowledge): AI Assistant는 Experience Platform, Real-time Customer Data Platform 및 Adobe Journey Optimizer에 대한 제품 지식 질문에 답변할 수 있습니다. Customer Journey Analytics을 위해 제품 지식 항목을 자세히 살펴볼 수도 있지만, Customer Journey Analytics UI를 통해서만 가능합니다.
* [Operational insights](./home.md#operational-insights): 속성, 대상, 데이터 흐름, 데이터 세트, 대상, 여정, 스키마 및 소스와 같은 데이터 개체에 대한 작동 통찰력에 대한 질문이 있는 경우 AI Assistant에 질문할 수 있습니다.

## 기능 액세스 {#feature-access}

AI Assistant에 대한 액세스는 다음 매개 변수에 의해 제어됩니다.

* **애플리케이션에 액세스:** Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer 및 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **계약 액세스:** 귀사는 다음 내용에 동의해야 합니다. [!DNL GenAI]- 조직에서 AI Assistant를 사용하기 전에 관련 약관. AI Assistant에 액세스할 수 없는 경우 조직의 관리자 또는 Adobe 계정 팀에 문의하십시오.
* **권한:** 사용 [권한 UI](../access-control/abac/ui/permissions.md) 조직의 AI Assistant에 대한 액세스 권한을 부여하거나 취소할 수 있습니다. AI Assistant를 사용하려면 지정된 사용자가 로 프로비저닝된 역할에 속해야 합니다. **AI Assistant 활성화** 및 **Operational Insights 보기** 사용 권한.
   * 관리자는 다음을 추가할 수 있습니다. **AI Assistant 활성화** 지정된 역할에 사용자를 추가하여 조직의 AI Assistant에 액세스할 수 있도록 합니다.
   * 관리자는 다음을 추가할 수 있습니다. **Operational Insights 보기** 지정된 역할에 사용자를 추가하여 해당 사용자가 AI Assistant의 Operational Insights 기능을 사용할 수 있도록 합니다. Operational Insights 는 현재 Beta 버전입니다.

![주어진 역할에 포함된 AI Assistant 활성화 및 Operational Insights 보기 권한이 있는 권한 UI 페이지입니다.](./images/permissions.png)

## 예제 질문 {#example-questions}

이 섹션에서는 워크플로우 중에 참조할 수 있는 예제 질문에 대해 설명합니다. 질문은 운영 통찰력, 목표 및 객체의 세 섹션으로 그룹화됩니다.

### 운영 통찰력별로 그룹화된 예제 질문 {#operational-insights-questions}

+++Operational Insight 질문 및 해당 사용 사례의 예를 보려면 선택하십시오.

| 질문 유형 | 사용 사례 | 예시 |
| --- | --- | --- | 
| 데이터 계보 | 다른 Experience Platform 오브젝트에서 하나 이상의 오브젝트 사용 추적 | <ul><li>어느 데이터 세트가 &quot;ACME 스키마&quot; 스키마를 사용합니까?</li><li>동일한 스키마를 사용하여 수집된 데이터 세트 수는 얼마입니까?</li><li>활성화된 대상에서 사용된 데이터 세트는 무엇입니까?</li><li>활성화된 대상자에 사용된 속성이 있는 스키마를 나열합니다.</li><li>&quot;ACME 대상&quot;에 활성화되고 1000개 이상의 프로필이 있는 대상을 표시합니다.</li><li>2023년 1월 이후에 수정된 활성화된 대상자에 사용되는 속성을 표시합니다.</li><li>&quot;ACME Amazon S3&quot; 소스를 통해 수집된 데이터 세트는 무엇입니까?</li><li>어떤 데이터 흐름이 &quot;ACME 충성도 데이터 흐름&quot;과 관련됩니까?</li><li>활성화된 대상과 관련되고 지난 1년에 생성된 스키마를 나열합니다.</li></ul> |
| 배포 및 집계 | Experience Platform 개체 사용에 대한 요약 기반 질문 | <ul><li>활성화된 대상의 비율은 얼마입니까?</li><li>세분화에는 몇 개의 필드가 사용됩니까?</li><li>가장 많은 대상에 활성화된 대상은 무엇입니까?</li><li>중복 대상을 나열합니다.</li><li>&quot;ACME 대상&quot;에 활성화된 대상자를 보여 주고 프로필 크기별로 등급을 매깁니다.</li><li>활성화되지 않았지만 프로필이 100개를 초과하는 대상자의 비율은 얼마입니까? 그들의 이름을 보여줘</li><li>내 데이터 세트로 데이터를 수집하는 3개의 소스 커넥터를 나열합니다.</li><li>발생 횟수에 따라 활성화된 대상자에 사용되는 상위 5개 속성을 나열합니다.</li></ul> |
| 오브젝트 조회 | Experience Platform 개체 또는 해당 속성을 검색하거나 액세스합니다. | <ul><li>연관된 스키마가 없는 데이터 세트</li><li>&quot;ACME 대상&quot;에 사용되는 속성을 나열하시겠습니까?</li><li>프로필이 활성화되었지만 생성 이후 수정되지 않은 스키마 목록을 제공합니다.</li><li>지난 주에 수정된 대상은 무엇입니까?</li><li>생성 날짜와 함께 동일한 세그먼트 정의를 가진 대상을 나열합니다.</li><li>프로필이 활성화된 데이터 세트이며 각 데이터 세트에서 만든 대상 수를 포함합니다.</li><li>데이터 세트 XYZ와 연관된 소스 계정은 무엇입니까?</li><li>&quot;ACME 대상&quot;의 세그먼트 정의 및 수정 날짜를 표시합니다.</li></ul> |
| 오브젝트 비교 | 중복 대상을 식별합니다. | <ul><li>세그먼트 정의에 따라 중복되는 대상을 나열합니다.</li><li>어떤 중복 대상이 &quot;ACME 대상&quot;에 활성화됩니까?</li></ul> |

{style="table-layout:auto"}

+++

### 목표별로 그룹화된 예제 질문 {#objectives-questions}

+++AI Assistant를 사용하여 달성할 수 있는 목표 목록을 보려면 선택

| 목표 | 설명 | 예 |
| --- | --- | --- |
| 학습 개념 및 지속적인 워크플로 | <ul><li>초보 사용자는 AI Assistant를 사용하여 Real-Time CDP 및 Adobe Journey Optimizer 개념을 학습하고 익숙하지 않은 제품 및 기능을 온보딩할 수 있습니다.</li><li>숙련된 사용자는 AI Assistant를 사용하여 워크플로우를 차단할 수 있는 경계 사례를 해결할 수 있습니다. | <ul><li>여정 분석에서 대시보드를 설정하려면 어떻게 해야 합니까?</li><li>Real-Time CDP의 사용 사례를 알려 주십시오.</li></ul> |
| 문제 해결 | AI Assistant를 사용하여 워크플로우에서 발생할 수 있는 기본 오류를 디버깅하는 방법을 학습합니다. | <ul><li>이 오류는 무엇입니까? {ERROR_MESSAGE} 비열해?</li><li>&quot;Luma: 이메일 대상자&quot;라는 대상자를 삭제할 수 없는 이유는 무엇입니까?</li></ul> |
| 샌드박스 위생 | AI Assistant를 사용하여 중복 또는 사용하지 않는 오브젝트를 식별하면 샌드박스를 효율적으로 관리할 수 있습니다. | <ul><li>비슷한 관객들을 보여주실 수 있나요?</li><li>연관된 데이터 세트가 없는 스키마가 있습니까?</li></ul> |
| 값 분석 | AI Assistant를 사용하여 가장 많이 사용되는 데이터 객체를 식별하고 성능 지표를 평가하거나 가장 중요한 데이터 객체를 찾습니다. | <ul><li>Luma: 이메일 대상자 세그먼트 정의에 있는 프로필은 몇 개입니까?</li><li>대상이 언제 대상 Experience Cloud 대상으로 활성화되었습니까?</li></ul> |
| 검색 | AI 비서를 사용하여 대상, 데이터 세트, 대상, 스키마 및 소스와 같은 지원되는 Experience Platform 개체를 찾습니다. | <ul><li>지난 분기에 생성된 이름에 &quot;Luma&quot;가 포함된 대상을 나열합니다.</li><li>Luma: 사용자 지정 작업 XDM 스키마에는 어떤 속성이 있습니까?</li></ul> |
| 영향 분석 | AI Assistant를 사용하여 특정 워크플로우에서 사용된 데이터 객체를 식별하여 변경 사항의 영향을 평가할 수 있습니다. | <ul><li>대상이 사용하는 항목 `homeAddress.city` &quot;Luma: PersonProfiles&quot; 스키마에서?</li><li>은(는) 어떤 데이터 세트입니까? `consents.marketing.push.val` 프로필 속성이에 저장됩니까?</li></ul> |

{style="table-layout:auto"}

+++

### 오브젝트별로 그룹화된 질문 예 {#objects-questions}

+++AI Assistant가 제공하는 예제 질문 목록을 보려면 다음을 선택하십시오.

| 오브젝트 | 설명 |
| --- | --- |
| 대상 - 운영 통찰력 | <ul><li>다른 대상을 사용하는 대상</li><li>대상자 간 프로필 수 분포는 어떻게 됩니까?</li><li>이전에 마지막으로 수정한 대상자 표시 {RELATIVE_DATE}.</li><li>프로필이 0개인 대상자는 무엇입니까?</li><li>다음과 같음 {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} 다른 대상자에서 사용하시겠습니까?</li></ul> |
| 속성 - Operational insights | <ul><li>XDM 속성이 있는 대상 {ATTRIBUTE_PATH} 세그먼트 정의에?</li><li>대상에서 사용되지 않는 XDM 스키마 속성 수는?</li><li>XDM 속성이 있는 스키마 {ATTRIBUTE_PATH} 안에?</li><li>활성화된 XDM 속성은 무엇입니까?</li><li>프로필이 10개 이상인 대상자에서 사용되는 XDM 속성</li></ul> |
| 데이터 흐름 - Operational insights | <ul><li>데이터 흐름이 기여하는 항목 {DATASET_NAME} 데이터 세트?</li><li>사용되지 않거나 더 이상 데이터가 수신되지 않는 소스 데이터 흐름</li><li> |
| 데이터 세트 - 운영 통찰력 | <ul><li>동일한 스키마를 사용하여 수집된 데이터 세트 수는 얼마입니까?</li><li>연결된 소스 커넥터 {DATASET_NAME} 데이터 세트></li><li>각 대상자에서 사용되는 데이터 세트는 무엇입니까?</li><li>데이터 세트에서 사용되지 않는 스키마는 무엇입니까?</li><li>보유한 데이터 세트는 몇 개입니까?</li></ul> |
| 대상 - 운영 통찰력 | <ul><li>활성 상태인 대상은 무엇입니까?</li><li>0개의 대상이 활성화된 대상 계정은 무엇입니까?</li><li> |
| 여정 - 운영 통찰력 | <ul><li>나에게 여정이 몇 개나 있습니까?</li><li>생성된 여정 {RELATIVE_DATE} (예: 지난 주) 또는 {RELATIVE_DATE} (예: 특정 날짜 이전/이후/날짜)</li><li>수정된 여정 목록 표시 {RELATIVE_DATE} (예: 지난 주) 또는 {RELATIVE_DATE} (예: 특정 날짜 이전/이후/날짜)</li><li>내가 가진 여정을 나열합니다.</li><li>라이브 여정에 사용되는 대상자를 나열합니다.</li></ul> |
| 스키마 - 운영 통찰력 | <ul><li>어떤 스키마의 필드가 가장 많은 대상자에게 기여했습니까?</li><li>프로필이 활성화된 스키마는 몇 개입니까?</li><li>지난 주에 수정된 모든 스키마를 나열합니다.</li><li>데이터 세트에서 사용되지 않는 스키마는 무엇입니까?</li><li>지난 주에 생성된 모든 스키마를 나열합니다.</li></ul> |
| 소스 - Operational insights | <ul><li>활성 상태인 소스는 무엇입니까?</li><li>데이터 세트와 연결된 소스 커넥터 {DATASET_NAME}?</li><li>연결된 계정 수가 가장 많은 소스 커넥터는 무엇입니까?</li><li>데이터 흐름과 관련 소스 커넥터를 보여 줍니다.</li></ul> |
| 중요 학습 - 제품 지식(Real-Time CDP 및 Journey Optimizer) | <ul><li>AI 어시스턴트가 도울 수 있는 것은 무엇입니까?</li><li>유사 대상은 무엇입니까?</li><li>사용자 그룹은 역할과 어떻게 관련됩니까?</li><li>데이터 유형과 필드 그룹은 언제 사용해야 합니까?</li><li>ID와 기본 또는 외래 키 간의 차이점은 무엇입니까?</li><li>프로필 풍부성은 어떻게 계산됩니까?</li></ul> |
| 문제 해결 - 제품 지식(Real-Time CDP 및 Journey Optimizer) | <ul><li>AI 어시스턴트가 도울 수 있는 것은 무엇입니까?</li><li>데이터를 수집한 후 프로필 활성화 스키마를 삭제할 수 있습니까?</li><li>대상을 삭제할 수 없는 이유</li><li>대상을 평가하고 결과를 타겟팅할 수 있는 데 시간이 얼마나 걸립니까?</li></ul> |

{style="table-layout:auto"}

+++

## 질문 표현 {#phrasing-your-questions}

가능한 한 정확한 응답을 얻기 위해 명확성과 컨텍스트를 사용하여 AI Assistant에 질문을 구해야 합니다. 컨텍스트에 따라 명확한 질문을 하는 방법에 대한 지침은 다음 팁 목록을 참조하십시오.

* 작업 및/또는 질문을 간결하게 진술하십시오.
* 이해가 용이하도록 모호한 언어나 지나치게 복잡한 구문은 피한다.
* AI Assistant가 더 연관성 있는 응답을 생성하는 데 도움이 될 수 있으므로 작업 및/또는 질문에 대한 관련 컨텍스트를 제공합니다.

AI Assistant에 질문을 할 때 따라야 할 모범 사례에 대한 자세한 지침은 아래 표를 참조하십시오.

+++질문을 작성할 때 따라야 할 모범 사례의 예를 보려면 선택

| 실행 | 예 |
| --- | --- |
| <ul><li>검색하거나 분석할 개체 또는 정보에 대해 구체적으로 지정합니다.</li><li>데이터 개체 이름을 따옴표로 묶어 보십시오. 개체 이름의 일부만 알고 있는 경우에는 질문에 이를 지정할 수도 있습니다.</li><li>사용 [오브젝트 자동 완성](./ui-guide.md#use-auto-complete) ai Assistant가 쿼리 컨텍스트를 더 잘 이해할 수 있도록 도와줍니다.</li></ul> | <ul><li>어느 데이터 세트가 &quot;Luma - 충성도&quot; 스키마를 사용합니까?</li><li>이름에 &quot;Luma&quot;가 있는 활성화된 세그먼트를 표시합니다. 프로필 개수별로 등급을 지정합니다.</li></ul> |
| <ul><li>모호함을 피하고 명확한 언어 사용</li><li>쿼리의 명확성을 높이려면 정확한 용어를 사용하십시오.</li><li>Adobe Experience Platform 관련 질문을 할 때는 응답의 관련성을 개선하기 위해 Experience Platform 관련 용어를 사용하십시오.</li></ul> | <ul><li>ACME Audience에는 프로필이 몇 개 있습니까?</li><li>활성화된 대상자에 사용된 상위 5개의 XDM 속성을 표시합니다.</li></ul> |
| <ul><li>컨텍스트를 제공하거나 결과를 필터링할 기준을 지정하십시오.</li><li>질문의 필터 기준을 사용하여 응답의 데이터 볼륨을 제한합니다.</li></ul> | <ul><li>활성화되지 않았으며 6개월 이상 전에 만들어지고 수정한 적이 없는 대상을 표시합니다.</li><li>&quot;ACME 대상&quot;에 활성화되고 프로필이 10000개 이상 있는 대상자 표시</li></ul> |

{style="table-layout:auto"}

| 안 함 | 예 |
| --- | --- |
| 모호하거나 모호한 언어를 사용하십시오. | <ul><li>데이터 세트에 대한 정보를 제공합니다.</li><li>ACME Audience에는 사용자가 몇 명입니까?</li><li>세그먼트를 표시합니다.</li><li>목록 속성입니다.</li></ul> |
| 완료되지 않은 요청을 수행합니다. | &quot;Luma - 충성도 데이터 세트&quot; |
| 컨텍스트가 없는 지식을 가정하십시오. | <ul><li>지난 6개월 동안의 대상자입니다.</li><li>나를 위해 쿼리를 만듭니다.</li></ul> |
| 너무 복잡한 쿼리를 만듭니다. | 모든 객체와 해당 종속 항목에 대한 데이터 계보를 포괄적으로 분석할 수 있습니다. |
| 기준이나 매개 변수를 생략합니다. | 데이터 세트 표시 |

{style="table-layout:auto"}

+++

## 다음 단계

이제 AI Assistant에 대해 전반적으로 이해했으므로 워크플로우 동안 AI Assistant를 계속 사용하여 사용할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [AI Assistant UI 안내서](./ui-guide.md)
* [AI Assistant의 개인정보 보호, 보안 및 거버넌스](./privacy.md)
* [FAQ](./faq.md)