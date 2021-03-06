---
keywords: Experience Platform;홈;인기 주제;oracle;언쇼어;oracle 웅변
solution: Experience Platform
title: Flow Service API를 사용하여 Oracle Eloqua Base Connection 생성
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Oracle Eloqua에 연결하는 방법을 알아봅니다.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# 만들기 [!DNL Oracle Eloqua] 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Oracle Eloqua] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Platform의 다음 구성 요소를 제대로 이해하고 있어야 합니다.

* [소스](../../../../home.md): 플랫폼을 사용하면 다양한 소스에서 데이터를 수집할 수 있으며 다음을 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공할 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): Platform은 단일 파티션으로 분할하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Oracle Eloqua] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Oracle Eloqua]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `endpoint` | 엔드포인트 [!DNL Oracle Eloqua]. |
| `username` | 사용자 이름 [!DNL Oracle Eloqua] 계정이 필요합니다. 사용자 이름은 `siteName + \\ + username`, 위치 `siteName` 은 로그인하는 데 사용한 회사 이름입니다 [!DNL Oracle Eloqua] 및 `username` 은 사용자 이름입니다. 예를 들어 로그인 사용자 이름은 다음과 같습니다. `adobe\\emily`. |
| `password` | 사용자 [!DNL Oracle Eloqua] 사용자 이름. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 연결 사양 ID의 값 [!DNL Oracle Eloqua] 소스는 다음과 같이 수정되었습니다. `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

의 인증 자격 증명에 대한 자세한 정보 [!DNL Oracle Eloqua]를 참조하고 [[!DNL Oracle Eloqua] 인증 안내서](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Oracle Eloqua] 요청 매개 변수의 일부로 인증 자격 증명.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `name` | 사용자 이름 [!DNL Oracle Eloqua] 기본 연결. 이 값을 사용하여 기본 연결을 조회할 수 있으므로 수사적 이름을 제공하는 것이 좋습니다. |
| `description` | (선택 사항) 기본 연결에 대한 추가 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `auth.specName` | 연결에 사용되는 인증 유형입니다. |
| `auth.params.endpoint` | 엔드포인트 [!DNL Oracle Eloqua] server. |
| `auth.params.username` | 사이트 이름 및 사용자 이름과 일치하는 사용자 이름을 포함하는 연결된 자격 증명입니다 [!DNL Oracle Eloqua] 계정이 필요합니다. |
| `auth.params.password` | 사용자의 [!DNL Oracle Eloqua] 계정이 필요합니다. |
| `connectionSpec.id` | 연결 사양 ID의 값 [!DNL Oracle Eloqua] 소스는 다음과 같이 수정되었습니다. `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Oracle Eloqua] 기본 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 다음을 사용하여 마케팅 자동화 데이터를 Platform으로 가져오기 [!DNL Flow Service] API](../../collect/marketing-automation.md)
