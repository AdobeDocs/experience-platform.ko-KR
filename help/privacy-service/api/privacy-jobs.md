---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 작업
topic: developer guide
translation-type: tm+mt
source-git-commit: e7bb3e8a418631e9220865e49a1651e4dc065daf
workflow-type: tm+mt
source-wordcount: '1782'
ht-degree: 2%

---


# 개인 정보 작업

이 문서에서는 API 호출을 사용하여 개인 정보 작업을 작업하는 방법에 대해 설명합니다. 특히 API에서 종단점의 사용을 `/job` [!DNL Privacy Service] 다룹니다. 이 안내서를 읽기 전에 [시작 섹션](./getting-started.md#getting-started) 에서 API를 성공적으로 호출하기 위해 필요한 필수 헤더 및 예제 API 호출 읽기 방법 등 알아야 하는 중요한 정보를 참조하십시오.

## 모든 작업 나열 {#list}

종단점에 GET 요청을 하여 조직 내에서 사용 가능한 모든 개인 정보 작업 목록을 볼 수 `/jobs` 있습니다.

**API 형식**

이 요청 형식은 끝점에 `regulation` 쿼리 매개 변수를 사용하므로 `/jobs` 아래와 같이 물음표(`?`)로 시작합니다. 응답에 페이지가 지정되어 다른 쿼리 매개 변수(및)를 사용하여 응답을 필터링할 수`page` 있습니다 `size`. 앰퍼샌드(앰퍼샌드)를 사용하여 여러 매개 변수를 분리할 수`&`있습니다.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{REGULATION}` | 쿼리할 규칙 유형입니다. 허용되는 값 `gdpr`은 `ccpa`, `lgpd_bra`및 `pdpa_tha`입니다. |
| `{PAGE}` | 0 기반 번호 지정을 사용하여 표시할 데이터 페이지입니다. 기본값은 `0`입니다. |
| `{SIZE}` | 각 페이지에 표시할 결과 수입니다. 기본값은 `1` 이며 최대값은 입니다 `100`. 최대값을 초과하면 API가 400코드 오류를 반환합니다. |

**요청**

다음 요청은 페이지 크기가 50인 세 번째 페이지에서 시작하여 IMS 조직 내의 모든 작업에 대한 페이지 지정 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적인 응답은 작업 목록을 반환하고 각 작업에는 작업 목록과 같은 세부 정보가 포함됩니다 `jobId`. 이 예에서 응답에는 결과의 세 번째 페이지에서 시작하는 50개 작업 목록이 포함됩니다.

### 후속 페이지 액세스

페이지의 지정 응답으로 다음 결과 집합을 가져오려면 동일한 종단점에 대해 다른 API 호출을 만들고 쿼리 매개 변수를 1로 증가시켜야 `page` 합니다.

## 개인 정보 작업 만들기 {#create-job}

새 작업 요청을 만들기 전에 먼저 액세스, 삭제 또는 판매를 거부할 데이터의 데이터 주체에 대한 식별 정보를 수집해야 합니다. 필요한 데이터가 있으면 종단점에 대한 POST 요청의 페이로드에서 제공해야 `/jobs` 합니다.

>[!NOTE]
>
>호환되는 Adobe Experience Cloud 응용 프로그램은 데이터 대상을 식별하는 데 서로 다른 값을 사용합니다. 응용 프로그램에 필요한 식별자에 대한 자세한 내용은 [Privacy Service 및 Experience Cloud 응용](../experience-cloud-apps.md) 프로그램에 대한 가이드를 참조하십시오. 전송할 ID를 결정하는 방법에 대한 일반적인 지침 [!DNL Privacy Service]은 개인 정보 요청의 [ID 데이터에 대한 문서를 참조하십시오](../identity-data.md).

API는 개인 데이터에 대한 두 가지 작업 요청을 지원합니다. [!DNL Privacy Service]

* [액세스 및/또는 삭제](#access-delete):개인 데이터에 액세스(읽기) 또는 삭제합니다.
* [판매](#opt-out)거부:개인 데이터를 판매하지 않도록 표시합니다.

>[!IMPORTANT]
>
>액세스 및 삭제 요청은 단일 API 호출로 결합할 수 있지만 옵트아웃 요청은 별도로 이루어져야 합니다.

### 액세스/삭제 작업 만들기 {#access-delete}

이 섹션에서는 API를 사용하여 액세스/삭제 작업 요청을 수행하는 방법을 보여 줍니다.

**API 형식**

```http
POST /jobs
```

**요청**

다음 요청은 아래와 같이 페이로드에서 제공된 속성으로 구성된 새 작업 요청을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| 속성 | 설명 |
| --- | --- |
| `companyContexts` **(필수 여부)** | 조직에 대한 인증 정보가 포함된 배열입니다. 나열된 각 식별자에는 다음 속성이 포함됩니다. <ul><li>`namespace`:식별자의 네임스페이스입니다.</li><li>`value`:식별자의 값입니다.</li></ul>IMS 조직의 고유 ID를 포함하는 식별자 중 **은** 식별자 `imsOrgId` 로 사용해야 `namespace``value` 합니다. <br/><br/>추가 식별자는 조직에 속하는 Adobe 응용 프로그램과의 통합을 식별하는 제품별 회사 한정자( `Campaign`예:)일 수 있습니다. 잠재적 값에는 계정 이름, 클라이언트 코드, 테넌트 ID 또는 기타 응용 프로그램 식별자가 포함됩니다. |
| `users` **(필수 여부)** | 액세스하거나 삭제하려는 정보가 있는 사용자 중 적어도 한 명의 컬렉션이 포함된 배열입니다. 단일 요청에서 최대 1,000개의 사용자 ID를 제공할 수 있습니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`:응답 데이터에서 개별 작업 ID의 자격을 규정하는 데 사용되는 사용자의 식별자입니다. 이 값에 대해 고유하고 쉽게 식별할 수 있는 문자열을 선택하여 나중에 쉽게 참조하거나 조회할 수 있도록 하는 것이 좋습니다.</li><li>`action`:사용자의 데이터에 적용할 원하는 작업을 나열하는 배열입니다. 수행하려는 작업에 따라 이 배열에 포함 `access`또는 둘 다 `delete`포함되어야 합니다.</li><li>`userIDs`:사용자의 ID 컬렉션입니다. 단일 사용자가 가질 수 있는 ID 수는 9개로 제한됩니다. 각 ID는 `namespace`a, a `value`및 네임스페이스 한정자(`type`)로 구성됩니다. 이러한 필수 속성에 대한 자세한 내용은 [부록을](appendix.md) 참조하십시오.</li></ul> 자세한 내용 `users` 및 `userIDs`은 [문제 해결 가이드를 참조하십시오](../troubleshooting-guide.md#user-ids). |
| `include` **(필수 여부)** | 처리에 포함할 Adobe 제품 배열. 이 값이 없거나 비어 있으면 요청이 거부됩니다. 조직에 통합된 제품만 포함합니다. 자세한 내용은 부록에 있는 [승인된 제품 값](appendix.md) 섹션을 참조하십시오. |
| `expandIDs` | 로 설정되면 응용 프로그램 `true`에서 ID 처리를 위한 최적화를 나타내는 선택적 속성(현재 [!DNL Analytics]에서 지원됨). If omitted, this value defaults to `false`. |
| `priority` | 요청 처리 우선 순위를 설정하는 Adobe Analytics에서 사용하는 선택적 속성입니다. 허용된 값은 `normal` 및 `low`입니다. 이 `priority` 를 생략하면 기본 동작이 사용됩니다 `normal`. |
| `analyticsDeleteMethod` | Adobe Analytics이 개인 데이터를 처리하는 방법을 지정하는 선택적 속성입니다. 이 속성에 대해 가능한 두 개의 값이 허용됩니다. <ul><li>`anonymize`:지정된 사용자 ID 컬렉션에서 참조되는 모든 데이터는 익명으로 처리됩니다. 이 `analyticsDeleteMethod` 를 생략하면 기본 동작입니다.</li><li>`purge`:모든 데이터가 완전히 제거됩니다.</li></ul> |
| `regulation` **(필수 여부)** | 요청에 대한 규정. 다음 4개 값 중 하나여야 합니다. <ul><li>`gdpr`</li><li>`ccpa`</li><li>`lgpd_bra`</li><li>`pdpa_tha`</li></ul> |

**응답**

성공적인 응답은 새로 만든 작업의 세부 정보를 반환합니다.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| 속성 | 설명 |
| --- | --- |
| `jobId` | 작업에 대한 읽기 전용, 고유한 시스템 생성 ID. 이 값은 특정 작업을 조회하는 다음 단계에서 사용됩니다. |

작업 요청을 성공적으로 제출하면 작업의 상태를 [확인하는 다음 단계로 진행할 수 있습니다](#check-status).

### 판매 거부 작업 만들기 {#opt-out}

이 섹션에서는 API를 사용하여 판매 거부 작업 요청을 수행하는 방법을 보여 줍니다.

**API 형식**

```http
POST /jobs
```

**요청**

다음 요청은 아래와 같이 페이로드에서 제공된 속성으로 구성된 새 작업 요청을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| 속성 | 설명 |
| --- | --- |
| `companyContexts` **(필수 여부)** | 조직에 대한 인증 정보가 포함된 배열입니다. 나열된 각 식별자에는 다음 속성이 포함됩니다. <ul><li>`namespace`:식별자의 네임스페이스입니다.</li><li>`value`:식별자의 값입니다.</li></ul>IMS 조직의 고유 ID를 포함하는 식별자 중 **은** 식별자 `imsOrgId` 로 사용해야 `namespace``value` 합니다. <br/><br/>추가 식별자는 조직에 속하는 Adobe 응용 프로그램과의 통합을 식별하는 제품별 회사 한정자( `Campaign`예:)일 수 있습니다. 잠재적 값에는 계정 이름, 클라이언트 코드, 테넌트 ID 또는 기타 응용 프로그램 식별자가 포함됩니다. |
| `users` **(필수 여부)** | 액세스하거나 삭제하려는 정보가 있는 사용자 중 적어도 한 명의 컬렉션이 포함된 배열입니다. 단일 요청에서 최대 1,000개의 사용자 ID를 제공할 수 있습니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`:응답 데이터에서 개별 작업 ID의 자격을 규정하는 데 사용되는 사용자의 식별자입니다. 이 값에 대해 고유하고 쉽게 식별할 수 있는 문자열을 선택하여 나중에 쉽게 참조하거나 조회할 수 있도록 하는 것이 좋습니다.</li><li>`action`:데이터에 적용할 원하는 작업을 나열하는 배열입니다. 판매 거부 요청의 경우 배열에는 값만 포함되어야 합니다 `opt-out-of-sale`.</li><li>`userIDs`:사용자의 ID 컬렉션입니다. 단일 사용자가 가질 수 있는 ID 수는 9개로 제한됩니다. 각 ID는 `namespace`a, a `value`및 네임스페이스 한정자(`type`)로 구성됩니다. 이러한 필수 속성에 대한 자세한 내용은 [부록을](appendix.md) 참조하십시오.</li></ul> 자세한 내용 `users` 및 `userIDs`은 [문제 해결 가이드를 참조하십시오](../troubleshooting-guide.md#user-ids). |
| `include` **(필수 여부)** | 처리에 포함할 Adobe 제품 배열. 이 값이 없거나 비어 있으면 요청이 거부됩니다. 조직에 통합된 제품만 포함합니다. 자세한 내용은 부록에 있는 [승인된 제품 값](appendix.md) 섹션을 참조하십시오. |
| `expandIDs` | 로 설정되면 응용 프로그램 `true`에서 ID 처리를 위한 최적화를 나타내는 선택적 속성(현재 [!DNL Analytics]에서 지원됨). If omitted, this value defaults to `false`. |
| `priority` | 요청 처리 우선 순위를 설정하는 Adobe Analytics에서 사용하는 선택적 속성입니다. 허용된 값은 `normal` 및 `low`입니다. 이 `priority` 를 생략하면 기본 동작이 사용됩니다 `normal`. |
| `analyticsDeleteMethod` | Adobe Analytics이 개인 데이터를 처리하는 방법을 지정하는 선택적 속성입니다. 이 속성에 대해 가능한 두 개의 값이 허용됩니다. <ul><li>`anonymize`:지정된 사용자 ID 컬렉션에서 참조되는 모든 데이터는 익명으로 처리됩니다. 이 `analyticsDeleteMethod` 를 생략하면 기본 동작입니다.</li><li>`purge`:모든 데이터가 완전히 제거됩니다.</li></ul> |
| `regulation` **(필수 여부)** | 요청에 대한 규정. 다음 4개 값 중 하나여야 합니다. <ul><li>`gdpr`</li><li>`ccpa`</li><li>`lgpd_bra`</li><li>`pdpa_tha`</li></ul> |

**응답**

성공적인 응답은 새로 만든 작업의 세부 정보를 반환합니다.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| 속성 | 설명 |
| --- | --- |
| `jobId` | 작업에 대한 읽기 전용, 고유한 시스템 생성 ID. 이 값은 다음 단계에서 특정 작업을 조회하는 데 사용됩니다. |

작업 요청을 성공적으로 제출하면 작업의 상태를 확인하는 다음 단계로 진행할 수 있습니다.

## 작업 상태 확인 {#check-status}

해당 작업을 종단점에 대한 GET 요청 경로 `jobId` 에 포함하여 특정 작업(예: 현재 처리 상태)에 대한 정보를 검색할 수 `/jobs` 있습니다.

>[!IMPORTANT]
>
>이전에 만든 작업에 대한 데이터는 작업 완료 날짜로부터 30일 이내에서만 검색할 수 있습니다.

**API 형식**

```http
GET /jobs/{JOB_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{JOB_ID}` | 조회하려는 작업의 ID입니다. 이 ID는 작업 `jobId` 을 만들고 모든 작업을 [나열하기 위해 성공적인 API 응답에서](#create-job) 반환됩니다 [](#list). |

**요청**

다음 요청은 요청 경로에 제공된 작업의 세부 사항 `jobId` 을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적인 응답은 지정된 작업의 세부 정보를 반환합니다.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| 속성 | 설명 |
| --- | --- |
| `productStatusResponse` | 배열 내의 각 객체에는 `productResponses` 특정 애플리케이션과 관련된 작업의 현재 상태에 대한 정보가 [!DNL Experience Cloud] 포함됩니다. |
| `productStatusResponse.status` | 작업의 현재 상태 범주입니다. 사용 가능한 상태 카테고리 [](#status-categories) 및 해당 의미에 대한 목록은 아래 표를 참조하십시오. |
| `productStatusResponse.message` | 작업의 특정 상태(상태 카테고리에 해당). |
| `productStatusResponse.responseMsgCode` | 수신한 제품 응답 메시지에 대한 표준 코드입니다 [!DNL Privacy Service]. 메시지의 세부 사항은 아래에 제공됩니다 `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 작업 상태에 대한 자세한 설명 비슷한 상태에 대한 메시지는 제품에 따라 다를 수 있습니다. |
| `productStatusResponse.results` | 특정 상태에 대해 일부 제품은 포함되지 않은 추가 정보를 제공하는 `results` 개체를 반환할 수 있습니다 `responseMsgDetail`. |
| `downloadURL` | 작업 상태가 `complete`ZIP 파일로 작업 결과를 다운로드하는 URL을 제공합니다. 이 파일은 작업이 완료된 후 60일 동안 다운로드할 수 있습니다. |

### 작업 상태 범주 {#status-categories}

다음 표에는 가능한 다양한 작업 상태 카테고리와 해당 의미가 나열됩니다.

| 상태 범주 | 의미 |
| -------------- | -------- |
| `complete` | 작업이 완료되고 (필요한 경우) 파일이 모든 응용 프로그램에서 업로드됩니다. |
| `processing` | 응용 프로그램이 작업을 승인했으며 현재 처리 중입니다. |
| `submitted` | 작업이 적용 가능한 모든 애플리케이션에 제출됩니다. |
| `error` | 작업을 처리하지 못했습니다. 개별 작업 세부 정보를 검색하여 더 구체적인 정보를 얻을 수 있습니다. |

>[!NOTE]
>
>제출된 작업이 여전히 처리 중인 종속 하위 작업이 있는 경우 상태로 유지될 수 있습니다. `processing`

## 다음 단계

이제 [!DNL Privacy Service] API를 사용하여 개인 정보 작업을 만들고 모니터링하는 방법을 알 수 있습니다. 사용자 인터페이스를 사용하여 동일한 작업을 수행하는 방법에 대한 자세한 내용은 [Privacy Service UI 개요를 참조하십시오](../ui/overview.md).
