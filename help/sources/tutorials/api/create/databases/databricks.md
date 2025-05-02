---
title: 흐름 서비스 API를 사용하여 Azure 데이터베이스를 Experience Platform에 연결
description: API를 사용하여 Azure Databricks를 Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 30f1c16084b3049fae45e26db0eed03888d35516
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Azure Databricks]을(를) Experience Platform에 연결

>[!IMPORTANT]
>
>[!DNL Azure Databricks] 소스는 Real-Time CDP Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Azure Databricks] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API를 시작하는 방법](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

### 사전 요구 사항 설정 구성

계정을 Experience Platform에 연결하기 전에 완료해야 하는 필수 구성 요소에 대한 자세한 내용은 [[!DNL Databricks] 개요](../../../../connectors/databases/databricks.md)를 참조하십시오.

### 필요한 자격 증명 수집

[!DNL Databricks]을(를) Experience Platform에 연결하려면 다음 자격 증명의 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `domain` | [!DNL Databricks] 작업 영역의 URL입니다. 예: `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | [!DNL Databricks]에 있는 클러스터의 ID입니다. 이 클러스터는 이미 기존 클러스터여야 하며 대화형 클러스터여야 합니다. |
| `accessToken` | [!DNL Databricks] 계정을 인증하는 액세스 토큰입니다. [!DNL Databricks] 작업 영역을 사용하여 액세스 토큰을 생성할 수 있습니다. |
| `database` | 델타 레이크에 있는 데이터베이스의 이름입니다. |
| `connectionSpec.Id` | 연결 사양 ID는 기본 및 소스 연결 생성과 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Databricks]의 연결 사양 ID는 `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`입니다. |

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 끝점에 POST를 요청하고 [!DNL Databricks] 계정에 적절한 인증 자격 증명을 제공하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 액세스 토큰 인증을 사용하여 [!DNL Databricks] 소스에 대한 기본 연결을 만듭니다.

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
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.domain` | [!DNL Databricks] 작업 영역의 URL입니다. |
| `auth.params.clusterId` | [!DNL Databricks]에 있는 클러스터의 ID입니다. 이 클러스터는 이미 기존 클러스터이고 대화형 클러스터여야 합니다. |
| `auth.params.accessToken` | [!DNL Databricks] 계정을 인증하는 액세스 토큰입니다. |
| `auth.params.database` | 델타 레이크에 있는 데이터베이스의 이름입니다. |
| `connectionSpec.id` | [!DNL Databricks] 연결 사양 ID. |

+++

**응답**

응답이 성공하면 기본 연결 ID를 포함하여 새로 만든 연결이 반환됩니다.

+++응답 보기 예

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## 다음 단계

이 자습서를 따라 [!DNL Databricks] 계정과 Experience Platform 간의 연결을 만들었습니다. 다음 자습서에서는 새로 생성된 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/database-nosql.md)
