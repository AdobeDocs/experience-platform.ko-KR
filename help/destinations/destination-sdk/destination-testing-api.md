---
description: 이 페이지에서는 '/authoring/testing/destinationInstance/' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명하며, 대상이 올바르게 구성되었는지 테스트하고 구성된 대상에 데이터 흐름의 무결성을 확인합니다.
title: 대상 테스트 API 작업
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 52ce788f6947300b607dfc2efa09d028f9c2ddd7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# 대상 테스트 API 작업 {#template-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

이 페이지에서는 를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/testing/destinationInstance/` API 엔드포인트. 대상이 올바르게 구성되었는지 테스트하고 구성된 대상에 데이터 흐름의 무결성을 확인합니다. 이 종단점에서 지원하는 기능에 대한 설명은 다음을 참조하십시오 [대상 구성 테스트](./test-destination.md).

호출에 프로필을 추가하지 않고 테스트 종단점에 요청을 합니다. 요청에 대해 프로필을 보내지 않는 경우 Adobe이 내부적으로 해당 프로필을 생성하여 요청에 추가합니다.

를 사용할 수 있습니다 [샘플 프로필 생성 API](./sample-profile-generation-api.md) 대상 테스트 API에 대한 요청에 사용할 프로필을 만들려면

## 대상 인스턴스 ID를 가져오는 방법 {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 이 API를 사용하려면 Experience Platform UI에서 대상에 대한 기존 연결이 있어야 합니다. 읽기 [대상에 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 및 [대상에 프로필 및 세그먼트 활성화](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 추가 정보. 대상에 연결을 설정한 후에는 URL에서 이 종단점에 대한 API 호출에 사용해야 하는 대상 인스턴스 ID를 가져옵니다 [대상과의 연결 찾아보기](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI 이미지 대상 인스턴스 ID를 가져오는 방법](./assets/get-destination-instance-id.png)


## 대상 테스트 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](./getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 호출에 프로필을 추가하지 않고 대상 구성을 테스트합니다 {#test-without-adding-profiles}

에 POST 요청을 수행하여 대상 구성을 테스트할 수 있습니다 `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 테스트할 대상의 대상 인스턴스 ID를 제공하는 종단점입니다.

**API 형식**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 테스트할 대상의 대상 인스턴스 ID입니다. |

**요청**

다음 요청은 대상의 REST API 엔드포인트를 호출합니다. 요청은 `{DESTINATION_INSTANCE_ID}` 쿼리 매개 변수.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 대상의 REST API 끝점의 API 응답과 함께 HTTP 상태 200을 반환합니다.

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
            "ECID":[
               {
                  "id":"ECID-vlnt6"
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

| 속성 | 설명 |
| -------- | ----------- |
| `aggregationKey` | 대상에 대해 구성된 집계 정책에 대한 정보를 포함합니다. 자세한 내용은 [집계 정책](./destination-configuration.md#aggregation) 섹션 을 참조하십시오. |
| `traceId` | 작업에 대한 고유 식별자입니다. 오류가 발생하면 문제 해결을 위해 이 ID를 Adobe 팀과 공유할 수 있습니다. |
| `results.httpCalls.request` | Adobe이 대상에 보낸 요청을 포함합니다. |
| `results.httpCalls.response` | 대상에서 Adobe이 받은 응답을 포함합니다. |
| `inputProfiles` | 대상에 대한 호출 시 내보낸 프로필을 포함합니다. 프로필이 소스 스키마와 일치합니다. |

{style=&quot;table-layout:auto&quot;}

## 호출에 추가된 프로필로 대상 구성을 테스트합니다 {#test-with-added-profiles}

에 POST 요청을 수행하여 대상 구성을 테스트할 수 있습니다 `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 테스트할 대상의 대상 인스턴스 ID를 제공하는 종단점입니다.

**API 형식**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 테스트할 대상의 대상 인스턴스 ID입니다. |

**요청**

다음 요청은 대상의 REST API 엔드포인트를 호출합니다. 요청은 페이로드 및 `{DESTINATION_INSTANCE_ID}` 쿼리 매개 변수.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**응답**

성공적인 응답은 대상의 REST API 끝점의 API 응답과 함께 HTTP 상태 200을 반환합니다.

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
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 및 [요청 헤더 오류](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) 을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상을 테스트하는 방법을 알 수 있습니다. 이제 Adobe을 사용할 수 있습니다 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md) 를 클릭하여 대상에 대한 설명서 페이지를 만듭니다.
