---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;python sdk;spark sdk;데이터 액세스 api;내보내기;내보내기
solution: Experience Platform
title: Data Access API 안내서
description: Data Access API는 개발자에게 Experience Platform 내에서 수집된 데이터 세트의 검색 가능성과 액세스 가능성에 초점을 맞춘 RESTful 인터페이스를 제공하여 Adobe Experience Platform을 지원합니다.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 5%

---

# 데이터 액세스 API 안내서

Data Access API는 내에서 수집된 데이터 세트의 검색 가능성과 액세스 가능성에 중점을 둔 RESTful 인터페이스를 사용자에게 제공하여 Adobe Experience Platform을 지원합니다 [!DNL Experience Platform].

![Experience Platform 데이터 액세스](images/Data_Access_Experience_Platform.png)

## API 사양 참조

Swagger API 참조 설명서를 찾을 수 있습니다 [여기](https://www.adobe.io/experience-platform-apis/references/data-access/).

## 용어

이 문서 전체에서 자주 사용되는 일부 용어에 대한 설명입니다.

| 용어 | 설명 |
| ----- | ------------ |
| 데이터 세트 | 스키마 및 필드를 포함하는 데이터 모음입니다. |
| 일괄 처리 | 일정 기간 동안 수집되어 단일 단위로 함께 처리되는 데이터 세트입니다. |

## 배치 내에서 파일 목록 검색

배치 식별자(batchID)를 사용하여 데이터 액세스 API는 해당 특정 배치에 속하는 파일 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/files
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 지정된 일괄 처리의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

다음 `"data"` 배열에는 지정된 일괄 처리 내의 모든 파일 목록이 포함됩니다. 반환된 각 파일의 고유 ID는 입니다(`{FILE_ID}`)에 포함되어 있습니다. `"dataSetFileId"` 필드. 그런 다음 이 고유 ID를 사용하여 파일에 액세스하거나 다운로드할 수 있습니다.

| 속성 | 설명 |
| -------- | ----------- |
| `data.dataSetFileId` | 지정된 배치에 있는 각 파일의 파일 ID입니다. |
| `data._links.self.href` | 파일에 액세스할 수 있는 URL입니다. |

## 배치 내에서 파일 액세스 및 다운로드

파일 식별자 사용(`{FILE_ID}`) 데이터 액세스 API를 사용하면 이름, 크기(바이트) 및 다운로드 링크를 포함하여 파일의 특정 세부 정보에 액세스할 수 있습니다.

응답에는 데이터 배열이 포함됩니다. ID가 가리키는 파일이 개별 파일인지 디렉터리인지에 따라 반환되는 데이터 배열에는 단일 항목이나 해당 디렉터리에 속하는 파일 목록이 포함될 수 있습니다. 각 파일 요소에는 파일의 세부 정보가 포함됩니다.

**API 형식**

```http
GET /files/{FILE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 다음과 같음 `"dataSetFileId"`: 액세스할 파일의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `data.length` | 파일 크기(바이트)입니다. |
| `data._links.self.href` | 파일을 다운로드할 URL입니다. |

**디렉터리 응답**

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

디렉토리가 반환되면 디렉토리 내의 모든 파일 배열이 포함됩니다.

| 속성 | 설명 |
| -------- | ----------- |
| `data.name` | 파일 이름(예: profiles.csv). |
| `data._links.self.href` | 파일을 다운로드할 URL입니다. |

## 파일의 내용에 액세스

다음 [!DNL Data Access] API를 사용하여 파일의 내용에 액세스할 수도 있습니다. 그런 다음 콘텐츠를 외부 소스로 다운로드하는 데 사용할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 데이터 세트 내 파일의 ID입니다. |
| `{FILE_NAME}` | 파일의 전체 이름(예: profiles.csv). |

**응답**

`Contents of the file`

## 추가 코드 샘플

추가 샘플은 다음을 참조하십시오. [데이터 액세스 자습서](tutorials/dataset-data.md).

## 데이터 수집 이벤트 구독

[!DNL Platform] 을(를) 통해 특정 고부가가치 이벤트를 구독에 사용할 수 있도록 함 [Adobe Developer 콘솔](https://www.adobe.com/go/devs_console_ui). 예를 들어 데이터 수집 이벤트에 가입하여 잠재적인 지연 및 실패를 알릴 수 있습니다. 다음 튜토리얼 참조: [데이터 수집 알림 구독](../ingestion/quality/subscribe-events.md) 추가 정보.
