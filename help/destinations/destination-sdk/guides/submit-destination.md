---
description: 이 페이지에서는 Destination SDK을 사용하여 작성된 제품화된 대상을 검토하기 위해 제출해야 하는 모든 정보를 제공합니다.
title: Destination SDK에서 작성된 제품화된 대상을 검토하기 위해 제출
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 2c778f98815af87453e84f24ba8bf077774349a1
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# Destination SDK에서 작성된 제품화된 대상을 검토하기 위해 제출

## 개요 {#overview}

>[!IMPORTANT]
>
>* 여기에 설명된 프로세스는 제품화된(공개) 대상을 제출하는 파트너에게만 필요합니다. 직접 사용할 수 있는 개인 대상을 만드는 경우 이러한 자료를 제작하여 Adobe과 공유할 필요가 없습니다.
>
>* Adobe이 대상 게시 요청을 검토하는 데 걸리는 표준 응답 시간은 영업일 기준으로 5일입니다.
>
>* Adobe 팀이 초기 제출 후 구성을 업데이트하라는 요청을 받으면 업데이트를 수행한 후 다른 대상 게시 요청을 제출해야 합니다.
>
>* 대상이 Experience Platform 카탈로그에 라이브된 후에도 구성을 업데이트해야 하는 경우 구성에 반영될 업데이트에 대해 새 대상 게시 요청을 제출해야 합니다.
>
>* 검토 타임라인과 필수 아티팩트는 업데이트하려는 새 대상 및 기존 대상에 대해 동일합니다.

대상을 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md)에 게시하려면 먼저 Adobe에게 대상과 수행한 테스트에 대한 특정 정보를 제공하여 사용자가 플랫폼으로 데이터를 활성화할 때 최상의 경험을 누릴 수 있도록 해야 합니다.

이 페이지에는 Adobe Experience Platform Destination SDK을 사용하여 작성한 대상을 제출하거나 업데이트할 때 제공해야 하는 모든 정보가 나열됩니다. Adobe Experience Platform에서 대상을 제출하려면 다음을 포함하는 전자 메일을 <aepdestsdk@adobe.com>에게 보내십시오.

* 대상이 해결하는 사용 사례에 대한 설명입니다. 새 대상 구성을 제출하는 경우에만 필요합니다.
* 대상을 제출하는 이유에 대한 설명입니다. 기존 대상 구성을 업데이트하는 경우에만 필요합니다.
* 테스트 대상 API 끝점을 사용하여 대상에 대한 HTTP 호출을 수행한 후 결과를 테스트합니다. 대상 엔드포인트에 대한 API 호출 및 대상 엔드포인트에서 수신된 API 응답을 Adobe과 공유하십시오.
* 파일 기반 대상에 대한 추가 요구 사항:
   * 테스트 API를 사용하여 [샘플 프로필로 파일 기반 대상을 테스트](../testing-api/batch-destinations/file-based-destination-testing-api.md)한 후 요청 및 응답 샘플을 공유합니다.
   * 대상에서 생성하여 저장소 위치로 내보낸 샘플 파일을 첨부합니다.
   * 내보낸 파일을 저장소 위치에서 시스템으로 성공적으로 수집했음을 입증하는 일부 양식을 제출합니다.
* [대상 게시 API](../publishing-api/create-publishing-request.md)를 사용하여 대상에 대한 대상 게시 요청을 제출했다는 증명입니다.
* [셀프 서비스 설명서 프로세스](../docs-framework/documentation-instructions.md)에 설명된 지침에 따른 설명서 PR(가져오기 요청).
* Experience Platform 대상 카탈로그에서 대상 카드의 로고로 표시되는 이미지 파일입니다.

각 항목에 대한 자세한 내용은 아래 섹션에서 확인할 수 있습니다.

## 사용 사례 설명 {#use-case-description}

Experience Platform 고객이 대상에서 해결하는 사용 사례에 대한 설명을 제공합니다. 설명은 기존 파트너의 사용 사례와 유사할 수 있습니다.

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): 고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX API는 Verizon Media(VMG)의 이메일 주소를 키로 사용하는 특정 대상 그룹을 타깃팅하려는 광고주가 사용할 수 있으며, VMG의 거의 실시간 API를 사용하여 새 대상을 빠르게 만들고 원하는 대상 그룹을 푸시할 수 있습니다.

## 업데이트 이유 {#reason-for-update}

>[!NOTE]
>
>이 섹션은 기존 구성을 업데이트할 때만 필요합니다.

제출이 기존 대상에 대해 해결하는 문제에 대한 간단한 설명을 제공합니다. 예를 들어 Beta에서 일반 출시로 이동할 때 제출 시 대상의 이름, 설명 및 로고가 업데이트될 수 있습니다. 또는 제출 시 대상 구성에서 발견된 버그가 수정될 수 있습니다.

## 테스트 대상 API 사용 후 테스트 결과 {#testing-api-response}

[테스트 대상 API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) 끝점을 사용하여 대상에 대한 HTTP 호출을 수행한 후 테스트 결과를 제공합니다. 여기에는 다음 항목이 포함되어 있습니다.

* 테스트 API를 사용하여 대상 엔드포인트에 대한 전체 API 요청(헤더 및 본문)입니다.
* 대상 끝점에서 받은 API 응답입니다.

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

## 파일 기반 대상에 대한 추가 요구 사항 {#additional-file-based-destination-requirements}

파일 기반 대상의 경우 대상을 올바로 설정했다는 추가 증명을 제공해야 합니다. 아래 항목을 포함해야 합니다.

### API 응답 테스트 {#testing-api-response-file-based}

테스트 API를 사용하여 [샘플 프로필로 파일 기반 대상을 테스트](../testing-api/batch-destinations/file-based-destination-testing-api.md)한 후 요청 및 응답 샘플을 포함하십시오.

### 내보낸 파일 첨부 {#attach-exported-file}

[제출 이메일](#download-sample-email)에서 설정한 대상이 저장소 위치로 내보낸 CSV 파일을 첨부합니다.

### 수집 성공 증명 {#proof-of-successful-ingestion}

마지막으로, 제공한 저장 위치로 데이터를 내보낸 후 데이터가 시스템에 성공적으로 수집되었다는 몇 가지 증명 양식을 제공해야 합니다. 아래 항목을 입력하십시오.

* 스토리지 위치에서 파일을 수동으로 가져와서 시스템에 수집하는 스크린샷 또는 간단한 화면 캡처 비디오
* Experience Platform에서 생성된 파일 이름이 시스템에 성공적으로 수집되었음을 시스템의 UI에서 확인하는 스크린샷 또는 간단한 화면 캡처 비디오.
* Adobe이 파일 이름 또는 Experience Platform에서 생성된 데이터와 상호 연관시킬 수 있는 시스템의 로그 라인입니다.

## 대상 게시 요청을 제출했다는 증명 {#destination-publishing-request-proof}

대상을 성공적으로 테스트한 후 [대상 게시 API](../publishing-api/create-publishing-request.md)를 사용하여 검토 및 게시를 위해 Adobe에 대상을 제출해야 합니다.

대상에 대한 게시 요청의 ID를 입력합니다. 게시 요청 ID를 검색하는 방법에 대한 자세한 내용은 [대상 게시 요청을 검색하는 방법](../publishing-api/retrieve-publishing-request.md)을 읽어 보십시오.

## 프로덕션 통합을 위한 대상 설명서 PR(끌어오기 요청) {#documentation-pr}

[제품화된 통합](../overview.md#productized-custom-integrations)을 만드는 ISV(독립 소프트웨어 공급업체) 또는 SI(시스템 통합자)인 경우 [셀프 서비스 설명서 프로세스](../docs-framework/documentation-instructions.md)를 사용하여 대상에 대한 제품 설명서 페이지를 만들어야 합니다. 제출 프로세스의 일부로 대상 문서에 대한 가져오기 요청(PR)을 제공합니다.

## 대상의 로고 {#logo}

대상 카탈로그에는 각 대상 카드에 대한 로고가 포함되어 있습니다. 제출 이메일에 대상에 대한 로고가 있는 이미지를 포함합니다.

이미지 요구 사항은 다음과 같습니다.
* **형식**: `SVG`
* **크기**: 2MB 미만

## 샘플 이메일 다운로드 {#download-sample-email}

[Adobe에 제공해야 하는 모든 정보가 포함된 샘플 이메일을 ](../assets/guides/sample-email-submit-destination.rtf)다운로드하십시오.
