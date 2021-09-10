---
description: 이 페이지에서는 메시지 변환 템플릿을 기반으로 대상에 대해 내보낸 데이터를 렌더링하기 위해 '/authoring/testing/template/render' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 템플릿 API 작업 렌더링
exl-id: e64ea89e-6064-4a05-9730-e0f7d7a3e1db
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 템플릿 API 작업 렌더링 {#render-template-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

이 페이지에서는 [메시지 변환 템플릿](./message-format.md#using-templating)을 기반으로 대상에 대해 내보낸 데이터를 렌더링하기 위해 `/authoring/testing/template/render` API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. 이 종단점에서 지원하는 기능에 대한 설명은 [템플릿 만들기](./create-template.md)를 참조하십시오.

## 렌더링 템플릿 API 작업 시작 {#get-started}

계속하기 전에 필요한 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보가 필요하면 [시작 안내서](./getting-started.md)를 검토하십시오.

## 템플릿을 기반으로 내보낸 데이터 렌더링 {#render-exported-data}

`authoring/testing/template/render` 종단점에 POST 요청을 만들고 [ 샘플 템플릿 API 엔드포인트](./sample-template-api.md)를 사용하여 만든 템플릿 및 대상 구성의 대상 ID를 제공하여 내보낸 데이터를 렌더링할 수 있습니다.

>[!TIP]
>
>* 여기서 사용해야 하는 대상 ID는 `/destinations` 종단점을 사용하여 만든 대상 구성에 해당하는 `instanceId` 입니다. [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list)를 참조하십시오.



**API 형식**


```http
POST authoring/testing/template/render
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `destinationId` | 내보낸 데이터를 렌더링하는 대상 구성의 ID입니다. |
| `template` | 내보낸 데이터를 렌더링하고 있는 템플릿에 대한 문자 이스케이프 처리된 버전입니다. |
| `profiles` | 호출 본문에 프로필을 추가하려면 [샘플 프로필 생성 API](./sample-profile-generation-api.md)를 사용하여 프로필을 생성할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}


아래 예와 같이 내보낸 데이터를 렌더링할 수 있습니다.

* [본문에 전송된 프로필이 없는 템플릿 렌더링](./render-template-api.md#multiple-profiles-no-body)
* [본문에 전송된 프로필로 템플릿 렌더링](./render-template-api.md#multiple-profiles-with-body)

<!--

### Render a template for single profile, no profiles sent in body {#single-profile-no-body}

**Request**

The following request renders sample profiles that match the format expected by your destination.

```shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "a9fb4f0f-3983-4756-b756-00cf25fe5a35",
    "template": "{# THIS is an example template for a single profile #}\r\n{\r\n    \"identities\": [\r\n        {% for email in input.profile.identityMap.email %}\r\n            {\r\n                \"type\": \"email\",\r\n                \"id\": \"{{ email.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n\r\n        {# Add a comma only if we have both emails and external_ids. #}\r\n        {% if input.profile.identityMap.email is not empty and input.profile.identityMap.external_id is not empty %}\r\n            ,\r\n        {% endif %}\r\n\r\n        {% for external in input.profile.identityMap.external_id %}\r\n            {\r\n                \"type\": \"external_id\",\r\n                \"id\": \"{{ external.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            {% for segment in input.profile.segmentMembership.ups | added %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n            {# Alternative syntax for filtering segments by status: #}\r\n            {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ]\r\n    }\r\n}"
}'

```

**Response**

The response returns the result of rendering the template, or any errors encountered.
A successful response returns HTTP status 200 with details of the exported data.
An unsuccessful response returns HTTP status 500 along with descriptions of the encountered errors.

```json

{
    "identities": [
        {
            "type": "email",
            "id": "email_lc_sha256-cBltJ"
        },
        {
            "type": "external_id",
            "id": "extern_id-cP732"
        }
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
            "segmentid1",
            "segmentid2"
        ],
        "remove": [
            "segmentid3"
        ]
    }
}

```

### Render a template for single profile, with profiles sent in body {#single-profile-with-body}

**Request**

The following request renders a profile that matches the format expected by your destination. You can generate profiles to send on the call by using the [sample profile generation API](./sample-profile-generation-api.md).

```shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "a9fb4f0f-3983-4756-b756-00cf25fe5a35",
    "template": "{# THIS is an example template for a single profile #}\r\n{\r\n    \"identities\": [\r\n        {% for email in input.profile.identityMap.email %}\r\n            {\r\n                \"type\": \"email\",\r\n                \"id\": \"{{ email.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n\r\n        {# Add a comma only if we have both emails and external_ids. #}\r\n        {% if input.profile.identityMap.email is not empty and input.profile.identityMap.external_id is not empty %}\r\n            ,\r\n        {% endif %}\r\n\r\n        {% for external in input.profile.identityMap.external_id %}\r\n            {\r\n                \"type\": \"external_id\",\r\n                \"id\": \"{{ external.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            {% for segment in input.profile.segmentMembership.ups | added %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n            {# Alternative syntax for filtering segments by status: #}\r\n            {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626238Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626240Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626240Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-c3fjU"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-VNq0z"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-HATAl"
                }
            ],
            "external_id": [
                {
                    "id": "extern_id-cP732"
                }
            ],
            "email": [
                {
                    "id": "email_lc_sha256-cBltJ"
                }
            ]
        }
    }
    ]
}'

```

**Response**

A successful response returns HTTP status 200 with details of the exported data.

```json

{
    "identities": [
        {
            "type": "email",
            "id": "email_lc_sha256-cBltJ"
        },
        {
            "type": "external_id",
            "id": "extern_id-cP732"
        }
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
            "segmentid1",
            "segmentid2"
        ],
        "remove": [
            "segmentid3"
        ]
    }
}

```

-->

### 본문에 전송된 프로필이 없는 템플릿 렌더링 {#multiple-profiles-no-body}

**요청**

다음 요청은 대상에 필요한 형식과 일치하는 여러 샘플 프로필을 렌더링합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
   "destinationId":"{DESTINATION_ID}",
   "template":"{# THIS is an example template for multiple profiles #}\r\n{\r\n    \"profiles\": [\r\n        {% for profile in input.profiles %}\r\n            {\r\n                \"identities\": [\r\n                    {% for email in profile.identityMap.email %}\r\n                        {\r\n                            \"type\": \"email\",\r\n                            \"id\": \"{{ email.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n\r\n                    {# Add a comma only if we have both emails and external_ids. #}\r\n                    {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}\r\n                        ,\r\n                    {% endif %}\r\n\r\n                    {% for external in profile.identityMap.external_id %}\r\n                        {\r\n                            \"type\": \"external_id\",\r\n                            \"id\": \"{{ external.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n                ],\r\n                \"AdobeExperiencePlatformSegments\": {\r\n                    \"add\": [\r\n                        {% for segment in profile.segmentMembership.ups | added %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ],\r\n                    \"remove\": [\r\n                        {# Alternative syntax for filtering segments by status: #}\r\n                        {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ]\r\n                }\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ]\r\n}",
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "segmentid1":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870859Z",
                  "status":"existing"
               },
               "segmentid3":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"exited"
               },
               "segmentid2":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "email":[
               {
                  "id":"Email-gq3zZ"
               }
            ],
            "external_id":[
               {
                  "id":"external_id"
               }
            ]
         }
      }
   ]
}'
```

**응답**

응답은 템플릿 렌더링 결과 또는 발생한 모든 오류를 반환합니다.
성공적인 응답은 내보낸 데이터의 세부 정보와 함께 HTTP 상태 200을 반환합니다.
실패한 응답은 발생한 오류에 대한 설명과 함께 HTTP 상태 500을 반환합니다.

```json
{
   "profiles":[
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      },
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      },
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      }
   ]
}       
```

### 본문에 전송된 프로필로 템플릿 렌더링 {#multiple-profiles-with-body}

**요청**

다음 요청은 대상에 필요한 형식과 일치하는 샘플 프로필을 렌더링합니다. [샘플 프로필 생성 API](./sample-profile-generation-api.md)를 사용하여 호출 시 전송할 프로필을 생성할 수 있습니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
   "destinationId":"{DESTINATION_ID}",
   "template":"{# THIS is an example template for multiple profiles #}\r\n{\r\n    \"profiles\": [\r\n        {% for profile in input.profiles %}\r\n            {\r\n                \"identities\": [\r\n                    {% for email in profile.identityMap.email %}\r\n                        {\r\n                            \"type\": \"email\",\r\n                            \"id\": \"{{ email.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n\r\n                    {# Add a comma only if we have both emails and external_ids. #}\r\n                    {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}\r\n                        ,\r\n                    {% endif %}\r\n\r\n                    {% for external in profile.identityMap.external_id %}\r\n                        {\r\n                            \"type\": \"external_id\",\r\n                            \"id\": \"{{ external.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n                ],\r\n                \"AdobeExperiencePlatformSegments\": {\r\n                    \"add\": [\r\n                        {% for segment in profile.segmentMembership.ups | added %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ],\r\n                    \"remove\": [\r\n                        {# Alternative syntax for filtering segments by status: #}\r\n                        {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ]\r\n                }\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ]\r\n}",
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "segmentid1":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870859Z",
                  "status":"existing"
               },
               "segmentid3":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"exited"
               },
               "segmentid2":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "email":[
               {
                  "id":"Email-gq3zZ"
               }
            ],
            "external_id":[
               {
                  "id":"external_id"
               }
            ]
         }
      }
   ]
}'
```

**응답**

응답은 템플릿 렌더링 결과 또는 발생한 모든 오류를 반환합니다.
성공적인 응답은 내보낸 데이터의 세부 정보와 함께 HTTP 상태 200을 반환합니다.
실패한 응답은 발생한 오류에 대한 설명과 함께 HTTP 상태 500을 반환합니다.

```json
{
   "profiles":[
      {
         "identities":[
            {
               "type":"email",
               "id":"Email-gq3zZ"
            },
            {
               "type":"external_id",
               "id":"external_id"
            }
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      }
   ]
}
```

## API 오류 처리 {#api-error-handling}

대상 SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 및 [요청 헤더 오류](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 메시지 변환 템플릿을 사용하여 대상의 예상 데이터 형식과 일치하는 내보낸 프로필을 생성하는 방법을 알 수 있습니다. [대상 SDK를 사용하여 대상](./configure-destination-instructions.md)을 구성하는 방법을 읽어 이 단계가 대상 구성 프로세스에 맞는 위치를 파악합니다.
