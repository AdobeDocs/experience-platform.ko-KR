---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성에 대한 샘플 PQL 표현식
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 기능을 사용하려면 유효한 PQL(프로필 쿼리 언어) 표현식을 사용해야 합니다. 이 안내서에서는 계산된 속성에 가장 일반적으로 사용되는 PQL 표현식 중 일부를 간략하게 설명합니다.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (알파) 계산된 속성에 대한 샘플 PQL 표현식

>[!IMPORTANT]
>
>계산된 특성 기능은 현재 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform에서 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다. 각 계산된 속성은 이름 및 설명, 값이 유지될 필드의 스키마 클래스 및 경로, 계산된 값이 계산된 속성에 저장할 값인 표현식과 같은 기본 정보로 정의됩니다.

계산된 속성에 사용된 표현식은 [!DNL Profile Query Language] (PQL) - 실시간 고객 프로필 데이터에 대한 쿼리의 정의 및 실행을 지원하도록 설계된 XDM(Experience Data Model) 호환 쿼리 언어입니다.

계산된 속성은 현재 다음 함수를 지원합니다. sum, count, min, max 및 boolean 이 안내서에서는 조직에 대해 자체 계산된 속성을 정의할 때 사용할 수 있는 가장 일반적으로 사용되는 PQL 표현식 중 일부를 간략하게 설명합니다. PQL 및 지원되는 쿼리의 추가 서식 지침 및 샘플에 대한 링크에 대한 자세한 내용은 [PQL 개요](../../segmentation/pql/overview.md).

## 스트리밍 표현식

다음 표에서는 스트리밍 모드에서 지원되는 일반적으로 사용되는 쿼리 표현식에 대한 세부 사항을 제공합니다.

| 설명 | PQL 표현식 | 입력 유형:<br/>프로필 또는 경험 이벤트(EE)[]) | 결과 유형 |
|---|---|---|---|
| 지난 7일 동안의 이미지 다운로드 수입니다. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot; 및 contentType = &quot;image&quot;].count() | 프로필 및 EE[] | 정수 |
| 지난 7일 동안의 스포츠 상품에 대한 고객의 지출 합계. | xEvent[(타임스탬프가(지금부터 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].sum(commerce.order.priceTotal) | 프로필 및 EE[] | 정수 또는 더블 |
| 지난 7일 동안 평균 고객이 스포츠 상품에 지출합니다.<br/><br/>**참고:** 세 개의 계산된 속성을 만들어야 합니다. | **ca1:** xEvent[(타임스탬프가(지금부터 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(타임스탬프가(지금부터 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | 프로필 및 EE[] | 이중 |
| 그 고객이 지난 7일 동안 스포츠 용품을 사는데 100달러 이상을 썼습니까?<br/><br/>**참고:** 계산된 두 속성을 만들어야 합니다. | **ca1:** xEvent[(타임스탬프가(지금부터 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | 프로필 및 EE[] | 부울 |
| 고객이 지난 7일 동안 구매했습니까? | chain(xEvent, 타임스탬프, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7일 전 현재)]) | 프로필 및 EE[] | 부울 |
| 지난 7일 동안 가장 적은 사용자가 스포츠 상품에 지출합니다. | xEvent[(타임스탬프가(지금부터 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].min(commerce.order.priceTotal) | 프로필 및 EE[] | 정수 또는 더블 |
| 가장 높은 사용자가 지난 7일 동안 스포츠 상품에 돈을 씁니다. | xEvent[(타임스탬프가(지금부터 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].max(commerce.order.priceTotal) | 프로필 및 EE[] | 정수 또는 더블 |
| 최근 7일 동안 제품별로 색인화된 다운로드한 각 제품의 다운로드 수입니다. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | 프로필 및 EE[] | 맵[문자열, 정수] |
| 최근 7일 동안 제품별로 색인화된 다운로드한 각 제품의 다운로드에 대한 숫자 속성의 합계. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | 프로필 및 EE[] | 맵[문자열, 정수] 또는 맵[문자열, 이중] |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품의 다운로드에 대한 숫자 속성의 평균.<br/><br/>**참고:** 세 개의 계산된 속성을 만들어야 합니다. | **ca1:** xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2 / ca1 | 프로필 및 EE[] | 맵[문자열, 이중] |
| 다운로드한 각 제품의 다운로드에 대한 최소 숫자 속성(최근 7일 동안 제품별로 색인화됨) | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | 프로필 및 EE[] | 맵[문자열, 정수] 또는 맵[문자열, 이중] |
| 다운로드한 각 제품의 다운로드를 통해 지난 7일 동안 제품별로 인덱싱된 최대 숫자 속성입니다. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | 프로필 및 EE[] | 맵[문자열, 정수] 또는 맵[문자열, 이중] |
| 이벤트가 아닌 프로필의 숫자 식입니다. | if(person.gender = &quot;female&quot;, 60, 65) | 프로필 | 정수 또는 더블 |
| 이벤트가 아닌 프로필의 부울 식입니다. | person.firstYear >= 2000 | 프로필 | 부울 |
| 이벤트가 아닌 프로필의 문자열 식입니다. | if(homeAddress.countryCode in) [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | 프로필 | 문자열 |

## 배치 표현식

다음 표는 일괄 처리 모드에서만 사용할 수 있는 쿼리 표현식에 대한 세부 사항을 제공하므로 현재 스트리밍에서 사용할 수 없습니다.

| 설명 | PQL 표현식 | 입력 유형:<br/>프로필 또는 경험 이벤트(EE)[]) | 결과 유형 |
|---|---|---|---|
| 최근 7일 동안의 제품 다운로드에 대한 숫자 표현식의 합계가 100을 초과하는지 여부, 제품별로 인덱싱됨. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | 프로필 및 EE[] | 맵[문자열, 부울] |
| 최근 7일 동안 제품 다운로드에 대한 숫자 표현식의 평균이 100을 초과하는지 여부, 제품별로 인덱싱됨. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | 프로필 및 EE[] | 맵[문자열, 부울] |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품에 대한 다양한 지표의 축적. | xEvent[(타임스탬프가 발생하기 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | 프로필 및 EE[] | 맵[문자열, 개체] 여기서 개체는 사용자 지정 XDM 유형입니다 |
