---
title: 흐름 서비스 API를 사용하여 Azure Synapse Analytics를 Experience Platform에 연결
description: API를 사용하여 Azure Synapse Analytics 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Azure Synapse Analytics]을(를) Experience Platform에 연결

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Azure Synapse Analytics] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Azure Synapse Analytics]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Azure Synapse Analytics] 개요](../../../../connectors/databases/synapse-analytics.md#prerequisites)를 읽어 보십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## Experience Platform에 [!DNL Azure Synapse Analytics] 연결

기본 연결을 만들고 [!DNL Azure Synapse Analytics] 계정을 Experience Platform에 연결하는 방법을 알아보려면 다음을 참조하세요.

### 기본 연결 만들기

**기본 연결**&#x200B;은(는) 소스 시스템을 Adobe Experience Platform에 연결하는 키 정보를 저장합니다. 여기에는 다음 항목이 포함되어 있습니다.

* 소스의 인증 자격 증명
* 현재 연결 상태
* 고유 **기본 연결 ID**

**기본 연결 ID**&#x200B;을(를) 사용하면 소스에서 파일을 탐색하고 탐색할 수 있으므로 데이터 형식 및 형식과 함께 수집할 항목을 식별하는 데 도움이 됩니다.

기본 연결 ID를 만들려면 요청 매개 변수에 [!DNL Azure Synapse Analytics] 인증 자격 증명을 포함하여 `/connections` 끝점에 POST 요청을 보냅니다.

**API 형식**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 연결 문자열 기반 인증]

**요청**

다음 요청은 연결 문자열 기반 인증을 사용하여 [!DNL Azure Synapse Analytics]에 대한 기본 연결을 만듭니다.

+++예제 요청 보기

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `auth.params.connectionString` | [!DNL Azure Synapse Analytics]에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Azure Synapse Analytics] 연결 문자열 패턴은 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`입니다. |
| `connectionSpec.id` | [!DNL Azure Synapse Analytics] 연결 사양 ID: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++예제 응답 보기

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB 서비스 사용자 키 기반 인증]

다음 요청은 서비스 사용자 키 기반 인증을 사용하여 [!DNL Azure Synapse Analytics]에 대한 기본 연결을 만듭니다.

**요청**

+++예제 요청 보기

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| 자격 증명 | 설명 |
| --- | --- |
| `auth.params.server` | [!DNL Azure Synapse Analytics] SQL 끝점의 정규화된 도메인 이름입니다. |
| `auth.params.database` | [!DNL Azure Synapse Analytics] 작업 영역의 특정 데이터베이스 이름입니다. |
| `auth.params.tenant` | [!DNL Azure] 구독과 연결된 [!DNL Azure Active Directory] 테넌트 ID입니다. |
| `auth.params.servicePrincipalId` | [!DNL Azure Active Directory] 응용 프로그램의 클라이언트 ID. |
| `auth.params.servicePrincipalKey` | 서비스 주체와 연계된 클라이언트 암호. |
| `connectSpec.id` | 연결 사양 ID [!DNL Azure Synapse Analytics]입니다. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++예제 응답 보기

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Azure Synapse Analytics] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/database-nosql.md)
