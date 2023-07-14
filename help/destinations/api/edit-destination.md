---
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 대상 연결 편집
type: Tutorial
description: 흐름 서비스 API를 사용하여 대상 연결의 다양한 구성 요소를 편집하는 방법에 대해 알아봅니다.
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 3%

---

# 흐름 서비스 API를 사용하여 대상 연결 편집

이 자습서에서는 대상 연결의 다양한 구성 요소를 편집하는 단계를 다룹니다. 를 사용하여 인증 자격 증명, 내보내기 위치 등을 업데이트하는 방법에 대해 알아봅니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 이 자습서에 설명된 편집 작업은 현재 흐름 서비스 API를 통해서만 지원됩니다.

## 시작하기 {#get-started}

이 자습서에서는 유효한 데이터 흐름 ID가 있어야 합니다. 유효한 데이터 흐름 ID가 없는 경우 [대상 카탈로그](../catalog/overview.md) 다음에 설명된 단계를 수행합니다. [대상에 연결](../ui/connect-destination.md) 및 [데이터 활성화](../ui/activation-overview.md) 이 자습서를 시도하기 전에.

>[!NOTE]
>
> 용어 *흐름* 및 *데이터 흐름* 는 이 자습서에서 서로 교환하여 사용할 수 있습니다. 이 자습서의 컨텍스트에서 동일한 의미를 갖습니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): [!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 다음을 사용하여 데이터 흐름을 성공적으로 업데이트하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 참조하십시오.

### 필수 헤더에 대한 값 수집 {#gather-values-for-required-headers}

Platform API를 호출하려면 먼저 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform에 속한 리소스를 포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스로 분리됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>다음과 같은 경우 `x-sandbox-name` 헤더가 지정되지 않았습니다. 요청은에서 확인됩니다. `prod` 샌드박스.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 흐름 세부 정보 조회 {#look-up-dataflow-details}

대상 연결을 편집하는 첫 번째 단계는 흐름 ID를 사용하여 데이터 흐름 세부 정보를 검색하는 것입니다. 에 GET 요청을 하여 기존 데이터 흐름의 현재 세부 정보를 볼 수 있습니다. `/flows` 엔드포인트.

>[!TIP]
>
>Experience Platform UI를 사용하여 대상의 원하는 데이터 흐름 ID를 가져올 수 있습니다. 다음으로 이동 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**&#x200B;에서 원하는 대상 데이터 흐름을 선택하고 오른쪽 레일에서 대상 ID를 찾습니다. 대상 ID는 다음 단계에서 흐름 ID로 사용할 값입니다.
>
> ![Experience Platform UI를 사용하여 대상 ID 가져오기](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API 형식**

```http
GET /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 고유 `id` 검색할 대상 데이터 흐름의 값입니다. |

**요청**

다음 요청은 플로우 ID와 관련된 정보를 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 버전, 고유 식별자( )를 포함하여 데이터 흐름의 현재 세부 정보를 반환합니다.`id`) 및 기타 관련 정보. 이 자습서와 가장 관련이 있는 것은 아래 응답에서 강조 표시된 대상 연결 및 기본 연결 ID입니다. 다음 섹션에서 이러한 ID를 사용하여 대상 연결의 다양한 구성 요소를 업데이트합니다.

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

## 대상 연결 구성 요소(저장소 위치 및 기타 구성 요소) 편집 {#patch-target-connection}

대상 연결의 구성 요소는 대상마다 다릅니다. 예를 들어 [!DNL Amazon S3] 대상 에서는 파일을 내보내는 버킷과 경로를 업데이트할 수 있습니다. 대상 [!DNL Pinterest] 대상, 다음을 업데이트할 수 있습니다. [!DNL Pinterest Advertiser ID] 및 [!DNL Google Customer Match] 다음을 업데이트할 수 있습니다. [!DNL Pinterest Account ID].

대상 연결의 구성 요소를 업데이트하려면에 대한 PATCH 요청을 수행합니다 `/targetConnections/{TARGET_CONNECTION_ID}` 대상 연결 ID, 버전 및 사용할 새 값을 제공하는 동안 끝점이 발생했습니다. 이전 단계에서 원하는 대상에 대한 기존 데이터 흐름을 검사했을 때 대상 연결 ID를 얻었다는 것을 기억하십시오.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 할 때 헤더가 필요합니다. 이 헤더 값은 업데이트하려는 대상 연결의 고유한 버전입니다. 데이터 흐름, 대상 연결 등 플로우 엔티티를 성공적으로 업데이트할 때마다 etag 값이 업데이트됩니다.
>
> GET 최신 버전의 etag 값을 가져오려면 `/targetConnections/{TARGET_CONNECTION_ID}` 끝점, 여기서 `{TARGET_CONNECTION_ID}` 는 업데이트하려는 타겟 연결 ID입니다.

다음은 다양한 대상 유형에 대한 대상 연결 사양의 매개 변수를 업데이트하는 몇 가지 예입니다. 그러나 모든 대상에 대한 매개 변수를 업데이트하는 일반 규칙은 다음과 같습니다.

연결의 데이터 흐름 ID 가져오기 > 대상 연결 ID 가져오기 > 원하는 매개 변수에 대해 업데이트된 값으로 대상 연결을 PATCH 합니다.

>[!BEGINSHADEBOX]

**API 형식**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

다음 요청은 `bucketName` 및 `path` 의 매개 변수 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 대상 연결.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 대상 연결 ID와 업데이트된 Etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] API, 대상 연결 ID 제공

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager 및 Google Ad Manager 360]

**요청**

다음 요청은 의 매개변수를 업데이트합니다. [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 또는 [[!DNL Google Ad Manager 360] 대상](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 연결을 통해 새 항목 추가 [**[!UICONTROL 대상 이름에 대상 ID 추가]**](/help/release-notes/2023/april-2023.md#destinations) 필드.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 대상 연결 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] API, 대상 연결 ID 제공

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**요청**

다음 요청은 `advertiserId` 매개 변수 [[!DNL Pinterest] 대상 연결](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 대상 연결 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] API, 대상 연결 ID 제공

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 기본 연결 구성 요소 편집(인증 매개 변수 및 기타 구성 요소) {#patch-base-connection}

대상의 자격 증명을 업데이트하려면 기본 연결을 편집합니다. 기본 연결의 구성 요소는 대상마다 다릅니다. 예를 들어 [!DNL Amazon S3] 대상, 액세스 키 및 비밀 키를 [!DNL Amazon S3] 위치.

PATCH 기본 연결의 구성 요소를 업데이트하려면 `/connections` 기본 연결 ID, 버전 및 사용할 새 값을 제공하는 동안 끝점이 발생했습니다.

에 기본 연결 ID가 있습니다. [이전 단계](#look-up-dataflow-details)매개 변수에 대해 원하는 대상으로 기존 데이터 흐름을 검사한 경우 `baseConnection`.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 할 때 헤더가 필요합니다. 이 헤더의 값은 업데이트하려는 기본 연결의 고유 버전입니다. 데이터 흐름, 기본 연결 등 흐름 엔티티가 성공적으로 업데이트될 때마다 etag 값이 업데이트됩니다.
>
> GET 최신 버전의 Etag 값을 가져오려면 `/connections/{BASE_CONNECTION_ID}` 끝점, 여기서 `{BASE_CONNECTION_ID}` 는 업데이트하려는 기본 연결 ID입니다.

다음은 다양한 유형의 대상에 대해 기본 연결 사양의 매개 변수를 업데이트하는 몇 가지 예입니다. 그러나 모든 대상에 대한 매개 변수를 업데이트하는 일반 규칙은 다음과 같습니다.

연결의 데이터 흐름 ID를 가져오고 > 기본 연결 ID를 가져오고 > 원하는 매개 변수에 대해 업데이트된 값으로 기본 연결을 PATCH 합니다.

>[!BEGINSHADEBOX]

**API 형식**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

다음 요청은 `accessId` 및 `secretKey` 의 매개 변수 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 대상 연결.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 기본 연결 ID를 제공하는 동안 API입니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**요청**

다음 요청은 의 매개변수를 업데이트합니다. [[!DNL Azure Blob] 대상](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) azure Blob 인스턴스에 연결하는 데 필요한 연결 문자열을 업데이트하는 연결입니다.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 기본 연결 ID를 제공하는 동안 API입니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API 오류 처리 {#api-error-handling}

이 자습서의 API 끝점은 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors) 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 안내서를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서를 따라 를 사용하여 대상 연결의 다양한 구성 요소를 업데이트하는 방법을 배웠습니다. [!DNL Flow Service] API. 대상에 대한 자세한 내용은 [대상 개요](../home.md).
