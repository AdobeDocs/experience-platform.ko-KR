---
title: 흐름 서비스 API를 사용하여 Snowflake 기반 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Snowflake에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---

# 만들기 [!DNL Snowflake] 를 사용한 기본 연결 [!DNL Flow Service] API

>[!IMPORTANT]
>
>다음 [!DNL Snowflake] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Snowflake] 사용 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Snowflake] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Snowflake], 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | 와(과) 연결된 전체 계정 이름 [!DNL Snowflake] 계정입니다. 완전한 자격을 갖춘 [!DNL Snowflake] 계정 이름에는 계정 이름, 지역 및 클라우드 플랫폼이 포함됩니다. 예, `cj12345.east-us-2.azure`. 계정 이름에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | 다음 [!DNL Snowflake] warehouse는 애플리케이션의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] warehouse는 서로 독립적이며 데이터를 Platform으로 가져올 때 개별적으로 액세스해야 합니다. |
| `database` | 다음 [!DNL Snowflake] 데이터베이스에는 플랫폼으로 가져올 데이터가 포함되어 있습니다. |
| `username` | 의 사용자 이름 [!DNL Snowflake] 계정입니다. |
| `password` | 에 대한 암호 [!DNL Snowflake] 사용자 계정입니다. |
| `role` | 에서 사용할 기본 액세스 제어 역할 [!DNL Snowflake] 세션. 역할은 지정된 사용자에게 이미 할당된 기존 역할이어야 합니다. 기본 역할은 입니다. `PUBLIC`. |
| `connectionString` | 에 연결하는 데 사용되는 연결 문자열 [!DNL Snowflake] 인스턴스. 에 대한 연결 문자열 패턴입니다 [!DNL Snowflake] 은(는) `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Snowflake] 은(는) `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Snowflake] 문서](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>다음을 설정해야 합니다. `PREVENT_UNLOAD_TO_INLINE_URL` 플래그 지정 대상 `FALSE` 에서 데이터 언로드를 허용하려면 [!DNL Snowflake] Experience Platform 대상 데이터베이스.

## 기본 연결을 만듭니다

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Snowflake] 요청 본문의 일부인 인증 자격 증명입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Snowflake]:

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
| `auth.params.connectionString` | 에 연결하는 데 사용되는 연결 문자열 [!DNL Snowflake] 인스턴스. 에 대한 연결 문자열 패턴입니다 [!DNL Snowflake] 은(는) `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | 다음 [!DNL Snowflake] 연결 사양 ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**응답**

성공한 응답은 고유 연결 식별자( )를 포함하여 새로 생성된 연결을 반환합니다.`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

이 자습서를 따라 [!DNL Snowflake] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/database-nosql.md)
