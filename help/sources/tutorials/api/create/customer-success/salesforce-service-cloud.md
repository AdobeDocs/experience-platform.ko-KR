---
keywords: Experience Platform;홈;인기 항목;Salesforce Service Cloud;Salesforce Service Cloud
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Salesforce 서비스 클라우드 소스 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Salesforce 서비스 클라우드에 연결하는 방법에 대해 알아봅니다.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 1f13b5fcad683b4c0ede96654e35d6f0c64d9eb7
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 4%

---

# 만들기 [!DNL Salesforce Service Cloud] 를 사용한 소스 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Salesforce Service Cloud] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Salesforce Service Cloud] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Salesforce Service Cloud], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | ---|
| `environmentUrl` | 의 URL [!DNL Salesforce] 소스 인스턴스. |
| `username` | 에 대한 사용자 이름 [!DNL Salesforce Service Cloud] 사용자 계정입니다. |
| `password` | 에 대한 암호 [!DNL Salesforce Service Cloud] 계정입니다. |
| `securityToken` | 에 대한 보안 토큰 [!DNL Salesforce Service Cloud] 계정입니다. |
| `apiVersion` | (선택 사항) 의 REST API 버전 [!DNL Salesforce Service Cloud] 사용 중인 인스턴스. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Salesforce Service Cloud] 은(는) `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [이 Salesforce 서비스 클라우드 문서](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Salesforce Service Cloud] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for salesforce service cloud",
      "description": "Base connection for salesforce service cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
              "username": "acme-salesforce-service-cloud",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 매개변수 | 설명 |
| ---| --- |
| `auth.params.environmentUrl` | 의 URL [!DNL Salesforce Service Cloud] 인스턴스. |
| `auth.params.username` | 와(과) 연계된 사용자 이름 [!DNL Salesforce Service Cloud] 계정입니다. |
| `auth.params.password` | 과(와) 연계된 암호 [!DNL Salesforce Service Cloud] 계정입니다. |
| `auth.params.securityToken` | 와(과) 연결된 보안 토큰 [!DNL Salesforce Service Cloud] 계정입니다. |
| `connectionSpec.id` | 다음 [!DNL Salesforce Service Cloud] 연결 사양 ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

**응답**

응답이 성공하면 고유 식별자를 포함하여 새로 만든 연결이 반환됩니다(`id`). 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Salesforce Service Cloud] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 다음을 사용하여 고객 성공 데이터를 Platform으로 가져오기 [!DNL Flow Service] API](../../collect/customer-success.md)
