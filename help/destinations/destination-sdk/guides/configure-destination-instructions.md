---
description: 이 페이지에서는 Destination SDK을 사용하여 스트리밍 대상을 구성하는 단계를 나열하고 설명합니다.
title: Destination SDK을 사용하여 스트리밍 대상 구성
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Destination SDK을 사용하여 스트리밍 대상 구성

## 개요 {#overview}

이 페이지에서는 의 정보를 사용하는 방법에 대해 설명합니다. [대상 SDK의 구성 옵션](../functionality/configuration-options.md) 을(를) 구성하기 위한 기타 Destination SDK 기능 및 API 참조 문서 [스트리밍 대상](../../destination-types.md#streaming-destinations). 단계는 아래에 순서대로 나열되어 있습니다.

## 사전 요구 사항 {#prerequisites}

아래 그림에 나와 있는 단계로 이동하기 전에 [Destination SDK 시작](../getting-started.md) Destination SDK API를 사용하여 작업하는 데 필요한 Adobe I/O 인증 자격 증명 및 기타 전제 조건을 얻는 방법에 대한 자세한 내용을 보려면 페이지 를 참조하십시오. 이는 파트너십 및 권한 사전 요구 사항을 완료하고 대상 개발을 시작할 준비가 되었다고 가정합니다.

## Destination SDK의 구성 옵션을 사용하여 대상을 설정하는 절차 {#steps}

![Destination SDK 엔드포인트 사용 단계 그림](../assets/guides/destination-sdk-steps.png)

## 1단계: 서버 및 템플릿 구성 만들기 {#create-server-template-configuration}

시작 기준 [서버 및 템플릿 구성 만들기](../authoring-api/destination-server/create-destination-server.md) 사용 `/destinations-server` 엔드포인트.

다음은 구성 예입니다. 의 메시지 변환 템플릿은 `requestBody.value` 매개 변수는 3단계에서 처리됩니다. [변형 템플릿 만들기](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
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

다음은 를 사용하여 만든 대상 템플릿에 대한 예제 구성입니다. `/destinations` API 엔드포인트. 다음을 참조하십시오 [대상 구성 만들기](../authoring-api/destination-configuration/create-destination-configuration.md) 추가 정보.

1단계의 서버 및 템플릿 구성을 이 대상 구성에 연결하려면 서버와 템플릿 구성의 인스턴스 ID를 `destinationServerId` 여기.

>[!IMPORTANT]
>
>올바르게 구성된 실시간(스트리밍) 대상을 만들려면 다음 작업을 수행하십시오 *필수* 에서 하나 이상의 대상 id 추가 `identityNamespaces`아래에 표시된 대로 를 클릭합니다. 대상 ID가 구성되지 않은 경우 사용자가 [매핑 단계](../../ui/activate-segment-streaming-destinations.md#mapping) 활성화 워크플로.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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

## 3단계: 메시지 변환 템플릿 만들기 - 템플릿 언어를 사용하여 메시지 출력 형식 지정 {#create-transformation-template}

대상이 지원하는 페이로드를 기반으로, 내보낸 데이터의 형식을 Adobe XDM 형식에서 대상이 지원하는 형식으로 변환하는 템플릿을 만들어야 합니다. 섹션에서 템플릿 예 를 참조하십시오 [ID, 속성 및 세그먼트 멤버십 변환에 템플릿 언어 사용](../functionality/destination-server/message-format.md#using-templating) 및 사용 [템플릿 작성 도구](../testing-api/streaming-destinations/create-template.md) Adobe 제공.

자신에게 적합한 메시지 변환 템플릿을 만들었으면 1단계에서 만든 서버 및 템플릿 구성에 추가합니다.

```json {line-numbers="true" highlight="13-14"}
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
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## 4단계: 대상 메타데이터 구성 만들기 {#create-audience-metadata-configuration}

일부 대상의 경우 Destination SDK에서 대상에서 대상을 프로그래밍 방식으로 생성, 업데이트 또는 삭제하도록 대상 메타데이터 구성을 구성해야 합니다. 을(를) 참조하십시오 [대상자 메타데이터 관리](../functionality/audience-metadata-management.md) 이 구성을 설정해야 하는 시기 및 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

대상 메타데이터 구성을 사용하는 경우 2단계에서 만든 대상 구성에 연결해야 합니다. 대상 구성에 대상 메타데이터 구성의 인스턴스 ID를 다음과 같이 추가합니다. `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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


## 5단계: 인증 설정 {#set-up-authentication}

지정 여부에 따라 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 또는 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 위의 대상 구성에서 다음을 사용하여 대상에 대한 인증을 설정할 수 있습니다. `/destination` 또는 `/credentials` 엔드포인트.

선택한 경우 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 대상 구성에서 대상 은 OAuth 2 인증 방법을 지원합니다. [OAuth 2 인증](../functionality/destination-configuration/oauth2-authentication.md).

선택한 경우 `"authenticationRule": "PLATFORM_AUTHENTICATION"`, 다음을 만들어야 합니다. [자격 증명 구성](../credentials-api/create-credential-configuration.md).

## 6단계: 대상 테스트 {#test-destination}

이전 단계에서 구성 끝점을 사용하여 대상을 설정한 후 [대상 테스트 도구](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) Adobe Experience Platform과 대상 간의 통합을 테스트합니다.

대상을 테스트하는 프로세스의 일부로 Experience Platform UI를 사용하여 대상에 활성화할 세그먼트를 만들어야 합니다. Experience Platform에서 세그먼트를 만드는 방법에 대한 지침은 아래 두 리소스를 참조하십시오.

* [세그먼트 설명서 페이지 만들기](/help/segmentation/ui/overview.md#create-segment)
* [세그먼트 만들기 비디오 연습](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## 7단계: 대상 게시 {#publish-destination}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

대상을 구성하고 테스트한 후 [대상 게시 API](../publishing-api/create-publishing-request.md) Adobe에 구성을 제출하여 검토합니다.

## 8단계: 대상 문서화 {#document-destination}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

ISV(Independent Software Vendor) 또는 SI(System Integrator)가 [제품화 통합](../overview.md#productized-custom-integrations), 사용 [셀프서비스 설명서 프로세스](../docs-framework/documentation-instructions.md) 에서 대상에 대한 제품 설명서 페이지를 만들려면 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md).

## 9단계: Adobe 검토를 위한 대상 제출 {#submit-for-review}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

마지막으로, 대상을 Experience Platform 카탈로그에 게시하여 모든 Experience Platform 고객에게 표시하려면 먼저 Adobe의 검토를 위해 대상을 공식적으로 제출해야 합니다. 다음 방법에 대한 전체 정보 찾기 [Destination SDK에서 작성된 제품화된 대상을 검토하기 위해 제출](../guides/submit-destination.md).
