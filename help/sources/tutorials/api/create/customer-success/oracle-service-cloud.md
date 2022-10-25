---
keywords: Experience Platform;홈;인기 항목;Oracle 서비스 클라우드;oracle 서비스 클라우드
title: Flow Service API를 사용하여 Oracle 서비스 클라우드 소스 연결 만들기
description: Flow Service API를 사용하여 Adobe Experience Platform을 Oracle Service Cloud에 연결하는 방법을 알아봅니다.
source-git-commit: 078a266967cd7b0818f958283a58a8af4c886a21
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# (베타) 를 사용하여 Oracle 서비스 클라우드 소스 연결을 만듭니다 [!DNL Flow Service] API

>[!NOTE]
>
>oracle 서비스 클라우드 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음을 사용하여 Oracle 서비스 클라우드에 대한 기본 연결을 만드는 단계를 안내합니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 사용하여 Oracle 서비스 클라우드에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] oracle 서비스 클라우드와 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | oracle 서비스 클라우드 인스턴스의 호스트 URL입니다. |
| `username` | oracle 서비스 클라우드 사용자 계정의 사용자 이름입니다. |
| `password` | oracle 서비스 클라우드 계정의 암호입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. oracle 서비스 클라우드의 연결 사양 ID는 다음과 같습니다. `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

oracle Service Cloud 계정 인증과 관련된 자세한 내용은 [[!DNL Oracle] 인증 안내서](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 요청 매개 변수의 일부로 Oracle 서비스 클라우드 인증 자격 증명을 제공하는 동안 끝점입니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 Oracle 서비스 클라우드에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.host` | oracle 서비스 클라우드 인스턴스의 호스트 URL입니다. |
| `auth.params.username` | oracle Service Cloud 계정과 연결된 사용자 이름입니다. |
| `auth.params.password` | oracle 서비스 클라우드 계정과 연결된 암호입니다. |
| `connectionSpec.id` | oracle 서비스 클라우드 연결 사양 ID: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**응답**

성공적인 응답은 해당 고유 식별자( )를 포함하여 새로 생성된 연결을 반환합니다`id`). 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 다음 단계

이 자습서에 따르면 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름 을 만들어 [!DNL Flow Service] API](../../collect/customer-success.md)
