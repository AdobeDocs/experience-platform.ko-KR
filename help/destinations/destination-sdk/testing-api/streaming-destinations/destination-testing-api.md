---
description: 대상 테스트 API를 사용하여 스트리밍 대상이 올바르게 구성되었는지 테스트하고 구성된 대상에 대한 데이터 흐름의 무결성을 확인하는 방법에 대해 알아봅니다.
title: 샘플 프로필을 사용하여 스트리밍 대상 테스트
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---


# 샘플 프로필을 사용하여 스트리밍 대상 테스트 {#template-api-operations}

>[!IMPORTANT]
>
>**API 끝점**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

이 페이지에서는 `/authoring/testing/destinationInstance/` API 끝점을 사용하여 대상이 올바르게 구성되었는지 테스트하고 구성된 대상에 대한 데이터 흐름의 무결성을 확인하기 위해 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. 이 끝점에서 지원하는 기능에 대한 설명은 [대상 구성을 테스트](streaming-destination-testing-overview.md)를 참조하십시오.

호출에 프로필을 추가하거나 추가하지 않고 테스트 끝점에 요청을 수행합니다. 요청에 프로필을 보내지 않는 경우 Adobe이 내부적으로 프로필을 생성하여 요청에 추가합니다.

[샘플 프로필 생성 API](sample-profile-generation-api.md)를 사용하여 대상 테스트 API에 대한 요청에 사용할 프로필을 만들 수 있습니다.

## 대상 인스턴스 ID를 가져오는 방법 {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 이 API를 사용하려면 Experience Platform UI에 대상에 대한 기존 연결이 있어야 합니다. 자세한 내용은 [대상에 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) 및 [대상에 프로필 및 대상자 활성화](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html)를 참조하십시오.
> * 대상에 대한 연결을 설정한 후 [대상과의 연결을 탐색](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html)할 때 이 끝점에 대한 API 호출에 사용해야 하는 대상 인스턴스 ID를 가져옵니다.
>![대상 인스턴스 ID](../../assets/testing-api/get-destination-instance-id.png)을(를) 가져오는 방법 UI 이미지

## 대상 테스트 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 호출에 프로필을 추가하지 않고 대상 구성을 테스트합니다 {#test-without-adding-profiles}

`authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 끝점에 대한 POST 요청을 만들고 테스트 중인 대상의 대상 인스턴스 ID를 제공하여 대상 구성을 테스트할 수 있습니다.

**API 형식**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 테스트 중인 대상의 대상 인스턴스 ID입니다. |

**요청**

다음 요청은 대상의 REST API 끝점을 호출합니다. `{DESTINATION_INSTANCE_ID}` 쿼리 매개 변수로 요청을 구성했습니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
| `aggregationKey` | 대상에 대해 구성된 집계 정책에 대한 정보를 포함합니다. 자세한 내용은 [집계 정책](../../functionality/destination-configuration/aggregation-policy.md) 설명서를 참조하십시오. |
| `traceId` | 작업의 고유 식별자입니다. 오류가 발생하면 문제 해결 목적으로 Adobe 팀과 이 ID를 공유할 수 있습니다. |
| `results.httpCalls.request` | Adobe이 대상으로 보낸 요청을 포함합니다. |
| `results.httpCalls.response` | 대상에서 Adobe이 받은 응답을 포함합니다. |
| `inputProfiles` | 대상 호출 시 내보낸 프로필을 포함합니다. 프로필이 소스 스키마와 일치합니다. |

{style="table-layout:auto"}

## 호출에 추가된 프로필을 사용하여 대상 구성 테스트 {#test-with-added-profiles}

`authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 끝점에 대한 POST 요청을 만들고 테스트 중인 대상의 대상 인스턴스 ID를 제공하여 대상 구성을 테스트할 수 있습니다.

**API 형식**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 테스트 중인 대상의 대상 인스턴스 ID입니다. |

**요청**

다음 요청은 대상의 REST API 끝점을 호출합니다. 페이로드에 제공된 매개 변수와 `{DESTINATION_INSTANCE_ID}` 쿼리 매개 변수로 요청을 구성합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
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

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽고 나면 이제 대상을 테스트하는 방법을 알 수 있습니다. 이제 Adobe [셀프 서비스 설명서 프로세스](../../docs-framework/documentation-instructions.md)를 사용하여 대상에 대한 설명서 페이지를 만들 수 있습니다.
