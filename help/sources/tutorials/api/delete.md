---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;계정 삭제;삭제;api
solution: Experience Platform
title: Flow Service API를 사용하여 계정 삭제
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 계정을 삭제하는 방법을 알아봅니다.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---

# Flow Service API를 사용하여 계정 삭제

Adobe Experience Platform을 사용하면 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Flow Service] Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 삭제하는 단계를 설명합니다.

## 시작하기

이 자습서에서는 올바른 연결 ID가 있어야 합니다. 올바른 연결 ID가 없는 경우 [소스 개요](../../home.md)에서 선택한 커넥터를 선택하고 이 자습서를 시작하기 전에 설명된 단계를 따르십시오.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md):  [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../sandboxes/home.md):  [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 연결을 성공적으로 삭제하려면 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 세부 정보 조회

>[!NOTE]
>이 자습서에서는 [Azure Blob 소스 커넥터](../../connectors/cloud-storage/blob.md)를 사용하지만, 요약된 단계는 [사용 가능한 소스 커넥터](../../home.md)에 적용됩니다.

연결 정보를 업데이트하는 첫 번째 단계는 연결 ID를 사용하여 연결 세부 사항을 검색하는 것입니다.

**API 형식**

```http
GET /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 검색할 연결의 고유한 `id` 값입니다. |

**요청**

다음은 연결 ID에 대한 정보를 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 해당 자격 증명, 고유 식별자(`id`) 및 버전을 포함하여 연결의 현재 세부 정보를 반환합니다.

```json
{
    "items": [
        {
            "createdAt": 1603514659165,
            "updatedAt": 1603514659165,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "dd3631cd-d0ea-4fea-b631-cdd0ea6fea21",
            "name": "Test Azure Blob Connector",
            "description": "A test connector for Azure Blob",
            "connectionSpec": {
                "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "ConnectionString",
                "params": {
                    "connectionString": "xxxx"
                }
            },
            "version": "\"07001eed-0000-0200-0000-5f93b1250000\"",
            "etag": "\"07001eed-0000-0200-0000-5f93b1250000\""
        }
    ]
}
```

## 연결 삭제

기존 연결 ID가 있는 경우 [!DNL Flow Service] API에 DELETE 요청을 수행합니다.

**API 형식**

```http
DELETE /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 삭제할 연결의 고유한 `id` 값입니다. |

**요청**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

연결에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다.

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 기존 계정을 삭제했습니다.

사용자 인터페이스를 사용하여 이러한 작업을 수행하는 방법에 대한 단계는 [UI](../../tutorials/ui/delete-accounts.md)에서 계정 삭제에서 자습서를 참조하십시오
