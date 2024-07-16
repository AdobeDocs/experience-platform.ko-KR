---
solution: Experience Platform
title: 세분화 서비스에서 지원되는 데이터 유형
description: 모든 XDM(Experience Data Model) 데이터 유형은 Adobe 세그멘테이션 서비스 내에서 지원됩니다. 세그먼트 정의를 구성하는 규칙은 다음 데이터 유형에 의해 컨텍스트화됩니다.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 3%

---

# 세분화 서비스에서 지원되는 데이터 유형

모든 XDM(Experience Data Model) 데이터 유형은 Adobe Experience Platform 세그멘테이션 서비스 내에서 지원됩니다. 세그먼트 정의를 구성하는 규칙은 다음 데이터 유형에 의해 컨텍스트화됩니다.

## 문자열 데이터

세그먼트 정의는 문자열 데이터를 사용하여 &quot;국가 이름&quot; 또는 &quot;충성도 프로그램 수준&quot;과 같은 대상에 대한 비숫자 제약 조건을 정의합니다.

문자열 데이터는 논리, 포함/제외 및 비교 문을 사용하여 세그먼트 정의에 포함됩니다. 문자열 속성이 세그먼트 정의에 추가되면 문자열 관련 문을 사용하여 다른 문자열 필드와 비교하여 문자열 속성을 평가할 수 있습니다.

| 명령문 유형 | 예시 |
| -------------- | -------- |
| 논리적 | `and`, `or`, `not` |
| 포괄적/배타적 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 비교 | `equals`, `does not equal`, `contains`, `starts with` |

## 날짜 데이터

날짜 데이터를 사용하면 특정 시작/종료 날짜를 사용하거나 아래 표에 표시된 것처럼 날짜 관련 문을 사용하여 세그먼트 정의에 시간 기반 컨텍스트를 할당할 수 있습니다. 한 구현에서 *올해*&#x200B;에는 언제든지 브랜드와 상호 작용하고 지난 며칠 동안은 *이내*&#x200B;에서도 활성 상태인 고객을 대상으로 만들 수 있습니다.

| 예제 필드 | 일자 관련 명세서 | 타임라인 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | 세그먼트 정의가 작성된 날짜와 관련이 있습니다. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 주어진 주/월 내에 관련성이 있습니다. |

## 경험 이벤트

[!DNL XDM ExperienceEvents]은(는) Adobe Experience Platform 스키마로서 [!DNL Platform] 통합 응용 프로그램과의 명시적 및 암시적 고객 상호 작용을 기록합니다. 여기에는 상호 작용이 발생한 시점의 시스템 스냅숏이 포함됩니다. [!DNL ExperienceEvents]은(는) 팩트 레코드입니다. 따라서 세그먼트 정의 중에 사용할 수 있는 데이터 소스입니다.

아래 표에서 볼 수 있듯이 이벤트 데이터는 이벤트 행동을 개선하고 이벤트 속성을 지정하는 데 도움이 되는 키워드를 사용하여 렌더링됩니다.

| 키워드 | 사용 |
| ------- | --- |
| 포함/제외 | 데이터의 포함 또는 누락을 통한 이벤트의 동작을 설명합니다. |
| 임의/모두 | 자격을 부여하는 세그먼트 정의의 수를 결정하는 데 도움이 됩니다. |
| &quot;시간 규칙 적용&quot; 토글 단추 | 날짜 데이터를 통합합니다. |
| 같음, 같지 않음, 다음으로 시작, 다음으로 시작하지 않음, 다음으로 끝남, 다음으로 끝나지 않음, 포함, 포함하지 않음, 존재, 존재하지 않음 | 문자열 데이터를 통합합니다. |

### 대상자 공유

외부 대상은 새 세그먼트 정의에 해당 속성 규칙을 추가하여 새 세그먼트 정의의 구성 요소로 사용할 수도 있습니다.

현재 Adobe Audience Manager만 외부 대상으로 지원되며 향후 추가 소스가 활성화됩니다. 플랫폼과 함께 Adobe Audience Manager 대상 사용에 대한 자세한 내용은 Adobe Audience Manager 설명서의 [대상 공유 안내서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)에서 확인할 수 있습니다.

### 세그먼트 정의 공유

플랫폼에서 만든 세그먼트 정의는 다른 [Adobe Experience Cloud 핵심 서비스](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=ko-KR) 내에서 사용할 수 있습니다. 이 기능을 활성화하려면 솔루션 설계자나 컨설턴트에게 문의해야 합니다.

## 기타 데이터 유형

위에 언급된 데이터 유형 외에도 지원되는 데이터 유형 목록에는 다음도 포함됩니다.

- URI(Uniform Resource Identifier)
- 열거형
- 숫자
- Long
- 정수
- 짧음
- 바이트
- 부울
- 배열
- 오브젝트
- 맵
