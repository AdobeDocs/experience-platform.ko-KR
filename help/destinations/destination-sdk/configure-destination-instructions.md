---
description: 이 페이지에서는 대상 SDK에 대한 구성 옵션에서 참조 정보를 사용하여 대상 SDK를 사용하여 대상을 구성하는 방법을 설명합니다.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: 대상 SDK를 사용하여 대상을 구성하는 방법
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 32b61276f3fe81ffa82fec1debf335ea51020ccd
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# 대상 SDK를 사용하여 대상을 구성하는 방법

## 개요 {#overview}

이 페이지에서는 대상 SDK](./configuration-options.md)의 [구성 옵션에서 참조 정보를 사용하여 대상을 구성하는 방법을 설명합니다. 단계는 아래의 순차적 순서로 수행됩니다.

## 전제 조건 {#prerequisites}

아래 표시된 단계로 이동하기 전에 [대상 SDK 시작하기](./getting-started.md) 페이지에서 대상 SDK API에서 사용할 필수 Adobe I/O 인증 자격 증명 및 기타 사전 요구 사항을 가져오는 방법에 대해 참조하십시오.

## 대상 SDK의 구성 옵션을 사용하여 대상을 설정하는 절차 {#steps}

![대상 SDK 엔드포인트를 사용하는 단계 설명](./assets/destination-sdk-steps.png)

## 1단계: 서버 및 템플릿 구성 만들기 {#create-server-template-configuration}

먼저 `/destinations-server` 종단점을 사용하여 서버 및 템플릿 구성을 만듭니다([API 참조](./destination-server-api.md) 읽기). 서버 및 템플릿 구성에 대한 자세한 내용은 참조 섹션의 [서버 및 템플릿 사양](./configuration-options.md#server-and-template)을 참조하십시오.

다음은 구성 예입니다. `requestBody.value` 매개 변수의 메시지 변환 템플릿은 3단계, [변형 템플릿 만들기](./configure-destination-instructions.md#create-transformation-template)에서 전달됩니다.

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## 2단계: 대상 구성 만들기 {#create-destination-configuration}

아래에 표시된 것은 `/destinations` API 엔드포인트를 사용하여 생성된 대상 템플릿에 대한 구성 예시입니다. 이 템플릿에 대한 자세한 내용은 [대상 구성](./destination-configuration.md)을 참조하십시오.

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## 3단계: 메시지 변환 템플릿 만들기 - 템플릿 언어를 사용하여 메시지 출력 형식을 지정합니다 {#create-transformation-template}

대상이 지원하는 페이로드를 기준으로 하여 내보낸 데이터의 형식을 Adobe XDM 포맷에서 대상에서 지원하는 형식으로 변환하는 템플릿을 만들어야 합니다. [ID, 특성 및 세그먼트 멤버 자격 변형에 템플릿 언어를 사용하는 섹션에서 템플릿 예를 보고 Adobe이 제공한 [템플릿 작성 도구](./create-template.md)를 사용하십시오.](./message-format.md#using-templating)

## 4단계: 대상 메타데이터 구성 만들기 {#create-audience-metadata-configuration}

일부 대상의 경우, 대상 SDK를 사용하려면 대상의 대상을 프로그래밍 방식으로 만들거나, 업데이트하거나, 삭제하도록 대상 메타데이터 템플릿을 구성해야 합니다. 이 구성을 설정해야 하는 시점 및 이 작업을 수행하는 방법에 대한 자세한 내용은 [대상 메타데이터 관리](./audience-metadata-management.md) 를 참조하십시오.

## 5단계: 자격 증명 구성 만들기 / 인증 설정 {#set-up-authentication}

위의 대상 구성에서 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 또는 `"authenticationRule": "PLATFORM_AUTHENTICATION"`을 지정하는지에 따라 `/destination` 또는 `/credentials` 종단점을 사용하여 대상에 대한 인증을 설정할 수 있습니다.

* **가장 일반적인 사례**: 을 선택하고 대상 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 이 OAuth 2 인증 방법을 지원하는 경우  [OAuth 2 인증을 읽으십시오](./oauth2-authentication.md).
* `"authenticationRule": "PLATFORM_AUTHENTICATION"`을 선택한 경우 참조 설명서의 [자격 증명 구성](./credentials-configuration.md)을 참조하십시오.

## 6단계: 대상 테스트 {#test-destination}

이전 단계의 템플릿을 사용하여 대상을 설정한 후에는 [대상 테스트 도구](./create-template.md)를 사용하여 Adobe Experience Platform과 대상 간의 통합을 테스트할 수 있습니다.

대상을 테스트하는 프로세스의 일부로, Experience Platform UI를 사용하여 세그먼트를 만들어 대상에 대해 활성화해야 합니다. Experience Platform에서 세그먼트를 만드는 방법에 대한 지침은 아래 두 리소스를 참조하십시오.

* [세그먼트 설명서 페이지 만들기](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [세그먼트 만들기 비디오 연습](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## 7단계: 대상 게시 {#publish-destination}

대상을 구성하고 테스트한 후 [대상 게시 API](./destination-publish-api.md)를 사용하여 구성을 Adobe에 제출하여 검토하십시오.

## 8단계: 대상을 문서화합니다. {#document-destination}

[제품화된 통합](./overview.md#productized-custom-integrations)을 작성하는 ISV(Independent Software Vendor) 또는 System Integrator(SI)인 경우 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md)를 사용하여 [Experience League 카탈로그 카탈로그](/help/destinations/catalog/overview.md)에서 대상에 대한 제품 설명서 페이지를 만듭니다.
