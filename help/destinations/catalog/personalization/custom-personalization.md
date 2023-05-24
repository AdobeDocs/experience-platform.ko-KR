---
keywords: 사용자 정의 개인화; 대상; experience platform 사용자 정의 대상;
title: 사용자 지정 개인화 연결
description: 이 대상은 Adobe Experience Platform에서 세그먼트 정보를 검색하는 방법을 통해 사이트에서 실행 중인 외부 개인화, 콘텐츠 관리 시스템, 광고 서버 및 기타 애플리케이션을 제공합니다. 이 대상은 사용자 프로필 세그먼트 멤버십을 기반으로 실시간 개인화를 제공합니다.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# 사용자 지정 개인화 연결 {#custom-personalization-connection}

## 대상 변경 로그 {#changelog}

확장 베타 릴리스 사용 **[!UICONTROL 사용자 정의 개인화]** 대상 커넥터, 다음 두 가지가 표시될 수 있습니다. **[!UICONTROL 사용자 정의 개인화]** 대상 카탈로그의 카드.

다음 **[!UICONTROL 속성을 사용한 사용자 지정 개인화]** 커넥터는 현재 beta 버전이며 일부 고객만 사용할 수 있습니다. 에서 제공하는 기능 외 에도 **[!UICONTROL 사용자 정의 개인화]**, **[!UICONTROL 속성을 사용한 사용자 지정 개인화]** 커넥터가 옵션 추가 [매핑 단계](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 프로필 속성을 사용자 지정 개인화 대상에 매핑하여 속성 기반 동일 페이지 및 다음 페이지 개인화를 활성화하는 활성화 작업 과정입니다.

>[!IMPORTANT]
>
>프로필 속성에 중요한 데이터가 포함될 수 있습니다. 이 데이터를 보호하려면 **[!UICONTROL 속성을 사용한 사용자 지정 개인화]** 대상을 사용하려면 다음을 사용해야 합니다. [Edge Network Server API](/help/server-api/overview.md) 데이터 수집용. 또한 모든 서버 API 호출은 [인증된 컨텍스트](../../../server-api/authentication.md).
>
>통합에 웹 SDK 또는 모바일 SDK를 이미 사용 중인 경우 다음 두 가지 방법으로 서버 API를 통해 속성을 검색할 수 있습니다.
>
> * 서버 API를 통해 속성을 검색하는 서버측 통합을 추가합니다.
> * 서버 API를 통해 속성을 검색하도록 사용자 지정 Javascript 코드로 클라이언트측 구성을 업데이트합니다.
>
> 위의 요구 사항을 따르지 않는 경우 개인화는 에서 제공하는 경험과 동일한 세그먼트 멤버십만을 기반으로 합니다 **[!UICONTROL 사용자 정의 개인화]** 커넥터.

![나란히 보기에 있는 두 개의 사용자 지정 개인화 대상 카드 이미지.](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## 개요 {#overview}

이 대상은 Adobe Experience Platform에서 외부 개인화 플랫폼, 콘텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행 중인 기타 애플리케이션으로 세그먼트 정보를 검색하는 방법을 제공합니다.

## 사전 요구 사항 {#prerequisites}

이 통합은 [Adobe Experience Platform 웹 SDK](../../../edge/home.md) 또는 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). 이 대상을 사용하려면 다음 SDK 중 하나를 사용해야 합니다.

>[!IMPORTANT]
>
>사용자 지정 개인화 연결을 만들기 전에 다음 방법에 대한 안내서를 참조하십시오 [동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](../../ui/configure-personalization-destinations.md). 이 안내서에서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

**프로필 요청** - 단일 프로필에 대해 사용자 지정 개인화 대상에서 매핑된 모든 세그먼트를 요청합니다. 서로 다른 사용자 정의 개인화 대상을 설정할 수 있습니다 [Adobe 데이터 수집 데이터스트림](../../../edge/datastreams/overview.md).

## 사용 사례 {#use-cases}

다음 [!DNL Custom Personalization Connection] 은 고유한 개인화 파트너 플랫폼을 사용할 수 있도록 해줍니다(예: [!DNL Optimizely], [!DNL Pega])와 독점 시스템(예: 사내 CMS)은 물론, Experience Platform Edge Network 데이터 수집 및 세분화 기능을 활용하여 보다 심층적인 고객 개인화 경험을 강화할 수 있습니다.

아래 설명된 사용 사례에는 사이트 개인화 및 타깃팅된 온사이트 광고가 모두 포함됩니다.

이러한 사용 사례를 활성화하려면 고객은 Experience Platform에서 세그먼트 정보를 검색하고 이 정보를 Experience Platform UI에서 사용자 지정 개인화 연결로 구성한 지정된 시스템으로 전송하는 빠르고 간소화된 방법이 필요합니다.

이러한 시스템은 외부 개인화 플랫폼, 콘텐츠 관리 시스템, 광고 서버 및 고객의 웹 및 모바일 속성에서 실행되는 기타 애플리케이션일 수 있습니다.

### 동일 페이지 개인화 {#same-page}

사용자가 웹 사이트의 페이지를 방문합니다. 고객은 현재 페이지 방문 정보(예: 참조 URL, 브라우저 언어, 임베드된 제품 정보)를 사용하여 Adobe이 아닌 플랫폼에 대한 사용자 지정 개인화 연결(예: )을 사용하여 다음 작업/결정(예: 개인화)을 선택할 수 있습니다. [!DNL Pega], [!DNL Optimizely]등).

### 다음 페이지 개인화 {#next-page}

사용자가 웹 사이트에서 페이지 A를 방문합니다. 이러한 상호 작용을 기반으로 사용자는 세그먼트 세트에 대한 자격이 있습니다. 그런 다음 페이지 A에서 페이지 B로 이동하는 링크를 클릭합니다. 현재 웹 사이트 방문에 의해 결정된 프로필 업데이트와 함께 페이지 A에서의 이전 상호 작용 동안 사용자가 적격이었던 세그먼트는 다음 작업/의사 결정(예: 방문자에게 표시할 광고 배너 또는 A/B 테스트의 경우 표시할 페이지 버전)을 수행하는 데 사용됩니다.

### 다음 세션 개인화 {#next-session}

사용자가 웹 사이트의 여러 페이지를 방문합니다. 이러한 상호 작용을 기반으로 사용자는 세그먼트 세트에 대한 자격이 있습니다. 그런 다음 사용자는 현재 탐색 세션을 종료합니다.

다음 날 사용자는 동일한 고객 웹 사이트로 돌아갑니다. 현재 웹 사이트 방문에 의해 결정된 프로필 업데이트와 함께, 방문한 모든 웹 사이트 페이지와의 이전 상호 작용 동안 자격이 부여된 세그먼트는 다음 작업/의사 결정(예: 방문자에게 표시할 광고 배너 또는 A/B 테스트의 경우 표시할 페이지 버전)을 선택하는 데 사용됩니다.

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="데이터스트림 ID 정보"
>abstract="이 옵션은 페이지에 대한 응답으로 세그먼트에 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 대상을 구성하려면 먼저 데이터스트림을 구성해야 합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ko" text="데이터스트림을 구성하는 방법에 대해 알아보기"

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **[!UICONTROL 통합 별칭]**: 이 값은 JSON 개체 이름으로 Experience Platform Web SDK에 전송됩니다.
* **[!UICONTROL 데이터 스트림 ID]**: 페이지에 대한 응답에 세그먼트가 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 다음을 참조하십시오 [데이터스트림 구성](../../../edge/datastreams/overview.md) 을 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [프로필 요청 대상에 프로필 및 세그먼트 활성화](../../ui/activate-profile-request-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

## 내보낸 데이터 {#exported-data}

을 사용하는 경우 [Adobe Experience Platform의 태그](../../../tags/home.md) Experience Platform Web SDK를 배포하려면 [이벤트 전송 완료](../../../edge/extension/event-types.md) 기능과 사용자 지정 코드 작업은 `event.destinations` 내보낸 데이터를 보는 데 사용할 수 있는 변수.

다음은 의 샘플 값입니다. `event.destinations` 변수:

```
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

을 사용하지 않는 경우 [태그](../../../tags/home.md) Experience Platform Web SDK를 배포하려면 [이벤트에서 응답 처리](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 내보낸 데이터를 보는 기능입니다.

Adobe Experience Platform의 JSON 응답을 구문 분석하여 Adobe Experience Platform과 통합 중인 애플리케이션의 해당 통합 별칭을 찾을 수 있습니다. 세그먼트 ID를 타겟팅 매개 변수로 애플리케이션의 코드에 전달할 수 있습니다. 다음은 대상 응답에만 적용되는 예제입니다.

```
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
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### 에 대한 응답 예 [!UICONTROL 속성을 사용한 사용자 지정 개인화]

사용 시 **[!UICONTROL 속성을 사용한 사용자 지정 개인화]**, API 응답은 아래 예와 유사합니다.

차이점 **[!UICONTROL 속성을 사용한 사용자 지정 개인화]** 및 **[!UICONTROL 사용자 정의 개인화]** 은(는) 다음을 포함합니다. `attributes` 섹션에 있는 섹션을 참조하십시오.

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

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](../../../data-governance/home.md).
