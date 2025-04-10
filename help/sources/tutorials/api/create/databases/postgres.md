---
title: 흐름 서비스 API를 사용하여 PostgreSQL을 Experience Platform에 연결
description: API를 사용하여  [!DNL PostgreSQL] 데이터베이스를 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 5348158f6de9fea1a9fe186a14409afb7e7a376e
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL PostgreSQL] 기본 연결 만들기

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL PostgreSQL] 데이터베이스를 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL PostgreSQL]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작하기](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL PostgreSQL] 개요](../../../../connectors/databases/postgres.md)를 참조하세요.

### 연결 문자열에 SSL 암호화 사용

다음 속성을 사용하여 연결 문자열을 추가하여 [!DNL PostgreSQL] 연결 문자열에 SSL 암호화를 사용하도록 설정할 수 있습니다.

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `EncryptionMethod` | [!DNL PostgreSQL] 데이터에 대해 SSL 암호화를 사용하도록 설정할 수 있습니다. | <uL><li>`EncryptionMethod=0`(사용 안 함)</li><li>`EncryptionMethod=1`(활성화됨)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | `EncryptionMethod`이(가) 적용되면 [!DNL PostgreSQL] 데이터베이스에서 보낸 인증서의 유효성을 검사합니다. | <uL><li>`ValidationServerCertificate=0`(사용 안 함)</li><li>`ValidationServerCertificate=1`(활성화됨)</li></ul> |

다음은 SSL 암호화가 추가된 [!DNL PostgreSQL] 연결 문자열의 예입니다. `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Azure에서 [!DNL PostgreSQL]을(를) Experience Platform에 연결 {#azure}

[!DNL PostgreSQL] 계정을 Azure의 Experience Platform에 연결하는 방법을 알아보려면 아래 단계를 참조하세요.

### 기본 연결 만들기 {#azure-base}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL PostgreSQL] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 계정 키 기반 인증]

**요청**

다음 요청은 계정 키 기반 인증을 사용하여 [!DNL PostgreSQL]에 대한 기본 연결을 만듭니다.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| ------------- | --------------- |
| `auth.params.connectionString` | [!DNL PostgreSQL] 계정과 연결된 연결 문자열입니다. [!DNL PostgreSQL] 연결 문자열 패턴은 `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`입니다. |
| `connectionSpec.id` | [!DNL PostgreSQL] 연결 사양 ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**응답**

성공한 응답은 새로 만든 기본 연결의 고유 식별자(`id`)를 반환합니다.

+++응답 보기 예

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB 기본 인증]

**요청**

다음 요청은 기본 인증을 사용하여 [!DNL PostgreSQL]에 대한 기본 연결을 만듭니다.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| ---| --- |
| `auth.params.server` | [!DNL PostgreSQL] 데이터베이스의 이름 또는 IP 주소입니다. |
| `auth.params.port` | 데이터베이스 서버의 포트 번호입니다. |
| `auth.params.database` | [!DNL PostgreSQL] 데이터베이스의 이름입니다. |
| `auth.params.username` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 사용자 이름입니다. |
| `auth.params.password` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 암호입니다. |
| `auth.params.sslMode` | 데이터를 전송하는 동안 데이터를 암호화하는 방법입니다. 사용 가능한 값은 `Disable`, `Allow`, `Prefer`, `Verify Ca` 및 `Verify Full`입니다. |
| `connectionSpec.id` | [!DNL PostgreSQL] 연결 사양 ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**응답**

성공한 응답은 새로 만든 기본 연결의 고유 식별자(`id`)를 반환합니다.

+++응답 보기 예

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Amazon Web Services에서 [!DNL PostgreSQL]을(를) Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL PostgreSQL] 데이터베이스를 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### 기본 연결 만들기 {#aws-base}

기본 연결 ID를 만들려면 [!DNL PostgreSQL] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL PostgreSQL]이(가) AWS의 Experience Platform에 연결할 수 있는 기본 연결을 만듭니다.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| ---| --- |
| `auth.params.server` | [!DNL PostgreSQL] 데이터베이스의 이름 또는 IP 주소입니다. |
| `auth.params.port` | 데이터베이스 서버의 포트 번호입니다. |
| `auth.params.database` | [!DNL PostgreSQL] 데이터베이스의 이름입니다. |
| `auth.params.username` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 사용자 이름입니다. |
| `auth.params.password` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 암호입니다. |
| `auth.params.sslMode` | 데이터를 전송하는 동안 데이터를 암호화하는 방법입니다. 사용 가능한 값은 `Disable`, `Allow`, `Prefer`, `Verify Ca` 및 `Verify Full`입니다. |
| `connectionSpec.id` | [!DNL PostgreSQL] 연결 사양 ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**응답**

성공한 응답은 새로 만든 기본 연결의 고유 식별자(`id`)를 반환합니다.

+++응답 보기 예

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## 다음 단계

[!DNL PostgreSQL] 데이터베이스와 Experience Platform을 연결했으므로 이제 다음 단계를 진행하여 [!DNL PostgreSQL] 데이터를 Experience Platform으로 가져올 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/database-nosql.md)
