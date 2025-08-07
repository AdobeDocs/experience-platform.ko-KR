---
title: 흐름 서비스 API를 사용하여 Oracle DB를 Experience Platform에 연결
description: API를 사용하여 Oracle DB를 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---

# [!DNL Oracle DB] API를 사용하여 [!DNL Flow Service]을(를) Experience Platform에 연결

[!DNL Oracle DB]API[[!DNL Flow Service] 를 사용하여 ](https://developer.adobe.com/experience-platform-apis/references/flow-service/) 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Oracle] API를 사용하여 [!DNL Flow Service]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Oracle DB] 개요](../../../../connectors/databases/oracle.md#prerequisites)를 읽어 보십시오.

## Azure에서 [!DNL Oracle DB]을(를) Experience Platform에 연결 {#azure}

[!DNL Oracle DB] 계정을 Azure의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하세요.

### Azure의 Experience Platform에서 [!DNL Oracle DB]에 대한 기본 연결 만들기 {#azure-base}

기본 연결은 소스를 Experience Platform에 연결하여 인증 세부 정보, 연결 상태 및 고유 ID를 저장합니다. 이 ID를 사용하여 소스 파일을 검색하고 데이터 유형 및 형식을 포함하여 수집할 특정 항목을 식별합니다.

**API 형식**

```https
POST /connections
```

기본 연결 ID를 만들려면 `/connections` 끝점에 POST를 요청하고 [!DNL Oracle DB] 인증 자격 증명을 요청 매개 변수의 일부로 제공합니다.

**요청**

다음 요청은 연결 문자열 인증을 사용하여 [!DNL Oracle DB]에 대한 기본 연결을 만듭니다.

+++요청 보기


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `auth.params.connectionString` | [!DNL Oracle DB]에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Oracle DB] 연결 문자열 패턴은 `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`입니다. |
| `connectionSpec.id` | [!DNL Oracle] 연결 사양 ID: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++응답 보기

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Amazon Web Services에서 [!DNL Oracle DB]을(를) Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL Oracle DB] 계정을 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### AWS의 Experience Platform에서 [!DNL Oracle DB]에 대한 기본 연결 만들기 {#aws-base}

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Oracle DB]이(가) AWS의 Experience Platform에 연결할 수 있는 기본 연결을 만듭니다.

+++요청 보기

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
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
| `auth.params.server` | [!DNL Oracle DB] 서버의 IP 주소 또는 호스트 이름입니다. |
| `auth.params.port` | [!DNL Oracle DB] 서버의 포트 번호입니다. |
| `auth.params.database` | 연결 중인 [!DNL Oracle DB] 인스턴스의 이름입니다. |
| `auth.params.username` | [!DNL Oracle DB] 인스턴스와 연결된 사용자 계정입니다. |
| `auth.prams.password` | [!DNL Oracle DB] 사용자 계정에 해당하는 암호입니다. |
| `auth.params.schema` | 데이터베이스 개체가 포함된 스키마. |
| `auth.params.sslMode` | SSL 측정의 적용 여부를 나타내는 부울 값입니다. |
| `connectionSpec.id` | [!DNL Oracle DB] 원본에 해당하는 연결 사양 ID입니다. 이 ID 값은 `d6b52d86-f0f8-475f-89d4-ce54c8527328.`(으)로 수정되었습니다. |

+++

**응답**

성공한 응답은 고유 식별자(`id`) 및 해당 식별자를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다. ID를 사용하여 [원본 연결을 만들고](../../collect/database-nosql.md#create-a-source-connection), `etag`을(를) 사용하여 [계정을 업데이트](../../update.md)할 수 있습니다.

+++응답 보기

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## [!DNL Oracle DB] 데이터에 대한 데이터 흐름 만들기

[!DNL Oracle DB] 계정을 연결했으므로 이제 [데이터 흐름을 만들고 데이터베이스의 데이터를 Experience Platform으로 수집](../../collect/database-nosql.md)할 수 있습니다.