---
keywords: Experience Platform;홈;자주 찾는 항목;Azure Data Lake Storage Gen2;azure Data Lake Storage;Azure
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Azure Data Lake Storage Gen2 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Azure Data Lake Storage Gen2에 연결하는 방법을 알아봅니다.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# 만들기 [!DNL Azure Data Lake Storage Gen2] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Azure Data Lake Storage Gen2] (이하 &quot;ADLS Gen2&quot;라 함) [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 사용하여 ADLS Gen2 소스 연결을 성공적으로 생성하기 위해 알아야 할 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] adls Gen2에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | ADLS Gen2의 종단점입니다. 끝점 패턴은 다음과 같습니다. `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | 애플리케이션의 클라이언트 ID. |
| `servicePrincipalKey` | 애플리케이션 키. |
| `tenant` | 애플리케이션이 포함된 테넌트 정보입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. ADLS Gen2의 연결 사양 ID는 다음과 같습니다. `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

이러한 값에 대한 자세한 내용은 [이 ADLS Gen2 문서](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 요청 매개 변수의 일부로 ADLS Gen2 인증 자격 증명을 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 ADLS Gen2에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.url` | ADLS Gen2 계정의 URL 엔드포인트. |
| `auth.params.servicePrincipalId` | ADLS Gen2 계정의 서비스 사용자 ID입니다. |
| `auth.params.servicePrincipalKey` | ADLS Gen2 계정의 서비스 사용자 키. |
| `auth.params.tenant` | ADLS Gen2 계정의 테넌트 정보입니다. |
| `connectionSpec.id` | ADLS Gen2 연결 사양 ID: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다(`id`). 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 다음 단계

이 자습서에 따라 API를 사용하여 ADLS Gen2 연결을 만들었고 고유 ID를 응답 본문의 일부로 가져왔습니다. 이 연결 ID를 사용하여 다음을 수행할 수 있습니다. [흐름 서비스 API를 사용하여 클라우드 저장소 살펴보기](../../explore/cloud-storage.md).
