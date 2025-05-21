---
title: 흐름 서비스 API를 사용하여 MariaDB를 Experience Platform에 연결
description: API를 사용하여 MariaDB 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL MariaDB]을(를) Experience Platform에 연결

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL MariaDB] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL MariaDB]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL MariaDB] 개요](../../../../connectors/databases/mariadb.md#prerequisites)를 읽어 보십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작하기](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## Experience Platform에 [!DNL MariaDB] 연결

[!DNL MariaDB] 계정을 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하세요.

### [!DNL MariaDB]에 대한 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

**API 형식**

```https
POST /connections
```

기본 연결 ID를 만들려면 `/connections` 끝점에 POST를 요청하고 [!DNL MariaDB] 계정에 적절한 인증 자격 증명을 제공하십시오.

>[!BEGINTABS]

>[!TAB 연결 문자열 기반 인증]

**요청**

다음 요청은 연결 문자열 기반 인증을 사용하여 [!DNL MariaDB] 소스에 대한 기본 연결을 만듭니다.

+++요청 보기 예

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.connectionString` | [!DNL MariaDB] 인증과 연결된 연결 문자열입니다. [!DNL MariaDB] 연결 문자열 패턴은 `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`입니다. |
| `connectionSpec.id` | [!DNL MariaDB] 연결 사양 ID: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++응답 보기 예

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB 기본 인증]

**요청**

다음 요청은 기본 인증을 사용하여 [!DNL MariaDB] 소스에 대한 기본 연결을 만듭니다.

+++요청 보기 예

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.server` | [!DNL MariaDB] 데이터베이스의 이름 또는 IP. |
| `auth.params.database` | 데이터베이스의 이름입니다. |
| `auth.params.username` | 데이터베이스에 해당하는 사용자 이름입니다. |
| `auth.params.password` | 데이터베이스에 해당하는 암호입니다. |
| `auth.params.sslMode` | 데이터를 전송하는 동안 데이터를 암호화하는 방법입니다. |
| `connectionSpec.id` | [!DNL MariaDB] 연결 사양 ID: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++응답 보기 예

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

>[!ENDTABS]


## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL MariaDB] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/database-nosql.md)
