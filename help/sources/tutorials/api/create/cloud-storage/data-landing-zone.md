---
title: 흐름 서비스 API를 사용하여 데이터 랜딩 영역을 Adobe Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 데이터 랜딩 영역에 연결하는 방법을 알아봅니다.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 527e62e5fb90bc32ef3788f261e0a24b680f29c0
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 3%

---

# 흐름 서비스 API를 사용하여 [!DNL Data Landing Zone]을(를) Adobe Experience Platform에 연결

>[!IMPORTANT]
>
>이 페이지는 Experience Platform의 [!DNL Data Landing Zone] *source* 커넥터에 한정됩니다. [!DNL Data Landing Zone] *대상* 커넥터에 연결하는 방법에 대한 자세한 내용은 [[!DNL Data Landing Zone] 대상 설명서 페이지](/help/destinations/catalog/cloud-storage/data-landing-zone.md)를 참조하세요.

[!DNL Data Landing Zone]은(는) Adobe Experience Platform으로 파일을 가져올 수 있는 안전한 클라우드 기반 파일 저장소 기능입니다. 데이터는 7일 후 [!DNL Data Landing Zone]에서 자동으로 삭제됩니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Data Landing Zone] 소스 연결을 만드는 방법에 대한 단계를 안내합니다. 이 자습서에서는 [!DNL Data Landing Zone]을(를) 검색하고 자격 증명을 보고 새로 고치는 방법에 대한 지침도 제공합니다.

## 시작하기

이 안내서를 사용하려면 다음 Experience Platform 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

또한 이 자습서에서는 [Platform API 시작하기](../../../../../landing/api-guide.md)에 대한 안내서를 읽고 Platform API를 인증하고 설명서에 제공된 예제 호출을 해석하는 방법을 알아봐야 합니다.

다음 절에서는 [!DNL Flow Service] API를 사용하여 [!DNL Data Landing Zone] 원본 연결을 만들기 위해 알아야 할 추가 정보를 제공합니다.

## 사용 가능한 랜딩 영역 검색

API를 사용하여 [!DNL Data Landing Zone]에 액세스하는 첫 번째 단계는 `type=user_drop_zone`을(를) 요청 헤더의 일부로 제공하는 동안 [!DNL Connectors] API의 `/landingzone` 끝점에 GET 요청을 하는 것입니다.

**API 형식**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| 헤더 | 설명 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone` 형식을 사용하면 API에서 랜딩 영역 컨테이너와 사용 가능한 다른 형식의 컨테이너를 구별할 수 있습니다. |

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

공급자에 따라 성공적인 요청은 다음을 반환합니다.

>[!BEGINTABS]

>[!TAB Azure의 응답]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | 검색한 랜딩 영역의 이름입니다. |
| `containerTTL` | 랜딩 영역 내의 데이터에 적용되는 만료 시간(일)입니다. 지정된 랜딩 영역 내의 모든 항목이 7일 후에 삭제됩니다. |


>[!TAB AWS의 응답]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## [!DNL Data Landing Zone] 자격 증명 검색

[!DNL Data Landing Zone]에 대한 자격 증명을 검색하려면 [!DNL Connectors] API의 `/credentials` 끝점에 대한 GET 요청을 만드십시오.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**요청**

다음 요청 예제는 기존 랜딩 영역에 대한 자격 증명을 검색합니다.

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

공급자에 따라 성공적인 요청은 다음을 반환합니다.

>[!BEGINTABS]

>[!TAB Azure의 응답]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | [!DNL Data Landing Zone]의 이름입니다. |
| `SASToken` | [!DNL Data Landing Zone]에 대한 공유 액세스 서명 토큰입니다. 이 문자열에는 요청을 승인하는 데 필요한 모든 정보가 포함되어 있습니다. |
| `storageAccountName` | 저장소 계정의 이름입니다. |
| `SASUri` | [!DNL Data Landing Zone]에 대한 공유 액세스 서명 URI입니다. 이 문자열은 인증 중인 [!DNL Data Landing Zone]에 대한 URI와 해당 SAS 토큰의 조합입니다. |
| `expiryDate` | SAS 토큰이 만료되는 날짜. 응용 프로그램에서 토큰을 사용하여 [!DNL Data Landing Zone]에 데이터를 업로드하려면 만료 날짜 전에 토큰을 새로 고쳐야 합니다. 명시된 만료 날짜 이전에 토큰을 수동으로 새로 고치지 않는 경우, GET 자격 증명 호출이 수행될 때 자동으로 새로 고침되고 새 토큰을 제공합니다. |

>[!TAB AWS의 응답]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| 속성 | 설명 |
| --- | --- |
| `credentials.clientId` | AWS에서 [!DNL Data Landing Zone]의 클라이언트 ID입니다. |
| `credentials.awsAccessKeyId` | AWS [!DNL Data Landing Zone]의 액세스 키 ID입니다. |
| `credentials.awsSecretAccessKey` | AWS에서 [!DNL Data Landing Zone]의 비밀 액세스 키입니다. |
| `credentials.awsSessionToken` | AWS 세션 토큰. |
| `dlzPath.bucketName` | AWS 버킷의 이름입니다. |
| `dlzPath.dlzFolder` | 액세스 중인 [!DNL Data Landing Zone] 폴더입니다. |
| `dlzProvider` | 사용 중인 [!DNL Data Landing Zone] 공급자입니다. Amazon의 경우 [!DNL Amazon S3]이(가) 됩니다. |
| `expiryTime` | 만료 시간(unix 시간)입니다. |

>[!ENDTABS]

### API를 사용하여 필수 필드 검색

토큰을 생성한 후에는 아래 요청 예제를 사용하여 필수 필드를 프로그래밍 방식으로 검색할 수 있습니다.

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## [!DNL Data Landing Zone] 자격 증명 업데이트

[!DNL Connectors] API의 `/credentials` 끝점에 POST 요청을 하여 `SASToken`을(를) 업데이트할 수 있습니다.

**API 형식**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 헤더 | 설명 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone` 형식을 사용하면 API에서 랜딩 영역 컨테이너와 사용 가능한 다른 형식의 컨테이너를 구별할 수 있습니다. |
| `refresh` | `refresh` 동작을 사용하면 랜딩 영역 자격 증명을 재설정하고 새 `SASToken`을(를) 자동으로 생성할 수 있습니다. |

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

다음 응답은 `SASToken` 및 `SASUri`에 대해 업데이트된 값을 반환합니다.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## 랜딩 영역 파일 구조 및 콘텐츠 탐색

[!DNL Flow Service] API의 `connectionSpecs` 끝점에 대한 GET 요청을 통해 랜딩 영역의 파일 구조 및 콘텐츠를 살펴볼 수 있습니다.

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 매개변수 | 설명 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | [!DNL Data Landing Zone]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `26f526f2-58f4-4712-961d-e41bf1ccc0e8`입니다. |

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

성공한 응답은 쿼리된 디렉터리 내에서 발견된 파일 및 폴더 배열을 반환합니다. 업로드할 파일의 `path` 속성을 기록해 두십시오. 파일의 구조를 검사하려면 다음 단계에서 해당 속성을 제공해야 합니다.

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

## 랜딩 영역 파일 구조 및 콘텐츠 미리보기

랜딩 영역의 파일 구조를 검사하려면 파일의 경로와 유형을 쿼리 매개 변수로 제공하면서 GET 요청을 수행합니다.

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | [!DNL Data Landing Zone]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `26f526f2-58f4-4712-961d-e41bf1ccc0e8`입니다. |
| `{OBJECT_TYPE}` | 액세스하려는 객체의 유형입니다. | `file` |
| `{OBJECT}` | 액세스하려는 객체의 경로 및 이름입니다. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 파일의 유형입니다. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 파일 미리 보기가 지원되는지 여부를 정의하는 부울 값. | </ul><li>`true`</li><li>`false`</li></ul> |

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

성공한 응답은 파일 이름 및 데이터 유형을 포함하여 쿼리된 파일의 구조를 반환합니다.

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

### `determineProperties`을(를) 사용하여 [!DNL Data Landing Zone]의 파일 속성 정보를 자동으로 검색

GET 호출을 통해 소스의 내용과 구조를 탐색할 때 `determineProperties` 매개 변수를 사용하여 [!DNL Data Landing Zone]의 파일 내용에 대한 속성 정보를 자동으로 검색할 수 있습니다.

#### `determineProperties`개의 사용 사례

다음 표에서는 `determineProperties` 쿼리 매개 변수를 사용하거나 파일에 대한 정보를 수동으로 제공할 때 발생할 수 있는 다양한 시나리오를 간략하게 설명합니다.

| `determineProperties` | `queryParams` | 응답 |
| --- | --- | --- |
| True | N/A | `determineProperties`이(가) 쿼리 매개 변수로 제공되면 파일 속성 검색이 발생하고 응답이 파일 형식, 압축 형식 및 열 구분 기호에 대한 정보를 포함하는 새 `properties` 키를 반환합니다. |
| N/A | True | 파일 형식, 압축 형식 및 열 구분 기호의 값이 `queryParams`의 일부로 수동으로 제공되는 경우 해당 값을 사용하여 스키마를 생성하고 동일한 속성이 응답의 일부로 반환됩니다. |
| True | True | 두 옵션이 동시에 수행되면 오류가 반환됩니다. |
| N/A | N/A | 두 옵션이 모두 제공되지 않으면 응답에 대한 속성을 가져올 수 없으므로 오류가 반환됩니다. |

**API 형식**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `determineProperties` | 이 쿼리 매개 변수를 사용하면 [!DNL Flow Service] API에서 파일 형식, 압축 형식 및 열 구분 기호에 대한 정보를 포함하여 파일의 속성에 대한 정보를 검색할 수 있습니다. | `true` |

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

성공한 응답은 파일 이름 및 데이터 형식을 포함한 쿼리된 파일의 구조와 `fileType`, `compressionType` 및 `columnDelimiter`에 대한 정보가 포함된 `properties` 키를 반환합니다.

+++내 클릭

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
| `properties.fileType` | 쿼리된 파일의 해당 파일 유형입니다. 지원되는 파일 형식은 `delimited`, `json` 및 `parquet`입니다. |
| `properties.compressionType` | 쿼리된 파일에 사용된 해당 압축 유형입니다. 지원되는 압축 유형은 다음과 같습니다. <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 쿼리된 파일에 사용된 해당 열 구분 기호입니다. 모든 단일 문자 값은 허용되는 열 구분 기호입니다. 기본값은 쉼표 `(,)`입니다. |


## 소스 연결 만들기

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 소스, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

소스 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 끝점에 대한 POST 요청을 만듭니다.


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
| `name` | [!DNL Data Landing Zone] 원본 연결의 이름입니다. |
| `data.format` | 플랫폼으로 가져올 데이터의 형식입니다. |
| `params.path` | 플랫폼으로 가져올 파일의 경로입니다. |
| `connectionSpec.id` | [!DNL Data Landing Zone]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `26f526f2-58f4-4712-961d-e41bf1ccc0e8`입니다. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 데이터 흐름을 만들려면 다음 자습서에서 이 ID가 필요합니다.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Data Landing Zone] 자격 증명을 검색하고, 플랫폼에 가져올 파일을 찾기 위해 해당 파일 구조를 탐색하고, 데이터를 플랫폼으로 가져오기 시작할 소스 연결을 만들었습니다. 이제 다음 자습서로 이동하여 [데이터 흐름을 만들어  [!DNL Flow Service] API](../../collect/cloud-storage.md)를 사용하여 클라우드 저장소 데이터를 플랫폼으로 가져오는 방법을 배울 수 있습니다.
