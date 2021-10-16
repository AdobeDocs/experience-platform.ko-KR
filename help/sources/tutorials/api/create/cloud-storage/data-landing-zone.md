---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Flow Service API를 사용하여 데이터 랜딩 영역을 Adobe Experience Platform에 연결
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 데이터 랜딩 영역에 연결하는 방법을 알아봅니다.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 3%

---

# Flow Service API를 사용하여 [!DNL Data Landing Zone]을 Adobe Experience Platform에 연결합니다

[!DNL Data Landing Zone] 는 Adobe Experience Platform에 프로비저닝된 임시 파일 저장소를 위한 클라우드 기반 데이터 저장소 기능입니다. 데이터는 7일 후 [!DNL Data Landing Zone]에서 자동으로 삭제됩니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Data Landing Zone] 소스 연결을 만드는 방법에 대한 단계를 안내합니다. 이 자습서에서는 자격 증명을 보고 새로 고치는 방법과 [!DNL Data Landing Zone] 을 검색하는 방법에 대한 지침도 제공합니다.

## 시작하기

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Data Landing Zone] 소스 연결을 성공적으로 만들기 위해 알고 있어야 하는 추가 정보를 제공합니다.

또한 이 자습서를 사용하려면 [플랫폼 API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 읽어 플랫폼 API를 인증하고 설명서에 제공된 예제 호출을 해석하는 방법을 학습해야 합니다.

## 사용 가능한 랜딩 영역 검색

API를 사용하여 [!DNL Data Landing Zone]에 액세스하는 첫 번째 단계는 요청 헤더의 일부로 `type=user_drop_zone` 를 제공하면서 [!DNL Connectors] API의 `/landingzone` 종단점에 GET 요청을 수행하는 것입니다.

**API 형식**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| 헤더 | 설명 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone` 유형을 사용하면 API에서 랜딩 영역 컨테이너를 사용 가능한 다른 유형의 컨테이너와 구별할 수 있습니다. |

**요청**

다음 요청은 기존 랜딩 영역을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**응답**

다음 응답은 해당 `containerName` 및 `containerTTL`을 포함하는 랜딩 영역에 대한 정보를 반환합니다.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | 검색한 랜딩 영역의 이름입니다. |
| `containerTTL` | 랜딩 영역 내의 데이터에 적용되는 Time-to-Live 설정입니다. 주어진 랜딩 영역 내의 모든 항목은 7일 후 삭제됩니다. |

## [!DNL Data Landing Zone] 자격 증명 검색

[!DNL Data Landing Zone]에 대한 자격 증명을 검색하려면 [!DNL Connectors] API의 `/credentials` 종단점에 GET 요청을 하십시오.

**API 형식**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**요청**

다음 요청 예는 기존 랜딩 영역에 대한 자격 증명을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**응답**

다음 응답은 랜딩 영역에 대한 자격 증명 정보와 현재 `SASToken` 및 `SASUri` 및 랜딩 영역 컨테이너에 해당하는 `storageAccountName` 를 반환합니다.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | 랜딩 영역의 이름입니다. |
| `SASToken` | 랜딩 영역에 대한 공유 액세스 서명 토큰. 이 문자열에는 요청을 승인하는 데 필요한 모든 정보가 들어 있습니다. |
| `SASUri` | 랜딩 영역에 대한 공유 액세스 서명 URI입니다. 이 문자열은 인증 대상 랜딩 영역에 대한 URI와 해당 SAS 토큰의 조합입니다. |


## [!DNL Data Landing Zone] 자격 증명 업데이트

[!DNL Connectors] API의 `/credentials` 종단점에 POST 요청을 하여 `SASToken`을 업데이트할 수 있습니다.

**API 형식**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 헤더 | 설명 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone` 유형을 사용하면 API에서 랜딩 영역 컨테이너를 사용 가능한 다른 유형의 컨테이너와 구별할 수 있습니다. |
| `refresh` | `refresh` 작업을 통해 랜딩 영역 자격 증명을 재설정하고 새 `SASToken`을(를) 자동으로 생성할 수 있습니다. |

**요청**

다음 요청은 랜딩 영역 자격 증명을 업데이트합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**응답**

다음 응답은 `SASToken` 및 `SASUri`에 대해 업데이트된 값을 반환합니다.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 랜딩 영역 파일 구조 및 콘텐츠 탐색

[!DNL Flow Service] API의 `connectionSpecs` 종단점에 GET을 요청하여 랜딩 영역의 파일 구조 및 콘텐츠를 탐색할 수 있습니다.

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | [!DNL Data Landing Zone]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `26f526f2-58f4-4712-961d-e41bf1ccc0e8` |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 쿼리된 디렉터리 내에 있는 파일 및 폴더의 배열을 반환합니다. 다음 단계에서 해당 구조를 검사하기 위해 파일을 제공해야 하므로 업로드할 파일의 `path` 속성을 주목하십시오.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## 랜딩 영역 파일 구조 및 콘텐츠 미리 보기

랜딩 영역에 있는 파일의 구조를 검사하려면 파일의 경로 및 유형을 쿼리 매개 변수로 제공하면서 GET 요청을 수행합니다.

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 매개 변수 | 설명 | 예 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | [!DNL Data Landing Zone]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `26f526f2-58f4-4712-961d-e41bf1ccc0e8` |
| `{OBJECT_TYPE}` | 액세스할 객체의 유형입니다. | `file` |
| `{OBJECT}` | 액세스할 개체의 경로와 이름입니다. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 파일의 유형입니다. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 파일 미리 보기가 지원되는지 여부를 정의하는 부울 값입니다. | </ul><li>`true`</li><li>`false`</li></ul> |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 테이블 이름 및 데이터 유형을 포함하여 쿼리된 파일의 구조를 반환합니다.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

## 소스 연결 만들기

소스 연결은 데이터를 수집하는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 흐름을 만드는 데 필요한 데이터 소스, 데이터 형식 및 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 IMS 조직에 따라 다릅니다.

소스 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 종단점에 대해 POST 요청을 수행하십시오.


**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | [!DNL Data Landing Zone] 소스 연결의 이름입니다. |
| `data.format` | Platform으로 가져올 데이터의 형식입니다. |
| `params.path` | Platform으로 가져올 파일의 경로입니다. |
| `connectionSpec.id` | [!DNL Data Landing Zone]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `26f526f2-58f4-4712-961d-e41bf1ccc0e8` |

**응답**

성공적으로 응답하면 새로 만든 소스 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 데이터 흐름을 만들려면 다음 자습서에서 필요합니다.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Data Landing Zone] 자격 증명을 검색하고, 해당 파일 구조를 탐색하여 Platform으로 가져올 파일을 찾고, 데이터를 Platform으로 가져오기 시작할 소스 연결을 만들었습니다. 이제 다음 자습서로 진행하여 [데이터 흐름을 만들어 [!DNL Flow Service] API](../../collect/cloud-storage.md)를 사용하여 클라우드 스토리지 데이터를 플랫폼으로 가져오는 방법을 알아봅니다.
