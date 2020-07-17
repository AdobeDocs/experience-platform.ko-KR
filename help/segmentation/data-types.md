---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 세그멘테이션 서비스 데이터 유형
topic: overview
translation-type: tm+mt
source-git-commit: cb6a2f91eb6c18835bd9542e5b66af4682227491
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---


# Adobe Experience Platform 세그멘테이션 서비스 지원 데이터 유형

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

Adobe Experience Platform 스키마로서 XDM ExperienceEvents는 상호 작용 발생 시 시스템의 스냅샷을 포함하여 [!DNL Platform]통합된 애플리케이션과의 명시적 및 암시적 고객 상호 작용을 기록합니다. ExperienceEvents는 팩트 레코드입니다. 따라서 세그먼트 정의 동안 사용할 수 있는 데이터 소스입니다.

아래 표에서 보듯이 이벤트 데이터는 이벤트 동작을 수정하고 이벤트 속성을 지정하는 데 도움이 되는 키워드를 사용하여 렌더링됩니다.

| 키워드 | 사용 |
| ------- | --- |
| 포함/제외 | 데이터의 포함 또는 생략을 통해 이벤트의 동작을 설명합니다. |
| 모두/모두 | 적격한 세그먼트 수를 결정하는 데 도움이 됩니다. |
| &quot;시간 규칙 적용&quot; 전환 단추 | 날짜 데이터를 통합합니다. |
| 같음, 같지 않음, 다음으로 시작, 다음으로 시작하지 않음, 다음으로 끝남, 포함하지 않음, 포함하지 않음, 존재하지 않음, 존재하지 않음 | 문자열 데이터를 통합합니다. |

## 세그먼트

기존 세그먼트 정의를 새 세그먼트 정의의 구성 요소로 사용하여 새 세그먼트에 속성 및 이벤트 기반 규칙을 추가할 수도 있습니다.

## 대상자

외부 대상을 새 세그먼트 정의의 구성 요소로 사용하여 새 세그먼트에 해당 속성 규칙을 추가할 수도 있습니다.

현재 Adobe Audience Manager만 대상으로 지원됩니다. 향후 추가 소스가 활성화됩니다.

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