---
title: Adobe Experience Platform용 AI Assistant
description: AI Assistant를 사용하여 Experience Platform 및 Real-time Customer Data Platform 개념과 객체에 대한 사용 정보를 탐색하고 이해하는 방법에 대해 알아봅니다.
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: ca606e4e29f4ba1df281f47a86b4e3cfa850ae35
workflow-type: tm+mt
source-wordcount: '2627'
ht-degree: 0%

---

# Adobe Experience Platform용 AI Assistant

>[!NOTE]
>
>Adobe Experience Platform용 AI Assistant는 현재 Alpha에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

Adobe Experience Platform용 AI 지원 기능은 Experience Platform 및 Real-time Customer Data Platform 개념과 개체에 대한 사용 정보를 탐색하고 이해하는 데 사용할 수 있는 UI 기능입니다.

AI Assistant를 질의하여 다음과 같은 정보를 얻을 수 있습니다.

* 데이터 및 대상과 관련된 작업을 수행하는 방법에 대한 지침입니다.
* 조직 내 기존 데이터 객체의 상태 및 지표.
* 속성, 데이터 세트, 대상, 스키마, 세그먼트 및 소스를 비롯한 데이터 개체를 더 잘 이해하려면 사례 예제와 뉘앙스를 사용하십시오.

이 문서에서는 AI Assistant에 액세스하고 이를 사용하여 Experience Platform 및 Real-Time CDP 개념에 대한 질문을 하고 답변을 받는 방법에 대해 설명합니다.

>[!BEGINSHADEBOX]

**AI 어시스턴트는 어떻게 작동합니까?**

AI Assistant는 데이터베이스를 쿼리한 다음 데이터베이스의 데이터를 사람이 읽을 수 있는 답변으로 변환하여 제출된 질문에 응답합니다.

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

## UI에서 Experience Platform을 위해 AI Assistant에 액세스

Experience Platform UI의 헤더 탐색에서 AI Assistant에 액세스할 수 있습니다.

다음 항목 선택 **[!UICONTROL AI Assistant 아이콘]** 헤더에서 AI 도우미 패널을 시작합니다.

![AI Assistant 아이콘이 선택된 Experience Platform UI 홈 페이지입니다.](./images/ai-assistant/ai-assistant.png)

여기에서 텍스트 상자에 질문을 입력하고 AI Assistant에 데이터 또는 대상자에 대한 개념을 쿼리할 수 있습니다. 각 사용 사례에서 데이터 개체를 사용하는 방법을 더 잘 이해하기 위해 데이터 개체에 대한 질문을 할 수도 있습니다.

### 예제 사용 사례: AI Assistant를 사용하여 스키마 생성 프로세스를 신속하게 진행합니다

>[!NOTE]
>
>다음 예제 워크플로에서는 ExperienceEvent 스키마 생성 프로세스를 사용하여 Experience Platform UI 사용 시 AI Assistant를 사용하는 방법을 보여 줍니다.

를 만드는 사용 사례를 고려하십시오. **이벤트 스키마의 디바이스 거래**. ExperienceEvent 스키마 생성 프로세스 중에 `eventType` 필드. 이 시점에서 워크플로우를 종료하고 의 설명서를 참조할 수 있습니다. [스키마 컴포지션 기본 사항](../xdm/schema/composition.md)또는 AI Assistant를 사용하여 질문에 대한 즉각적인 답변을 검색할 수 있습니다.

시작하려면 제공된 텍스트 상자에 질문을 입력합니다. 아래 예제에서 AI 도우미에게 &quot; 라는 질문이 제공됩니다.**경험 이벤트 스키마의 eventType 필드는 무엇입니까?**&quot;

![다음 질문이 있는 Experience Platform AI 비서: &quot;ExperienceEvent 스키마의 eventType 필드는 무엇입니까?](./images/ai-assistant/question.png)

그런 다음 AI Assistant가 기술 자료를 쿼리하고 답을 계산합니다. 잠시 후 AI 도우미가 후속 프롬프트로 사용할 수 있는 답변 및 관련 제안을 반환합니다.

![이전 쿼리에 대한 답변이 있는 Experience Platform AI 지원 .](./images/ai-assistant/answer.png)

후속 질문을 통해 특정 주제에 대해 자세히 알아볼 수 있습니다. 다음 예에서는 AI Assistant에 eventType을 세그먼테이션에서 사용할 수 있는 방법을 묻습니다.

![Experience Platform을 위한 AI Assistant에 표시되는 후속 질문 및 답변입니다.](./images/ai-assistant/follow-up-answer.png)

데이터 사용과 관련하여 AI Assistant에 질문을 할 수도 있습니다. 데이터 사용에 대해 문의할 때 AI Assistant가 질문에 답변하도록 하려면 활성 샌드박스에 있어야 합니다.

![사용자에게 있는 세그먼트 수를 묻는 데이터 사용 질문입니다.](./images/ai-assistant/data-usage-question.png)

AI 도우미가 모든 질문에 대한 답변을 제공하므로 소스를 보고 답변을 검증할 수 있습니다. 개념 질문에는 설명서 링크가 제공되며, 답변이 계산된 방식을 보여 주는 SQL 쿼리를 통해 데이터 사용 질문을 확인할 수 있습니다.

>[!BEGINSHADEBOX]

**피드백이 요청되었습니다.**

이 알파 단계 동안 AI 어시스턴트에서 받은 응답에 대한 피드백을 제공할 수 있습니다. AI Assistant 경험을 지속적으로 개선하기 위해 모든 응답 및 제출된 피드백을 검토합니다.

피드백을 제공하려면 AI Assistant의 응답을 받은 후 엄지손가락을 위로 또는 아래로 선택한 다음 제공된 텍스트 상자에 피드백을 입력합니다. 그런 다음 을 선택합니다. **[!UICONTROL 피드백 제출]** 제출합니다.

>[!ENDSHADEBOX]

>[!BEGINTABS]

>[!TAB 소스 표시]

선택 **[!UICONTROL 소스 표시]** AI Assistant가 응답을 계산하기 위해 참조하는 설명서에 대한 링크 목록.

![AI Assistant에 표시되는 소스에 대한 링크입니다.](./images/ai-assistant/show-sources.png)

>[!TAB 엄지 손가락 위로]

썸네일 위로 아이콘을 선택하여 AI 어시스턴트와 함께 경험한 것에 대한 피드백을 제공합니다.

![긍정적인 피드백 창.](./images/ai-assistant/positive-feedback.png)

>[!TAB 엄지 손가락 아래로]

썸네일 아래쪽 아이콘을 선택하여 AI Assistant에 대한 경험을 기반으로 개선될 수 있는 사항에 대한 피드백을 제공합니다. 이 단계에서 경험에 대한 특정 설명을 제공할 수도 있습니다. 의견에 제공된 피드백은 매일 검토됩니다.

![부정적 피드백 창.](./images/ai-assistant/negative-feedback.png)

>[!TAB 플래그]

플래그 아이콘을 선택하여 AI Assistant를 사용한 사용자 경험에 대한 추가 보고서를 제공합니다.

![보고서 결과 창.](./images/ai-assistant/report-results.png)

>[!ENDTABS]

### 시작하기 위한 아이디어

시작하려면 AI Assistant가 제공하는 사전 설정 프롬프트를 사용할 수도 있습니다.

![AI 지원 패널에 메시지가 표시됩니다.](./images/ai-assistant/ideas.png)

## 추가 정보

AI Assistant for Experience Platform에 대한 자세한 내용은 이 섹션 을 참조하십시오.

### 범위

AI Assistant는 설명서 및 데이터 사용량을 기반으로 쿼리에 응답할 수 있습니다.

#### 설명서

Real-time Customer Data Platform 및 대상 을 기반으로 설명서 질문을 할 수 있습니다. 현재 설명서 색인은 Adobe Experience Platform(Real-Time CDP 및 대상)를 포함합니다. 색인은 정기적으로 업데이트됩니다.

설명서 검색 모델은 Experience Platform(Real-Time CDP 및 대상)에 대해 교육됩니다. Adobe Target 및 Creative Cloud 세트와 같은 Adobe Experience PlatformAdobe 의 범위를 벗어난 질문에 대해서는 답변할 수 없습니다.

#### 데이터 사용

또한 다음 도메인에서 데이터 사용에 대해 AI Assistant에 질문할 수 있습니다.

* 속성
* 데이터 세트
* 대상
* 스키마
* 세그먼트
* 소스

사용 데이터 쿼리의 경우, 답변이 UI의 현재 상태를 반영하지 않을 수 있습니다. 이러한 질문에 대한 데이터는 12~24시간마다 업데이트됩니다. 다음과 같은 질문의 형식을 지정해야 할 수 있습니다. &quot;제목이 있는 세그먼트는 언제입니까? {TITLE} 생성됨?&quot; 대신, &quot;언제 {TITLE} 세그먼트를 만들었습니까?&quot;

스키마, 데이터 세트, 속성, 대상 및 세그먼트와 같은 객체와 관련된 특정 데이터를 조회하려면 샌드박스에 로그인해야 합니다.

+++지원되는 데이터 사용 질문 목록을 보려면 선택

다음은 도메인별로 그룹화된 현재 지원되는 데이터 사용 질문 목록입니다.

>[!BEGINTABS]

>[!TAB 세그먼트]

* 중복 세그먼트가 있습니까?
* 모든 스트리밍 세그먼트를 표시합니다.
* 세그먼트 이름이 임 {SEGMENT_ID} 일괄 처리 또는 스트림에서 평가됩니까?
* 중복 세그먼트는 무엇입니까?
* 총 몇 개의 세그먼트가 있습니까?
* 이름은 같지만 ID가 다른 세그먼트가 있습니까?
* 세그먼트 간 평가 방법(일괄 처리, 에지, 스트리밍)의 분포는 무엇입니까?
* 지난 달에 마지막으로 수정된 세그먼트 목록 표시
* 지난 주에 수정된 세그먼트는 무엇입니까?
* 지난 6개월 동안 수정되지 않은 세그먼트가 있습니까?
* 지난 해에 생성된 세그먼트를 나열합니다.
* 오늘 이전에 마지막으로 수정한 세그먼트를 표시합니다.
* 지난 1년간의 세그먼트 생성 날짜에 대한 패턴이나 트렌드가 있습니까?
* 세그먼트 생성 후 수정되지 않은 세그먼트를 식별할 수 있습니까?
* 생성 후 수정되지 않은 세그먼트가 있습니까?
* 시간 경과에 따른 세그먼트 생성의 트렌드는 무엇입니까?
* 세그먼트 생성 날짜의 분포는 얼마입니까?
* 세그먼트 수정 날짜 분포는 무엇입니까?
* 어떤 세그먼트에 가장 많은 사용자 프로필이 있습니까?
* 사용자 프로필이 가장 적은 세그먼트는 무엇입니까?
* 모든 일괄 처리 세그먼트를 나열합니다.
* 모든 가장자리 세그먼트를 나열합니다.
* 활성화된 세그먼트
* facebook에 전달되는 세그먼트는 무엇입니까?
* 세그먼트 이름이 &quot;APAC 고객&quot;인 일괄 처리 또는 스트리밍입니까?
* 활성 작업 세그먼트에는 몇 개의 프로필이 있습니까?
* 내 세그먼트에 0개의 프로필이 있습니까?
* 브론즈 로열티 세그먼트에 영향을 주는 데이터 세트는 무엇입니까?
* 어떤 세그먼트 정의가 &quot;gender&quot;를 포함하는 XDM 필드를 사용합니까?
* 스트리밍 세그먼트에서 어떤 채워진 XDM 필드가 발생합니까?
* 모든 세그먼트 정의에 몇 개의 XDM 필드가 있습니까?
* &quot;전문 사용자&quot; 데이터 세트가 영향을 미치는 세그먼트는 무엇입니까?
* HTTP API로 전달되는 세그먼트는 무엇입니까?
* 활성화된 세그먼트 중 어떤 세그먼트가 가장 많은 대상 유형으로 활성화됩니까?
* 활성화된 세그먼트의 총 수는 얼마입니까?
* 몇 개의 세그먼트가 활성화됩니까?
* 얼마나 많은 중복 세그먼트가 활성화됩니까?
* 각 대상에 대해 얼마나 많은 세그먼트가 활성화됩니까?
* 0, 1 또는 여러 대상에 활성화된 세그먼트는 무엇입니까? 분포를 표시합니다.
* 가장 많은 대상에 활성화된 세그먼트는 무엇입니까?
* 활성화된 중복 세그먼트는 무엇입니까?
* Adobe Target에 활성화된 세그먼트
* 모든 세그먼트에서 각 병합 정책은 몇 번 사용됩니까?

>[!TAB 스키마]

* 몇 개의 XDM 스키마가 정의됩니까?
* 가장 최근에 생성된 스키마는 무엇입니까?
* 각 XDM 클래스에 대해 몇 개의 스키마를 사용합니까?
* 세그먼트 수집 데이터 세트는 어떤 스키마를 사용합니까?
* 데이터 세트에서 사용되지 않는 스키마는 무엇입니까?

>[!TAB 대상]

* 존재하는 대상 수
* 가장 최근에 만들어진 대상은 무엇입니까?
* 각 세그먼트와 연관된 대상은 무엇입니까?

>[!TAB 소스]

* 생성된 소스는 몇 개입니까?
* 가장 최근에 생성된 소스는 무엇입니까?
* 몇 개의 소스를 사용할 수 있으며 카테고리별로 분류합니까?
* S3에서 소스 연결을 만들 수 있습니까?
* Mutual365 데이터 세트에 기여한 소스는 무엇입니까?

>[!TAB 데이터 세트]

* 데이터 세트가 몇 개 있습니까?
* 가장 최근에 만들어진 데이터 세트는 무엇입니까?
* 통합 프로필에 대해 활성화된 데이터 세트는 무엇입니까?
* 세그먼트 수집 데이터 세트에 대한 TTL 세트가 있습니까?
* Professional 사용자 데이터 세트의 TTL은 무엇입니까?
* 전문 사용자 스키마를 사용하는 데이터 세트는 무엇입니까?

>[!TAB 속성]

* 모든 데이터 세트에서 가장 일반적으로 채워지는 XDM 필드는 무엇입니까?
* 스키마에서 가장 일반적으로 사용되는 XDM 필드 및 속성은 무엇입니까?
* 전문 사용자 스키마에서 어떤 XDM 필드 및 속성을 사용합니까?
* ID를 사용하여 이 세그먼트에 사용된 속성 나열 {SEGMENT_ID}.
* 2개 이상의 세그먼트에서 사용되는 XDM 필드는 몇 개입니까?
* 세그먼트 간에 가장 일반적으로 사용되는 필드는 무엇입니까?
* 한 세그먼트에서만 사용되는 필드가 있습니까?
* 브론즈 충성도 세그먼트에 사용되는 속성은 무엇입니까?
* 어떤 세그먼트에서도 사용되지 않는 속성은 무엇입니까?
* 세그먼트에서 가장 일반적으로 사용되는 속성은 무엇입니까?

>[!ENDTABS]

+++

### 대화 경험

AI Assistant를 쿼리할 때 대화 경험에 대한 몇 가지 뉘앙스를 고려해야 합니다.

>[!NOTE]
>
>이러한 제한 사항은 일시적이며 알파 과정 전체에서 개선되고 있습니다.

>[!BEGINTABS]

>[!TAB 이전 토론에서 컨텍스트를 유추할 수 없음]

현재 AI 도우미는 주어진 질문에 대한 컨텍스트로 이전 토론을 참조할 수 없습니다. 예제는 아래 표를 참조하십시오.

| 애매한 질문 | 질문 지우기 | 참고 |
| --- | --- | --- |
| <ul><li>첫 번째 질문: &quot;세그먼트란 무엇입니까?&quot;</li><li>후속 질문: &quot;다른 유형이 있습니까?&quot;</li></ul> | <ul><li>첫 번째 질문: &quot;세그먼트란 무엇입니까?&quot;</li><li>후속 질문: &quot;다른 유형이 있습니까? **세그먼트**?&quot;</li></ul> | AI 비서는 &quot;이러한 것&quot;이 무엇을 의미하는지 유추할 수 없습니다. |
| <ul><li>첫 번째 질문: &quot;세그먼트란 무엇입니까?&quot;</li><li>다음 질문: &quot;더 자세히 설명할 수 있습니까?&quot;</li></ul> | <ul><li>첫 번째 질문: &quot;세그먼트란 무엇입니까?&quot;</li><li>추가 질문: &quot;세그먼트에 대한 세부 사항 설명&quot;</li></ul> | AI Assistant가 &quot;자세히&quot;를 기반으로 설명서를 지능적으로 참조할 수 없습니다. |
| <ul><li>첫 번째 질문: &quot;세그먼트란 무엇입니까?&quot;</li><li>다음 질문: &quot;예를 하나 들어주시겠어요?&quot;</li></ul> | <ul><li>첫 번째 질문: &quot;세그먼트란 무엇입니까?&quot;</li><li>후속 질문: &quot;세그먼트에 대한 예를 제공할 수 있습니까?&quot;</li></ul> | AI 도우미는 예를 나타낼 내용을 유추할 수 없습니다. |
| <ul><li>첫 번째 질문: &quot;일괄 처리 세그먼트란 무엇입니까?&quot;</li><li>후속 질문: &quot;스트리밍 세그먼트와 어떻게 비교됩니까?&quot;</li></ul> | <ul><li>첫 번째 질문: &quot;일괄 처리 세그먼트란 무엇입니까?&quot;</li><li>후속 질문: &quot;스트리밍 세그먼트를 배치 세그먼트와 비교할 수 있습니까?&quot;</li></ul> | AI 도우미는 &quot;그것&quot;이 무엇을 지칭하는지 유추할 수 없으므로 스트리밍 세그먼트를 비교할 수 없습니다. |
| <ul><li>첫 번째 질문: &quot;나에게 세그먼트가 몇 개 있습니까?&quot;</li><li>후속 질문: &quot;이들 중 몇 명이 대상으로 Facebook을 사용합니까?&quot;</li></ul> | <ul><li>첫 번째 질문: &quot;나에게 세그먼트가 몇 개 있습니까?&quot;</li><li>후속 질문: &quot;내가 대상으로 Facebook을 사용하고 있는 세그먼트 중 몇 개나?&quot;</li></ul> | AI 도우미는 &quot;그들&quot;이 무엇을 지칭하는지 유추할 수 없습니다. |

{style="table-layout:auto"}

>[!TAB 페이지에서 컨텍스트를 유추할 수 없음]

사용자가 진행 중인 Experience Platform UI 페이지의 특정 요소에 대해 AI 도우미에게 질문할 때 질문 내에서 특정 요소를 명확히 정의해야 합니다.

| 애매한 질문 | 질문 지우기 | 참고 |
| --- | --- | --- |
| &quot;이 기능은 무엇입니까?&quot; | &quot;역할 {PAGE_NAME} 할 수 있습니까? | AI 도우미는 &quot;이&quot;가 무엇을 가리키는지 유추할 수 없습니다. 쿼리하는 특정 페이지 요소를 제공해야 합니다. |
| &quot;왜 구하지 않는 거죠?&quot; | &quot;라는 새 샌드박스를 저장할 수 없는 이유 {NAME}?&quot; | AI 어시스턴트는 &quot;그것&quot;이 무엇을 지칭하는지 유추할 수 없으며 엔티티에 문제가 있다는 것을 알 수 없습니다. |

{style="table-layout:auto"}

또한 오류가 Experience League에 문서화되어 있는 경우 AI 도우미는 오류 메시지와 관련된 질문에만 답변할 수 있습니다.

>[!TAB 모호성]

AI Assistant는 현재 질문을 명확히 구별할 수 없으므로 질문을 명확히 구를 지정하고 제품, 애플리케이션 또는 도메인 내에서 질문을 범위로 표현해야 합니다.

| 애매한 질문 | 질문 지우기 | 참고 |
| --- | --- | --- |
| &quot;필터를 만들려면 어떻게 해야 합니까? | 프로필 쿼리 언어로 필터를 만드는 방법 | 다양한 Experience Platform 기능이 필터링을 지원하므로 필터링할 기능을 지정해야 합니다. |
| &quot;어떻게 시작합니까? | 대상 사용을 시작하려면 어떻게 해야 합니까? | 지나치게 넓은 개념은 포괄적이거나 불필요하게 구체적인 답변을 도출해낼 수 있기 때문에 목표 및 사용 사례에 대한 명확성을 제공해야 합니다. |

{style="table-layout:auto"}

>[!ENDTABS]

### 제한된 잡담

AI Assistant를 사용하여 잡담도 할 수 있지만 이 용량은 현재 제한적입니다.

### 기능 질문

AI 도우미가 수행할 수 있는 작업에 대해 부정확한 인상을 줄 수 있습니다. 다음 유형의 질문에 잘못 답변할 수 있습니다.

| 예제 질문 | 참고 |
| --- | --- |
| &quot;다음 질문에 답변할 수 있습니까? {ENTITY}?&quot; | AI 도우미가 색인에서 지정된 엔티티를 참조하는 단일 페이지를 찾을 수 있는 한 예 로 응답합니다. |
| &quot;혹시... **x** 언어?&quot; | AI 어시스턴트는 현재 영어만 지원하지만, 기본 모델이 지원할 수 있어 &#39;예&#39;라고 답할 수도 있다. |
| &quot;할 수 있어?&quot; | AI 도우미가 아니더라도 예라고 답할 수 있습니다. |

### 팁

#### 잘못된 정보 출처로 질문에 대한 응답이 있을 수 있습니다

사용 데이터에 대한 질문이 설명서를 기반으로 답변을 도출하는 경우가 있습니다. AI 어시스턴트가 질문을 잘못된 정보 소스로 잘못 라우팅할 수 있기 때문이다. 다음을 수행하여 이를 방지할 수 있습니다.

* 더 많은 SQL 유사 언어를 사용하도록 질문 구문 변경
* 사용할 정보 소스를 명시적으로 호출합니다.

예를 보려면 아래 표를 참조하십시오.

| 나쁜 질문 | 좋은 질문 | 참고 |
| --- | --- | --- |
| 가장 큰 세그먼트는 무엇입니까? | 가장 큰 세그먼트는 무엇입니까? 데이터 사용. | 답변이 데이터를 기반으로 하도록 AI 도우미에 명시적으로 지시합니다. |
| 가장 큰 세그먼트는 무엇입니까? | 내 가장 큰 세그먼트를 나열합니다. | &quot;...&quot;라는 질문이 문서 기반 질문으로 오인될 수 있는 경우가 있습니다. &quot;list&quot;와 같은 명령을 사용하는 것은 컨텍스트에 있는 데이터로 질문을 하는 것이 더 강력합니다. |
| 보유한 데이터 세트는 몇 개입니까? | 내 데이터 세트를 카운트합니다. | 원래 질문이 세그먼트화되면 데이터 세트에서는 작동하지 않습니다. |