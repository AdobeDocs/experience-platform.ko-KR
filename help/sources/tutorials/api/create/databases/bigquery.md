---
keywords: Experience Platform;홈;인기 항목;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Flow Service API를 사용하여 Google BigQuery Base 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Google BigQuery에 연결하는 방법을 알아봅니다.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 015a4fa06fc2157bb8374228380bb31826add37e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 만들기 [!DNL Google BigQuery] 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Google BigQuery] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Google BigQuery] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Google BigQuery] platform에 다음 OAuth 2.0 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `project` | 기본값은 프로젝트 ID입니다 [!DNL Google BigQuery] 쿼리할 프로젝트입니다. |
| `clientID` | 새로 고침 토큰을 생성하는 데 사용되는 ID 값입니다. |
| `clientSecret` | 새로 고침 토큰을 생성하는 데 사용되는 암호 값입니다. |
| `refreshToken` | 에서 가져온 새로 고침 토큰 [!DNL Google] 액세스 권한을 인증하는 데 사용됩니다. [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | 미리 만들어진  [!DNL Google BigQuery] 큰 결과 세트에 대한 지원을 활성화하기 위해 필요한 데이터 세트 ID입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Google BigQuery] is: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

이러한 값에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Google BigQuery] 문서](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Google BigQuery] 요청 매개 변수의 일부로 인증 자격 증명.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Google BigQuery]:

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
| `auth.params.project` | 기본값은 프로젝트 ID입니다 [!DNL Google BigQuery] 쿼리할 프로젝트입니다. 반대입니다. |
| `auth.params.clientId` | 새로 고침 토큰을 생성하는 데 사용되는 ID 값입니다. |
| `auth.params.clientSecret` | 새로 고침 토큰을 생성하는 데 사용되는 클라이언트 값입니다. |
| `auth.params.refreshToken` | 에서 가져온 새로 고침 토큰 [!DNL Google] 액세스 권한을 인증하는 데 사용됩니다. [!DNL Google BigQuery]. |
| `connectionSpec.id` | 다음 [!DNL Google BigQuery] 연결 사양 ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Google BigQuery] 기본 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 [!DNL Flow Service] API](../../collect/database-nosql.md)
