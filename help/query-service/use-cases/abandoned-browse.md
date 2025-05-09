---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;쿼리
title: Adobe Experience Platform 쿼리 서비스에 대한 사용 사례 예
description: Adobe Experience Platform 쿼리 서비스의 다기능성과 이점을 보여주는 전체적인 예입니다.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Adobe Experience Platform [!DNL Query Service]의 사용 사례 예

이 문서와 함께 제공되는 비디오 프레젠테이션은 Adobe Experience Platform [!DNL Query Service]이(가) 조직의 전략적 비즈니스 통찰력에 어떤 이점을 제공하는지 보여 주는 전체적인 워크플로를 제공합니다. 찾아보기 포기 사용 사례를 예로 들자면 이 안내서에서는 다음 주요 개념을 보여줍니다.

* Adobe Experience Platform의 잠재력을 극대화하기 위한 데이터 처리의 핵심 중요성입니다.
* 기존 데이터 아키텍처를 기반으로 쿼리를 작성하는 방법입니다.
* 요구 사항에 맞는 데이터 품질을 확인하고 부족한 부분을 완화할 수 있는 방법을 마련합니다.
* 세분화 및 개인화 대상에서 다운스트림을 사용하도록 설정된 빈도로 쿼리를 실행하도록 예약하는 프로세스입니다.
* 마케터는 [!DNL Query Service]의 기능을 통해 파생 데이터 세트를 대상자에 포함하기 쉽습니다.

## 목표 {#objectives}

이 워크플로우 데모는 여러 Adobe Experience Platform 서비스를 사용합니다. 계속 사용하려면 다음 기능 및 서비스를 잘 이해하는 것이 좋습니다.

* XDM(경험 데이터 모델) 스키마 컴포지션의 [기본 사항](../../xdm/schema/composition.md)
* [데이터 집합을 만들고 데이터를 수집하는 방법](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
* Adobe Analytics 소스 커넥터를 사용하여 데이터를 [수집하는 방법](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=ko)
* [세그먼테이션](../../segmentation/home.md)
* [대상](../../destinations/home.md)

찾아보기 포기 예제는 Adobe [!DNL Analytics] 데이터를 사용하여 특정 실행 가능한 대상을 만드는 것을 중심으로 합니다. 대상자는 지난 4일 동안 웹 사이트를 열람했지만 구매하지 않은 모든 고객을 포함하도록 개선됩니다. 대상자의 각 프로필은 고객의 행동 패턴에서 비롯된 가장 높은 가격의 SKU로 타깃팅됩니다.

쿼리 자체는 매우 규정적이며 세그먼트 정의에 대한 사용 사례 기준을 충족하는 데이터만 포함합니다. 이렇게 하면 처리되는 [!DNL Analytics]개의 데이터 양을 최소화하여 성능이 향상됩니다. 또한 데이터를 가장 높은 가격에서 가장 낮은 가격으로 주문하고 사용자가 탐색 중인 가장 높은 가격의 SKU를 선택합니다.

프레젠테이션에 사용된 쿼리는 아래에서 볼 수 있습니다.

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## adobe analytics를 사용한 [!DNL Query Service] 찾아보기 포기 예 {#video-example}

아래에 표시된 비디오 프레젠테이션은 [!DNL Query Service] 및 Adobe 분석 통합에 중점을 둔 Experience Platform 데이터에 대한 전체적인 실제 사용 사례를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3454951?quality=12&learn=on&captions=kor)

## [!DNL Query Service]의 이점 {#benefits}

[!DNL Query Service]이(가) 제공하는 기능은 다양한 용도로 사용됩니다. 이를 사용하여 세그멘테이션에 대한 복잡한 논리를 수용하거나, 다운스트림에 사용할 다양한 개인화된 특성을 계산하거나, 대상을 구성하는 방법을 크게 단순화할 수 있습니다.

[!DNL Query Service]을(를) 사용하면 쿼리에 제약 조건을 포함하여 대상 구축 프로세스를 단순화할 수 있습니다. 이렇게 하면 대상자에게 적합한 데이터를 확보하여 데이터 품질이 향상됩니다. 쿼리의 품질을 유지 관리하면 정확한 대상자가 되고 데이터 안정성이 향상됩니다. 쿼리에서 파생된 특성을 기반으로 스키마 및 사용자 지정 테이블을 만들어 대상자를 저장할 수도 있습니다. 프로필에 대해 사용자 지정 테이블을 활성화할 수 있으며 이러한 데이터 포인트를 세분화 및 개인화에 사용할 수 있습니다. 이 기능은 명확한 사람 대상을 만들려는 마케터를 지원합니다.

또한 [!DNL Query Service]은(는) 자동연장 또는 정적 조건을 충족하는 논리를 쿼리에 포함시켜 정교한 세분화를 가능하게 합니다.

Adobe Experience Platform은 효율적이고 안정적인 방식으로 데이터를 활성화하는 데 필요한 데이터 저장소 및 도구를 제공합니다. Experience Platform 내에 데이터를 유지하면 다른 프로세스를 실행하는 동안 속성을 파생할 수 있으며, 조작 및 처리를 위해 데이터를 서드파티 도구로 내보낼 필요가 없습니다. 이러한 처리 오버헤드는 수백 개의 속성 또는 캠페인을 처리할 때 프로젝트 타임라인에 큰 영향을 줄 수 있습니다. 이렇게 하면 마케터가 데이터에 액세스하고 캠페인을 구축할 수 있는 단일 위치뿐만 아니라 메시지를 세그먼트화하고 개인화할 수 있는 매우 동적인 수단을 제공합니다.

## 다음 단계

이 문서를 읽으면 이제 [!DNL Query Service]이(가) 전체 통합 워크플로우를 위해 데이터의 품질과 세그먼테이션의 용이성뿐만 아니라 데이터 아키텍처 내에서 데이터의 중요성에 어떤 영향을 미치는지 이해할 수 있습니다. Adobe Analytics을 [!DNL Query Service]과(와) 함께 사용하는 적용 가능한 SQL 예제는 [Adobe Analytics 머천다이징 변수 사용 사례](./merchandising-variables.md)를 참조하십시오.

조직의 전략적 비즈니스 인사이트에 대한 [!DNL Query Service]의 이점을 보여 주는 다른 문서는 [보트 필터링 사용 사례](./bot-filtering.md) 예입니다.

또는 다음 문서를 통해 [!DNL Query Service] 기능을 이해할 수 있습니다.

* [쿼리 실행 지침](../best-practices/writing-queries.md)
* [데이터 자산 조직에 대한 지침](../best-practices/organize-data-assets.md).


