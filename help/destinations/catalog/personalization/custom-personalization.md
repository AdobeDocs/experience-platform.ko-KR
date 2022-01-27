---
keywords: 사용자 지정 개인화; 대상; experience platform 사용자 지정 대상
title: 사용자 지정 개인화 연결
description: 이 대상은 Adobe Experience Platform에서 세그먼트 정보를 검색하는 방법으로 사이트에서 실행 중인 외부 개인화, 콘텐츠 관리 시스템, 광고 서버 및 기타 애플리케이션을 제공합니다. 이 대상은 사용자 프로필 세그먼트 멤버십에 따라 실시간 개인화를 제공합니다.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: cfbf8fb29d15badd10bafe35c558d95e534d23e8
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 사용자 지정 개인화 연결 {#custom-personalization-connection}

## 개요 {#overview}

이 대상은 Adobe Experience Platform에서 외부 개인화 플랫폼, 콘텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행 중인 기타 응용 프로그램으로 세그먼트 정보를 검색하는 방법을 제공합니다.

## 전제 조건 {#prerequisites}

이 통합은 [Adobe Experience Platform Web SDK](../../../edge/home.md) 또는 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). 이 대상을 사용하려면 이 SDK 중 하나를 사용해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 요청** - 단일 프로필에 대해 사용자 지정 개인화 대상에 매핑된 모든 세그먼트를 요청합니다. 서로 다른 사용자 지정 개인화 대상을 설정할 수 있습니다 [Adobe 데이터 수집 데이터 스트림](../../../edge/fundamentals/datastreams.md).

## 사용 사례 {#use-cases}

이 대상은 웹 사이트에 표시되어야 하는 광고 사용자를 결정하기 위해 실시간으로 사용할 광고 서버 및 비Adobe 개인화 애플리케이션과 대상을 공유합니다.

### 사용 사례 #1

**홈 페이지 개인화**

홈 대여 및 판매 웹 사이트에서 Adobe Experience Platform의 세그먼트 자격에 따라 홈 페이지를 개인화하려고 합니다. 회사는 개인화된 경험을 제공해야 하는 대상을 선택하고, 타깃팅 기준으로 비Adobe 개인화 애플리케이션에 대해 설정된 사용자 지정 개인화 대상에 매핑할 수 있습니다.

**타깃팅된 온사이트 광고**

광고 서버에 대해 별도의 사용자 지정 개인화 대상을 사용하는 동일한 웹 사이트에서는 타깃팅 기준으로 Adobe Experience Platform의 다른 세그먼트 세트를 사용하여 온사이트 광고를 타깃팅할 수 있습니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **[!UICONTROL 통합 별칭]**: 이 값은 JSON 개체 이름으로 Experience Platform Web SDK에 전송됩니다.
* **[!UICONTROL 데이터 스트림 ID]**: 이에 따라 페이지에 대한 응답에 세그먼트를 포함할 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에는 대상 구성이 활성화된 데이터 세트만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](../../../edge/fundamentals/datastreams.md) 자세한 내용

## 세그먼트를 이 대상에 활성화 {#activate}

읽기 [프로필 요청 대상에 프로필 및 세그먼트 활성화](../../ui/activate-profile-request-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

사용 중인 경우 [Adobe 태그](../../../tags/home.md) Experience Platform 웹 SDK를 배포하려면 [이벤트 완료 보내기](../../../edge/extension/event-types.md) 기능 및 사용자 지정 코드 작업에는 `event.destinations` 내보낸 데이터를 보는 데 사용할 수 있는 변수입니다.

다음은 의 샘플 값입니다 `event.destinations` 변수:

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

을 사용하지 않는 경우 [Adobe 태그](../../../tags/home.md) Experience Platform 웹 SDK를 배포하려면 [이벤트에서 응답 처리](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 내보낸 데이터를 확인하는 기능입니다.

Adobe Experience Platform의 JSON 응답을 구문 분석하여 Adobe Experience Platform과 통합하는 애플리케이션의 해당 통합 별칭을 찾을 수 있습니다. 세그먼트 ID를 타깃팅 매개 변수로 애플리케이션의 코드에 전달할 수 있습니다. 아래는 대상 응답에만 적용되는 샘플입니다.

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](../../../data-governance/home.md).
