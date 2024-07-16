---
description: 이 페이지에서는 Destination SDK을 사용하여 스트리밍 대상을 구성하는 단계를 나열하고 설명합니다.
title: Destination SDK을 사용하여 스트리밍 대상 구성
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Destination SDK을 사용하여 스트리밍 대상 구성

## 개요 {#overview}

이 페이지에서는 [스트리밍 대상](../../destination-types.md#streaming-destinations)을(를) 구성하기 위해 대상 SDK](../functionality/configuration-options.md)의 [구성 옵션과 기타 Destination SDK 기능 및 API 참조 문서의 정보를 사용하는 방법에 대해 설명합니다. 단계는 아래에 순서대로 나열되어 있습니다.

## 전제 조건 {#prerequisites}

아래 표시된 단계로 진행하기 전에 [Destination SDK 시작](../getting-started.md) 페이지에서 Destination SDK API를 사용하는 데 필요한 Adobe I/O 인증 자격 증명 및 기타 필수 구성 요소를 얻는 방법에 대한 정보를 읽어 보십시오. 이는 파트너십 및 권한 사전 요구 사항을 완료하고 대상 개발을 시작할 준비가 되었다고 가정합니다.

## Destination SDK의 구성 옵션을 사용하여 대상을 설정하는 절차 {#steps}

![Destination SDK 끝점을 사용하는 예시 단계](../assets/guides/destination-sdk-steps.png)

## 1단계: 서버 및 템플릿 구성 만들기 {#create-server-template-configuration}

`/destinations-server` 끝점을 사용하여 [서버 및 템플릿 구성을 만드는](../authoring-api/destination-server/create-destination-server.md)부터 시작합니다.

다음은 구성 예입니다. `requestBody.value` 매개 변수의 메시지 변환 템플릿은 3단계, [변환 템플릿 만들기](#create-transformation-template)에서 처리됩니다.

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

다음은 `/destinations` API 끝점을 사용하여 만든 대상 템플릿에 대한 예제 구성입니다. 자세한 내용은 [대상 구성 만들기](../authoring-api/destination-configuration/create-destination-configuration.md)를 참조하십시오.

1단계의 서버 및 템플릿 구성을 이 대상 구성에 연결하려면 여기에 서버 및 템플릿 구성의 인스턴스 ID를 `destinationServerId`(으)로 추가하십시오.

>[!IMPORTANT]
>
>올바르게 구성된 실시간(스트리밍) 대상을 만들려면 *아래 그림과 같이 `identityNamespaces`에 하나 이상의 대상 ID를 추가해야*&#x200B;합니다. 대상 ID가 구성되어 있지 않으면 사용자는 활성화 워크플로의 [매핑 단계](../../ui/activate-segment-streaming-destinations.md#mapping)을(를) 지나서 진행할 수 없습니다.

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

대상이 지원하는 페이로드를 기반으로, 내보낸 데이터의 형식을 Adobe XDM 형식에서 대상이 지원하는 형식으로 변환하는 템플릿을 만들어야 합니다. [ID, 특성 및 대상 멤버십 변환에 템플릿 언어 사용](../functionality/destination-server/message-format.md#using-templating) 섹션의 템플릿 예제를 참조하고 Adobe에서 제공하는 [템플릿 작성 도구](../testing-api/streaming-destinations/create-template.md)를 사용하십시오.

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

일부 대상의 경우 Destination SDK에서 대상에서 대상을 프로그래밍 방식으로 생성, 업데이트 또는 삭제하도록 대상 메타데이터 구성을 구성해야 합니다. 이 구성을 설정해야 하는 시기 및 방법에 대한 자세한 내용은 [대상 메타데이터 관리](../functionality/audience-metadata-management.md)를 참조하십시오.

대상 메타데이터 구성을 사용하는 경우 2단계에서 만든 대상 구성에 연결해야 합니다. 대상 구성에 대상 메타데이터 구성의 인스턴스 ID를 `audienceTemplateId`(으)로 추가합니다.

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

위의 대상 구성에서 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 또는 `"authenticationRule": "PLATFORM_AUTHENTICATION"`을(를) 지정하는지 여부에 따라 `/destination` 또는 `/credentials` 끝점을 사용하여 대상에 대한 인증을 설정할 수 있습니다.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION`은(는) 두 인증 규칙 중 더 일반적이며 사용자가 연결을 설정하고 데이터를 내보내기 전에 대상에 일부 인증 형식을 제공해야 하는 경우 사용할 수 있는 규칙입니다.

대상 구성에서 `"authenticationRule": "CUSTOMER_AUTHENTICATION"`을(를) 선택했으며 대상이 OAuth 2 인증 방법을 지원하는 경우 [OAuth 2 인증](../functionality/destination-configuration/oauth2-authorization.md)을 읽으십시오.

`"authenticationRule": "PLATFORM_AUTHENTICATION"`을(를) 선택한 경우 [자격 증명 구성](../credentials-api/create-credential-configuration.md)을 만들어야 합니다.

## 6단계: 대상 테스트 {#test-destination}

이전 단계의 구성 끝점을 사용하여 대상을 설정한 후 [대상 테스트 도구](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)를 사용하여 Adobe Experience Platform과 대상 간의 통합을 테스트할 수 있습니다.

대상을 테스트하는 프로세스의 일부로 Experience Platform UI를 사용하여 대상에 활성화할 세그먼트를 만들어야 합니다. Experience Platform에서 대상자를 만드는 방법에 대한 지침은 아래 두 리소스를 참조하십시오.

* [대상 설명서 페이지 만들기](/help/segmentation/ui/audience-portal.md#create-audience)
* [대상 비디오 연습 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## 7단계: 대상 Publish {#publish-destination}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

대상을 구성하고 테스트한 후 [대상 게시 API](../publishing-api/create-publishing-request.md)를 사용하여 검토를 위해 Adobe에 구성을 제출하십시오.

## 8단계: 대상 문서화 {#document-destination}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

[제품화된 통합을 만드는 ISV(독립 소프트웨어 공급업체) 또는 SI(시스템 통합자)인 경우](../overview.md#productized-custom-integrations) [셀프서비스 설명서 프로세스](../docs-framework/documentation-instructions.md)를 사용하여 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md)에서 대상에 대한 제품 설명서 페이지를 만드십시오.

## 9단계: Adobe 검토를 위한 대상 제출 {#submit-for-review}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

마지막으로, 대상을 Experience Platform 카탈로그에 게시하여 모든 Experience Platform 고객에게 표시하려면 먼저 Adobe의 검토를 위해 대상을 공식적으로 제출해야 합니다. [Destination SDK에서 작성된 제품화된 대상을 검토하기 위해 제출](../guides/submit-destination.md)하는 방법에 대한 전체 정보를 찾으십시오.
