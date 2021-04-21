---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 개인 정보 작업 API 끝점
topic-legacy: developer guide
description: Privacy Service API를 사용하여 Experience Cloud 응용 프로그램의 개인 정보 작업을 관리하는 방법에 대해 알아보십시오.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 1%

---

# 개인 정보 작업 끝점

이 문서에서는 API 호출을 사용하여 개인 정보 작업을 사용하는 방법에 대해 설명합니다. 특히 [!DNL Privacy Service] API에서 `/job` 끝점의 사용을 다룹니다. 이 안내서를 읽기 전에 필수 헤더 및 예제 API 호출 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보는 [시작 섹션](./getting-started.md#getting-started)을 참조하십시오.

>[!NOTE]
>
>고객의 동의 또는 수신 거부 요청을 관리하려는 경우 [동의 끝점 안내서](./consent.md)를 참조하십시오.

## 모든 작업 목록 {#list}

`/jobs` 종단점에 GET 요청을 함으로써 조직 내에서 사용 가능한 모든 개인 정보 작업 목록을 볼 수 있습니다.

**API 형식**

이 요청 형식은 `/jobs` 끝점에 `regulation` 쿼리 매개 변수를 사용하므로 아래와 같이 물음표(`?`)로 시작합니다. 응답이 페이지에 지정되어 있으므로 다른 쿼리 매개 변수(`page` 및 `size`)를 사용하여 응답을 필터링할 수 있습니다. 앰퍼샌드(`&`)를 사용하여 여러 매개 변수를 분리할 수 있습니다.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{REGULATION}` | 쿼리할 규칙 유형입니다. 허용되는 값은 다음과 같습니다. <ul><li>`gdpr` (유럽 연합)</li><li>`ccpa` (캘리포니아)</li><li>`lgpd_bra` (브라질)</li><li>`nzpa_nzl` (뉴질랜드)</li><li>`pdpa_tha` (태국)</li></ul> |
| `{PAGE}` | 0 기반 번호 매기기를 사용하여 표시할 데이터 페이지입니다. 기본값은 `0`입니다. |
| `{SIZE}` | 각 페이지에 표시할 결과 수입니다. 기본값은 `1`이고 최대값은 `100`입니다. 최대값을 초과하면 API가 400-코드 오류를 반환합니다. |

**요청**

다음 요청은 페이지 크기가 50인 3번째 페이지에서 시작하여 IMS 조직 내의 모든 작업에 대한 페이지로 구분된 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적인 응답은 작업 목록을 반환하고 각 작업에는 `jobId`과 같은 세부 정보가 포함됩니다. 이 예에서 응답에는 결과의 세 번째 페이지에서 시작하는 50개의 작업 목록이 포함됩니다.

### 다음 페이지 액세스

다음 결과 집합을 페이지로 구분된 응답으로 가져오려면 같은 끝점에 대해 다른 API 호출을 수행하고 `page` 쿼리 매개 변수를 1로 증가시켜야 합니다.

## 개인 정보 작업 {#create-job} 만들기

새 작업 요청을 만들기 전에 먼저 액세스, 삭제 또는 판매 수신을 원하는 데이터의 데이터 주체의 식별 정보를 수집해야 합니다. 필요한 데이터가 있으면 POST 요청의 페이로드에서 `/jobs` 끝점에 제공해야 합니다.

>[!NOTE]
>
>호환 가능한 Adobe Experience Cloud 애플리케이션은 데이터 주체의 식별에 서로 다른 값을 사용합니다. 응용 프로그램에 필요한 식별자에 대한 자세한 내용은 [Privacy Service 및 Experience Cloud 응용 프로그램](../experience-cloud-apps.md)의 안내서를 참조하십시오. [!DNL Privacy Service]에 보낼 ID를 결정하는 방법에 대한 일반적인 지침은 개인 정보 요청](../identity-data.md)의 [ID 데이터에 있는 문서를 참조하십시오.

[!DNL Privacy Service] API는 개인 데이터에 대한 두 가지 작업 요청을 지원합니다.

* [액세스 및/또는 삭제](#access-delete):개인 데이터를 액세스(읽기)하거나 삭제합니다.
* [판매](#opt-out) 거부:개인 데이터를 판매하지 않도록 표시합니다.

>[!IMPORTANT]
>
>액세스 및 삭제 요청은 단일 API 호출로 결합할 수 있지만 옵트아웃 요청은 별도로 해야 합니다.

### 액세스/삭제 작업 {#access-delete} 만들기

이 섹션에서는 API를 사용하여 액세스/삭제 작업 요청을 수행하는 방법을 보여 줍니다.

**API 형식**

```http
POST /jobs
```

**요청**

다음 요청은 아래 설명된 대로 페이로드에서 제공된 속성에 의해 구성된 새 작업 요청을 만듭니다.

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
| `companyContexts` **(필수 여부)** | 조직에 대한 인증 정보가 포함된 배열입니다. 나열된 각 식별자에는 다음 속성이 포함됩니다. <ul><li>`namespace`:식별자의 네임스페이스입니다.</li><li>`value`:식별자의 값입니다.</li></ul>식별자 중 하나가 `imsOrgId`을(를) 자신의 IMS 조직에 대한 고유 ID를 포함하는 `value`과(와) 함께 `namespace`으로 사용하는 것은 **필수**&#x200B;입니다. <br/><br/>추가 식별자는 조직에 속하는 Adobe 응용 프로그램과의 통합을 식별하는 제품별 회사 한정자( `Campaign`예:)일 수 있습니다. 잠재적 값에는 계정 이름, 클라이언트 코드, 테넌트 ID 또는 기타 응용 프로그램 식별자가 포함됩니다. |
| `users` **(필수 여부)** | 액세스하거나 삭제하려는 정보가 있는 사용자 중 적어도 한 명의 컬렉션을 포함하는 배열입니다. 단일 요청에서 최대 1,000개의 사용자 ID를 제공할 수 있습니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`:응답 데이터에서 개별 작업 ID의 자격을 평가하는 데 사용되는 사용자의 식별자입니다. 이 값을 쉽게 참조하거나 나중에 조회할 수 있도록 하기 위해 이 값에 대한 고유하고 쉽게 식별 가능한 문자열을 선택하는 것이 좋습니다.</li><li>`action`:사용자의 데이터에 대해 수행할 작업을 나열하는 배열입니다. 수행할 작업에 따라 이 배열에 `access`, `delete` 또는 둘 다 포함되어야 합니다.</li><li>`userIDs`:사용자의 ID 컬렉션입니다. 단일 사용자가 가질 수 있는 ID 수는 9개로 제한됩니다. 각 ID는 `namespace`, `value` 및 네임스페이스 한정자(`type`)로 구성됩니다. 이러한 필수 속성에 대한 자세한 내용은 [부록](appendix.md)을 참조하십시오.</li></ul> `users` 및 `userIDs`에 대한 자세한 설명은 [문제 해결 안내서](../troubleshooting-guide.md#user-ids)를 참조하십시오. |
| `include` **(필수 여부)** | 처리에 포함할 Adobe 제품 배열입니다. 이 값이 없거나 비어 있으면 요청이 거부됩니다. 조직에 통합된 제품만 포함합니다. 자세한 내용은 부록의 [승인된 제품 값](appendix.md)에 대한 섹션을 참조하십시오. |
| `expandIDs` | `true`으로 설정된 경우 응용 프로그램에서 ID 처리를 위한 최적화를 나타내는 선택적 속성(현재 [!DNL Analytics]에서만 지원)입니다. 생략하면 이 값의 기본값은 `false`입니다. |
| `priority` | 요청 처리 우선 순위를 설정하는 Adobe Analytics에서 사용하는 선택적 속성입니다. 허용된 값은 `normal` 및 `low`입니다. `priority`을(를) 생략하면 기본 동작은 `normal`입니다. |
| `analyticsDeleteMethod` | Adobe Analytics이 개인 데이터를 처리하는 방법을 지정하는 선택적 속성입니다. 이 속성에 사용할 수 있는 2개의 값이 있습니다. <ul><li>`anonymize`:지정된 사용자 ID 컬렉션에서 참조하는 모든 데이터는 익명으로 처리됩니다. `analyticsDeleteMethod`을(를) 생략하면 기본 동작입니다.</li><li>`purge`:모든 데이터가 완전히 제거됩니다.</li></ul> |
| `regulation` **(필수 여부)** | 개인 정보 보호 업무에 대한 규정. 다음 값이 허용됩니다. <ul><li>`gdpr` (유럽 연합)</li><li>`ccpa` (캘리포니아)</li><li>`lgpd_bra` (브라질)</li><li>`nzpa_nzl` (뉴질랜드)</li><li>`pdpa_tha` (태국)</li></ul> |

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

작업 요청을 성공적으로 제출하면 작업의 상태](#check-status)을 확인하는 다음 단계로 진행할 수 있습니다.[

## 작업 상태 확인 {#check-status}

`/jobs` 종단점에 대한 GET 요청 경로에 해당 작업의 `jobId`을 포함하여 현재 처리 상태와 같은 특정 작업에 대한 정보를 검색할 수 있습니다.

>[!IMPORTANT]
>
>이전에 생성한 작업에 대한 데이터는 작업 완료 날짜로부터 30일 이내에만 검색할 수 있습니다.

**API 형식**

```http
GET /jobs/{JOB_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{JOB_ID}` | 조회할 작업의 ID입니다. 이 ID는 [작업](#create-job) 만들기 및 [모든 작업](#list)을 나열하는 동안 성공한 API 응답에서 `jobId` 아래에 반환됩니다. |

**요청**

다음 요청은 요청 경로에 `jobId`이 제공된 작업의 세부 정보를 검색합니다.

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
| `productStatusResponse` | `productResponses` 배열 내의 각 객체에는 특정 [!DNL Experience Cloud] 응용 프로그램과 관련된 작업의 현재 상태에 대한 정보가 포함되어 있습니다. |
| `productStatusResponse.status` | 작업의 현재 상태 범주입니다. [사용 가능한 상태 범주](#status-categories)의 목록과 해당 의미를 보려면 아래 표를 참조하십시오. |
| `productStatusResponse.message` | 작업의 특정 상태(상태 카테고리에 해당). |
| `productStatusResponse.responseMsgCode` | [!DNL Privacy Service]에서 받은 제품 응답 메시지의 표준 코드입니다. 메시지의 세부 사항은 `responseMsgDetail` 아래에 제공됩니다. |
| `productStatusResponse.responseMsgDetail` | 작업 상태에 대한 자세한 설명. 비슷한 상태에 대한 메시지는 제품에 따라 다를 수 있습니다. |
| `productStatusResponse.results` | 특정 상태에 대해 일부 제품은 `responseMsgDetail`에서 다루지 않는 추가 정보를 제공하는 `results` 개체를 반환할 수 있습니다. |
| `downloadURL` | 작업 상태가 `complete`인 경우 이 속성은 작업 결과를 ZIP 파일로 다운로드할 수 있는 URL을 제공합니다. 작업이 완료된 후 60일 동안 이 파일을 다운로드할 수 있습니다. |

### 작업 상태 범주 {#status-categories}

다음 표에는 가능한 다양한 작업 상태 카테고리와 해당 의미가 나열됩니다.

| 상태 범주 | 의미 |
| -------------- | -------- |
| `complete` | 작업이 완료되었으며(필요한 경우) 파일이 모든 응용 프로그램에서 업로드됩니다. |
| `processing` | 응용 프로그램에서 작업을 승인했으며 현재 처리 중입니다. |
| `submitted` | 작업이 모든 해당 애플리케이션에 제출됩니다. |
| `error` | 작업 처리에 오류가 발생했습니다. 개별 작업 세부 정보를 검색하여 자세한 정보를 얻을 수 있습니다. |

>[!NOTE]
>
>제출된 작업이 여전히 처리 중인 종속 하위 작업이 있는 경우 `processing` 상태로 유지될 수 있습니다.

## 다음 단계

이제 [!DNL Privacy Service] API를 사용하여 개인 정보 작업을 만들고 모니터링하는 방법을 알 수 있습니다. 사용자 인터페이스를 사용하여 동일한 작업을 수행하는 방법에 대한 자세한 내용은 [Privacy Service UI 개요](../ui/overview.md)를 참조하십시오.
