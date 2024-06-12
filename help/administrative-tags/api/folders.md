---
title: 폴더 끝점
description: Adobe Experience Platform API를 사용하여 폴더를 만들고, 업데이트하고, 관리하고, 삭제하는 방법에 대해 알아봅니다.
role: Developer
source-git-commit: 8f9a2b5a2063b76518302eb9de38b628c87416e1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 4%

---


# 폴더 엔드포인트

>[!IMPORTANT]
>
>이 끝점 세트의 끝점 URL은 `https://experience.adobe.io`.

폴더는 보다 쉽게 탐색하고 분류할 수 있도록 비즈니스 객체를 보다 효율적으로 구성할 수 있는 기능입니다.

이 안내서에서는 폴더를 더 잘 이해하는 데 도움이 되는 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 폴더 목록 검색 {#list}

에 GET 요청을 하여 조직에 속한 폴더 목록을 검색할 수 있습니다. `/folder` 끝점 및 폴더 유형 및 상위 폴더 ID 지정.

**API 형식**

```http
GET /folder/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 폴더 내에 포함된 객체의 유형입니다. 지원되는 값은 다음과 같습니다 `segment` 및 `dataset`. |
| `{PARENT_FOLDER_ID}` | 폴더 목록을 검색하는 상위 폴더의 ID입니다. 모든 상위 폴더 목록을 보려면 폴더 ID를 사용하십시오 `root`. |

**요청**

+++모든 최상위 데이터 세트 폴더를 나열하는 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 조직의 데이터 세트에 대한 모든 최상위 폴더 목록과 함께 HTTP 상태 200을 반환합니다.

+++조직의 데이터 세트에 대한 모든 최상위 폴더 목록을 포함하는 샘플 응답입니다.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## 새 폴더 만들기 {#create}

에 POST 요청을 하여 새 폴더를 만들 수 있습니다. `/folder` 끝점 및 폴더 유형 지정.

**API 형식**

```http
POST /folder/{FOLDER_TYPE}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 폴더 내에 포함된 객체의 유형입니다. 지원되는 값은 다음과 같습니다 `segment` 및 `dataset`. |

**요청**

+++새 폴더를 만들기 위한 샘플 요청입니다.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folder/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 만들려는 폴더의 이름입니다. |
| `parentId` | 상위 폴더의 ID입니다. |

+++

**응답**

성공한 응답은 새로 만든 폴더의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++새로 만든 폴더의 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 생성된 폴더의 ID입니다. |
| `createdBy` | 폴더를 만든 사용자의 ID입니다. |
| `createdAt` | 폴더가 생성된 시간의 타임스탬프입니다. |
| `modifiedBy` | 폴더를 마지막으로 수정한 사용자의 ID입니다. |
| `modifiedAt` | 폴더가 마지막으로 업데이트된 시간의 타임스탬프입니다. |

+++

## 특정 폴더 검색 {#get}

에 GET 요청을 하여 조직에 속한 특정 폴더를 검색할 수 있습니다. `/folder` 끝점 및 폴더 유형 및 폴더의 ID를 지정합니다.

**API 형식**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 폴더 내에 포함된 객체의 유형입니다. 지원되는 값은 다음과 같습니다 `segment` 및 `dataset`. |
| `{FOLDER_ID}` | 검색 중인 폴더의 ID입니다. |

**요청**

+++특정 폴더를 검색하기 위한 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 요청된 폴더의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++요청된 폴더의 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 요청한 폴더의 ID입니다. |
| `name` | 요청한 폴더의 이름입니다. |
| `parentId` | 상위 폴더의 ID입니다. |
| `createdBy` | 폴더를 만든 사용자의 ID입니다. |
| `createdAt` | 폴더가 생성된 시간의 타임스탬프입니다. |
| `modifiedBy` | 폴더를 마지막으로 업데이트한 사용자의 ID입니다. |
| `modifiedAt` | 폴더가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `status` | 요청한 폴더의 상태입니다. 지원되는 값: `IN_USE` 및 `ARCHIVED`. |

+++

## 지정된 폴더의 유효성 검사 {#validate}

에 GET 요청을 하여 폴더에 객체가 있을 수 있는지 확인할 수 있습니다. `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` 을 종료하고 폴더 유형과 ID를 모두 제공합니다.

**API 형식**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 폴더 내에 포함된 객체의 유형입니다. 지원되는 값은 다음과 같습니다 `segment` 및 `dataset`. |
| `{FOLDER_ID}` | 확인 중인 폴더의 ID입니다. |

**요청**

+++특정 폴더의 유효성을 검사하는 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공 상태는 확인 중인 폴더의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++샘플 응답에는 검증된 폴더의 세부 정보가 포함됩니다

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## 특정 폴더 업데이트 {#update}

에 PATCH 요청을 하여 조직에 속한 특정 폴더의 세부 정보를 업데이트할 수 있습니다. `/folder` 끝점 및 폴더 유형 및 폴더의 ID를 지정합니다.

**API 형식**

```http
PATCH /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 폴더 내에 포함된 객체의 유형입니다. 지원되는 값은 다음과 같습니다 `segment` 및 `dataset`. |
| `{FOLDER_ID}` | 업데이트 중인 폴더의 ID입니다. |

**요청**

+++특정 폴더를 업데이트하기 위한 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**응답**

성공적인 응답은 새로 업데이트된 폴더에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## 특정 폴더 삭제 {#delete}

에 DELETE 요청을 하여 조직에 속한 특정 폴더를 삭제할 수 있습니다. `/folder` 폴더 유형 및 폴더의 ID를 지정합니다.

***API 형식**

```http
DELETE /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 폴더 내에 포함된 객체의 유형입니다. 지원되는 값은 다음과 같습니다 `segment` 및 `dataset`. |
| `{FOLDER_ID}` | 삭제 중인 폴더의 ID입니다. |

**요청**

+++특정 폴더 삭제에 대한 샘플 요청

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 폴더의 삭제를 알리는 메시지 본문과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "message": "delete request accepted successfully"
}
```

## 다음 단계

이제 이 안내서를 읽고 Adobe Experience Platform API를 사용하여 폴더를 만들고 관리하고 삭제하는 방법을 더 잘 이해할 수 있습니다.
