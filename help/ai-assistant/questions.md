---
title: AI Assistant 질문 안내서
description: AI Assistant를 쿼리할 때 사용할 수 있는 예제 질문에 대해 알려면 이 문서를 참조하십시오.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# AI Assistant 질문 안내서

AI Assistant를 쿼리할 때 사용할 수 있는 예제 질문 세트는에 대해 이 문서를 참조하십시오.

이 문서를 사용하여 다음에 대한 팁을 배울 수도 있습니다. [질문 문구 작성 방법](#phrasing-your-questions) 를 사용하면 AI Assistant에서 최적의 응답을 얻을 수 있습니다.

## 목표 기반 질문 {#objectives-questions}

다음 예제 질문은 AI Assistant를 사용할 때 달성할 수 있는 목표별로 그룹화됩니다.

| 목표 | 설명 | 예 |
| --- | --- | --- |
| 학습 개념 및 지속적인 워크플로 | <ul><li>초보 사용자는 AI Assistant를 사용하여 Real-Time CDP 및 Adobe Journey Optimizer 개념을 학습하고 익숙하지 않은 제품 및 기능을 온보딩할 수 있습니다.</li><li>숙련된 사용자는 AI Assistant를 사용하여 워크플로우를 차단할 수 있는 경계 사례를 해결할 수 있습니다. | <ul><li>여정 분석에서 대시보드를 설정하려면 어떻게 해야 합니까?</li><li>Real-Time CDP의 사용 사례를 알려 주십시오.</li></ul> |
| 문제 해결 | AI Assistant를 사용하여 워크플로우에서 발생할 수 있는 기본 오류를 디버깅하는 방법을 학습합니다. | <ul><li>이 오류는 무엇입니까? {ERROR_MESSAGE} 비열해?</li><li>&quot;Luma: 이메일 대상자&quot;라는 대상자를 삭제할 수 없는 이유는 무엇입니까?</li></ul> |
| 샌드박스 위생 | AI Assistant를 사용하여 중복 또는 사용하지 않는 오브젝트를 식별하면 샌드박스를 효율적으로 관리할 수 있습니다. | <ul><li>비슷한 관객들을 보여주실 수 있나요?</li><li>연관된 데이터 세트가 없는 스키마가 있습니까?</li></ul> |
| 값 분석 | AI Assistant를 사용하여 가장 많이 사용되는 데이터 객체를 식별하고 성능 지표를 평가하거나 가장 중요한 데이터 객체를 찾습니다. | <ul><li>Luma: 이메일 대상자 세그먼트 정의에 있는 프로필은 몇 개입니까?</li><li>대상이 언제 대상 Experience Cloud 대상으로 활성화되었습니까?</li></ul> |
| 검색 | AI 비서를 사용하여 대상, 데이터 세트, 대상, 스키마 및 소스와 같은 지원되는 Experience Platform 개체를 찾습니다. | <ul><li>지난 분기에 생성된 이름에 &quot;Luma&quot;가 포함된 대상을 나열합니다.</li><li>Luma: 사용자 지정 작업 XDM 스키마에는 어떤 속성이 있습니까?</li></ul> |
| 영향 분석 | AI Assistant를 사용하여 특정 워크플로우에서 사용된 데이터 객체를 식별하여 변경 사항의 영향을 평가할 수 있습니다. | <ul><li>대상이 사용하는 항목 `homeAddress.city` &quot;Luma: PersonProfiles&quot; 스키마에서?</li><li>은(는) 어떤 데이터 세트입니까? `consents.marketing.push.val` 프로필 속성이에 저장됩니까?</li></ul> |

{style="table-layout:auto"}

## 엔티티별 운영 통찰력 및 제품 지식 질문{#objects-questions}

다음 질문은 데이터 객체별로 그룹화되며 다음 중 하나로 분류됩니다 [운영 통찰력](./home.md#operational-insights) 또는 [제품 지식](./home.md#product-knowledge).

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

## 질문 표현 {#phrasing-your-questions}

가능한 한 정확한 응답을 얻기 위해 명확성과 컨텍스트를 사용하여 AI Assistant에 질문을 구해야 합니다. 컨텍스트에 따라 명확한 질문을 하는 방법에 대한 지침은 다음 팁 목록을 참조하십시오.

* 작업 및/또는 질문을 간결하게 진술하십시오.
* 이해가 용이하도록 모호한 언어나 지나치게 복잡한 구문은 피한다.
* AI Assistant가 더 연관성 있는 응답을 생성하는 데 도움이 될 수 있으므로 작업 및/또는 질문에 대한 관련 컨텍스트를 제공합니다.

AI Assistant에 질문을 할 때 따라야 할 모범 사례에 대한 자세한 지침은 아래 표를 참조하십시오.

다음 표에서는 AI Assistant 사용 시 따를 수 있는 모범 사례에 대해 간략히 설명합니다.

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

## 다음 단계

이제 이 문서를 읽고 AI Assistant에 대한 질문을 최적화하는 방법에 대해 이해할 수 있습니다. 워크플로우 중에 기능을 사용하는 방법에 대한 자세한 내용은 [AI Assistant UI 안내서](ui-guide.md).
