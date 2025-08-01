---
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 대상 연결 편집
type: Tutorial
description: 흐름 서비스 API를 사용하여 대상 연결의 다양한 구성 요소를 편집하는 방법에 대해 알아봅니다.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: ea397360e5277bef478b2173bfb5e4be4ac1fab4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 흐름 서비스 API를 사용하여 대상 연결 편집

이 자습서에서는 대상 연결의 다양한 구성 요소를 편집하는 단계를 다룹니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 인증 자격 증명, 내보내기 위치 등을 업데이트하는 방법에 대해 알아봅니다.

>[!NOTE]
>
> 이 자습서에 설명된 편집 작업은 Experience Platform UI에서도 지원됩니다. 자세한 내용은 UI에서 대상을 [편집](/help/destinations/ui/edit-destination.md)하는 방법에 대한 자습서를 참조하십시오.

## 시작 {#get-started}

이 자습서에서는 유효한 데이터 흐름 ID가 있어야 합니다. 유효한 데이터 흐름 ID가 없는 경우 [대상 카탈로그](../catalog/overview.md)에서 선택한 대상을 선택하고 [대상에 연결](../ui/connect-destination.md) 및 [데이터 활성화](../ui/activation-overview.md)에 설명된 단계를 따라 이 자습서를 시작하십시오.

>[!NOTE]
>
> 이 자습서에서는 용어 *흐름*&#x200B;과(와) *데이터 흐름*&#x200B;을(를) 교환하여 사용합니다. 이 자습서의 컨텍스트에서 동일한 의미를 갖습니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): [!DNL Destinations]은(는) Adobe Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 데이터 흐름을 성공적으로 업데이트하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집 {#gather-values-for-required-headers}

Experience Platform API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Flow Service]에 속하는 리소스를 포함한 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 격리됩니다. Experience Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>`x-sandbox-name` 헤더를 지정하지 않으면 `prod` 샌드박스에서 요청이 확인됩니다.

페이로드(`POST`, `PUT`, `PATCH`)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 흐름 세부 정보 조회 {#look-up-dataflow-details}

대상 연결을 편집하는 첫 번째 단계는 흐름 ID를 사용하여 데이터 흐름 세부 정보를 검색하는 것입니다. `/flows` 끝점에 대한 GET 요청을 수행하면 기존 데이터 흐름의 현재 세부 정보를 볼 수 있습니다.

>[!TIP]
>
>Experience Platform UI를 사용하여 원하는 대상 데이터 흐름 ID를 가져올 수 있습니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**(으)로 이동하여 원하는 대상 데이터 흐름을 선택하고 오른쪽 레일에서 대상 ID를 찾습니다. 대상 ID는 다음 단계에서 흐름 ID로 사용할 값입니다.
>
> ![Experience Platform UI를 사용하여 대상 ID 가져오기](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API 형식**

```http
GET /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 검색할 대상 데이터 흐름의 고유한 `id` 값입니다. |

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

성공적인 응답은 버전, 고유 식별자(`id`) 및 기타 관련 정보를 포함하여 데이터 흐름의 현재 세부 정보를 반환합니다. 이 자습서와 가장 관련이 있는 것은 아래 응답에서 강조 표시된 대상 연결 및 기본 연결 ID입니다. 다음 섹션에서 이러한 ID를 사용하여 대상 연결의 다양한 구성 요소를 업데이트합니다.

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

대상 연결의 구성 요소는 대상마다 다릅니다. 예를 들어 [!DNL Amazon S3] 대상의 경우 파일을 내보내는 버킷 및 경로를 업데이트할 수 있습니다. [!DNL Pinterest] 대상의 경우 [!DNL Pinterest Advertiser ID]을(를) 업데이트할 수 있으며 [!DNL Google Customer Match]의 경우 [!DNL Pinterest Account ID]을(를) 업데이트할 수 있습니다.

대상 연결의 구성 요소를 업데이트하려면 대상 연결 ID, 버전 및 사용할 새 값을 제공하는 동안 `PATCH` 끝점에 대해 `/targetConnections/{TARGET_CONNECTION_ID}` 요청을 수행합니다. 이전 단계에서 원하는 대상에 대한 기존 데이터 흐름을 검사했을 때 대상 연결 ID를 얻었다는 것을 기억하십시오.

>[!IMPORTANT]
>
>`If-Match`을(를) 요청할 때 `PATCH` 헤더가 필요합니다. 이 헤더 값은 업데이트하려는 대상 연결의 고유한 버전입니다. 데이터 흐름, 대상 연결 등 플로우 엔티티를 성공적으로 업데이트할 때마다 etag 값이 업데이트됩니다.
>
> 최신 버전의 etag 값을 가져오려면 `/targetConnections/{TARGET_CONNECTION_ID}` 끝점에 대한 GET 요청을 수행합니다. 여기서 `{TARGET_CONNECTION_ID}`은(는) 업데이트하려는 대상 연결 ID입니다.
>
> `If-Match`개의 요청을 할 때는 아래 예제와 같이 `PATCH` 헤더의 값을 큰따옴표로 묶어야 합니다.

다음은 다양한 대상 유형에 대한 대상 연결 사양의 매개 변수를 업데이트하는 몇 가지 예입니다. 그러나 모든 대상에 대한 매개 변수를 업데이트하는 일반 규칙은 다음과 같습니다.

연결의 데이터 흐름 ID를 가져오고 > 대상 연결 ID를 가져오고 > 원하는 매개 변수에 대해 업데이트된 값이 있는 대상 연결을 `PATCH`합니다.

>[!BEGINSHADEBOX]

**API 형식**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

다음 요청은 `bucketName` 대상 연결의 `path` 및 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 매개 변수를 업데이트합니다.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 대상 연결 ID와 업데이트된 Etag를 반환합니다. 대상 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 업데이트를 확인할 수 있습니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google 광고 관리자 및 Google 광고 관리자 360]

**요청**

다음 요청은 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 또는 [[!DNL Google Ad Manager 360] 대상](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 연결의 매개 변수를 업데이트하여 새 [**[!UICONTROL 대상 ID를 대상 이름에 추가]**](/help/release-notes/2023/april-2023.md#destinations) 필드를 추가합니다.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 대상 연결 ID와 업데이트된 etag를 반환합니다. 대상 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 업데이트를 확인할 수 있습니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**요청**

다음 요청은 `advertiserId`대상 연결[[!DNL Pinterest] 의 ](/help/destinations/catalog/advertising/pinterest.md#parameters) 매개 변수를 업데이트합니다.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 대상 연결 ID와 업데이트된 etag를 반환합니다. 대상 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 업데이트를 확인할 수 있습니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 기본 연결 구성 요소 편집(인증 매개 변수 및 기타 구성 요소) {#patch-base-connection}

대상의 자격 증명을 업데이트하려면 기본 연결을 편집합니다. 기본 연결의 구성 요소는 대상마다 다릅니다. 예를 들어 [!DNL Amazon S3] 대상의 경우 [!DNL Amazon S3] 위치에 액세스 키와 비밀 키를 업데이트할 수 있습니다.

기본 연결의 구성 요소를 업데이트하려면 기본 연결 ID, 버전 및 사용할 새 값을 제공하는 동안 `PATCH` 끝점에 대해 `/connections` 요청을 수행합니다.

매개 변수 [에 대해 원하는 대상으로 기존 데이터 흐름을 검사했을 때 ](#look-up-dataflow-details)이전 단계`baseConnection`에서 기본 연결 ID를 얻었습니다.

>[!IMPORTANT]
>
>`If-Match`을(를) 요청할 때 `PATCH` 헤더가 필요합니다. 이 헤더의 값은 업데이트하려는 기본 연결의 고유 버전입니다. 데이터 흐름, 기본 연결 등 흐름 엔티티가 성공적으로 업데이트될 때마다 etag 값이 업데이트됩니다.
>
> 최신 버전의 Etag 값을 가져오려면 `/connections/{BASE_CONNECTION_ID}` 끝점에 대한 GET 요청을 수행합니다. 여기서 `{BASE_CONNECTION_ID}`은(는) 업데이트하려는 기본 연결 ID입니다.
>
> `If-Match`개의 요청을 할 때는 아래 예제와 같이 `PATCH` 헤더의 값을 큰따옴표로 묶어야 합니다.

다음은 다양한 유형의 대상에 대해 기본 연결 사양의 매개 변수를 업데이트하는 몇 가지 예입니다. 그러나 모든 대상에 대한 매개 변수를 업데이트하는 일반 규칙은 다음과 같습니다.

연결의 데이터 흐름 ID를 가져오고 > 기본 연결 ID를 가져오고 > 원하는 매개 변수에 대해 업데이트된 값이 있는 기본 연결을 `PATCH`합니다.

>[!BEGINSHADEBOX]

**API 형식**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

다음 요청은 `accessId` 대상 연결의 `secretKey` 및 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 매개 변수를 업데이트합니다.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 etag를 반환합니다. 기본 연결 ID를 제공하면서 [!DNL Flow Service] API에 대한 GET 요청을 만들어 업데이트를 확인할 수 있습니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**요청**

다음 요청은 [[!DNL Azure Blob] destination](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 연결의 매개 변수를 업데이트하여 Azure Blob 인스턴스에 연결하는 데 필요한 연결 문자열을 업데이트합니다.

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
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 etag를 반환합니다. 기본 연결 ID를 제공하면서 [!DNL Flow Service] API에 대한 GET 요청을 만들어 업데이트를 확인할 수 있습니다.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API 오류 처리 {#api-error-handling}

이 자습서의 API 끝점은 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 오류 응답 해석에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서를 통해 [!DNL Flow Service] API를 사용하여 대상 연결의 다양한 구성 요소를 업데이트하는 방법을 배웠습니다. 대상에 대한 자세한 내용은 [대상 개요](../home.md)를 참조하십시오.
