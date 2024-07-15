---
keywords: 사용자 정의 개인화; 대상; experience platform 사용자 정의 대상;
title: 사용자 지정 개인화 연결
description: 이 대상은 Adobe Experience Platform에서 대상 정보를 검색할 수 있는 방법을 통해 사이트에서 실행 중인 외부 개인화, 콘텐츠 관리 시스템, 광고 서버 및 기타 애플리케이션을 제공합니다. 이 대상은 사용자 프로필 대상 멤버십을 기반으로 실시간 개인화를 제공합니다.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 182176aa2e588aa356d5fea23b49f17bc8a50314
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 9%

---


# 사용자 지정 개인화 연결 {#custom-personalization-connection}

## 대상 변경 로그 {#changelog}

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 5월 | 기능 및 설명서 업데이트 | 2023년 5월부터 **[!UICONTROL 사용자 지정 개인화]** 연결은 [특성 기반 개인화](../../ui/activate-edge-personalization-destinations.md#map-attributes)를 지원하며 일반적으로 모든 고객이 사용할 수 있습니다. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>프로필 속성에 중요한 데이터가 포함될 수 있습니다. 이 데이터를 보호하려면 특성 기반 개인화를 위해 **[!UICONTROL Edge Network 지정 Personalization]** 대상을 구성할 때 [사용자 지정 서버 API](/help/server-api/overview.md)를 사용해야 합니다. 모든 서버 API 호출은 [인증된 컨텍스트](../../../server-api/authentication.md)에서 수행되어야 합니다.
>
><br>웹 또는 Mobile SDK 구현에 이미 사용하고 있는 것과 동일한 데이터 스트림을 사용하는 서버측 통합을 추가하여 [Edge Network 서버 API](/help/server-api/overview.md)를 통해 프로필 특성을 검색할 수 있습니다.
>
><br>위의 요구 사항을 따르지 않는 경우 개인화는 대상자 멤버십만 기반으로 합니다.

## 개요 {#overview}

외부 개인화 플랫폼, 컨텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행 중인 기타 애플리케이션이 Adobe Experience Platform에서 대상 정보를 검색할 수 있도록 하려면 이 대상을 설정하십시오.

## 전제 조건 {#prerequisites}

이 통합은 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) 또는 [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)에서 제공됩니다. 이 대상을 사용하려면 다음 SDK 중 하나를 사용해야 합니다.

>[!IMPORTANT]
>
>사용자 지정 개인화 연결을 만들기 전에 [대상 데이터를 Edge 개인화 대상으로 활성화](../../ui/activate-edge-personalization-destinations.md)하는 방법에 대한 안내서를 읽어 보십시오. 이 안내서에서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ 덧신 | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!DNL Profile request]** | 단일 프로필에 대해 사용자 지정 개인화 대상에서 매핑된 모든 대상을 요청합니다. 다른 [Adobe 데이터 수집 데이터스트림](../../../datastreams/overview.md)에 대해 다른 사용자 지정 개인화 대상을 설정할 수 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="데이터스트림 ID 정보"
>abstract="이 옵션은 페이지에 대한 응답으로 대상자에 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 대상을 구성하려면 먼저 데이터스트림을 구성해야 합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ko-KR" text="데이터스트림을 구성하는 방법에 대해 알아보기"

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력하십시오. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **[!UICONTROL 통합 별칭]**: 이 값은 JSON 개체 이름으로 Experience Platform Web SDK에 전송됩니다.
* **[!UICONTROL 데이터 스트림 ID]**: 페이지 응답에 대상이 포함될 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](../../../datastreams/overview.md)을 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 대한 대상자 활성화에 대한 지침은 [프로필 및 대상자 에지 개인화 대상 활성화](../../ui/activate-edge-personalization-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

[Adobe Experience Platform의 태그](../../../tags/home.md)를 사용하여 Experience Platform Web SDK를 배포하는 경우 [완료 보내기](../../../tags/extensions/client/web-sdk/event-types.md) 기능을 사용하면 사용자 지정 코드 작업에 `event.destinations` 변수가 포함되며, 이 변수를 사용하여 내보낸 데이터를 볼 수 있습니다.

다음은 `event.destinations` 변수의 샘플 값입니다.

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

[태그](/help/tags/home.md)를 사용하여 Experience Platform Web SDK를 배포하지 않는 경우 [명령 응답](/help/web-sdk/commands/command-responses.md)을 사용하여 내보낸 데이터를 봅니다.

Adobe Experience Platform의 JSON 응답을 구문 분석하여 Adobe Experience Platform과 통합 중인 애플리케이션의 해당 통합 별칭을 찾을 수 있습니다. 대상 ID는 타깃팅 매개 변수로 애플리케이션의 코드에 전달될 수 있습니다. 다음은 대상 응답에만 적용되는 예제입니다.

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

### 특성이 있는 [!UICONTROL 사용자 지정 Personalization]에 대한 응답 예

특성이 있는 **[!UICONTROL 사용자 지정 Personalization]**&#x200B;을(를) 사용하는 경우 API 응답은 아래 예와 비슷합니다.

**[!UICONTROL 특성이 있는 사용자 지정 Personalization]**&#x200B;과(와) **[!UICONTROL 사용자 지정 Personalization]**&#x200B;의 차이점은 API 응답에 `attributes` 섹션이 포함되어 있다는 것입니다.

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

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../../data-governance/home.md)를 참조하십시오.
