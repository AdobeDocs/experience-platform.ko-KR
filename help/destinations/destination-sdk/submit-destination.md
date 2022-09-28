---
description: 이 페이지에서는 Destination SDK을 사용하여 작성된 제품 대상 검토를 위해 제출하는 모든 정보를 제공합니다.
title: Destination SDK에서 작성된 제품 대상 검토를 위해 제출
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: e68ae7d1cb87d078d9fce5a5df501cc6ce944403
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Destination SDK에서 작성된 제품 대상 검토를 위해 제출

## 개요 {#overview}

>[!IMPORTANT]
>
>* 여기에 설명된 프로세스는 제품(공개) 대상을 제출하는 파트너에게만 필요합니다. 직접 사용할 전용 대상을 만드는 경우 이러한 자료를 만들고 Adobe과 공유할 필요가 없습니다.
>
>* 대상 게시 요청을 검토하는 Adobe의 표준 응답 시간은 5영업일.
>
>* Adobe 팀이 초기 제출 시 구성에 대한 업데이트를 수행하도록 요청하는 경우 업데이트를 수행한 후 다른 대상 게시 요청을 제출해야 합니다.
>
>* 대상이 Experience Platform 카탈로그에 라이브 상태가 된 후에도 구성을 업데이트해야 하는 경우 구성에 반영되도록 새 대상 게시 요청을 제출해야 합니다.


대상을 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md)를 채울 때는 Adobe이 데이터를 플랫폼에 활성화할 때 최상의 경험을 누릴 수 있도록 대상 및 수행한 테스트에 대한 특정 정보를 제공해야 합니다.

이 페이지에는 Adobe Experience Platform Destination SDK을 사용하여 작성된 대상을 제출하거나 업데이트할 때 제공하는 모든 정보가 나열됩니다. Adobe Experience Platform에서 대상을 성공적으로 제출하려면 전자 메일을 로 보내십시오 <aepdestsdk@adobe.com> 에는 다음이 포함됩니다.

* 대상이 해결하는 사용 사례에 대한 설명입니다. 기존 대상 구성을 업데이트하는 경우에는 필요하지 않습니다.
* 테스트 대상 API 종단점을 사용하여 대상에 대한 HTTP 호출을 수행한 후 결과를 테스트합니다. Adobe과 공유하십시오.
   * 대상 종단점에 대한 API 호출.
   * 대상 종단점에서 받은 API 응답입니다.
* 를 사용하여 대상에 대한 대상 게시 요청을 제출했는지 확인 [대상 게시 API](./destination-publish-api.md).
* 에 설명된 지침에 따라 설명서 PR(끌어오기 요청) [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md).
* Experience Platform 대상 카탈로그에 대상 카드에 대한 로고로 표시되는 이미지 파일입니다.

아래 섹션에서 각 항목에 대한 자세한 정보를 찾을 수 있습니다.

## 사용 사례 설명

대상이 Experience Platform 고객을 위해 해결하는 사용 사례에 대한 설명을 제공합니다. 설명은 기존 파트너의 사용 사례와 비슷합니다.

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): 고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX API는 VMG(Verizon Media)에서 이메일 주소를 키로 사용하는 특정 대상 그룹을 타겟팅하려는 광고주가 VMG의 근실시간 API를 사용하여 새로운 세그먼트를 신속하게 생성하고 원하는 대상 그룹을 푸시할 수 있습니다.

## 테스트 대상 API 사용 후 결과 테스트

를 사용한 후 테스트 결과 제공 [테스트 대상 API](./test-destination.md) 대상에 대한 HTTP 호출을 수행하는 끝점입니다. 여기에는 다음 항목이 포함되어 있습니다.

* 테스트 API를 사용하여 대상 종단점에 대한 전체 API 요청(헤더 및 본문)입니다.
* 대상 종단점에서 받은 API 응답입니다.

예를 들어 요청 및 응답은 아래 샘플과 유사할 수 있습니다.

**요청**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**응답**

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

## 대상 게시 요청을 제출했는지 확인

대상을 성공적으로 테스트한 후에는 [대상 게시 API](./destination-publish-api.md) 검토 및 게시를 위해 Adobe에 대상을 제출하려면 다음을 수행하십시오.

대상에 대한 게시 요청의 ID를 제공합니다. 게시 요청 ID를 검색하는 방법에 대한 자세한 내용은 [대상 게시 요청 나열](./destination-publish-api.md#retrieve-list).

## 프로덕션 통합을 위한 대상 설명서 PR(끌어오기 요청)

ISV(Independent Software Vendor) 또는 SI(System Integrator)가 [제품 통합](./overview.md#productized-custom-integrations)를 사용하려면 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md) 를 클릭하여 대상에 대한 제품 설명서 페이지를 만듭니다. 제출 프로세스의 일부로 대상 설명서에 대한 PR(끌어오기 요청)을 제공합니다.

## 대상의 로고 {#logo}

대상 카탈로그에는 각 대상 카드에 대한 로고가 포함되어 있습니다. 제출 이메일에 대상에 대한 로고가 있는 이미지를 포함합니다.

이미지 요구 사항은 다음과 같습니다.
* **포맷**: `SVG`
* **크기**: 2MB 미만

## 샘플 이메일 다운로드

[다운로드](./assets/sample-email-submit-destination.rtf) Adobe에 제공해야 하는 모든 정보가 포함된 샘플 이메일.
