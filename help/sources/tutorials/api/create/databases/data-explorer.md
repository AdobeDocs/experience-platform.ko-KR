---
keywords: Experience Platform;홈;인기 항목;Azure Azure Data Explorer;Azure Data Explorer;Azure Data Explorer
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Azure Data Explorer 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Azure Azure Data Explorer을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Azure Azure Data Explorer] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Azure Data Explorer]에 대한 기본 연결을 만드는 단계를 안내합니다.


## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Azure Data Explorer]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Azure Data Explorer]과(와) 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `endpoint` | [!DNL Azure Data Explorer] 서버의 끝점입니다. |
| `database` | [!DNL Azure Data Explorer] 데이터베이스의 이름입니다. |
| `tenant` | [!DNL Azure Data Explorer] 데이터베이스에 연결하는 데 사용되는 고유한 테넌트 ID입니다. |
| `servicePrincipalId` | [!DNL Azure Data Explorer] 데이터베이스에 연결하는 데 사용되는 고유한 서비스 사용자 ID입니다. |
| `servicePrincipalKey` | [!DNL Azure Data Explorer] 데이터베이스에 연결하는 데 사용되는 고유한 서비스 사용자 키. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Azure Data Explorer]의 연결 사양 ID는 `0479cc14-7651-4354-b233-7480606c2ac3`입니다. |

시작에 대한 자세한 내용은 이 [[!DNL Azure Data Explorer] 문서](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)를 참조하세요.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Azure Data Explorer] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Azure Data Explorer]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `auth.params.endpoint` | [!DNL Azure Data Explorer] 서버의 끝점입니다. |
| `auth.params.database` | [!DNL Azure Data Explorer] 데이터베이스의 이름입니다. |
| `auth.params.tenant` | [!DNL Azure Data Explorer] 데이터베이스에 연결하는 데 사용되는 고유한 테넌트 ID입니다. |
| `auth.params.servicePrincipalId` | [!DNL Azure Data Explorer] 데이터베이스에 연결하는 데 사용되는 고유한 서비스 사용자 ID입니다. |
| `auth.params.servicePrincipalKey` | [!DNL Azure Data Explorer] 데이터베이스에 연결하는 데 사용되는 고유한 서비스 사용자 키. |
| `connectionSpec.id` | [!DNL Azure Data Explorer] 연결 사양 ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Azure Data Explorer] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/database-nosql.md)
