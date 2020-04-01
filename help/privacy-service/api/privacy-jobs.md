---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 작업
topic: developer guide
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 개인 정보 보호 작업

다음 섹션에서는 Privacy Service API에서 루트 끝점(`/`)을 사용하여 수행할 수 있는 호출을 안내합니다. 각 호출에는 일반 API 형식, 필요한 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

## 개인 정보 작업 만들기

새 작업 요청을 만들기 전에 먼저 액세스, 삭제 또는 판매를 거부할 데이터의 데이터 주체에 대한 식별 정보를 수집해야 합니다. 필요한 데이터가 있으면 POST 요청의 페이로드에서 루트 끝점에 제공해야 합니다.

>[!NOTE] 호환되는 Adobe Experience Cloud 애플리케이션은 데이터 주체 식별에 서로 다른 값을 사용합니다. 응용 프로그램에 필요한 [식별자에 대한 자세한 내용은 개인 정보 보호 서비스 및 Experience Cloud 응용](../experience-cloud-apps.md) 프로그램에 대한 안내서를 참조하십시오.

개인 정보 서비스 API는 개인 데이터에 대한 두 가지 유형의 작업 요청을 지원합니다.

* [액세스 및/또는 삭제](#access-delete):개인 데이터에 액세스(읽기) 또는 삭제
* [판매](#opt-out)거부:개인 데이터를 판매하지 않도록 표시합니다.

>[!IMPORTANT] 액세스 및 삭제 요청은 단일 API 호출로 결합할 수 있지만 옵트아웃 요청은 별도로 이루어져야 합니다.

### 액세스/삭제 작업 만들기 {#access-delete}

이 섹션에서는 API를 사용하여 액세스/삭제 작업 요청을 수행하는 방법을 보여 줍니다.

**API 형식**

```http
POST /
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
| `companyContexts` **(필수 여부)** | 조직에 대한 인증 정보가 들어 있는 배열입니다. 나열된 각 식별자는 다음 속성을 포함합니다. <ul><li>`namespace`:식별자의 네임스페이스입니다.</li><li>`value`:식별자의 값입니다.</li></ul>식별자 중 하나가 **IMS 조직에 대한 고유 ID를 포함하는 식별자와 함께** 이것을 `imsOrgId` 사용해야 `namespace``value` 합니다. <br/><br/>추가 식별자는 조직에 속한 Adobe 애플리케이션과의 통합을 식별하는 제품별 회사 한정자( `Campaign`예:)일 수 있습니다. 잠재적 값에는 계정 이름, 클라이언트 코드, 테넌트 ID 또는 기타 애플리케이션 식별자가 포함됩니다. |
| `users` **(필수 여부)** | 액세스하거나 삭제하려는 정보가 있는 사용자 중 적어도 한 명의 컬렉션이 포함된 배열입니다. 단일 요청에서 최대 1,000개의 사용자 ID를 제공할 수 있습니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`:응답 데이터에서 개별 작업 ID를 평가하는 데 사용되는 식별자입니다. 이 값에 대해 고유하고 쉽게 식별할 수 있는 문자열을 선택하여 참조하거나 나중에 조회할 수 있도록 하는 것이 좋습니다.</li><li>`action`:데이터에 적용할 원하는 작업을 나열하는 배열입니다. 수행하려는 작업에 따라 이 배열은 `access`포함되거나 `delete`둘 다 포함되어야 합니다.</li><li>`userIDs`:특정 사용자에 대한 ID 모음입니다. 단일 사용자가 가질 수 있는 ID 수는 9개로 제한됩니다. 각 ID는 `namespace`a, `value`및 네임스페이스 한정자(`type`)로 구성됩니다. 이러한 필수 속성에 대한 자세한 내용은 [부록을](appendix.md) 참조하십시오.</li></ul> |
| `include` **(필수 여부)** | 처리에 포함할 Adobe 제품 배열 이 값이 없거나 비어 있으면 요청이 거부됩니다. 조직에 통합된 제품만 포함합니다. 자세한 내용은 부칙의 [승인된 제품 값에](appendix.md) 대한 섹션을 참조하십시오. |
| `expandIDs` | 로 설정되면 응용 프로그램에서 ID 처리를 위한 최적화를 나타내는 선택적 속성입니다(현재 Analytics에서만 지원). `true` If omitted, this value defaults to `false`. |
| `priority` | 요청 처리 우선 순위를 설정하는 Adobe Analytics에서 사용하는 선택적 속성입니다. 허용된 값은 `normal` 및 `low`입니다. 을 `priority` 생략하면 기본 동작이 `normal`사용됩니다. |
| `analyticsDeleteMethod` | Adobe Analytics에서 개인 데이터를 처리하는 방법을 지정하는 선택적 속성입니다. 이 속성에 사용할 수 있는 두 가지 값이 있습니다. <ul><li>`anonymize`:지정된 사용자 ID 컬렉션에서 참조한 모든 데이터는 익명으로 처리됩니다. 이 `analyticsDeleteMethod` 값을 생략하면 기본 비헤이비어가 됩니다.</li><li>`purge`:모든 데이터가 완전히 제거됩니다.</li></ul> |
| `regulation` **(필수 여부)** | 요청에 대한 규정(&quot;gdpr&quot; 또는 &quot;ccpa&quot; 중 하나여야 함) |

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

작업 요청을 성공적으로 제출하면 작업의 상태를 [확인하는 다음 단계로 진행할 수 있습니다](#check-the-status-of-a-job).

### 판매 거부 작업 만들기 {#opt-out}

이 섹션에서는 API 파섹

**API 형식**

```http
POST /
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
| `companyContexts` **(필수 여부)** | 조직에 대한 인증 정보가 들어 있는 배열입니다. 나열된 각 식별자는 다음 속성을 포함합니다. <ul><li>`namespace`:식별자의 네임스페이스입니다.</li><li>`value`:식별자의 값입니다.</li></ul>식별자 중 하나가 **IMS 조직에 대한 고유 ID를 포함하는 식별자와 함께** 이것을 `imsOrgId` 사용해야 `namespace``value` 합니다. <br/><br/>추가 식별자는 조직에 속한 Adobe 애플리케이션과의 통합을 식별하는 제품별 회사 한정자( `Campaign`예:)일 수 있습니다. 잠재적 값에는 계정 이름, 클라이언트 코드, 테넌트 ID 또는 기타 애플리케이션 식별자가 포함됩니다. |
| `users` **(필수 여부)** | 액세스하거나 삭제하려는 정보가 있는 사용자 중 적어도 한 명의 컬렉션이 포함된 배열입니다. 단일 요청에서 최대 1,000개의 사용자 ID를 제공할 수 있습니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`:응답 데이터에서 개별 작업 ID를 평가하는 데 사용되는 식별자입니다. 이 값에 대해 고유하고 쉽게 식별할 수 있는 문자열을 선택하여 참조하거나 나중에 조회할 수 있도록 하는 것이 좋습니다.</li><li>`action`:데이터에 적용할 원하는 작업을 나열하는 배열입니다. 판매 거부 요청의 경우 배열에는 값만 포함되어야 합니다 `opt-out-of-sale`.</li><li>`userIDs`:특정 사용자에 대한 ID 모음입니다. 단일 사용자가 가질 수 있는 ID 수는 9개로 제한됩니다. 각 ID는 `namespace`a, `value`및 네임스페이스 한정자(`type`)로 구성됩니다. 이러한 필수 속성에 대한 자세한 내용은 [부록을](appendix.md) 참조하십시오.</li></ul> |
| `include` **(필수 여부)** | 처리에 포함할 Adobe 제품 배열 이 값이 없거나 비어 있으면 요청이 거부됩니다. 조직에 통합된 제품만 포함합니다. 자세한 내용은 부칙의 [승인된 제품 값에](appendix.md) 대한 섹션을 참조하십시오. |
| `expandIDs` | 로 설정되면 응용 프로그램에서 ID 처리를 위한 최적화를 나타내는 선택적 속성입니다(현재 Analytics에서만 지원). `true` If omitted, this value defaults to `false`. |
| `priority` | 요청 처리 우선 순위를 설정하는 Adobe Analytics에서 사용하는 선택적 속성입니다. 허용된 값은 `normal` 및 `low`입니다. 을 `priority` 생략하면 기본 동작이 `normal`사용됩니다. |
| `analyticsDeleteMethod` | Adobe Analytics에서 개인 데이터를 처리하는 방법을 지정하는 선택적 속성입니다. 이 속성에 사용할 수 있는 두 가지 값이 있습니다. <ul><li>`anonymize`:지정된 사용자 ID 컬렉션에서 참조한 모든 데이터는 익명으로 처리됩니다. 이 `analyticsDeleteMethod` 값을 생략하면 기본 비헤이비어가 됩니다.</li><li>`purge`:모든 데이터가 완전히 제거됩니다.</li></ul> |
| `regulation` **(필수 여부)** | 요청에 대한 규정(&quot;gdpr&quot; 또는 &quot;ccpa&quot; 중 하나여야 함) |

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
| `jobId` | 작업에 대한 읽기 전용, 고유한 시스템 생성 ID. 이 값은 다음 단계에서 특정 작업을 찾는 데 사용됩니다. |

작업 요청을 성공적으로 제출하면 작업의 상태를 확인하는 다음 단계로 진행할 수 있습니다.

## 작업 상태 확인

이전 단계에서 반환된 `jobId` 값 중 하나를 사용하여 현재 처리 상태와 같은 해당 작업에 대한 정보를 검색할 수 있습니다.

>[!IMPORTANT] 이전에 생성한 작업에 대한 데이터는 작업 완료 날짜로부터 30일 이내에서만 검색할 수 있습니다.

**API 형식**

```http
GET /{JOB_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{JOB_ID}` | 조회할 작업의 ID로 `jobId` 이전 단계의 [](#create-a-job-request)응답으로 반환됩니다. |

**요청**

다음 요청은 요청 경로에 제공된 작업의 세부 정보를 `jobId` 검색합니다.

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
    "jobId": "527ef92d-6cd9-45cc-9bf1-477cfa1e2ca2",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "error",
    "submittedBy": "02b38adf-6573-401e-b4cc-6b08dbc0e61c@techacct.adobe.com",
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
                "status": "submitted",
                "message": "processing"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| 속성 | 설명 |
| --- | --- |
| `productStatusResponse` | 작업의 현재 상태입니다. 가능한 각 상태에 대한 세부 사항은 아래 표에 나와 있습니다. |
| `downloadURL` | 작업 상태가 `complete`ZIP 파일인 경우 이 속성은 작업 결과를 다운로드할 수 있는 URL을 제공합니다. 이 파일은 작업이 완료된 후 60일 동안 다운로드할 수 있습니다. |

### 작업 상태 응답

다음 표에는 가능한 여러 작업 상태와 해당 의미가 나열됩니다.

| 상태 코드 | 상태 메시지 | 의미 |
| ----------- | -------------- | -------- |
| 1 | 완료 | 작업이 완료되었으며(필요한 경우) 파일이 모든 응용 프로그램에서 업로드됩니다. |
| 2 | 처리 중 | 응용 프로그램이 작업을 승인했으며 현재 처리 중입니다. |
| 3 | 제출됨 | 작업이 모든 해당 애플리케이션에 제출됩니다. |
| 4 | 오류 | 작업을 처리하지 못했습니다. 개별 작업 세부 정보를 검색하여 더 구체적인 정보를 얻을 수 있습니다. |

>[!NOTE] 제출된 작업이 여전히 처리 중인 종속 하위 작업이 있는 경우 처리 상태로 유지될 수 있습니다.

## 모든 작업 나열

루트(`/`) 끝점에 GET 요청을 만들어 조직 내에서 사용 가능한 모든 작업 요청 목록을 볼 수 있습니다.

**API 형식**

이 요청 형식은 루트( `regulation` ) 끝점에`/`쿼리 매개 변수를 사용하므로, 아래와 같이 물음표(`?`)로 시작합니다. 응답에 페이지가 지정되어 다른 쿼리 매개 변수(`page` 및 `size`)를 사용하여 응답을 필터링할 수 있습니다. 앰퍼샌드(`&`)를 사용하여 여러 매개 변수를 분리할 수 있습니다.

```http
GET ?regulation={REGULATION}
GET ?regulation={REGULATION}&page={PAGE}
GET ?regulation={REGULATION}&size={SIZE}
GET ?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{REGULATION}` | 쿼리할 규칙 유형입니다. 허용된 값은 `gdpr` 및 `ccpa`입니다. |
| `{PAGE}` | 0 기반 번호 지정을 사용하여 표시할 데이터 페이지입니다. 기본값은 `0`입니다. |
| `{SIZE}` | 각 페이지에 표시할 결과 수입니다. 기본값은 `1` 이며 최대값은 `100`입니다. 최대값을 초과하면 API가 400 코드 오류를 반환합니다. |

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

성공적인 응답은 작업 목록을 반환하고 각 작업에는 작업 목록과 `jobId`같은 세부 사항이 포함됩니다. 이 예에서 응답에는 결과의 세 번째 페이지에서 시작하여 50개의 작업 목록이 포함됩니다.

### 후속 페이지 액세스

페이지 지정 응답으로 다음 결과 세트를 가져오려면 쿼리 매개 변수를 1만큼 증가시키면서 동일한 종단점에 대해 다른 API 호출을 `page` 수행해야 합니다.

## 다음 단계

이제 개인 정보 서비스 API를 사용하여 개인 정보 작업을 만들고 모니터링하는 방법을 알고 있습니다. 사용자 인터페이스를 사용하여 동일한 작업을 수행하는 방법에 대한 자세한 내용은 개인 정보 서비스 [UI 개요를](../ui/overview.md)참조하십시오.
