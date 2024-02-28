---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 개인 정보 작업 API 엔드포인트
description: Privacy Service API를 사용하여 Experience Cloud 애플리케이션에 대한 개인 정보 작업을 관리하는 방법을 알아봅니다.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 1%

---

# 개인 정보 작업 엔드포인트

이 문서에서는 API 호출을 사용하여 개인 정보 작업을 사용하는 방법을 다룹니다. 특히 다음의 사용에 적용됩니다. `/job` 의 엔드포인트 [!DNL Privacy Service] API. 이 안내서를 읽기 전에 [시작 안내서](./getting-started.md) 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

>[!NOTE]
>
>고객의 동의 또는 옵트아웃 요청을 관리하려는 경우 다음을 참조하십시오. [동의 엔드포인트 안내서](./consent.md).

## 모든 작업 나열 {#list}

에 GET 요청을 하여 조직 내에서 사용 가능한 모든 개인 정보 작업 목록을 볼 수 있습니다. `/jobs` 엔드포인트.

**API 형식**

이 요청 형식은 `regulation` 쿼리 매개 변수 `/jobs` 끝점이므로 물음표(`?`)을 참조하십시오. 응답은 페이지 번호를 매겨 다른 쿼리 매개 변수를 사용할 수 있습니다(`page` 및 `size`)을 클릭하여 응답을 필터링합니다. 앰퍼샌드( )를 사용하여 여러 매개 변수를 분리할 수 있습니다`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 매개변수 | 설명 |
| --- | --- |
| `{REGULATION}` | 쿼리할 규정 유형. 허용되는 값은 다음과 같습니다. <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa`</li><li>`cpra_usa`</li><li>`ctdpa`</li><li>`ctdpa_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>의 개요 보기 [지원되는 규정](../regulations/overview.md) 위의 값이 나타내는 개인 정보 보호 규정에 대한 자세한 정보입니다. |
| `{PAGE}` | 0 기반 번호 매기기를 사용하여 표시할 데이터 페이지입니다. 기본값은 `0`입니다. |
| `{SIZE}` | 각 페이지에 표시할 결과 수. 기본값은 입니다 `1` 최대값은 입니다. `100`. 최대값을 초과하면 API가 400 코드 오류를 반환합니다. |

{style="table-layout:auto"}

<!-- Not released yet:
<li>`pdpd_vnm`</li>
 -->

**요청**

다음 요청은 페이지 크기가 50인 세 번째 페이지부터 시작하여 조직 내의 모든 작업에 대한 페이지 매김된 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 작업 목록을 반환하며 각 작업에는 와 같은 세부 사항이 포함됩니다 `jobId`. 이 예에서 응답에는 결과의 세 번째 페이지에서 시작하는 50개의 작업 목록이 포함됩니다.

### 후속 페이지 액세스

페이지가 매겨진 응답에서 다음 결과 세트를 가져오려면 를 늘리는 동안 동일한 끝점에 대한 다른 API 호출을 수행해야 합니다. `page` 쿼리 매개 변수 1씩

## 개인 정보 작업 만들기 {#create-job}

>[!IMPORTANT]
>
>Privacy Service은 데이터 주체 및 소비자 권한 요청용으로만 사용됩니다. 데이터 정리 또는 유지 관리를 위한 다른 Privacy Service 사용은 지원되지 않거나 허용되지 않습니다. Adobe은 적시에 이를 이행할 법적 의무가 있다. 따라서 프로덕션 전용 환경이며 유효한 개인 정보 보호 요청에 대한 불필요한 백로그를 만들기 때문에 Privacy Service에 대한 로드 테스트는 허용되지 않습니다.
>
>이제 서비스 남용을 방지하기 위해 엄격한 일일 업로드 제한이 적용됩니다. 시스템을 남용하는 것으로 확인된 사용자는 서비스에 액세스할 수 없게 됩니다. 그런 다음 후속 회의가 그들과 함께 개최되어 그들의 행동에 대해 이야기하고 Privacy Service에 허용되는 사용에 대해 논의합니다.

새 Job 요청을 작성하기 전에 먼저 데이터에 액세스하거나, 삭제하거나, 판매를 거부하려는 데이터 주체에 대한 식별 정보를 수집해야 합니다. 필요한 데이터가 있으면에서 POST 요청의 페이로드에 제공되어야 합니다. `/jobs` 엔드포인트.

>[!NOTE]
>
>호환 가능한 Adobe Experience Cloud 애플리케이션은 데이터 주체를 식별하기 위해 다양한 값을 사용합니다. 다음 안내서를 참조하십시오 [Privacy Service 및 Experience Cloud 애플리케이션](../experience-cloud-apps.md) 를 참조하십시오. 전송할 ID 확인에 대한 일반적인 지침 [!DNL Privacy Service], 다음에 대한 문서 참조 [개인 정보 보호 요청의 id 데이터](../identity-data.md).

다음 [!DNL Privacy Service] API는 개인 데이터에 대한 두 가지 유형의 작업 요청을 지원합니다.

* [액세스 및/또는 삭제](#access-delete): 개인 데이터에 액세스(읽기) 또는 삭제합니다.
* [판매 거부](#opt-out): 개인 데이터를 판매하지 않도록 표시합니다.

>[!IMPORTANT]
>
>액세스 및 삭제 요청은 단일 API 호출로 결합할 수 있지만 옵트아웃 요청은 별도로 수행해야 합니다.

### 액세스/삭제 작업 만들기 {#access-delete}

이 섹션에서는 API를 사용하여 액세스/삭제 작업을 요청하는 방법을 보여줍니다.

**API 형식**

```http
POST /jobs
```

**요청**

다음 요청은 아래 설명된 대로 페이로드에 제공된 속성으로 구성된 새 작업 요청을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 속성 | 설명 |
| --- | --- |
| `companyContexts` **(필수)** | 조직의 인증 정보가 포함된 배열입니다. 나열된 각 식별자에는 다음 속성이 포함됩니다. <ul><li>`namespace`: 식별자의 네임스페이스입니다.</li><li>`value`: 식별자의 값입니다.</li></ul>다음과 같습니다. **필수** 식별자 중 하나가 `imsOrgId` as its `namespace`, 포함 `value` 조직의 고유 ID를 포함합니다. <br/><br/>추가 식별자는 제품별 회사 한정자일 수 있습니다(예: `Campaign`) - 조직에 속한 Adobe 애플리케이션과의 통합을 식별합니다. 잠재적 값에는 계정 이름, 클라이언트 코드, 테넌트 ID 또는 기타 애플리케이션 식별자가 포함됩니다. |
| `users` **(필수)** | 액세스하거나 삭제하려는 정보를 가진 하나 이상의 사용자 컬렉션이 포함된 배열입니다. 단일 요청으로 최대 1000명의 사용자를 제공할 수 있습니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`: 응답 데이터에서 개별 작업 ID를 구분하는 데 사용되는 사용자의 식별자입니다. 이 값을 쉽게 참조하거나 나중에 조회할 수 있도록 고유하고 쉽게 식별 가능한 문자열을 선택하는 것이 좋습니다.</li><li>`action`: 사용자 데이터에 대해 수행할 작업을 나열하는 배열입니다. 수행하려는 작업에 따라 이 배열에는 다음이 포함되어야 합니다. `access`, `delete`또는 둘 다.</li><li>`userIDs`: 사용자의 ID 컬렉션입니다. 단일 사용자가 가질 수 있는 ID의 수는 9개로 제한됩니다. 각 ID는 `namespace`, a `value`및 네임스페이스 한정자(`type`). 다음을 참조하십시오. [부록](appendix.md) 이러한 필수 속성에 대해 자세히 알아보십시오.</li></ul> 에 대한 자세한 설명은 `users` 및 `userIDs`, 다음을 참조하십시오. [문제 해결 안내서](../troubleshooting-guide.md#user-ids). |
| `include` **(필수)** | 처리에 포함할 Adobe 제품의 배열입니다. 이 값이 없거나 비어 있으면 요청이 거부됩니다. 조직이 통합한 제품만 포함합니다. 의 섹션을 참조하십시오. [허용된 제품 값](appendix.md) 자세한 내용은 부록에서 확인하십시오. |
| `expandIDs` | 로 설정된 경우 선택 사항인 속성 `true`는 애플리케이션에서 ID를 처리하기 위한 최적화를 나타냅니다(현재는 에서만 지원됨). [!DNL Analytics]). 생략하면 이 값의 기본값은 입니다. `false`. |
| `priority` | 요청 처리에 대한 우선 순위를 설정하는 Adobe Analytics에서 사용하는 선택적 속성입니다. 허용되는 값은 다음과 같습니다 `normal` 및 `low`. If `priority` 생략된 경우 기본 동작은 다음과 같습니다. `normal`. |
| `analyticsDeleteMethod` | Adobe Analytics에서 개인 데이터를 처리하는 방법을 지정하는 선택적 속성입니다. 이 속성에는 두 가지 가능한 값이 허용됩니다. <ul><li>`anonymize`: 특정 사용자 ID 컬렉션에서 참조하는 모든 데이터는 익명으로 처리됩니다. If `analyticsDeleteMethod` 가 생략되면 기본 동작입니다.</li><li>`purge`: 모든 데이터가 완전히 제거됩니다.</li></ul> |
| `mergePolicyId` | 실시간 고객 프로필에 대한 개인 정보 요청을 할 때(`profileService`)에 대해 선택적으로 특정 항목의 ID를 제공할 수 있습니다 [병합 정책](../../profile/merge-policies/overview.md) ID 결합에 사용할 수 있습니다. 병합 정책을 지정하여 개인 정보 보호 요청은 고객에 대한 데이터를 반환할 때 대상 정보를 포함할 수 있습니다. 요청당 하나의 병합 정책만 지정할 수 있습니다. 병합 정책이 제공되지 않으면 세그멘테이션 정보가 응답에 포함되지 않습니다. |
| `regulation` **(필수)** | 개인 정보 보호 작업에 대한 규정. 다음 값이 허용됩니다. <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>의 개요 보기 [지원되는 규정](../regulations/overview.md) 위의 값이 나타내는 개인 정보 보호 규정에 대한 자세한 정보입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 새로 생성된 작업의 세부 정보를 반환합니다.

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
| `jobId` | 작업에 대한 읽기 전용의 고유한 시스템 생성 ID입니다. 이 값은 특정 작업을 조회하는 다음 단계에서 사용됩니다. |

{style="table-layout:auto"}

작업 요청을 성공적으로 제출했으면 의 다음 단계로 진행할 수 있습니다. [작업 상태 확인](#check-status).

## 작업 상태 확인 {#check-status}

현재 처리 상태와 같은 특정 작업에 대한 정보를 해당 작업의 `jobId` 에 대한 GET 요청 경로 `/jobs` 엔드포인트.

>[!IMPORTANT]
>
>이전에 생성된 작업의 데이터는 작업 완료 날짜로부터 30일 이내에만 검색할 수 있습니다.

**API 형식**

```http
GET /jobs/{JOB_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{JOB_ID}` | 조회할 작업의 ID입니다. 이 ID는에 반환됩니다 `jobId` 에 대한 성공적인 API 응답 [작업 생성](#create-job) 및 [모든 작업 나열](#list). |

{style="table-layout:auto"}

**요청**

다음 요청은 다음과 같은 작업의 세부 정보를 검색합니다. `jobId` 은 요청 경로에 제공됩니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답은 지정된 작업의 세부 정보를 반환합니다.

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
| `productStatusResponse` | 내의 각 개체 `productResponses` 배열에는 특정 작업에 대한 현재 상태 정보가 포함되어 있습니다. [!DNL Experience Cloud] 응용 프로그램. |
| `productStatusResponse.status` | 작업의 현재 상태 범주입니다. 다음 목록을 보려면 아래 표를 참조하십시오. [사용 가능한 상태 범주](#status-categories) 및 해당 의미. |
| `productStatusResponse.message` | 상태 범주에 해당하는 작업별 상태. |
| `productStatusResponse.responseMsgCode` | 에 의해 수신된 제품 응답 메시지에 대한 표준 코드 [!DNL Privacy Service]. 메시지의 세부 사항은 아래에 제공됩니다. `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 작업 상태에 대한 자세한 설명. 유사한 상태에 대한 메시지는 제품마다 다를 수 있습니다. |
| `productStatusResponse.results` | 특정 상태의 경우 일부 제품은 `results` 다음에서 다루지 않는 추가 정보를 제공하는 개체 `responseMsgDetail`. |
| `downloadURL` | 작업 상태가 다음과 같은 경우 `complete`, 이 속성은 작업 결과를 ZIP 파일로 다운로드할 URL을 제공합니다. 이 파일은 작업이 완료된 후 60일 동안 다운로드할 수 있습니다. |

{style="table-layout:auto"}

### 작업 상태 범주 {#status-categories}

다음 표에는 가능한 다양한 작업 상태 범주와 해당 의미가 나열되어 있습니다.

| 상태 범주 | 의미 |
| -------------- | -------- |
| `complete` | 작업이 완료되었으며 필요한 경우 모든 애플리케이션에서 파일이 업로드됩니다. |
| `processing` | 응용 프로그램이 작업을 승인했으며 현재 처리 중입니다. |
| `submitted` | 해당하는 모든 애플리케이션에 작업이 제출됩니다. |
| `error` | 작업 처리에 오류가 발생했습니다. 개별 작업 세부 정보를 검색하여 보다 구체적인 정보를 얻을 수 있습니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>제출된 작업은에 남아 있을 수 있음 `processing` 아직 처리 중인 종속 하위 작업이 있는 경우 상태를 지정합니다.

## 다음 단계

이제 다음을 사용하여 개인 정보 작업을 만들고 모니터링하는 방법을 배웁니다. [!DNL Privacy Service] API. 사용자 인터페이스를 사용하여 동일한 작업을 수행하는 방법에 대한 자세한 내용은 [Privacy Service UI 개요](../ui/overview.md).
