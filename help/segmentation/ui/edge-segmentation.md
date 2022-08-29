---
keywords: Experience Platform;홈;인기 항목;에지 세그멘테이션;세그멘테이션 서비스;세그멘테이션 서비스;ui 안내서;스트리밍 에지;
solution: Experience Platform
title: Edge Segmentation UI 안내서
topic-legacy: ui guide
description: Edge Segmentation은 Platform의 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지 개인화 사용 사례를 가능하게 하는 기능입니다.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 75583d9688f0c5ee0fe4627ce64b5436ca621aa1
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Edge Segmentation UI 안내서

>[!NOTE]
>
>이제 모든 Platform 사용자가 Edge 세그멘테이션을 사용할 수 있습니다. 베타 동안 에지 세그먼트를 만든 경우 이러한 세그먼트가 계속 작동합니다.

에지 세그먼테이션은 즉시 Adobe Experience Platform의 세그먼트를 평가하는 기능입니다 [끝](../../edge/home.md), 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

>[!IMPORTANT]
>
> 에지 데이터는 수집된 위치와 가장 가까운 Edge Server 위치에 저장되며, 허브(또는 주체) Adobe Experience Platform 데이터 센터로 지정된 위치 이외의 위치에 저장할 수 있습니다.
>
> 또한 에지 세그먼테이션 엔진은 가 있는 에지만 요청을 처리합니다 **하나** 에지 기반 기본 ID와 일치하는 기본 표시 id입니다.

## 에지 세그멘테이션 쿼리 유형

현재 선택한 쿼리 유형만 에지 세그먼테이션으로 평가할 수 있습니다. 다음 섹션에서는 에지 세그먼테이션으로 평가할 수 있는 쿼리 유형 목록과 현재 지원되지 않는 쿼리 유형 목록을 제공합니다.

### 지원되는 쿼리 유형 {#query-types}

쿼리는 다음 표에 요약된 기준을 충족하는 경우 에지 세그먼테이션으로 평가할 수 있습니다.

>[!NOTE]
>
>쿼리가 다음 테이블의 쿼리 유형과 일치하는 경우 에지 세그멘테이션을 사용하여 자동으로 평가됩니다. 시스템은 쿼리 식을 기반으로 이 기능을 자동으로 결정합니다.

| 쿼리 유형 | 세부 사항 | 예 | PQL 예 |
| ---------- | ------- | ------- | ----------- |
| 단일 이벤트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. | 장바구니에 항목을 추가한 사람. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 단일 프로필 | 단일 프로필 전용 속성을 참조하는 모든 세그먼트 정의 | 미국에 사는 사람들. | `homeAddress.countryCode = "US"` |
| 프로필을 참조하는 단일 이벤트 | 하나 이상의 프로필 속성 및 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. | 미국에 거주하는 사람들이 홈페이지를 방문했습니다. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 프로필 속성을 사용하여 단일 이벤트 무효화 | 무효화된 단일 수신 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의 | 미국에 살고 **not** 홈 페이지를 방문했습니다. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 시간 창 내의 단일 이벤트 | 설정된 기간 내에 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. | 지난 24시간 동안 홈페이지를 방문한 사람들. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 시간 창 내에 프로필 속성이 있는 단일 이벤트 | 설정된 기간 내에 하나 이상의 프로필 속성 및 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. | 미국에 거주하는 사람들이 지난 24시간 동안 홈페이지를 방문했습니다. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 시간 창 내에서 프로필 속성이 있는 단일 이벤트를 무효화했습니다. | 일정 기간 내에 하나 이상의 프로필 속성 및 무효화된 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. | 미국에 살고 **not** 지난 24시간 동안 홈페이지를 방문했다. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| 24시간 시간 기간 내의 빈도 이벤트 | 24시간의 시간 창 내에서 특정 시간에 발생하는 이벤트를 참조하는 모든 세그먼트 정의입니다. | 홈 페이지를 방문한 사람 **적어도** 지난 24시간 동안 5번 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 24시간 시간 창 내에 프로필 속성이 있는 빈도 이벤트 | 하나 이상의 프로필 속성 및 24시간의 시간 창 내에서 특정 횟수를 발생하는 이벤트를 참조하는 모든 세그먼트 정의입니다. | 홈페이지를 방문한 미국 출신 **적어도** 지난 24시간 동안 5번 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 24시간 시간 창 내에서 프로필이 무효화된 빈도 이벤트 | 24시간의 시간 창 내에서 특정 시간에 발생하는 하나 이상의 프로필 속성 및 무효화된 이벤트를 참조하는 모든 세그먼트 정의. | 홈 페이지를 방문하지 않은 사람 **자세히** 지난 24시간 동안 5번 이상 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24시간의 시간 프로필 내에 여러 수신 히트 | 24시간의 시간 창 내에서 발생하는 여러 이벤트를 참조하는 모든 세그먼트 정의입니다. | 홈 페이지를 방문한 사람 **또는** 지난 24시간 내에 체크아웃 페이지를 방문했습니다. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 24시간 기간 내에 프로필이 있는 여러 이벤트 | 24시간의 시간 창 내에서 발생하는 하나 이상의 프로필 속성 및 여러 이벤트를 참조하는 모든 세그먼트 정의입니다. | 홈페이지를 방문한 미국 출신 **및** 지난 24시간 내에 체크아웃 페이지를 방문했습니다. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의. | 미국에 살고 &quot;기존 세그먼트&quot;에 있는 사람. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 맵을 참조하는 쿼리 | 속성 맵을 참조하는 모든 세그먼트 정의입니다. | 외부 세그먼트 데이터를 기반으로 장바구니에 추가한 사람. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

## 다음 단계

이 안내서에서는 Adobe Experience Platform에서 에지 세그먼테이션을 사용하여 세그먼트를 평가하는 방법을 설명합니다. Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그멘테이션 사용 안내서](./overview.md). 유사한 작업을 수행하고 Experience Platform API를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [edge segmentation API 안내서](../api/edge-segmentation.md).
