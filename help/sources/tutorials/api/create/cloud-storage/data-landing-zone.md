---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Flow Service API를 사용하여 데이터 랜딩 영역을 Adobe Experience Platform에 연결
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 데이터 랜딩 영역에 연결하는 방법을 알아봅니다.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 4%

---

# Connect [!DNL Data Landing Zone] Flow Service API를 사용하여 Adobe Experience Platform으로 이동

>[!IMPORTANT]
>
>이 페이지는 [!DNL Data Landing Zone] *소스* Experience Platform의 커넥터. 연결 방법에 대한 자세한 내용 [!DNL Data Landing Zone] *대상* 커넥터 [[!DNL Data Landing Zone] 대상 설명서 페이지](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 는 Adobe Experience Platform으로 파일을 가져올 수 있는 안전한 클라우드 기반 파일 저장 기능입니다. 데이터는 [!DNL Data Landing Zone] 7일 후

이 튜토리얼에서는 다음을 만드는 방법에 대한 단계를 설명합니다 [!DNL Data Landing Zone] 소스 연결 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 이 자습서에서는 을 검색하는 방법에 대한 지침도 제공합니다 [!DNL Data Landing Zone]를 업데이트하여 자격 증명을 보고 새로 고칠 수 있습니다.

## 시작하기

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 성공적으로 만들기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Data Landing Zone] 소스 연결 [!DNL Flow Service] API.

또한 이 자습서에서는 안내서를 읽어야 합니다 [플랫폼 API 시작](../../../../../landing/api-guide.md) platform API를 인증하고 설명서에서 제공된 예제 호출을 해석하는 방법을 알아봅니다.

## 사용 가능한 랜딩 영역 검색

API를 사용하여 액세스하는 첫 번째 단계 [!DNL Data Landing Zone] 는 `/landingzone` 의 끝점 [!DNL Connectors] 을 제공하는 동안 API `type=user_drop_zone` 을 요청 헤더의 일부로,

**API 형식**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| 헤더 | 설명 |
| --- | --- |
| `user_drop_zone` | 다음 `user_drop_zone` 유형을 사용하면 API에서 랜딩 영역 컨테이너를 사용 가능한 다른 유형의 컨테이너와 구별할 수 있습니다. |

**요청**

다음 요청은 기존 랜딩 영역을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**응답**

다음 응답은 랜딩 영역에 대한 정보를 반환하며, 여기에 해당하는 정보를 포함합니다 `containerName` 및 `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | 검색한 랜딩 영역의 이름입니다. |
| `containerTTL` | 랜딩 영역 내의 데이터에 적용되는 만료 시간(일)입니다. 주어진 랜딩 영역 내의 모든 항목은 7일 후 삭제됩니다. |

## 검색 [!DNL Data Landing Zone] 자격 증명

에 대한 자격 증명을 검색하려면 [!DNL Data Landing Zone]에 대해 GET 요청을 수행합니다. `/credentials` 의 끝점 [!DNL Connectors] API.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**요청**

다음 요청 예는 기존 랜딩 영역에 대한 자격 증명을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**응답**

다음 응답에서는 현재 사용자를 포함하여 랜딩 영역에 대한 자격 증명 정보를 반환합니다 `SASToken` 및 `SASUri`뿐만 아니라 `storageAccountName` 랜딩 영역 컨테이너에 해당합니다.

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


## 업데이트 [!DNL Data Landing Zone] 자격 증명

을(를) 업데이트할 수 있습니다 `SASToken` 에 POST 요청을 수행하여 `/credentials` 의 끝점 [!DNL Connectors] API.

**API 형식**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 헤더 | 설명 |
| --- | --- |
| `user_drop_zone` | 다음 `user_drop_zone` 유형을 사용하면 API에서 랜딩 영역 컨테이너를 사용 가능한 다른 유형의 컨테이너와 구별할 수 있습니다. |
| `refresh` | 다음 `refresh` 작업을 통해 랜딩 영역 자격 증명을 재설정하고 자동으로 새 사용자를 생성할 수 있습니다 `SASToken`. |

**요청**

다음 요청은 랜딩 영역 자격 증명을 업데이트합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**응답**

다음 응답은 `SASToken` 및 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 랜딩 영역 파일 구조 및 콘텐츠 탐색

에 GET 요청을 수행하여 랜딩 영역의 파일 구조 및 콘텐츠를 탐색할 수 있습니다 `connectionSpecs` 의 끝점 [!DNL Flow Service] API.

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 에 해당하는 연결 사양 ID [!DNL Data Landing Zone]. 이 고정 ID는 다음과 같습니다. `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 쿼리된 디렉터리 내에 있는 파일 및 폴더의 배열을 반환합니다. 다음 사항을 주목하십시오. `path` 다음 단계에서 제공해야 하므로 업로드할 파일의 구조를 검사해야 합니다.

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
| `{CONNECTION_SPEC_ID}` | 에 해당하는 연결 사양 ID [!DNL Data Landing Zone]. 이 고정 ID는 다음과 같습니다. `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 파일 이름 및 데이터 유형을 포함하여 쿼리된 파일의 구조를 반환합니다.

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

### 사용 `determineProperties` 의 파일 속성 정보를 자동으로 검색하려면 [!DNL Data Landing Zone]

를 사용할 수 있습니다 `determineProperties` 매개 변수를 사용하여 파일 내용의 속성 정보를 자동으로 검색합니다. [!DNL Data Landing Zone] GET을 호출하여 소스의 내용 및 구조를 탐색할 때

#### `determineProperties` 사용 사례

다음 표에서는 를 사용할 때 발생할 수 있는 다양한 시나리오에 대해 설명합니다 `determineProperties` 쿼리 매개 변수 또는 파일에 대한 정보를 수동으로 제공합니다.

| `determineProperties` | `queryParams` | 응답 |
| --- | --- | --- |
| True | 해당 없음 | If `determineProperties` 이 쿼리 매개 변수로 제공되면 파일 속성 감지가 발생하고 응답이 새 `properties` 파일 형식, 압축 유형 및 열 구분 기호에 대한 정보가 포함된 키입니다. |
| 해당 없음 | True | 파일 형식, 압축 유형 및 열 구분 기호의 값이 `queryParams`를 입력하면 스키마를 생성하는 데 사용되며 동일한 속성이 응답의 일부로 반환됩니다. |
| True | True | 두 옵션이 동시에 수행되면 오류가 반환됩니다. |
| N/A | N/A | 두 옵션이 모두 제공되지 않으면 응답에 대한 속성을 가져올 방법이 없으므로 오류가 반환됩니다. |

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 매개 변수 | 설명 | 예 |
| --- | --- | --- |
| `determineProperties` | 이 쿼리 매개 변수는 [!DNL Flow Service] 파일 형식, 압축 유형 및 열 구분 기호에 대한 정보를 포함하여 파일의 속성과 관련된 정보를 감지하는 API입니다. | `true` |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 파일 이름 및 데이터 유형을 비롯하여 쿼리된 파일의 구조를 반환합니다. `properties` 키, `fileType`, `compressionType`, 및 `columnDelimiter`.

+++여기 클릭

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| 속성 | 설명 |
| --- | --- |
| `properties.fileType` | 쿼리된 파일의 해당 파일 유형입니다. 지원되는 파일 유형은 다음과 같습니다. `delimited`, `json`, 및 `parquet`. |
| `properties.compressionType` | 쿼리된 파일에 사용된 해당 압축 유형입니다. 지원되는 압축 유형은 다음과 같습니다. <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 쿼리된 파일에 사용되는 해당 열 구분 기호입니다. 단일 문자 값은 허용 열 구분 기호입니다. 기본값은 쉼표입니다 `(,)`. |


## 소스 연결 만들기

소스 연결은 데이터를 수집하는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 흐름을 만드는 데 필요한 데이터 소스, 데이터 형식 및 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 IMS 조직에 따라 다릅니다.

소스 연결을 만들려면 `/sourceConnections` 의 끝점 [!DNL Flow Service] API.


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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | 사용자 이름 [!DNL Data Landing Zone] 소스 연결. |
| `data.format` | Platform으로 가져올 데이터의 형식입니다. |
| `params.path` | Platform으로 가져올 파일의 경로입니다. |
| `connectionSpec.id` | 에 해당하는 연결 사양 ID [!DNL Data Landing Zone]. 이 고정 ID는 다음과 같습니다. `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 데이터 흐름을 만들려면 다음 자습서에서 필요합니다.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Data Landing Zone] 자격 증명과 해당 파일 구조를 탐색하여 Platform으로 가져올 파일을 찾고, Platform으로 데이터를 가져오기 위한 소스 연결을 만들었습니다. 이제 다음 자습서를 진행하여 다음 방법을 배울 수 있습니다 [데이터 흐름을 만들어 [!DNL Flow Service] API](../../collect/cloud-storage.md).
