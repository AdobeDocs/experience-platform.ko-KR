---
title: Algolia 태그 확장 개요
description: Adobe Experience Platform의 Algolia 태그 확장에 대해 알아봅니다.
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 6eee26df3841a7829625361fc726bf59a278f867
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 1%

---

# [!DNL Algolia] 태그 확장 개요

[!DNL Algolia] 태그 확장을 사용하면 마케터가 사용자 상호 작용 데이터를 [!DNL Algolia]에 보내는 규칙을 쉽게 설정할 수 있으므로 보다 개인화된 AI 검색 및 검색 경험을 제공할 수 있습니다.

이 확장은 다음과 같은 주요 기능을 통해 제공됩니다.

* **[!DNL Algolia]인사이트**: 사용자 상호 작용 이벤트를 자동으로 캡처하여 [!DNL Algolia]에 보내어 강력한 분석, 개인화된 경험 및 향상된 검색 관련성을 가능하게 합니다.

## 전제 조건 {#prerequisites}

이 확장을 사용하려면 올바른 [!DNL Algolia] 계정이 있어야 합니다. 계정이 아직 없는 경우 [[!DNL Algolia] 등록 페이지](https://dashboard.algolia.com/users/sign_up)&#x200B;(으)로 이동하여 계정을 만드십시오.

### 필요한 구성 세부 정보 수집 {#configuration-details}

[!DNL Algolia]을(를) Adobe Experience Platform에 연결하려면 다음 정보가 필요합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 애플리케이션 ID | 응용 프로그램 ID는 [ 대시보드의 ](https://www.algolia.com/account/api-keys/all)API 키[!DNL Algolia] 섹션에서 찾을 수 있습니다. | 0ABCDEPG12 |
| API 키 검색 | 검색 API 키는 [ 대시보드의 ](https://www.algolia.com/account/api-keys/all)API 키[!DNL Algolia] 섹션에서 찾을 수 있습니다. | 1234a12345678901b1234567890c1ab1 |

## [!DNL Algolia] Insights 확장 설치 및 구성 {#install-configure}

[!DNL Algolia] Insights 확장을 설치하려면 [!UICONTROL Data Collection UI]&#x200B;(으)로 이동하여 왼쪽 탐색에서 **[!UICONTROL Tags]**&#x200B;을(를) 선택하십시오. 여기에서 확장을 추가할 속성을 선택하거나 새 속성을 대신 만듭니다.

원하는 속성을 선택하거나 만들었으면 왼쪽 탐색에서 **[!UICONTROL Extensions]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Catalog]** 탭을 선택합니다. [!DNL Algolia] 인사이트 카드를 검색한 다음 **[!UICONTROL Install]**&#x200B;을(를) 선택합니다.

![](../../../images/extensions/client/algolia/install.png)

표시되는 구성 보기에서 다음 세부 정보를 제공해야 합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Application ID] | 이전에 [!UICONTROL Application Id]구성 세부 정보[ 섹션에서 수집한 ](#configuration-details)을(를) 입력하십시오. |
| [!UICONTROL Search API Key] | 이전에 [!UICONTROL Search API Key]구성 세부 정보[ 섹션에서 수집한 ](#configuration-details)을(를) 입력하십시오. |
| [!UICONTROL Index Name] | [!UICONTROL Index Name]에 제품 또는 콘텐츠가 포함되어 있습니다.  이 색인은 기본값으로 사용됩니다. |
| [!UICONTROL User Token Data Element] | 사용자 토큰을 반환하는 데이터 요소입니다. |
| [!UICONTROL Authenticated User Token Data Element] | 인증된 사용자 토큰을 반환하는 데이터 요소를 설정합니다. |
| [!UICONTROL Currency Code] | USD 또는 EUR과 같은 ISO-4217 형식의 통화 코드를 입력합니다. 이 필드는 데이터 요소를 지원합니다. |

![](../../../images/extensions/client/algolia/configure.png)

## [!DNL Algolia] Insights 확장 작업 유형 {#action-types}

[!DNL Algolia]은(는) 특정 컨텍스트 및 속성을 포함하는 미리 정의된 표준 이벤트 집합을 지원합니다. [!DNL Algolia] 확장에서 사용할 수 있는 작업은 이러한 이벤트 유형에 맞게 조정되므로 해당 유형에 따라 [!DNL Algolia]에 보내는 이벤트를 쉽게 분류하고 구성할 수 있습니다.

### 인사이트 로드 {#load-insights}

>[!NOTE]
>
>대부분의 경우 사이트의 모든 페이지에서 [!DNL Algolia] 인사이트를 로드하는 것이 좋습니다.

규칙 컨텍스트에 따라 **[!UICONTROL Load Insights]** 인사이트를 로드하는 것이 가장 적절할 때마다 [!DNL Algolia] 작업을 태그 규칙에 추가하십시오. 이 작업은 `search-insights.js` 라이브러리를 페이지에 로드합니다.

새 태그 규칙을 만들거나 기존 태그 규칙을 엽니다. 요구 사항에 따라 조건을 정의한 다음 **[!UICONTROL Algolia]**&#x200B;을(를) [!UICONTROL Extension]&#x200B;(으)로 선택하고 **[!UICONTROL Load Insights]**&#x200B;을(를) [!UICONTROL Action Type]&#x200B;(으)로 선택합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Insight Library Version] | [!DNL Algolia] Insights 버전입니다. 기본값은 `2.17.3`입니다. |
| [!UICONTROL User Opt Out Data Element] | 사용자의 추적 환경 설정을 캡처하는 데이터 요소입니다. |
| [!UICONTROL Use User Token Cookie] | [!DNL Algolia]이(가) 사용자 토큰 쿠키를 생성할 수 있도록 하려면 이 확인란을 선택하십시오. 기본적으로 이 옵션은 `true`(으)로 설정됩니다. |

![](../../../images/extensions/client/algolia/load-insights.png)

### 클릭됨 {#clicked}

클릭한 이벤트를 **[!UICONTROL Click]**(으)로 보내려면 태그 규칙에 [!DNL Algolia] 작업을 추가하십시오. 새 태그 규칙을 만들거나 기존 태그 규칙을 엽니다. 요구 사항에 따라 조건을 정의한 다음 **[!UICONTROL Algolia]**&#x200B;을(를) [!UICONTROL Extension]&#x200B;(으)로 선택하고 **[!UICONTROL Clicked]**&#x200B;을(를) [!UICONTROL Action Type]&#x200B;(으)로 선택합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Event Name] | 이 클릭 이벤트를 세분화하는 데 사용할 수 있는 이벤트 이름입니다. |
| [!UICONTROL Event Details Data Element] | 데이터 요소는 다음을 포함하여 이벤트 세부 사항을 JSON 형식으로 반환합니다. <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID`(선택 사항)</li><li>`positions`(선택 사항)</li><li>`price`(선택 사항)</li><li>`quantity`(선택 사항)</li><li>`discount`(선택 사항)</li><li>`objectData`(선택 사항)</li><li>`currency`(선택 사항)</li></ul> |


>[!NOTE]
>
>`queryID`과(와) `positions`이(가) 모두 포함된 경우 이벤트는 **검색 후 클릭한 개체 ID**(으)로 분류됩니다. 그렇지 않으면 **클릭한 개체 ID** 이벤트로 클래스화됩니다.
><br>
>데이터 요소가 `indexName`을(를) 제공하지 않으면 이벤트를 보낼 때 **기본 인덱스 이름**&#x200B;이(가) 사용됩니다.

![](../../../images/extensions/client/algolia/clicked.png)

이벤트 범주에 대한 자세한 내용은 [검색 후 클릭한 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)를 참조하십시오.
및 [클릭한 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/) 안내서입니다.

### 전환됨 {#converted}

**[!UICONTROL Converted]** 작업을 태그 규칙에 추가하여 변환된 이벤트를 [!DNL Algolia]&#x200B;(으)로 보냅니다. 새 태그 규칙을 만들거나 기존 태그 규칙을 엽니다. 요구 사항에 따라 조건을 정의한 다음 **[!UICONTROL Algolia]**&#x200B;을(를) [!UICONTROL Extension]&#x200B;(으)로 선택하고 **[!UICONTROL Converted]**&#x200B;을(를) [!UICONTROL Action Type]&#x200B;(으)로 선택합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Event Name] | 이 **convert** 이벤트를 세분화하는 데 사용할 이벤트 이름입니다. |
| [!UICONTROL Event Details Data Element] | 데이터 요소는 다음을 포함한 이벤트 세부 정보를 반환합니다. <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID`(선택 사항)</li><li>`recordID`(선택 사항)</li></ul> |

>[!NOTE]
>
>데이터 요소에 `queryId`이(가) 포함된 경우 이벤트는 **검색 후 변환됨**(으)로 분류됩니다. 그렇지 않으면 **변환** 이벤트로 분류됩니다.
><br>
>데이터 요소가 `indexName`을(를) 제공하지 않으면 이벤트를 보낼 때 **기본 인덱스 이름**&#x200B;이(가) 사용됩니다.

![](../../../images/extensions/client/algolia/converted.png)

이벤트 범주에 대한 자세한 내용은 [검색 후 변환된 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/) 및 [변환된 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/) 안내서를 참조하십시오.

### 장바구니에 추가됨 {#added-to-cart}

장바구니에 추가한 이벤트를 **[!UICONTROL Added to Cart]**(으)로 보내려면 태그 규칙에 [!DNL Algolia] 작업을 추가하십시오. 새 태그 규칙을 만들거나 기존 태그 규칙을 엽니다. 요구 사항에 따라 조건을 정의한 다음 **[!UICONTROL Algolia]**&#x200B;을(를) [!UICONTROL Extension]&#x200B;(으)로 선택하고 **[!UICONTROL Added to cart]**&#x200B;을(를) [!UICONTROL Action Type]&#x200B;(으)로 선택합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Event Name] | 이 **장바구니에 추가** 이벤트를 세분화하는 데 사용할 이벤트 이름. |
| [!UICONTROL Event Details Data Element] | 데이터 요소는 다음을 포함하여 이벤트 세부 사항을 JSON 형식으로 반환합니다. <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount`(선택 사항)</li><li>`queryID`(선택 사항)</li><li>`currency`(선택 사항)</li></ul>. |

>[!NOTE]
>
>데이터 요소에 `queryId`이(가) 포함된 경우 이벤트는 **검색 후 장바구니 개체 ID에 추가됨**(으)로 분류됩니다. 그렇지 않으면 **장바구니 개체 ID에 추가됨** 이벤트로 분류됩니다.
><br>
>데이터 요소가 `indexName`을(를) 제공하지 않으면 이벤트를 보낼 때 **기본 인덱스 이름**이(가) 사용됩니다.
><br>
>기본 데이터 요소가 요구 사항을 충족하지 않는 경우 사용자 지정 데이터 요소를 만들어 원하는 이벤트 세부 정보를 반환할 수 있습니다.

![](../../../images/extensions/client/algolia/added-to-cart.png)

이벤트 범주에 대한 자세한 내용은 [검색 후 장바구니 개체 ID에 추가됨](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/) 및 [장바구니 개체 ID에 추가됨](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/) 안내서를 참조하십시오.

### 구매됨 {#purchased}

**[!UICONTROL Purchased]** 작업을 태그 규칙에 추가하여 구매한 이벤트를 [!DNL Algolia]&#x200B;(으)로 보냅니다. 새 태그 규칙을 만들거나 기존 태그 규칙을 엽니다. 요구 사항에 따라 조건을 정의한 다음 **[!UICONTROL Algolia]**&#x200B;을(를) [!UICONTROL Extension]&#x200B;(으)로 선택하고 **[!UICONTROL Purchased]**&#x200B;을(를) [!UICONTROL Action Type]&#x200B;(으)로 선택합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Event Name] | 이 **구매** 이벤트를 세분화하는 데 사용할 이벤트 이름. |
| [!UICONTROL Event Details Data Element] | 데이터 요소는 다음을 포함하여 이벤트 세부 사항을 JSON 형식으로 반환합니다. <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount`(선택 사항)</li><li>`queryID`(선택 사항)</li><li>`currency`(선택 사항)</li></ul>. |

>[!NOTE]
>
>구매 작업은 구매한 항목 ID를 기반으로 브라우저 저장소에서 이벤트 데이터를 검색합니다. 구매한 항목 중 저장된 데이터에 `queryID`이(가) 포함된 항목이 있으면 이벤트는 **검색 후 구매한 개체 ID**(으)로 분류됩니다. 그렇지 않으면 **구매한 개체 ID** 이벤트로 분류됩니다.
><br>
>이 접근 방식을 사용하면 구매 이벤트에 사용자와 항목의 이전 상호 작용에서 모든 관련 컨텍스트(쿼리 ID, 색인명, 가격, 수량, 할인)가 자동으로 포함될 수 있습니다.

![](../../../images/extensions/client/algolia/purchased.png)

이벤트 범주에 대한 자세한 내용은 [검색 후 구매한 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)를 참조하십시오.
및 [구매한 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/) 가이드가 있습니다.

### 조회함 {#viewed}

**[!UICONTROL Viewed]** 작업을 태그 규칙에 추가하여 구매한 이벤트를 [!DNL Algolia]&#x200B;(으)로 보냅니다. 새 태그 규칙을 만들거나 기존 태그 규칙을 엽니다. 요구 사항에 따라 조건을 정의한 다음 **[!UICONTROL Algolia]**&#x200B;을(를) [!UICONTROL Extension]&#x200B;(으)로 선택하고 **[!UICONTROL Viewed]**&#x200B;을(를) [!UICONTROL Action Type]&#x200B;(으)로 선택합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Event Name] | 이 **보기** 이벤트를 세분화하는 데 사용할 이벤트 이름입니다. |
| [!UICONTROL Event Details Data Element] | 데이터 요소는 다음을 포함하여 이벤트 세부 사항을 JSON 형식으로 반환합니다. <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>데이터 요소가 `indexName`을(를) 제공하지 않으면 이벤트를 보낼 때 **기본 인덱스 이름**&#x200B;이(가) 사용됩니다.

![](../../../images/extensions/client/algolia/viewed.png)

보기 이벤트에 대한 자세한 내용은 [본 개체 ID](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/) 안내서를 참조하십시오.

## [!DNL Algolia] Insights 확장 데이터 요소 {#data-elements}

[!DNL Algolia]은(는) 특정 컨텍스트 및 속성을 포함하는 미리 정의된 데이터 요소 집합을 지원합니다. 다음 섹션에서는 [!DNL Algolia] Insights 확장에서 사용할 수 있는 데이터 요소에 대해 설명합니다.

### 데이터 집합 {#dataset}

DataSet Data Element는 HTML 요소와 관련된 데이터를 검색하여 [!DNL Algolia] 작업에 사용합니다. 이 데이터 요소는 검색한 이벤트 데이터를 나중에 사용할 수 있도록 브라우저 저장소에 자동으로 저장합니다(예: 전환 또는 구매 이벤트).

**일반 구성:**

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Hit Element Div/Class Name] | HTML 요소 이름 및/또는 HTML 요소의 `data-insights-object-id` 및 `data-insights-query-id` 및 `data-insights-position`을(를) 포함하는 데이터 세트 특성을 포함하는 CSS 클래스 이름입니다. |
| [!UICONTROL Index Name Element Div/Class Name] | HTML 요소에 데이터 집합 특성(`data-indexname`)이 있는 HTML 요소 이름 및/또는 CSS 클래스 이름입니다. |

**Commerce 구성(선택 사항):**

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Price Data Element] | 항목에 대한 가격을 반환하는 데이터 요소입니다. 제공되면 상거래 이벤트에 대한 저장된 이벤트 데이터에 포함됩니다. |
| [!UICONTROL Quantity Data Element] | 항목에 대한 수량을 반환하는 데이터 요소입니다. 지정하지 않은 경우 기본값은 1입니다. |
| [!UICONTROL Discount Data Element] | 항목에 대한 할인 십진수 값을 반환하는 데이터 요소입니다. |
| [!UICONTROL Currency Code] | ISO-4217 형식의 통화 코드. 통화 코드를 지정하지 않으면 확장 구성의 기본 통화가 사용됩니다. |

**재정의(선택 사항):**

이러한 필드를 사용하면 HTML 데이터 세트 속성에서 데이터를 검색하는 기본 동작을 재정의할 수 있습니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Record ID Data Element] | 페이지 URL을 레코드 ID로 사용하는 기본 접근 방식을 무시합니다. 레코드 ID는 이 제품/페이지의 [!DNL Algolia]&#x200B;(으)로 보낼 데이터를 저장하고 찾는 데 사용됩니다. |
| [!UICONTROL Query ID Data Element] | 쿼리 ID는 HTML 요소의 데이터 세트에서 검색됩니다. 이 동작을 무시하려면 이 속성을 사용하여 쿼리 ID를 문자열로 반환하는 데이터 요소를 제공합니다. |
| [!UICONTROL Object IDs Data Element] | 개체 ID는 HTML 요소의 데이터 세트에서 검색됩니다. 이 동작을 무시하려면 이 속성을 사용하여 개체 ID를 배열로 반환하는 데이터 요소를 제공합니다. |
| [!UICONTROL Positions Data Element] | 위치는 HTML 요소의 데이터 세트에서 검색됩니다. 이 동작을 무시하려면 이 속성을 사용하여 Position을 배열로 반환하는 데이터 요소를 제공합니다. |
| [!UICONTROL Index Name Data Element] | 색인 이름 은 HTML 요소의 데이터 세트에서 검색됩니다. 이 동작을 무시하려면 이 속성을 사용하여 인덱스 이름을 문자열로 반환하는 데이터 요소를 제공합니다. |

![](../../../images/extensions/client/algolia/dataset.png)

이 데이터 요소는 다음을 반환합니다.

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,
  objectData,  // Optional: commerce data if price is provided
  currency,    // Optional: if provided
  recordID
}
```

데이터 세트가 포함된 HTML의 예:

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### 쿼리 문자열 {#query-string}

쿼리 문자열 데이터 요소는 [!DNL Algolia] 작업에 사용할 URL 쿼리 문자열에서 데이터를 추출합니다.

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Object ID Param Name] | 개체 ID를 포함하는 쿼리 매개 변수 이름입니다. |
| [!UICONTROL Index Name Param Name] | 인덱스 이름을 포함하는 쿼리 매개 변수 이름입니다. |
| [!UICONTROL Query ID Param Name] | 쿼리 ID를 포함하는 쿼리 매개 변수 이름입니다. |
| [!UICONTROL Position Param Name] | Position을 포함하는 쿼리 매개변수 이름. |

![](../../../images/extensions/client/algolia/query-string.png)

이 데이터 요소는 다음을 반환합니다.

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions
}
```

쿼리 매개 변수를 포함하는 HTML의 예:

```html
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### 스토리지 {#storage}

저장소 데이터 요소는 [!DNL Algolia] 작업에 사용할 데이터를 브라우저 세션 저장소에서 검색합니다. 이 데이터 요소를 사용하여 추가 상거래 정보로 저장된 데이터를 보강할 수도 있습니다.

이 데이터 요소는 이전에 세션 저장소에 저장된 이벤트 세부 정보를 검색합니다(일반적으로 클릭 이벤트 동안 DataSet 데이터 요소에 의해). 제거 기능이 명시적으로 비활성화되어 있지 않은 한 전환 이벤트 중에 데이터가 자동으로 제거됩니다.

**재정의(선택 사항):**

| 속성 | 설명 |
| --- | --- |
| [!UICONTROL Record ID Data Element] | 레코드 ID는 브라우저 저장소에 저장된 이벤트 데이터를 조회하는 키로 사용됩니다. 페이지 URL은 기본 레코드 ID입니다. 이 동작을 무시하려면 이 속성을 사용하여 레코드 ID를 문자열로 반환하는 데이터 요소를 제공합니다. |
| [!UICONTROL Price Data Element] | 항목에 대한 가격을 반환하는 데이터 요소입니다. 제공된 경우 저장된 이벤트 데이터가 가격 정보로 업데이트됩니다. |
| [!UICONTROL Quantity Data Element] | 항목에 대한 수량을 반환하는 데이터 요소입니다. 제공된 경우 수량 정보로 저장된 이벤트 데이터가 업데이트됩니다. |
| [!UICONTROL Discount Data Element] | 항목에 대한 할인 십진수 값을 반환하는 데이터 요소입니다. 제공된 경우 저장된 이벤트 데이터가 할인 정보로 업데이트됩니다. |
| [!UICONTROL Currency Code] | 통화 코드를 ISO-4217 형식으로 입력합니다. 제공된 경우 저장된 이벤트 데이터가 통화 정보로 업데이트됩니다. |

![](../../../images/extensions/client/algolia/storage.png)

이 데이터 요소는 증강된 상거래 데이터를 포함하여 세션 저장소에 저장된 것을 반환합니다.

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,      // If available from original event
  objectData,     // Optional: commerce data if price is provided
  currency,       // Optional: if provided
  recordID
}
```

## 검색 후 클릭 또는 변환됨 {#clicked-converted-after-search}

*검색 후 클릭* 또는 *검색 후 전환* 이벤트에는 `queryID`이 필요하며 `positions`은(는) *검색 후 클릭*&#x200B;에도 필요합니다. 이러한 속성은 InstantSearch 및/또는 Autocomplete 쿼리 매개 변수에서 `insights` 플래그를 사용하도록 설정한 경우 사용할 수 있습니다. 사이트에 대한 Insights를 구성하는 방법에 대해 알아보려면 다음 리소스를 참조하십시오.

* [자동 완성에 대한 인사이트 설정](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [InstantSearch.js에 대한 인사이트 설정](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [클릭 및 전환 이벤트 시작](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [Insights 이벤트 보내기 [!DNL Algolia] 2}](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Launch 확장 GitHub 저장소](https://github.com/algolia/algolia-launch-extension)
* [InstantSearch.js 설명서](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] Insights API 설명서](https://www.algolia.com/doc/rest-api/insights/)
* [Algolia Launch 확장 코드 리포지토리](https://github.com/algolia/algolia-launch-extension)

## 다음 단계 {#next-steps}

이 안내서에서는 [!DNL Algolia] 태그 확장을 사용하여 데이터를 [!DNL Algolia Insights]에 보내는 방법을 다룹니다. [!DNL Algolia]에도 서버측 이벤트를 보낼 계획이라면 [[!DNL Conversions API] 이벤트 전달 확장](../../server/algolia/overview.md)을 설치하고 구성할 수 있습니다.

Experience Platform의 태그에 대한 자세한 내용은 [태그 개요](../../../home.md)를 참조하세요.
