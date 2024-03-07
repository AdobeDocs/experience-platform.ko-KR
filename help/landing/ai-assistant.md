---
title: Adobe Experience Platform용 AI Assistant
description: AI Assistant를 사용하여 Experience Platform 및 Real-time Customer Data Platform 개념과 객체에 대한 사용 정보를 탐색하고 이해하는 방법에 대해 알아봅니다.
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: b1f2d85f5a1cf6bb38344c87496488a919800029
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 0%

---

# Adobe Experience Platform용 AI Assistant

>[!NOTE]
>
> Adobe Experience Platform용 AI Assistant는 현재 Alpha 중입니다. 기능 및 설명서는 변경될 수 있습니다.

AI Assistant는 Adobe Experience Platform 및 Real-time Customer Data Platform 개념과 객체에 대한 사용 정보를 탐색하고 이해하는 데 사용할 수 있는 UI 기능입니다.

AI Assistant에 다음과 같은 정보를 쿼리할 수 있습니다.

* 데이터 및 대상과 관련된 작업을 수행하는 방법에 대한 지침입니다.
* 조직 내 기존 데이터 객체의 상태 및 지표.
* 속성, 데이터 흐름, 데이터 세트, 대상, 스키마, 세그먼트 및 소스를 비롯한 데이터 개체를 더 잘 이해하려면 사례 예제와 뉘앙스를 사용하십시오.

아래 안내서를 읽고 AI Assistant를 사용하여 Experience Platform 및 Real-Time CDP 워크플로를 탐색하고 이해하는 방법에 대해 알아보십시오.

>[!BEGINSHADEBOX]

**AI 어시스턴트는 어떻게 작동합니까?**

AI Assistant는 데이터베이스에 질의한 다음 데이터베이스의 데이터를 사람이 읽을 수 있는 답변으로 변환하여 제출된 질문에 응답합니다.

기본 데이터에 대한 이러한 내부 표현은 지식 그래프라고도 하며, 지정된 질문에 대한 개념, 데이터 및 메타데이터의 포괄적인 웹입니다.

지식 그래프는 쿼리가 제출될 때마다 참조되는 하위 그래프로 구성됩니다.

* 고객 사용 데이터.
* 다양한 메타 스토어에서 고객 사용 데이터.
* Experience League 설명서입니다.

AI Assistant를 쿼리하기 전에 고려해야 할 두 가지 유형의 질문이 있습니다.

* **개념 질문**: 개념 질문은 데이터 또는 대상과 관련된 Adobe 개념에 대한 것입니다. 개념 질문의 몇 가지 예는 다음과 같습니다.
   * 일괄 처리와 스트리밍 세분화 간의 차이점은 무엇입니까?
   * 업계 데이터 모델이 있습니까? 그리고 어떻게 사용해야 합니까?
   * Real-Time CDP의 가장 좋은 용도는 무엇입니까?
* **사용 질문**: 사용 질문은 조직 내의 데이터 개체에 대한 것입니다. 사용 관련 질문의 몇 가지 예는 다음과 같습니다.
   * 보유한 데이터 세트는 몇 개입니까?
   * 사용된 적이 없는 스키마 속성 수는 몇 개입니까?
   * 활성화된 세그먼트

>[!ENDSHADEBOX]

## AI Assistant를 통해 달성할 수 있는 목표

다음과 같은 목표에 AI Assistant를 사용할 수 있습니다.

| 목표 | 설명 |
| --- | --- |
| 학습 Experience Platform 및 Real-Time CDP 개념 | Experience Platform 및 Real-Time CDP에 온보딩할 수 있도록 AI Assistant 개념 질문을 할 수 있습니다. AI Assistant를 사용하여 익숙하지 않은 객체와 행동에 대해 학습할 수도 있습니다. |
| 샌드박스 내 데이터 청결 보장 | AI Assistant를 사용하여 중복 또는 사용하지 않는 객체를 식별하여 샌드박스의 청정도를 효율적으로 관리할 수 있습니다. |
| 값 분석 오케스트레이션 | AI Assistant를 사용하여 가장 많이 사용되는 객체를 식별하고 성능 지표를 평가하거나 가장 중요한 데이터를 찾을 수 있습니다. |
| 영향 분석 이해 | AI Assistant를 사용하여 특정 워크플로우에서 사용된 객체를 식별하여 변경 사항의 영향을 평가할 수 있습니다. |
| 데이터 모니터링 | AI Assistant를 사용하여 데이터 흐름, 수집 또는 평가 작업을 모니터링하여 불일치를 보거나 진행 상황을 보고할 수 있습니다. |

## Experience Platform UI에서 AI 지원에 액세스

AI Assistant를 실행하려면 **[!UICONTROL AI Assistant 아이콘]** Experience Platform UI의 상단 헤더에서

![AI Assistant 아이콘이 선택되고 AI Assistant 인터페이스가 열린 Experience Platform 홈 페이지.](./images/ai-assistant/ai-assistant.png)

AI Assistant 인터페이스가 나타나고 시작하기 위한 정보가 즉시 제공됩니다. 아래에 제공된 옵션을 사용할 수 있습니다. [!UICONTROL 시작하기 위한 아이디어] 다음과 같은 질문과 명령에 답변하려면

* [!UICONTROL 내 세그먼트 중 어떤 세그먼트가 활성화됩니까?]
* [!UICONTROL 스키마란?]
* [!UICONTROL Real-Time CDP의 일반적인 사용 사례 설명]

![AI Assistant의 &quot;시작하기 위한 아이디어&quot; 섹션.](./images/ai-assistant/ideas-to-get-started.png)

AI Assistant와 상호 작용하려면 입력 상자를 사용하여 쿼리 또는 명령을 입력합니다. (**`+`**) 자동 완성 기능과 책갈피 아이콘을 사용하여 책갈피가 지정된 쿼리 및 명령에 액세스할 수 있는 기호를 제공합니다.

![AI Assistant 입력 상자가 강조 표시됩니다.](./images/ai-assistant/interact.png)

## 사용 사례 예: AI Assistant를 사용하여 스키마 생성 프로세스 가속화

>[!NOTE]
>
>다음 워크플로우는 경험 이벤트 스키마 생성 프로세스를 사용하여 Experience Platform UI 사용 시 AI Assistant를 사용하는 방법을 보여 주는 예제입니다.

를 만드는 사용 사례를 고려하십시오. **이벤트 스키마의 디바이스 거래**. 경험 이벤트 스키마 생성 프로세스 중에 `eventType` 필드. &quot;이 시점에서 워크플로를 종료하고 [스키마 컴포지션 기본 사항](../xdm/schema/composition.md) 설명서 또는 AI Assistant를 사용하여 질문에 대한 답변을 검색하고 AI Assistant에서 권장하는 설명서 링크를 통해 추가 리소스를 찾을 수 있습니다.&quot;

시작하려면 제공된 텍스트 상자에 질문을 입력합니다. 아래 예제에서 AI 도우미에게 &quot; 라는 질문이 제공됩니다.**ExperienceEvent 스키마의 eventType 필드는 무엇입니까?**&quot;

![다음 질문이 있는 Experience Platform AI 비서: &quot;ExperienceEvent 스키마의 eventType 필드는 무엇입니까?](./images/ai-assistant/question.png)

그런 다음 AI Assistant는 기술 자료를 쿼리하고 답을 계산합니다. 잠시 후 AI 도우미가 후속 프롬프트로 사용할 수 있는 답변 및 관련 제안을 반환합니다.

![이전 쿼리에 대한 답변이 있는 Experience Platform AI 지원.](./images/ai-assistant/answer.png)

AI Assistant로부터 응답을 받은 후 여러 옵션 중에서 선택하여 진행할 방법을 결정할 수 있습니다.

### 쿼리 저장 {#save-your-query}

+++쿼리 저장 방법의 예를 보려면 선택

쿼리를 저장하려면 질문 옆에 있는 책갈피 아이콘을 선택합니다.

![선택한 책갈피의 스크린샷입니다.](./images/ai-assistant/save-your-query.png)

저장된 쿼리에 액세스하려면 입력 상자 아래의 책갈피 아이콘을 선택한 다음 실행할 쿼리를 선택합니다.

![책갈피 아이콘 및 저장된 쿼리 목록의 스크린샷입니다.](./images/ai-assistant/bookmarks.png)

+++

### 샌드박스에서 데이터 보기 {#view-data-in-your-sandbox}

+++예를 보려면 선택

쿼리에 따라 AI Assistant는 샌드박스의 데이터와 관련된 추가 정보를 제공합니다. 쿼리에 대한 응답이 샌드박스에 어떻게 적용되는지 보려면 을 선택합니다. **[!UICONTROL 샌드박스에서].**

이 단계에서 AI 도우미는 해당 특정 오브젝트의 UI 페이지로 직접 연결되는 링크를 제공할 수 있습니다. 아래 예에서 AI 어시스턴트는 [!UICONTROL 스키마] 및 [!UICONTROL 세그먼트] UI 페이지.

![&quot;샌드박스에서&quot; 옵션의 스크린샷입니다.](./images/ai-assistant/in-your-sandbox.png)

+++

### 응답 확인 {#verify-the-response}

+++소스 표시 방법의 예를 보려면 선택

인용을 보고 AI Assistant의 응답을 확인하려면 다음을 선택합니다. **[!UICONTROL 소스 표시]**. AI Assistant는 해당 응답을 확증하는 설명서에 대한 링크를 제공합니다. AI Assistant에서 제공하는 쿼리를 사용할 수도 있습니다 [!UICONTROL 관련 제안] 원본 쿼리와 관련된 항목을 더 자세히 살펴보십시오.

![&quot;소스 표시&quot;의 스크린샷.](./images/ai-assistant/show-sources.png)

+++

### 데이터 사용 및 시각화 {#data-usage-and-visualization}

+++데이터 사용 질문 및 데이터 시각화의 예를 보려면 선택

AI Assistant가 조직 내 데이터 사용에 대한 쿼리에 응답하려면 활성 샌드박스에 있어야 합니다.

아래 예에서는 AI Assistant에 다음 쿼리가 제공됩니다. **&quot;1000개 이상의 프로필이 있는 세그먼트 정의를 표시하고 활성화 상태를 포함합니다.&quot;** 그런 다음 AI Assistant가 세그먼트 및 프로필 데이터를 시각화하는 차트로 응답합니다.

![데이터 사용에 대한 추가 질문입니다.](./images/ai-assistant/data-usage-question.png)

개별 막대에 마우스를 가져다 대면 특정 데이터를 볼 수 있습니다. 확장 아이콘을 선택하여 차트를 더 크게 볼 수도 있습니다.

![데이터 시각화를 보여 주는 후속 질문입니다.](./images/ai-assistant/data-visualization.png)

시각화의 확장된 보기가 나타납니다. 확장된 모달을 사용하여 데이터를 추가로 검사할 수 있으며, 시각화가 많은 열을 반환할 때 특히 유용합니다.

![확장된 차트입니다.](./images/ai-assistant/chart-expanded.png)

데이터 사용 질문을 묻는 메시지가 뜨면 AI 어시스턴트가 답을 계산하는 방식에 대한 설명을 제공한다. 아래 예에서 AI Assistant는 1000개 이상의 프로필이 있는 세그먼트 정의와 각각의 활성화 상태를 표시하기 위해 수행한 단계를 간략하게 설명합니다.

![AI Assistant가 응답을 계산한 방법을 보여 주는 세그먼트에 대한 후속 질문입니다.](./images/ai-assistant/results-explained.png)

쿼리에 필터 및 수정 사항을 제공할 수도 있으며, 포함하는 필터를 기반으로 검색 결과를 렌더링하도록 AI Assistant에 지시할 수 있습니다. 예를 들어, AI Assistant에 카운트 세그먼트 정의의 추세를 생성 날짜 순서로 표시하도록 요청하고, 합계 프로필이 0인 세그먼트 정의를 제거하고, 데이터를 표시할 때 정수 대신 월 이름을 사용할 수 있습니다.

+++

### 자동 완성 사용 {#use-auto-complete}

+++자동 완성의 예를 보려면 선택

자동 완성 기능을 사용하여 샌드박스에 있는 데이터 객체 목록을 수신할 수 있습니다. 세그먼트, 스키마, 데이터 세트, 소스 및 대상 도메인에서 자동 완성 권장 사항을 사용할 수 있습니다.

더하기 기호()를 포함하여 자동 완성을 사용할 수 있습니다&#x200B;**`+`**)을 클릭하여 검색할 수 있습니다. 또는 더하기 기호(**`+`**)를 입력합니다. 샌드박스의 권장 데이터 개체 목록이 표시된 창이 나타납니다.

![자동 완성의 예](./images/ai-assistant/auto-complete-one.png)

그런 다음 쿼리할 데이터 개체를 선택하여 질문을 완료한 다음 질문을 제출합니다.

![질문 및 답변이 포함된 자동 완성의 예](./images/ai-assistant/auto-complete-two.png)

+++

### 멀티턴 사용 {#use-multi-turn}

+++다중 회전의 예를 보려면 선택

AI 어시스턴트의 멀티턴 기능을 활용해 경험 중 보다 자연스러운 대화가 가능하다. 주어진 후속 질문에 AI 비서가 답변할 수 있습니다. 그 맥락은 이전의 상호 작용으로부터 추론될 수 있다.

아래 예에서는 AI Assistant에 현재 조직의 총 데이터 흐름 수가 요청되었습니다.

![다중 회전의 예](./images/ai-assistant/multi-turn-one.png)

다음으로 AI 어시스턴트가 또 다른 후속 요청을 받는다. 이번에는 AI 도우미가 조직에 현재 존재하는 데이터 흐름을 나열하여 응답합니다.

![질문과 대답이 있는 다중 회전의 예](./images/ai-assistant/multi-turn-two.png)

+++

## 설명서 {#documentation}

현재 설명서 색인은 Adobe Experience Platform(Real-Time CDP 및 대상)를 포함합니다. 색인은 정기적으로 업데이트됩니다.

설명서 검색 모델은 Experience Platform(Real-Time CDP 및 대상)에 대해 교육됩니다. Adobe Target 및 Creative Cloud 세트와 같은 Adobe Experience PlatformAdobe 의 범위를 벗어난 질문에 대해서는 답변할 수 없습니다.

## 데이터 사용 {#data-usage}

또한 다음 도메인에서 데이터 사용에 대해 AI Assistant에 질문할 수 있습니다.

* 속성
* 데이터 흐름
* 데이터 세트
* 대상 _(계정에 대한 질문과 데이터 흐름에 대한 일부 질문은 현재 답변할 수 없습니다.)_
* 스키마 _(필드 그룹에 대한 질문에 지금은 답변할 수 없습니다.)_
* 세그먼트
* 소스 _(현재 계정에 대한 질문에 답변할 수 없습니다.)_

사용 데이터 쿼리의 경우, 답변이 UI의 현재 상태를 반영하지 않을 수 있습니다. 이러한 질문에 대한 데이터는 24시간마다 한 번씩 업데이트됩니다. 예를 들어 사용자가 낮에 Real-Time CDP에서 수행하는 변경 사항은 밤에 데이터 스토어와 동기화된 다음 아침에 사용자 질문에 대해 사용할 수 있게 됩니다. 질문의 서식을 다음과 같이 지정해야 할 수 있습니다. &quot;제목이 있는 세그먼트는 언제입니까? {TITLE} 생성됨?&quot; 대신, &quot;언제 {TITLE} 세그먼트를 만들었습니까?&quot;

스키마, 데이터 세트, 속성, 대상 및 세그먼트와 같은 객체와 관련된 특정 데이터를 조회하려면 샌드박스에 로그인해야 합니다.

### 데이터 사용 질문 예 {#example-data-usage-questions}

+++예제 데이터 사용 질문 목록을 보려면 선택

| 질문 유형 | 설명 | 예시 |
| --- | --- | --- | 
| 데이터 계보 | 다른 Experience Platform 오브젝트에서 하나 이상의 오브젝트 사용 추적 | <ul><li>사용 데이터 세트 {SCHEMA_NAME} 스키마?</li><li>동일한 스키마를 사용하여 수집된 데이터 세트 수는 얼마입니까?</li><li>활성화된 세그먼트에서 사용된 데이터 세트</li><li>활성화된 세그먼트에 사용된 속성이 있는 스키마를 나열합니다.</li><li>활성화된 세그먼트 표시 {DESTINATION_ACCOUNT_NAME} 와 에는 1000개 이상의 프로필이 있습니다.</li><li>2023년 1월 이후에 수정된 활성화된 세그먼트에 사용되는 속성을 표시합니다.</li><li>을 통해 수집된 데이터 세트 {SOURCE_NAME}?</li><li>연계된 데이터 흐름 {DATAFLOW_NAME}</li><li>활성화된 세그먼트와 관련되고 지난 1년 동안 생성된 스키마를 나열합니다.</li></ul> |
| 배포 및 집계 | Experience Platform 개체 사용에 대한 요약 기반 질문 | <ul><li>활성화된 세그먼트의 비율은 얼마입니까?</li><li>세분화에는 몇 개의 필드가 사용됩니까?</li><li>가장 많은 대상에 활성화된 세그먼트는 무엇입니까?</li><li>중복 세그먼트를 나열합니다.</li><li>활성화된 세그먼트 표시 {DESTINATION_ACCOUNT_NAME} 프로필 크기별로 등급을 매깁니다.</li><li>활성화되지 않았지만 프로필이 100개를 초과하는 세그먼트의 백분율입니다. 그들의 이름을 보여줘</li><li>내 데이터 세트로 데이터를 수집하는 3개의 소스 커넥터를 나열합니다.</li><li>발생에 따라 활성화된 세그먼트에 사용된 상위 5개 속성을 나열합니다.</li></ul> |
| 오브젝트 조회 | Experience Platform 개체 또는 해당 속성을 검색하거나 액세스합니다. | <ul><li>연관된 스키마가 없는 데이터 세트</li><li>에 사용된 속성 나열 {SEGMENT_NAME}?</li><li>프로필이 활성화되었지만 생성 이후 수정되지 않은 스키마 목록을 제공합니다.</li><li>지난 주에 수정된 세그먼트는 무엇입니까?</li><li>세그먼트 정의가 같은 세그먼트를 만든 날짜와 함께 나열합니다.</li><li>프로필이 활성화된 데이터 세트이며 각 데이터 세트에서 생성된 세그먼트 수를 포함합니다.</li><li>데이터 세트 XYZ와 연관된 소스 계정은 무엇입니까?</li><li>다음의 세그먼트 정의 및 수정 날짜 표시 {SEGMENT_NAME}.</li></ul> |

+++

## 피드백 제공 {#feedback}

>[!BEGINSHADEBOX]

**피드백이 요청되었습니다.**

이 Alpha 단계에서 AI Assistant로부터 받은 응답에 대한 피드백을 제공할 수 있습니다. AI Assistant 경험을 지속적으로 개선하기 위해 모든 응답 및 제출된 피드백을 검토합니다.

피드백을 제공하려면 AI Assistant의 응답을 받은 후 엄지손가락을 위로 또는 아래로 선택한 다음 제공된 텍스트 상자에 피드백을 입력합니다. 그런 다음 을 선택합니다. **[!UICONTROL 피드백 제출]** 제출합니다.

>[!ENDSHADEBOX]

+++피드백 제공

>[!BEGINTABS]

>[!TAB 엄지 손가락 위로]

썸네일 위로 아이콘을 선택하여 AI 어시스턴트와 함께 경험한 것에 대한 피드백을 제공합니다.

![긍정적인 피드백 창.](./images/ai-assistant/thumbs-up.png)

>[!TAB 엄지 손가락 아래로]

썸네일 아래쪽 아이콘을 선택하여 AI Assistant에 대한 경험을 기반으로 개선될 수 있는 사항에 대한 피드백을 제공합니다. 이 단계에서 경험에 대한 특정 설명을 제공할 수도 있습니다. 의견에 제공된 피드백은 매일 검토됩니다.

![부정적 피드백 창.](./images/ai-assistant/thumbs-down.png)

>[!TAB 플래그]

플래그 아이콘을 선택하여 AI Assistant를 사용한 사용자 경험에 대한 추가 보고서를 제공합니다.

![보고서 결과 창.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## 추가 정보 {#additional-information}

AI Assistant for Experience Platform에 대한 자세한 내용은 이 섹션 을 참조하십시오.

### 주의 사항 및 제한 사항 {#caveats-and-limitations}

다음 섹션에서는 AI Assistant 사용 시 고려해야 할 현재 주의 사항 및 제한 사항에 대해 간략히 설명합니다.
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the AI Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The AI Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The AI Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The AI Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The AI Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The AI Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The AI Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the AI Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The AI Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The AI Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the AI Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the AI Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### 제한된 잡담

AI Assistant를 사용하여 잡담도 할 수 있지만 이 용량은 현재 제한적입니다.

#### 기능 질문

AI 도우미가 수행할 수 있는 작업에 대해 부정확한 인상을 줄 수 있습니다. 다음 유형의 질문에 잘못 답변할 수 있습니다.

| 예제 질문 | 참고 |
| --- | --- |
| &quot;다음 질문에 답변할 수 있습니까? {ENTITY}?&quot; | AI 도우미가 색인에서 지정된 엔티티를 참조하는 단일 페이지를 찾을 수 있는 한 예 로 응답합니다. |
| &quot;혹시... **x** 언어?&quot; | AI 어시스턴트는 현재 영어만 지원하지만, 기본 모델이 지원할 수 있어 &#39;예&#39;라고 답할 수도 있다. |
| &quot;할 수 있어?&quot; | AI 도우미가 아니더라도 예라고 답할 수 있습니다. |

### 팁 {#tips}

다음 섹션에서는 AI Assistant 사용 시 고려해야 할 몇 가지 팁과 해결 방법에 대해 간략하게 설명합니다.

#### 잘못된 정보 출처로 질문에 대한 응답이 있을 수 있습니다

사용 데이터에 대한 질문이 설명서를 기반으로 답변을 도출하는 경우가 있습니다. AI 어시스턴트가 질문을 잘못된 정보 소스로 잘못 라우팅할 수 있기 때문이다. 다음을 수행하여 이를 방지할 수 있습니다.

* 더 많은 SQL 유사 언어를 사용하도록 질문 구문 변경
* 사용할 정보 소스를 명시적으로 호출합니다.

예를 보려면 아래 표를 참조하십시오.

| 나쁜 질문 | 좋은 질문 | 참고 |
| --- | --- | --- |
| 가장 큰 세그먼트는 무엇입니까? | 가장 큰 세그먼트는 무엇입니까? 데이터 사용. | 답변이 데이터를 기반으로 하도록 AI 도우미에 명시적으로 지시합니다. |
| 가장 큰 세그먼트는 무엇입니까? | 내 가장 큰 세그먼트를 나열합니다. | &quot;...&quot;라는 질문이 문서 기반 질문으로 오인될 수 있는 경우가 있습니다. &quot;list&quot;와 같은 명령을 사용하는 것은 컨텍스트에 있는 데이터로 질문을 하는 것이 더 강력합니다. |
| 보유한 데이터 세트는 몇 개입니까? | 내 데이터 세트를 카운트합니다. | 원래 질문은 세그먼트에 대해 작동하지만 데이터 세트에서는 작동하지 않을 수 있습니다. |
