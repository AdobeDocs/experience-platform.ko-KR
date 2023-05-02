---
solution: Experience Platform
title: Flow Service API를 사용하여 대상 연결 편집
type: Tutorial
description: Flow Service API를 사용하여 대상 연결의 다양한 구성 요소를 편집하는 방법을 알아봅니다.
source-git-commit: 52fe0ef2ab195756c381b3ef0a5792dffe459b8d
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 2%

---

# Flow Service API를 사용하여 대상 연결 편집

이 자습서에서는 대상 연결의 다양한 구성 요소를 편집하는 단계를 설명합니다. 를 사용하여 인증 자격 증명을 업데이트하고 위치를 내보내는 방법을 알아봅니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 이 자습서에서 설명하는 편집 작업은 현재 Flow Service API를 통해서만 지원됩니다.

## 시작하기 {#get-started}

이 자습서에서는 유효한 데이터 흐름 ID가 있어야 합니다. 유효한 데이터 흐름 ID가 없는 경우, [대상 카탈로그](../catalog/overview.md) 및 다음에 요약된 단계를 따릅니다. [대상에 연결](../ui/connect-destination.md) 및 [데이터 활성화](../ui/activation-overview.md) 이 자습서를 시작하기 전에

>[!NOTE]
>
> 용어 *흐름* 및 *데이터 흐름* 는 이 자습서에서 서로 교환하여 사용됩니다. 이 자습서의 컨텍스트에서는 동일한 의미가 있습니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): [!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 사용하여 데이터 흐름을 성공적으로 업데이트하려면 알아야 하는 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다 {#gather-values-for-required-headers}

플랫폼 API를 호출하려면 먼저 를 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

에 속하는 리소스를 포함하여 Experience Platform의 모든 리소스 [!DNL Flow Service]은 특정 가상 샌드박스로 구분됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>만약 `x-sandbox-name` 헤더를 지정하지 않으면 요청이 `prod` 샌드박스

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 흐름 세부 정보 보기 {#look-up-dataflow-details}

대상 연결을 편집하는 첫 번째 단계는 흐름 ID를 사용하여 데이터 흐름 세부 사항을 검색하는 것입니다. 에 GET 요청을 수행하여 기존 데이터 흐름의 현재 세부 사항을 볼 수 있습니다 `/flows` 엔드포인트.

>[!TIP]
>
>Experience Platform UI를 사용하여 대상의 데이터 흐름 ID를 가져올 수 있습니다. 이동 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**&#x200B;원하는 대상 데이터 흐름을 선택하고 오른쪽 레일에서 대상 ID를 찾습니다. 대상 ID는 다음 단계에서 흐름 ID로 사용할 값입니다.
>
> ![Experience Platform UI를 사용하여 대상 ID 가져오기](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API 형식**

```http
GET /flows/{FLOW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 고유 `id` 검색할 대상 데이터 흐름의 값입니다. |

**요청**

다음 요청은 흐름 ID에 대한 정보를 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 해당 버전, 고유 식별자( )를 포함하여 데이터 흐름의 현재 세부 사항을 반환합니다`id`) 및 기타 관련 정보. 이 자습서에 가장 적절한 것은 아래 응답에 강조 표시된 target 연결 및 기본 연결 ID입니다. 다음 섹션에서 이러한 ID를 사용하여 대상 연결의 다양한 구성 요소를 업데이트합니다.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## 대상 연결 구성 요소 편집(저장소 위치 및 기타 구성 요소) {#patch-target-connection}

대상 연결의 구성 요소는 대상에 따라 다릅니다. 예, 예 [!DNL Amazon S3] 대상, 파일을 내보내는 버킷과 경로를 업데이트할 수 있습니다. 대상 [!DNL Pinterest] 대상, 업데이트 [!DNL Pinterest Advertiser ID] 및 대상 [!DNL Google Customer Match] 을(를) 업데이트할 수 있습니다. [!DNL Pinterest Account ID].

대상 연결의 구성 요소를 업데이트하려면 `/targetConnections/{TARGET_CONNECTION_ID}` target 연결 ID, 버전 및 사용할 새 값을 제공하는 동안 종단점입니다. 기존 데이터 흐름을 원하는 대상으로 검사할 때 이전 단계에서 대상 연결 ID를 받았음을 기억하십시오.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 만들 때는 헤더가 필요합니다. 이 헤더의 값은 업데이트할 대상 연결의 고유한 버전입니다. 태그 값은 데이터 흐름, 타겟 연결 등과 같은 흐름 엔터티를 성공적으로 업데이트할 때마다 업데이트됩니다.
>
> 최신 버전의 태그 값을 얻으려면 `/targetConnections/{TARGET_CONNECTION_ID}` 엔드포인트, 위치 `{TARGET_CONNECTION_ID}` 는 업데이트할 target 연결 ID입니다.

다음은 다양한 유형의 대상에 대한 target 연결 사양에서 매개 변수를 업데이트하는 몇 가지 예입니다. 그러나 대상에 대한 매개 변수를 업데이트하는 일반적인 규칙은 다음과 같습니다.

연결의 데이터 흐름 ID를 가져오고 > 타겟 연결 ID 가져오기 > 원하는 매개 변수에 대해 업데이트된 값으로 타겟 연결을 PATCH 합니다.

>[!BEGINSHADEBOX]

**API 형식**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!ENDSHADEBOX]


>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

다음 요청은 를 업데이트합니다 `bucketName` 및 `path` 의 매개 변수 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 대상 연결.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 흐름의 일부를 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 타겟 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 타겟 연결 ID를 제공하는 동안

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager 360]

**요청**

다음 요청은 의 매개 변수를 업데이트합니다 [[!DNL Google Ad Manager 360] 대상](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 세그먼트 이름에 새 세그먼트 ID 추가 필드를 추가하기 위한 연결입니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 흐름의 일부를 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 타겟 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 타겟 연결 ID를 제공하는 동안

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**요청**

다음 요청은 를 업데이트합니다 `advertiserId` 의 매개 변수 [[!DNL Pinterest] 대상 연결](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 흐름의 일부를 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 타겟 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 타겟 연결 ID를 제공하는 동안

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

## 기본 연결 구성 요소(인증 매개 변수 및 기타 구성 요소) 편집 {#patch-base-connection}

기본 연결의 구성 요소는 대상에 따라 다릅니다. 예, 예 [!DNL Amazon S3] 대상, 액세스 키 및 비밀 키를 [!DNL Amazon S3] 위치.

기본 연결의 구성 요소를 업데이트하려면 `/connections` 기본 연결 ID, 버전 및 사용할 새 값을 제공하는 동안 종단점입니다.

기존 데이터 흐름을 원하는 대상으로 검사할 때 이전 단계에서 기본 연결 ID를 얻었다는 것을 기억하십시오.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 만들 때는 헤더가 필요합니다. 이 헤더의 값은 업데이트할 기본 연결의 고유한 버전입니다. 태그 값은 데이터 흐름, 기본 연결 등과 같은 흐름 엔터티를 성공적으로 업데이트할 때마다 업데이트됩니다.
>
> 최신 버전의 태그 값을 얻으려면 `/connections/{BASE_CONNECTION_ID}` 엔드포인트, 위치 `{BASE_CONNECTION_ID}` 는 업데이트할 기본 연결 ID입니다.

다음은 다양한 유형의 대상에 대한 기본 연결 사양에서 매개 변수를 업데이트하는 몇 가지 예입니다. 그러나 대상에 대한 매개 변수를 업데이트하는 일반적인 규칙은 다음과 같습니다.

연결의 데이터 흐름 ID를 가져오고 > 기본 연결 ID 가져오기 > 원하는 매개 변수에 대해 업데이트된 값으로 기본 연결을 PATCH 합니다.

**API 형식**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

다음 요청은 를 업데이트합니다 `accessId` 및 `secretKey` 의 매개 변수 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 대상 연결.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 흐름의 일부를 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 기본 연결 ID를 제공하는 동안

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**요청**

다음 요청은 의 매개 변수를 업데이트합니다 [[!DNL Azure Blob] 대상](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 연결 을 사용하여 Azure Blob 인스턴스에 연결하는 데 필요한 연결 문자열을 업데이트합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 흐름의 일부를 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 기본 연결 ID를 제공하는 동안

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

## API 오류 처리 {#api-error-handling}

이 자습서의 API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors) 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 가이드를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서에서는 를 사용하여 대상 연결의 다양한 구성 요소를 업데이트하는 방법을 알아보았습니다 [!DNL Flow Service] API. 대상에 대한 자세한 내용은 [대상 개요](../home.md).
