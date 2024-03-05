---
solution: Experience Platform
title: Edge 세그멘테이션 UI 안내서
description: 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화하면서 에지 세분화를 사용하여 에지에서 즉시 플랫폼의 세그먼트 정의를 평가하는 방법을 알아봅니다.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 에지 세분화 UI 안내서

>[!NOTE]
>
>이제 모든 Platform 사용자가 Edge 세그멘테이션을 일반적으로 사용할 수 있습니다. Beta 실행 중에 에지 세그먼트 정의를 생성한 경우 이러한 세그먼트 정의는 계속 작동합니다.

에지 세그멘테이션은 Adobe Experience Platform의 세그먼트를 즉시 평가하는 기능입니다 [가장자리에](../../web-sdk/home.md), 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

>[!IMPORTANT]
>
> 에지 데이터는 수집된 위치에서 가장 가까운 에지 서버 위치에 저장되고 허브(또는 주) Adobe Experience Platform 데이터 센터로 지정된 위치 이외의 위치에 저장될 수 있다.
>
> 또한 에지 세분화 엔진은 가 있는 에지의 요청만 처리합니다 **1** 에지 기반이 아닌 기본 id와 일치하는 기본 표시 id.

## Edge 세그멘테이션 쿼리 유형 {#query-types}

현재 선택한 쿼리 유형만 가장자리 세분화를 통해 평가할 수 있습니다. 다음 섹션에서는 에지 세분화를 통해 평가할 수 있는 쿼리 유형과 현재 지원되지 않는 쿼리 유형 목록을 제공합니다.

쿼리가 다음 표에 요약된 기준을 충족하는 경우 가장자리 세분화를 사용하여 평가할 수 있습니다.

>[!NOTE]
>
>쿼리가 다음 표의 쿼리 유형과 일치하는 경우, 가장자리 세분화를 사용하여 자동으로 평가됩니다. 시스템은 쿼리 표현식을 기반으로 이 기능을 자동으로 결정합니다.

| 쿼리 유형 | 세부 사항 | 예 | PQL 예 |
| ---------- | ------- | ------- | ----------- |
| 단일 이벤트 | 시간 제한 없이 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의. | 장바구니에 항목을 추가한 사람. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 단일 프로필 | 단일 프로필 전용 속성을 참조하는 모든 세그먼트 정의 | 미국에 사는 사람들. | `homeAddress.countryCode = "US"` |
| 프로필을 참조하는 단일 이벤트 | 하나 이상의 프로필 속성 및 시간 제한 없이 수신되는 단일 이벤트를 참조하는 모든 세그먼트 정의. | 홈페이지를 방문한 미국 거주자. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| 프로필 속성을 사용하여 단일 이벤트 무효화 | 무효화된 단일 수신 이벤트와 하나 이상의 프로필 속성을 참조하는 세그먼트 정의 | 미국에 거주하고 다음을 보유한 사람 **아님** 홈페이지를 방문했습니다. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 기간 내 단일 이벤트 | 설정된 기간 내의 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. | 지난 24시간 동안 홈페이지를 방문한 사람. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| 24시간 미만의 상대 시간 창 내에 프로필 속성이 있는 단일 이벤트 | 하나 이상의 프로필 속성을 가진 단일 수신 이벤트를 참조하고 24시간 미만의 상대 시간 창 내에서 발생하는 모든 세그먼트 정의입니다. | 지난 24시간 동안 홈페이지를 방문한 미국 거주자. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| 기간 내에 프로필 속성이 있는 단일 이벤트가 무효화됨 | 일정 기간 내에 하나 이상의 프로필 속성 및 차단된 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. | 미국에 거주하고 다음을 보유한 사람 **아님** 지난 24시간 동안 홈페이지를 방문했습니다. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]))` |
| 24시간 기간 내 빈도 이벤트 | 24시간의 기간 내에서 특정 횟수로 발생하는 이벤트를 참조하는 세그먼트 정의입니다. | 홈 페이지를 방문한 사람 **최소** 지난 24시간 동안 5번 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 24시간 기간 내에 프로필 속성이 있는 빈도 이벤트 | 하나 이상의 프로필 속성을 참조하는 세그먼트 정의와 24시간의 기간 내에서 특정 횟수만큼 발생하는 이벤트. | 홈페이지를 방문한 미국 출신 **최소** 지난 24시간 동안 5번 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 24시간 기간 내에 프로필로 빈도 이벤트를 무효화했습니다. | 하나 이상의 프로필 속성을 참조하는 세그먼트 정의와 24시간의 기간 내에서 특정 횟수만큼 발생하는 차단된 이벤트입니다. | 홈 페이지를 방문하지 않은 사람 **기타** 지난 24시간 동안 5번 이상 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24시간의 시간 프로필 내에 여러 개의 수신 히트 | 24시간의 기간 내에 발생하는 여러 이벤트를 참조하는 모든 세그먼트 정의. | 홈 페이지를 방문한 사람 **또는** 지난 24시간 내에 체크아웃 페이지를 방문했습니다. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 24시간 기간 내에 프로필이 있는 여러 이벤트 | 24시간의 기간 내에 발생하는 하나 이상의 프로필 속성 및 여러 이벤트를 참조하는 모든 세그먼트 정의. | 홈페이지를 방문한 미국 출신 **및** 지난 24시간 내에 체크아웃 페이지를 방문했습니다. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의입니다. | 미국에 거주하며 &quot;기존 세그먼트&quot; 세그먼트에 있는 사람. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 맵을 참조하는 쿼리 | 속성 맵을 참조하는 모든 세그먼트 정의입니다. | 외부 세그먼트 데이터를 기반으로 장바구니에 추가한 사람입니다. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

세그먼트 정의는 **아님** 다음 시나리오에서 에지 세그멘테이션에 대해 활성화하십시오.

- 세그먼트 정의는 단일 이벤트와 `inSegment` 이벤트.
   - 그러나 세그먼트 정의에 가 포함된 경우 `inSegment` 이벤트는 프로필 전용이며, 세그먼트 정의는 입니다. **의지** 에지 세분화에 대해 활성화되어야 합니다.

## 다음 단계

이 안내서에서는 Adobe Experience Platform에서 에지 세분화를 사용하여 세그먼트 정의를 평가하는 방법을 설명합니다. Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그먼테이션 사용 안내서](./overview.md). Experience Platform API를 사용하여 유사한 작업을 수행하고 세그먼트 정의를 사용하는 방법을 알아보려면 다음을 방문하십시오. [edge segmentation API 안내서](../api/edge-segmentation.md).

## 부록

다음 섹션에는 에지 세분화에 대해 자주 묻는 질문이 나와 있습니다.

### Edge Network에서 세그먼트 정의를 사용하려면 얼마나 걸립니까?

Edge Network에서 세그먼트 정의를 사용할 수 있으려면 최대 1시간이 걸립니다.
