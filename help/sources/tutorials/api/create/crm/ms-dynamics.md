---
title: 흐름 서비스 API를 사용하여 Microsoft Dynamics 기본 연결 만들기
description: 흐름 서비스 API를 사용하여 Microsoft Dynamics 계정에 플랫폼을 연결하는 방법을 알아봅니다.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 4e119056c0ab89cfc79eeb46e6f870c89356dc7d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 3%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Microsoft Dynamics]을(를) Experience Platform에 연결

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Microsoft Dynamics] 소스를 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 Dynamics 계정에 플랫폼을 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Dynamics]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics] 인스턴스의 서비스 URL. |
| `username` | [!DNL Dynamics] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Dynamics] 계정의 암호입니다. |

>[!TAB 서비스 주체 및 키 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID. 서비스 주체 및 키 기반 인증을 사용할 때 이 ID가 필요합니다. |
| `servicePrincipalKey` | 서비스 주체 비밀 키. 서비스 주체 및 키 기반 인증을 사용할 때 이 자격 증명이 필요합니다. |

>[!ENDTABS]

시작하기에 대한 자세한 내용은 [이 [!DNL Dynamics] 문서](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)를 참조하세요.

## 기본 연결 만들기

>[!TIP]
>
>만든 후에는 [!DNL Dynamics] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Dynamics] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL Dynamics] 기본 연결을 만들려면 연결의 `serviceUri`, `username` 및 `password`에 대한 값을 제공하는 동안 [!DNL Flow Service] API에 대한 POST 요청을 만듭니다.

**요청**

다음 요청은 기본 인증을 사용하여 [!DNL Dynamics] 소스에 대한 기본 연결을 만듭니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.serviceUri` | [!DNL Dynamics] 인스턴스와 연결된 서비스 URI입니다. |
| `auth.params.username` | [!DNL Dynamics] 계정과 연결된 사용자 이름. |
| `auth.params.password` | [!DNL Dynamics] 계정과 연결된 암호입니다. |
| `connectionSpec.id` | [!DNL Dynamics] 연결 사양 ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다.

+++응답 예를 보려면 선택

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 서비스 사용자 키 기반 인증]

서비스 사용자 키 기반 인증을 사용하여 [!DNL Dynamics] 기본 연결을 만들려면 연결의 `serviceUri`, `servicePrincipalId` 및 `servicePrincipalKey`에 대한 값을 제공하는 동안 [!DNL Flow Service] API에 POST 요청을 수행합니다.

**요청**

다음 요청은 기본 서비스 사용자 키 기반 인증을 사용하여 [!DNL Dynamics] 소스에 대한 기본 연결을 만듭니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.serviceUri` | [!DNL Dynamics] 인스턴스와 연결된 서비스 URI입니다. |
| `auth.params.servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID. 서비스 주체 및 키 기반 인증을 사용할 때 이 ID가 필요합니다. |
| `auth.params.servicePrincipalKey` | 서비스 주체 비밀 키. 서비스 주체 및 키 기반 인증을 사용할 때 이 자격 증명이 필요합니다. |
| `connectionSpec.id` | [!DNL Dynamics] 연결 사양 ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결이 반환됩니다.

+++응답 예를 보려면 선택

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## 데이터 테이블 탐색

[!DNL Dynamics] 데이터 테이블을 탐색하려면 `/connections/{BASE_CONNECTION_ID}/explore` 끝점에 GET 요청을 만들고 기본 연결 ID를 쿼리 매개 변수의 일부로 제공합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 기본 연결의 ID입니다. 이 ID를 사용하여 소스의 콘텐츠와 구조를 살펴보십시오. |

**요청**

다음 요청은 기본 연결 ID가 `dd668808-25da-493f-8782-f3433b976d1e`인 [!DNL Dynamics] 소스에 대해 사용 가능한 테이블 및 보기 목록을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공한 응답은 루트 수준에서 [!DNL Dynamics]개의 테이블 및 뷰 디렉터리를 반환합니다.

+++응답 예를 보려면 선택

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### 기본 키를 사용하여 데이터 탐색 최적화

>[!NOTE]
>
>최적화에 대한 기본 키 접근 방식을 사용할 때는 비조회 속성만 사용할 수 있습니다.

`primaryKey`을(를) 쿼리 매개 변수의 일부로 제공하여 탐색 쿼리를 최적화할 수 있습니다. `primaryKey`을(를) 쿼리 매개 변수로 포함할 때 [!DNL Dynamics] 테이블의 기본 키를 지정해야 합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 기본 연결의 ID입니다. 이 ID를 사용하여 소스의 콘텐츠와 구조를 살펴보십시오. |
| `preview` | 데이터 미리 보기를 활성화하는 부울 값. |
| `{OBJECT}` | 탐색할 [!DNL Dynamics] 개체입니다. |
| `{OBJECT_TYPE}` | 개체의 형식입니다. |
| `previewCount` | 반환된 미리보기를 특정 수의 레코드로만 제한하는 제한 사항입니다. |
| `{PRIMARY_KEY}` | 미리보기를 위해 검색 중인 테이블의 기본 키입니다. |

**요청**

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## 테이블 구조 검사

특정 테이블의 구조를 검사하려면 `/connections/{BASE_CONNECTION_ID}/explore`에 GET 요청을 하고 특정 테이블에 대한 경로를 쿼리 매개 변수로 제공하십시오.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 기본 연결의 ID입니다. 이 ID를 사용하여 소스의 콘텐츠와 구조를 살펴보십시오. |
| `{TABLE_PATH}` | 탐색할 특정 표의 경로입니다. |

**요청**

다음 요청은 경로가 `workflowdependency`인 [!DNL Dynamics] 테이블의 구조와 내용을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공한 응답이 `workflowdependency` 경로의 내용을 반환합니다.

+++응답 예를 보려면 선택

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## 보기 구조 검사

[!DNL Dynamics]에서 보기는 표시할 열, 각 열의 너비, 레코드 목록이 정렬되는 기본 시스템 및 목록에 표시될 레코드를 제한하는 데 적용되는 기본 필터를 참조합니다.

보기의 구조를 검사하려면 `/connections/{BASE_CONNECTION_ID}/explore`에 GET 요청을 만들고 쿼리 매개 변수에 보기 경로를 지정하십시오. 또한 `objectType`을(를) `view`(으)로 지정해야 합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 기본 연결의 ID입니다. 이 ID를 사용하여 소스의 콘텐츠와 구조를 살펴보십시오. |
| `{VIEW_PATH}` | 검사할 보기에 대한 경로입니다. |

**요청**

다음 요청은 `accountView1`을(를) 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

응답이 성공하면 `accountView1` 구조가 반환됩니다.

+++응답 예를 보려면 선택

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## 엔터티 형식 보기 미리 보기

보기의 내용을 미리 보려면 `/connections/{BASE_CONNECTION_ID}/explore`에 GET을 요청하고 쿼리 매개 변수에 보기 경로와 `preview=true`을(를) 포함하십시오.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 기본 연결의 ID입니다. 이 ID를 사용하여 소스의 콘텐츠와 구조를 살펴보십시오. |
| `{VIEW_PATH}` | 검사할 보기에 대한 경로입니다. |


**요청**

다음 요청은 `accountView1`의 내용을 미리 봅니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

응답이 성공하면 `accountView1`의 내용이 반환됩니다.

+++응답 예를 보려면 선택

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## 수집 보기에 대한 소스 연결 만들기

소스 연결을 만들고 보기를 수집하려면 `/sourceConnections` 끝점에 대한 POST 요청을 만들고 테이블 이름을 제공한 다음 요청 본문에서 `entityType`을(를) `view`(으)로 지정하십시오.

**API 형식**

```http
POST /sourceConnections
```

**요청**

다음 요청은 [!DNL Dynamics] 소스 연결을 만들고 보기를 수집합니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**응답**

성공한 응답은 새로 생성된 소스 연결 ID와 해당 etag를 반환합니다.

+++응답 예를 보려면 선택

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### 기본 키를 사용하여 데이터 흐름 최적화

기본 키를 요청 본문 매개 변수의 일부로 지정하여 [!DNL Dynamics] 데이터 흐름을 최적화할 수도 있습니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

다음 요청은 기본 키를 `contactid`(으)로 지정하는 동안 [!DNL Dynamics] 원본 연결을 만듭니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `baseConnectionId` | 기본 연결의 ID입니다. |
| `data.format` | 데이터의 형식입니다. |
| `params.tableName` | [!DNL Dynamics]의 테이블 이름입니다. |
| `params.primaryKey` | 쿼리를 최적화할 테이블의 기본 키입니다. |
| `connectionSpec.id` | [!DNL Dynamics] 원본에 해당하는 연결 사양 ID입니다. |

+++

**응답**

성공한 응답은 새로 생성된 소스 연결 ID와 해당 etag를 반환합니다.

+++응답 예를 보려면 선택

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Microsoft Dynamics] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 CRM 데이터를 플랫폼으로 가져오는 데이터 흐름을 만듭니다.](../../collect/crm.md)
