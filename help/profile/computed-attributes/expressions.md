---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성에 대한 샘플 PQL 표현식
topic-legacy: guide
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이 함수에는 유효한 PQL(Profile Query Language) 표현식을 사용해야 합니다. 이 안내서에서는 계산된 속성에 가장 일반적으로 사용되는 PQL 표현식의 일부를 설명합니다.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%

---

# (알파) 계산된 속성에 대한 샘플 PQL 표현식

>[!IMPORTANT]
>
>계산된 속성 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform에서 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세분화, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다. 계산된 각 속성은 이름 및 설명, 값이 포함될 필드의 스키마 클래스 및 경로, 계산된 값이 계산된 속성에 저장하려는 값과 같은 기본 정보로 정의됩니다.

계산된 속성에 사용되는 표현식은 실시간 고객 프로필 데이터에 대한 쿼리의 정의 및 실행을 지원하기 위해 설계된 XDM(Experience Data Model) 호환 쿼리 언어인 [!DNL Profile Query Language](PQL)을 사용하여 만들어집니다.

계산된 속성은 현재 다음 함수를 지원합니다.sum, count, min, max 및 boolean을 선택합니다. 이 안내서에서는 조직의 계산된 속성을 정의할 때 사용할 수 있는 가장 일반적으로 사용되는 PQL 표현식의 일부를 설명합니다. PQL 및 지원되는 쿼리의 추가 서식 지침 및 샘플에 대한 링크에 대한 자세한 내용은 [PQL 개요](../../segmentation/pql/overview.md)를 참조하십시오.

## 스트리밍 표현식

다음 표에서는 스트리밍 모드에서 지원되는 일반적으로 사용되는 쿼리 표현식에 대한 세부 사항을 제공합니다.

| 설명 | PQL 표현식 | 입력 유형:<br/>프로필 또는 경험 이벤트(EE[]) | 결과 유형 |
|---|---|---|---|
| 지난 7일 동안 이미지 다운로드 수입니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot; 및 contentType = &quot;image&quot;].count() | 프로필 및 EE[] | 정수 |
| 지난 7일 동안의 스포츠 용품 구입의 합계입니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].sum(commerce.order.priceTotal) | 프로필 및 EE[] | 정수 또는 이중 |
| 지난 7일 동안 평균 고객이 스포츠 용품 구입을 합니다.<br/><br/>**참고:** 3개의 계산된 속성을 만들어야 합니다. | **ca1:** xEvent[(timestamp는  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;> <br/><br/>**** (timestamp_occurs)ca3:caca / ca2]] | 프로필 및 EE[] | 이중 |
| 고객이 지난 7일 동안 스포츠 용품 구입에 100달러 이상을 지출했습니까?<br/><br/>**참고:** 계산된 2개의 속성을 만들어야 합니다. | **ca1:** xEvent[(timestamp)  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | 프로필 및 EE[] | 부울 |
| 고객이 지난 7일 동안 구매했습니까? | chain(xEvent, timestamp, [A:WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7일 전)]) | 프로필 및 EE[] | 부울 |
| 지난 7일 동안 가장 낮은 이용자는 스포츠 용품 구입을 한다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].min(commerce.order.priceTotal) | 프로필 및 EE[] | 정수 또는 이중 |
| 지난 7일 동안 가장 많은 사용자가 스포츠 용품 구입을 합니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;transaction&quot; 및 category = &quot;sporting products&quot;].max(commerce.order.priceTotal) | 프로필 및 EE[] | 정수 또는 이중 |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품의 다운로드 수입니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | 프로필 및 EE[] | 맵[문자열, 정수] |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품의 다운로드에 대한 숫자 속성의 합계입니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | 프로필 및 EE[] | 맵[문자열, 정수] 또는 맵[문자열, 이중] |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품의 다운로드에 대한 숫자 속성의 평균입니다.<br/><br/>**참고:** 3개의 계산된 속성을 만들어야 합니다. | **ca1:** xEvent[(timestamp는  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(timestamp occesses  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;> <br/><br/>**** .groupBy(product, G) => mapEntry (K, G.count())ca3:ca / ca1]] | 프로필 및 EE[] | 맵[문자열, 이중] |
| 최근 7일 동안 다운로드된 각 제품의 다운로드보다 더 적은 숫자 속성을 제품별로 색인화합니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | 프로필 및 EE[] | 맵[문자열, 정수] 또는 맵[문자열, 이중] |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품의 다운로드보다 높은 숫자 속성의 최대값입니다. | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | 프로필 및 EE[] | 맵[문자열, 정수] 또는 맵[문자열, 이중] |
| 프로필 상의 숫자 표현식으로, 이벤트를 참조하지 않습니다. | if(person.gender = &quot;female&quot;, 60, 65) | 프로필 | 정수 또는 이중 |
| 이벤트를 참조하지 않고 프로필의 부울 표현식입니다. | person.birthYear >= 2000 | 프로필 | 부울 |
| 프로필 상의 문자열 표현식으로, 이벤트를 참조하지 않습니다. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | 프로필 | 문자열 |

## 일괄 처리 표현식

다음 표에서는 일괄 처리 모드에서만 사용할 수 있는 쿼리 표현식에 대한 세부 사항을 제공합니다. 즉, 현재 스트리밍에서 사용할 수 없음을 의미합니다.

| 설명 | PQL 표현식 | 입력 유형:<br/>프로필 또는 경험 이벤트(EE[]) | 결과 유형 |
|---|---|---|---|
| 지난 7일 동안 제품 다운로드에 대한 숫자 표현식의 합계가 100을 초과하는지 여부(제품별로 색인화). | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | 프로필 및 EE[] | 맵[문자열, 부울] |
| 지난 7일 동안 제품 다운로드에 대한 숫자 표현식의 평균이 100을 초과하는지 여부(제품별로 색인화). | xEvent[(타임스탬프는 현재 발생 7일 전) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | 프로필 및 EE[] | 맵[문자열, 부울] |
| 최근 7일 동안 제품별로 색인화된 다운로드된 각 제품에 대한 다양한 지표의 누적 | xEvent[(timestamp는 현재 시작 7일 전에 발생) 및 eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;:G.count(), &quot;sum&quot;:G.sum(commerce.order.priceTotal)}) | 프로필 및 EE[] | 맵[문자열, 개체]에 있습니다. 여기서 개체는 사용자 지정 XDM 유형입니다. |
