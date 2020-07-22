---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 세그멘테이션 서비스 데이터 유형
topic: overview
translation-type: tm+mt
source-git-commit: 96b6f820e5d372446c4927e7719aedadb2b11bc9
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 3%

---


# Adobe Experience Platform [!DNL Segmentation Service] 지원 데이터 유형

모든 XDM 데이터 유형은 내에서 지원됩니다 [!DNL Segmentation Service]. 세그먼트 정의를 구성하는 규칙은 다음 데이터 유형에 따라 상황에 맞게 지정됩니다.

## 문자열 데이터

세그먼트 정의는 문자열 데이터를 사용하여 &quot;국가 이름&quot; 또는 &quot;충성도 프로그램 수준&quot;과 같은 세그먼트 대상에 대한 비숫자 제한을 정의합니다.

문자열 데이터는 논리, 포함/제외 및 비교 문을 사용하여 세그먼트 정의에 포함됩니다. 문자열 속성이 세그먼트 정의에 추가되면 문자열 관련 문을 사용하여 다른 문자열 필드에 대해 평가할 수 있습니다.

| 문 유형 | 예 |
| -------------- | -------- |
| 논리 | `and`, `or`, `not` |
| 포함/전용 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 비교 | `equals`, `does not equal`, `contains`, `starts with` |

## 날짜 데이터

날짜 데이터를 사용하면 특정 시작/종료 날짜를 사용하거나 아래 표에 표시된 날짜 관련 문을 사용하여 세그먼트 정의에 시간 기반 컨텍스트를 할당할 수 있습니다. 한 가지 구현으로 *올해* 언제든지 브랜드와 상호 작용하여 지난 며칠 *이내에* 적극적으로 활동했던 고객을 모집할 수 있습니다.

| 예제 필드 | 날짜 관련 명세서 | 타임라인 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | 세그먼트가 작성된 날짜와 관련이 있습니다. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 해당 주/월 내 연관성 |

## 경험 이벤트

Adobe Experience Platform 스키마로서 [!DNL XDM ExperienceEvents] 인터랙션이 발생할 당시 시스템의 스냅샷을 비롯하여 [!DNL Platform]통합 애플리케이션과 명시적 및 암시적 고객 상호 작용을 기록할 수 있습니다. [!DNL ExperienceEvents] 사실 기록입니다. 따라서 세그먼트 정의 동안 사용할 수 있는 데이터 소스입니다.

아래 표에서 보듯이 이벤트 데이터는 이벤트 동작을 수정하고 이벤트 속성을 지정하는 데 도움이 되는 키워드를 사용하여 렌더링됩니다.

| 키워드 | 사용 |
| ------- | --- |
| 포함/제외 | 데이터의 포함 또는 생략을 통해 이벤트의 동작을 설명합니다. |
| 모두/모두 | 적격한 세그먼트 수를 결정하는 데 도움이 됩니다. |
| &quot;시간 규칙 적용&quot; 전환 단추 | 날짜 데이터를 통합합니다. |
| 같음, 같지 않음, 다음으로 시작, 다음으로 시작하지 않음, 다음으로 끝남, 포함하지 않음, 포함하지 않음, 존재하지 않음, 존재하지 않음 | 문자열 데이터를 통합합니다. |

### 고객 공유

외부 대상을 새 세그먼트 정의의 구성 요소로 사용하여 새 세그먼트에 해당 속성 규칙을 추가할 수도 있습니다.

현재 Adobe Audience Manager만 외부 대상으로서 지원되며 향후 추가 소스가 활성화됩니다. Platform에서 Adobe Audience Manager 대상을 사용하는 방법에 대한 자세한 내용은 Adobe Audience Manager 설명서 [의 대상 공유 안내서를 참조하십시오](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### 세그먼트 공유

Platform에서 만든 세그먼트는 다른 [Adobe Experience Cloud 코어 서비스 내에서 사용할 수 있습니다](https://docs.adobe.com/content/help/ko-KR/core-services/interface/experience-cloud.html). 이 기능을 사용하려면 솔루션 설계자 또는 컨설턴트에게 문의해야 합니다.

## 기타 데이터 유형

위에 언급된 데이터 유형 외에 지원되는 데이터 유형 목록에도 다음이 포함됩니다.

- URI(Uniform Resource identifier)
- 열거형
- 숫자
- Long
- 정수
- Short
- 바이트
- 부울
- Array
- 개체
- 맵