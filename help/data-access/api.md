---
keywords: Experience Platform;home;popular topics;data access;python sdk;spark sdk;data access api
solution: Experience Platform
title: 데이터 액세스 개발자 가이드
topic: developer guide
description: 데이터 액세스 API는 사용자에게 Experience Platform 내에서 인제스트된 데이터 집합의 검색 기능과 액세스 가능성에 초점을 맞춘 RESTful 인터페이스를 제공하여 Adobe Experience Platform을 지원합니다.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 5%

---


# 데이터 액세스 개발자 가이드

데이터 액세스 API는 데이터 세트 내에서 인제스트된 데이터 세트의 검색 기능과 액세스 가능성에 초점을 맞춘 RESTful 인터페이스를 사용자에게 제공하여 Adobe Experience Platform을 지원합니다 [!DNL Experience Platform].

![Experience Platform의 데이터 액세스](images/Data_Access_Experience_Platform.png)

## API 사양 참조

Swagger API 참조 설명서는 [여기에서 찾을 수 있습니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## 용어

이 문서 전체에서 일반적으로 사용되는 용어의 설명입니다.

| 용어 | 설명 |
| ----- | ------------ |
| 데이터 집합 | 스키마 및 필드를 포함하는 데이터 컬렉션입니다. |
| 일괄 처리 | 일정 기간 동안 수집되어 단일 단위로 함께 처리된 데이터 집합. |

## 일괄 처리 내의 파일 목록 검색

데이터 액세스 API는 배치 식별자(batchID)를 사용하여 특정 배치에 속하는 파일 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/files
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 지정된 일괄 처리의 ID. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

이 배열은 지정된 일괄 처리 내의 모든 파일 목록을 포함합니다. `"data"` 반환된 각 파일의 고유한 ID(`{FILE_ID}`)는 `"dataSetFileId"` 필드 내에 들어 있습니다. 그런 다음 이 고유 ID를 사용하여 파일에 액세스하거나 다운로드할 수 있습니다.

| 속성 | 설명 |
| -------- | ----------- |
| `data.dataSetFileId` | 지정된 일괄 처리에 있는 각 파일의 파일 ID. |
| `data._links.self.href` | 파일에 액세스할 수 있는 URL입니다. |

## 일괄 처리 내에서 파일 액세스 및 다운로드

데이터 액세스 API는 파일 식별자(`{FILE_ID}`)를 사용하여 파일 이름, 크기(바이트), 다운로드 링크 등 파일의 특정 세부 정보에 액세스할 수 있습니다.

응답에는 데이터 배열이 포함됩니다. ID로 가리키는 파일이 개별 파일인지 디렉토리인지에 따라, 반환된 데이터 배열에 해당 디렉토리에 속하는 파일 목록이나 단일 항목이 포함될 수 있습니다. 각 파일 요소에는 파일의 세부 사항이 포함됩니다.

**API 형식**

```http
GET /files/{FILE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 액세스할 파일의 `"dataSetFileId"`ID와 같습니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**단일 파일 응답**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `data.name` | 파일 이름(예: profiles.csv). |
| `data.length` | 파일의 크기(바이트)입니다. |
| `data._links.self.href` | 파일을 다운로드할 URL입니다. |

**디렉토리 응답**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

디렉토리가 반환되면 디렉토리 내에 있는 모든 파일의 배열이 포함됩니다.

| 속성 | 설명 |
| -------- | ----------- |
| `data.name` | 파일 이름(예: profiles.csv). |
| `data._links.self.href` | 파일을 다운로드할 URL입니다. |

## 파일 내용 액세스

API를 사용하여 파일의 컨텐츠에 액세스할 수도 있습니다. [!DNL Data Access] 그런 다음 컨텐츠를 외부 소스로 다운로드하는 데 사용할 수 있습니다.

**API 형식**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_NAME}` | 액세스하려는 파일의 이름입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 데이터 집합 내의 파일 ID입니다. |
| `{FILE_NAME}` | 파일의 전체 이름(예: profiles.csv). |

**응답**

`Contents of the file`

## 추가 코드 샘플

추가 샘플은 [데이터 액세스 자습서를 참조하십시오](tutorials/dataset-data.md).

## 데이터 수집 이벤트 가입

[!DNL Platform] 은 [Adobe 개발자 콘솔을 통해 구독에 특정 고부가가치 이벤트를 사용할 수 있도록 합니다](https://www.adobe.com/go/devs_console_ui). 예를 들어 데이터 수집 이벤트에 가입하여 예상되는 지연 및 실패에 대한 알림을 받을 수 있습니다. 자세한 내용은 데이터 수집 알림 [가입에](../ingestion/quality/subscribe-events.md) 대한 자습서를 참조하십시오.