---
keywords: 사용자 정의 개인화; 대상; experience platform 사용자 정의 대상;
title: 사용자 지정 Personalization 연결
description: 실시간 온사이트 개인화를 위해 Adobe Experience Platform에서 대상 데이터를 검색하도록 사용자 지정 Personalization 대상을 설정하는 방법에 대해 알아봅니다.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 3779531814cbf7e5718db0ac88aca266f14a1b21
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 8%

---


# 사용자 지정 Personalization 연결 {#custom-personalization-connection}

## 대상 변경 로그 {#changelog}

이 변경 로그를 사용하여 사용자 지정 Personalization 대상에 대한 업데이트를 추적합니다.

| 릴리스 월 | 업데이트 유형 | 설명 |
| --- | --- | --- |
| 2023년 5월 | 기능 및 설명서 업데이트 | 2023년 5월부터 **[!UICONTROL Custom personalization]** 연결은 [특성 기반 개인화](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes)를 지원하며 일반적으로 모든 고객이 사용할 수 있습니다. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>프로필 속성에 중요한 데이터가 포함될 수 있습니다. 이 데이터를 보호하려면 특성 기반 개인화에 대해 [&#x200B; 대상을 구성할 때 &#x200B;](https://developer.adobe.com/data-collection-apis/docs/)Edge Network API **[!UICONTROL Custom Personalization]**&#x200B;를 사용하십시오. 모든 Edge Network API 호출은 [인증된 컨텍스트](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication)에서 수행되어야 합니다.
>
>웹 또는 모바일 SDK 구현에 이미 사용하고 있는 동일한 데이터 스트림을 사용하는 서버측 통합을 추가하여 [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)를 통해 프로필 속성을 검색합니다.
>
>위의 요구 사항을 따르지 않는 경우 개인화는 대상 멤버십만 기반으로 합니다.

## 개요 {#overview}

외부 개인화 플랫폼, 콘텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행 중인 기타 응용 프로그램이 [!DNL Adobe Experience Platform]에서 대상 정보를 검색할 수 있도록 하려면 이 대상을 설정하십시오.

## 전제 조건 {#prerequisites}

이 대상을 사용하려면 구현에 따라 다음 데이터 수집 방법 중 하나가 필요합니다.

* [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md)를 사용하여 웹 사이트에서 데이터를 수집합니다.
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)를 사용하여 모바일 애플리케이션에서 데이터를 수집합니다.
* Web SDK 또는 Mobile SDK을 사용하지 않거나 프로필 특성을 기반으로 사용자 경험을 개인화하려면 [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)를 사용하십시오.

>[!IMPORTANT]
>
>**특성 기반 개인화 요구 사항:** 프로필 특성(대상 멤버십뿐만 아니라)을 기반으로 개인화하려면 **인증된 서버측 통합과 함께** Edge Network API[를 사용](https://developer.adobe.com/data-collection-apis/docs/)해야 합니다. 데이터 수집에 Web SDK나 Mobile SDK도 사용하는지 여부에 관계없이.
>
>웹 SDK 및 모바일 SDK만 대상 멤버십을 기반으로 한 개인화를 지원합니다. Edge Network API는 개인화를 위해 프로필 특성을 안전하게 검색하는 **필수**&#x200B;입니다.

>[!IMPORTANT]
>
>사용자 지정 Personalization 연결을 만들기 전에 [대상 데이터를 Edge 개인화 대상으로 활성화](/help/destinations/ui/activate-edge-personalization-destinations.md)하는 방법에 대한 안내서를 읽어 보십시오. 이 안내서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다.

## 지원되는 대상자 {#supported-audiences}

다음 표에는 이 대상으로 내보낼 수 있는 대상 유형이 나열되어 있습니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](/help/segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 예 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li>CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](/help/segmentation/ui/audience-portal.md#import-audience),</li><li>유사 대상,</li><li>페더레이션 대상,</li><li>[!DNL Adobe Journey Optimizer]과(와) 같은 다른 Experience Platform 앱에서 생성된 대상,</li><li>등.</li></ul> |

{style="table-layout:auto"}

대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 특정 사용자 그룹을 타깃팅합니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

다음 표에서는 이 대상의 내보내기 유형 및 빈도에 대해 설명합니다.

| 항목 | 유형 | 참고 |
| --- | --- | --- |
| 내보내기 유형 | **[!UICONTROL Profile request]** | 사용자 지정 Personalization 대상에 매핑된 모든 대상을 단일 프로필에 대해 요청합니다. 다른 [Personalization 데이터 수집 데이터스트림](/help/datastreams/overview.md)에 대해 다른 사용자 지정 Adobe 대상을 설정할 수 있습니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 항상 API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="데이터 스트림 정보"
>abstract="이 옵션은 페이지에 대한 응답으로 대상자에 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 대상을 구성하려면 먼저 데이터스트림을 구성해야 합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ko" text="데이터스트림을 구성하는 방법에 대해 알아보기"

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](/help/destinations/ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](/help/destinations/ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL Name]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL Description]**: 대상에 대한 설명을 입력하십시오. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **[!UICONTROL Integration alias]**: 개인화 응답에서 이 대상을 식별하는 필수 문자열입니다. 별칭 값은 이 대상과 연결된 대상(및 구성된 경우 속성)과 함께 웹 사이트 또는 앱에 반환됩니다. 클라이언트측 또는 서버측 코드의 별칭을 사용하여 동일한 데이터스트림에서 여러 개인화 대상이 활성화될 때 올바른 개인화 개체를 찾아 처리합니다. 별칭은 모든 사용자 지정 Personalization 대상에 걸쳐 샌드박스 내에서 고유해야 합니다.
* **[!UICONTROL Datastream]**: 페이지 응답에 대상이 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](/help/datastreams/overview.md)을 참조하십시오.

### 경고 활성화 {#enable-alerts}

이 대상에 대한 데이터 흐름 상태에 대한 알림을 받으려면 경고를 활성화하십시오. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](/help/destinations/ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 대한 대상자 활성화에 대한 지침은 [프로필 및 대상자를 Edge 개인화 대상으로 활성화](/help/destinations/ui/activate-edge-personalization-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

[Adobe Experience Platform의 태그](/help/tags/home.md)를 사용하여 Experience Platform Web SDK을 배포하는 경우 [이벤트 보내기 완료](/help/tags/extensions/client/web-sdk/event-types.md) 기능을 사용하십시오. 사용자 지정 코드 작업에는 내보낸 데이터를 보는 데 사용할 수 있는 `event.destinations` 변수가 있습니다.

다음은 `event.destinations` 변수의 샘플 값입니다.

```json
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

[태그](/help/tags/home.md)를 사용하여 Experience Platform Web SDK을 배포하지 않는 경우 [명령 응답](/help/collection/js/commands/command-responses.md)을 사용하여 내보낸 데이터를 확인합니다.

[!DNL Adobe Experience Platform]의 JSON 응답을 구문 분석하여 [!DNL Adobe Experience Platform]과(와) 통합 중인 응용 프로그램의 통합 별칭을 찾습니다. 타깃팅 매개 변수로 대상 ID를 애플리케이션의 코드에 전달합니다. 다음은 대상 응답에만 적용되는 예제입니다.

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there

        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### 속성이 있는 사용자 지정 Personalization에 대한 응답 예 {#example-response-attributes}

**[!UICONTROL Custom Personalization With Attributes]**&#x200B;을(를) 사용하는 경우 API 응답은 아래 예와 비슷합니다.

**[!UICONTROL Custom Personalization With Attributes]**&#x200B;과(와) **[!UICONTROL Custom Personalization]**&#x200B;의 차이점은 API 응답에 `attributes` 섹션이 포함되어 있다는 것입니다.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
