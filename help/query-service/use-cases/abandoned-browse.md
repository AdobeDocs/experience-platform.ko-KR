---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;쿼리
title: Adobe Experience Platform 쿼리 서비스에 대한 사용 사례 예
description: Adobe Experience Platform Query Service의 다기능성과 이점을 보여주는 완벽한 예입니다.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Adobe Experience Platform 사용 사례 예 [!DNL Query Service]

이 문서 및 함께 제공되는 비디오 프레젠테이션은 Adobe Experience Platform을 어떻게 구현하는지 보여주는 포괄적인 워크플로우를 제공합니다 [!DNL Query Service] 조직의 전략적 비즈니스 통찰력을 얻을 수 있습니다. 이 안내서에서는 찾아보기 포기 사용 사례를 예로 사용하여 다음과 같은 주요 개념을 보여줍니다.

* Adobe Experience Platform의 잠재력을 극대화하기 위한 데이터 처리의 주요 중요성입니다.
* 기존 데이터 아키텍처를 기반으로 쿼리를 빌드하는 방법입니다.
* 요구 사항에 맞는 데이터 품질 및 단점을 완화하는 방법을 보장합니다.
* 세분화 및 개인화를 위한 대상의 다운스트림으로 사용하기 위해 설정된 빈도에서 쿼리를 실행하도록 예약하는 프로세스입니다.
* 마케터는 의 기능을 통해 세그먼트에 파생 속성을 쉽게 포함할 수 있습니다. [!DNL Query Service].

## 목표 {#objectives}

이 워크플로우 데모는 여러 Adobe Experience Platform 서비스를 사용합니다. 계속 진행하려면 다음 기능 및 서비스를 잘 이해하는 것이 좋습니다.

* 다음 [xdm(Experience Data Model) 스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md)
* 방법 [데이터 세트 생성 및 데이터 수집](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 방법 [Adobe Analytics 소스 커넥터를 사용하여 데이터 수집](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=ko-KR)
* [세그먼테이션](../../segmentation/home.md)
* [대상](../../destinations/home.md)

찾아보기 포기 예제에서는 Adobe 사용을 중심으로 합니다 [!DNL Analytics] 데이터를 추가하여 실행 가능한 특정 대상을 만들 수 있습니다. 지난 4일 동안 웹 사이트를 탐색했지만 구매하지 않은 모든 고객을 포함하도록 대상을 다듬습니다. 그런 다음 대상의 각 프로필은 고객의 행동 패턴으로 인한 가장 높은 가격 SKU로 타겟팅됩니다.

쿼리 자체는 매우 규범적이며 세그먼트 정의에 대한 사용 사례 기준을 충족하는 데이터만 포함합니다. 이렇게 하면 [!DNL Analytics] 처리 중인 데이터. 또한 가장 높은 가격에서 가장 낮은 가격으로 데이터를 주문하고 사용자가 탐색하고 있던 가장 높은 가격의 SKU를 선택합니다.

프레젠테이션에 사용된 쿼리는 다음과 같습니다.

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

## [!DNL Query Service] adobe analytics를 사용한 찾아보기 포기 예 {#video-example}

아래 표시된 비디오 프레젠테이션은 중점을 둔 Experience Platform 데이터를 위한 전체적이고 실세계 사용 사례를 제공합니다 [!DNL Query Service] Adobe 분석 통합을 사용할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## 이점 [!DNL Query Service] {#benefits}

에서 제공하는 기능 [!DNL Query Service] 은 많은 용도로 사용됩니다. 이를 사용하여 세그먼테이션에 대한 복잡한 논리를 수용하거나, 다운스트림으로 사용할 수 있도록 다양한 개인화된 특성을 계산하거나, 세그먼트를 작성하는 방법을 크게 간소화할 수 있습니다.

[!DNL Query Service] 쿼리에 제한을 포함하여 세그먼트 작성 프로세스를 단순화할 수 있습니다. 이렇게 하면 올바른 데이터가 세그먼트에 적합하고 더 정확한 대상을 만들 수 있으므로 데이터 품질이 향상됩니다. 쿼리의 품질을 유지하면 정확한 대상이 되고 데이터 신뢰성이 향상됩니다. 쿼리에서 파생된 특성을 기반으로 스키마와 사용자 지정 테이블을 만들어 대상을 저장할 수도 있습니다. 프로필에 대해 사용자 지정 테이블을 활성화할 수 있으며, 이러한 데이터 포인트를 세그멘테이션 및 개인화에 사용할 수 있습니다. 이 기능은 명확한 사용자 대상자를 만들려는 마케터를 지원합니다.

또한 쿼리에 로직을 포함하여 반복되는 조건이나 정적 조건을 만족합니다. [!DNL Query Service] 정교한 세그멘테이션의 부담을 추출하다.

Adobe Experience Platform은 효율적이고 안정적인 방식으로 데이터를 활성화하는 데 필요한 도구와 데이터 저장소를 제공합니다. 데이터를 Platform 내에 유지하면 다른 프로세스를 실행하는 동안 속성을 파생하고 조작 및 처리를 위해 데이터를 타사 도구로 내보낼 필요성을 제거할 수 있습니다. 이러한 처리 오버헤드는 수백 개의 속성 또는 캠페인을 처리할 때 프로젝트 타임라인에 큰 영향을 줄 수 있습니다. 이를 통해 마케터는 데이터에 액세스하고 캠페인을 구축할 수 있는 단일 위치와 메시지를 세그먼트화하고 개인화하는 매우 동적인 방법을 제공합니다.

## 다음 단계

이 문서를 읽은 후에는 [!DNL Query Service] 는 데이터의 품질 및 세그먼테이션의 용이성뿐만 아니라 전체 전체 워크플로우에 대한 데이터 아키텍처 내의 중요성에도 영향을 줍니다. Adobe Analytics과 함께 사용하는 적용 가능한 SQL 예가 필요하면 [!DNL Query Service]를 참조하고 [Adobe Analytics 머천다이징 변수 사용 사례](./merchandising-variables.md).

다음과 같은 이점을 보여주는 기타 문서 [!DNL Query Service] 조직의 전략적 비즈니스 인사이트는 [보트 필터링 사용 사례](./bot-filtering.md) 예.

또는 이러한 문서를 사용하면 [!DNL Query Service] 기능:

* [쿼리 실행 지침](../best-practices/writing-queries.md)
* [데이터 자산 조직에 대한 지침](../best-practices/organize-data-assets.md).


