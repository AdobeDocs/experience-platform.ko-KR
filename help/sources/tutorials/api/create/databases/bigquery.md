---
title: 흐름 서비스 API를 사용하여 Google BigQuery 기본 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google BigQuery에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Google BigQuery] 기본 연결 만들기

>[!IMPORTANT]
>
>[!DNL Google BigQuery] 원본은 Real-time Customer Data Platform Ultimate를 구입한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Google BigQuery]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 다음 Experience Platform 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Google BigQuery]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Google BigQuery]을(를) 플랫폼에 연결하려면 다음 OAuth 2.0 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `project` | 쿼리할 기본 [!DNL Google BigQuery] 프로젝트의 프로젝트 ID. |
| `clientID` | 새로 고침 토큰을 생성하는 데 사용되는 ID 값입니다. |
| `clientSecret` | 새로 고침 토큰을 생성하는 데 사용되는 비밀 값. |
| `refreshToken` | [!DNL Google BigQuery]에 대한 액세스를 승인하는 데 사용되는 [!DNL Google]에서 얻은 새로 고침 토큰입니다. |
| `largeResultsDataSetId` | 대용량 결과 집합을 지원하는 데 필요한 미리 만들어진 [!DNL Google BigQuery] 데이터 집합 ID입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Google BigQuery]의 연결 사양 ID는 `3c9b37f8-13a6-43d8-bad3-b863b941fedd`입니다. |

이러한 값에 대한 자세한 내용은 이 [[!DNL Google BigQuery] 문서](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)를 참조하세요.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Google BigQuery] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Google BigQuery]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.project` | 쿼리할 기본 [!DNL Google BigQuery] 프로젝트의 프로젝트 ID. 에 대해. |
| `auth.params.clientId` | 새로 고침 토큰을 생성하는 데 사용되는 ID 값입니다. |
| `auth.params.clientSecret` | 새로 고침 토큰을 생성하는 데 사용되는 클라이언트 값입니다. |
| `auth.params.refreshToken` | [!DNL Google BigQuery]에 대한 액세스를 승인하는 데 사용되는 [!DNL Google]에서 얻은 새로 고침 토큰입니다. |
| `connectionSpec.id` | [!DNL Google BigQuery] 연결 사양 ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Google BigQuery] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만드십시오.](../../collect/database-nosql.md)
