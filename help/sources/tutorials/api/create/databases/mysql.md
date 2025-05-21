---
title: 흐름 서비스 API를 사용하여 MySQL을 Experience Platform에 연결
description: API를 사용하여 MySQL 데이터베이스를 Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 [!DNL MySQL]을(를) Experience Platform에 연결

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL MySQL] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL MySQL]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL MySQL] 개요](../../../../connectors/databases/mysql.md#prerequisites)를 읽어 보십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작하기](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## Azure에서 [!DNL MySQL]을(를) Experience Platform에 연결 {#azure}

[!DNL MySQL] 계정을 Azure의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하세요.

### Azure의 Experience Platform에서 [!DNL MySQL]에 대한 기본 연결 만들기 {#azure-base}

기본 연결은 소스를 Experience Platform에 연결하여 인증 세부 정보, 연결 상태 및 고유 ID를 저장합니다. 이 ID를 사용하여 소스 파일을 검색하고 데이터 유형 및 형식을 포함하여 수집할 특정 항목을 식별합니다.

**API 형식**

```https
POST /connections
```

기본 연결 ID를 만들려면 `/connections` 끝점에 POST를 요청하고 [!DNL MySQL] 인증 자격 증명을 요청 매개 변수의 일부로 제공합니다.

>[!BEGINTABS]

>[!TAB 연결 문자열 기반 인증]

**요청**

다음 요청은 연결 문자열 기반 인증을 사용하여 [!DNL MySQL]에 대한 기본 연결을 만듭니다.

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
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.connectionString` | 계정과 연결된 [!DNL MySQL] 연결 문자열입니다. [!DNL MySQL] 연결 문자열 패턴은 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`입니다. |
| `connectionSpec.id` | [!DNL MySQL] 연결 사양 ID: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++응답 보기 예

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB 기본 인증]

**요청**

다음 요청은 기본 인증을 사용하여 [!DNL MySQL] 소스에 대한 기본 연결을 만듭니다.

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
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.server` | [!DNL MySQL] 데이터베이스의 이름 또는 IP. |
| `auth.params.database` | 데이터베이스의 이름입니다. |
| `auth.params.username` | 데이터베이스에 해당하는 사용자 이름입니다. |
| `auth.params.password` | 데이터베이스에 해당하는 암호입니다. |
| `auth.params.sslMode` | 데이터를 전송하는 동안 데이터를 암호화하는 방법입니다. |
| `connectionSpec.id` | [!DNL MySQL] 연결 사양 ID: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++응답 보기 예

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Amazon Web Services에서 [!DNL MySQL]을(를) Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL MySQL] 계정을 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### AWS의 Experience Platform에서 [!DNL MySQL]에 대한 기본 연결 만들기 {#aws-base}

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL MySQL]이(가) AWS의 Experience Platform에 연결할 수 있는 기본 연결을 만듭니다.

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
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.server` | [!DNL MySQL] 데이터베이스의 이름 또는 IP. |
| `auth.params.database` | 데이터베이스의 이름입니다. |
| `auth.params.username` | 데이터베이스에 해당하는 사용자 이름입니다. |
| `auth.params.password` | 데이터베이스에 해당하는 암호입니다. |
| `auth.params.sslMode` | 서버 지원에 따라 SSL의 적용 여부를 제어하는 부울 값입니다. 이 구성은 기본적으로 `false`입니다. |
| `connectionSpec.id` | [!DNL MySQL] 연결 사양 ID: `26d738e0-8963-47ea-aadf-c60de735468a`. |

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

## [!DNL MySQL] 데이터에 대한 데이터 흐름 만들기

[!DNL MySQL] 데이터베이스를 연결했으므로 이제 [데이터 흐름을 만들고 데이터베이스에서 Experience Platform으로 데이터를 수집](../../collect/database-nosql.md)할 수 있습니다.