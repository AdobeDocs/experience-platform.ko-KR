---
title: 흐름 서비스 API를 사용하여 Snowflake을 Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Snowflake에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: cde31b692e9a11b15cf91a505133f75f69604cba
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 3%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Snowflake]을(를) Experience Platform에 연결

>[!IMPORTANT]
>
>[!DNL Snowflake] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Snowflake] 소스 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Snowflake]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

## Azure에서 [!DNL Snowflake]을(를) Experience Platform에 연결 {#azure}

[!DNL Snowflake] 소스를 Azure의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하세요.

### 필요한 자격 증명 수집

[!DNL Snowflake] 원본을 인증하려면 다음 자격 증명 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `account` | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 추가 지침은 [계정 식별자 검색 [!DNL Snowflake] 에 대한 안내서를 참조하십시오](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이며 데이터를 플랫폼으로 가져올 때 개별적으로 액세스해야 합니다. |
| `database` | [!DNL Snowflake] 데이터베이스에 플랫폼에 가져올 데이터가 있습니다. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `password` | [!DNL Snowflake] 사용자 계정의 암호입니다. |
| `role` | [!DNL Snowflake] 세션에서 사용할 기본 액세스 제어 역할입니다. 역할은 지정된 사용자에게 이미 할당된 기존 역할이어야 합니다. 기본 역할은 `PUBLIC`입니다. |
| `connectionString` | [!DNL Snowflake] 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Snowflake]에 대한 연결 문자열 패턴은 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`입니다. |

>[!TAB 키 쌍 인증]

키 쌍 인증을 사용하려면 2048비트 RSA 키 쌍을 생성한 다음 [!DNL Snowflake] 소스에 대한 계정을 만들 때 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 추가 지침은 [계정 식별자 검색 [!DNL Snowflake] 에 대한 안내서를 참조하십시오](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `privateKey` | [!DNL Snowflake] 계정의 [!DNL Base64-]인코딩된 개인 키입니다. 암호화되거나 암호화되지 않은 개인 키를 생성할 수 있습니다. 암호화된 개인 키를 사용하는 경우 Experience Platform에 대해 인증할 때 개인 키 암호도 제공해야 합니다. 자세한 내용은 [개인 키 검색 [!DNL Snowflake] 2}에 대한 안내서를 참조하십시오.](../../../../connectors/databases/snowflake.md) |
| `privateKeyPassphrase` | 개인 키 암호는 암호화된 개인 키로 인증할 때 사용해야 하는 추가 보안 계층입니다. 암호화되지 않은 개인 키를 사용하는 경우에는 암호를 제공할 필요가 없습니다. |
| `database` | Experience Platform으로 수집할 데이터가 포함된 [!DNL Snowflake] 데이터베이스입니다. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |

이러한 값에 대한 자세한 내용은 [[!DNL Snowflake] 키 쌍 인증 가이드](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)를 참조하십시오.

>[!ENDTABS]

>[!NOTE]
>
>[!DNL Snowflake] 데이터베이스에서 Experience Platform으로 데이터를 언로드하려면 `PREVENT_UNLOAD_TO_INLINE_URL` 플래그를 `FALSE`(으)로 설정해야 합니다.

### Azure의 Experience Platform에서 [!DNL Snowflake]에 대한 기본 연결 만들기 {#azure-base}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Snowflake] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 연결 문자열]

+++요청

다음 요청은 [!DNL Snowflake]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.connectionString` | [!DNL Snowflake] 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Snowflake]에 대한 연결 문자열 패턴은 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`입니다. |
| `connectionSpec.id` | [!DNL Snowflake] 연결 사양 ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++응답

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>암호화된 개인 키를 사용한 [!TAB 키 쌍 인증]

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.account` | [!DNL Snowflake] 계정의 이름입니다. |
| `auth.params.username` | [!DNL Snowflake] 계정과 연결된 사용자 이름. |
| `auth.params.database` | 데이터를 가져올 위치의 [!DNL Snowflake] 데이터베이스입니다. |
| `auth.params.privateKey` | [!DNL Snowflake] 계정의 [!DNL Base64-]암호화된 개인 키입니다. |
| `auth.params.privateKeyPassphrase` | 개인 키에 해당하는 암호입니다. |
| `auth.params.warehouse` | 사용 중인 [!DNL Snowflake] 웨어하우스입니다. |
| `connectionSpec.id` | [!DNL Snowflake] 연결 사양 ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++응답

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>암호화되지 않은 개인 키를 사용한 [!TAB 키 쌍 인증]

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.account` | [!DNL Snowflake] 계정의 이름입니다. |
| `auth.params.username` | [!DNL Snowflake] 계정과 연결된 사용자 이름. |
| `auth.params.database` | 데이터를 가져올 위치의 [!DNL Snowflake] 데이터베이스입니다. |
| `auth.params.privateKey` | [!DNL Snowflake] 계정의 [!DNL Base64-]암호화되지 않은 개인 키입니다. |
| `auth.params.warehouse` | 사용 중인 [!DNL Snowflake] 웨어하우스입니다. |
| `connectionSpec.id` | [!DNL Snowflake] 연결 사양 ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++응답

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Amazon Web Services(AWS)의 Experience Platform에 [!DNL Snowflake] 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL Snowflake] 소스를 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### AWS의 Experience Platform에서 [!DNL Snowflake]에 대한 기본 연결 만들기 {#aws-base}

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL Snowflake]이(가) AWS에서 Experience Platform으로 날짜를 수집하기 위한 기본 연결을 만듭니다.

+++예를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.host` | [!DNL Snowflake] 계정이 연결되는 호스트 URL입니다. |
| `auth.params.port` | [!DNL Snowflake]이(가) 인터넷을 통해 서버에 연결할 때 사용하는 포트 번호입니다. |
| `auth.params.username` | [!DNL Snowflake] 계정과 연결된 사용자 이름. |
| `auth.params.database` | 데이터를 가져올 위치의 [!DNL Snowflake] 데이터베이스입니다. |
| `auth.params.password` | [!DNL Snowflake] 계정과 연결된 암호입니다. |
| `auth.params.warehouse` | 사용 중인 [!DNL Snowflake] 웨어하우스입니다. |
| `auth.params.schema` | [!DNL Snowflake] 데이터베이스와 연결된 스키마의 이름입니다. 데이터베이스 액세스 권한을 부여할 사용자도 이 스키마에 액세스할 수 있는지 확인해야 합니다. |

+++

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 다음 자습서에서 저장소를 탐색하려면 이 ID가 필요합니다.

+++예를 보려면 선택

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Snowflake] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만드십시오.](../../collect/database-nosql.md)
