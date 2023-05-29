---
title: 흐름 서비스 API를 사용하여 Google Ads Base 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google 광고에 연결하는 방법을 알아봅니다.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 를 사용하여 Google 광고 기본 연결 만들기 [!DNL Flow Service] API

>[!NOTE]
>
>Google Ads 소스는 Beta 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 튜토리얼에서는 다음을 사용하여 Google Ads에 대한 기본 연결을 만드는 단계를 설명합니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 사용하여 Google Ads에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] Google Ads와 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `clientCustomerId` | 클라이언트 고객 ID는 Google Ads API로 관리하려는 Google Ads 클라이언트 계정에 해당하는 계정 번호입니다. 이 ID는 의 템플릿을 따릅니다. `123-456-7890`. |
| `loginCustomerId` | 로그인 고객 ID는 Google Ads Manager 계정에 해당하는 계정 번호이며 특정 운영 고객으로부터 보고서 데이터를 가져오는 데 사용됩니다. 로그인 고객 ID에 대한 자세한 내용은 [Google Ads API 설명서](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| `developerToken` | 개발자 토큰을 사용하면 Google Ads API에 액세스할 수 있습니다. 동일한 개발자 토큰을 사용하여 모든 Google Ads 계정에 대해 요청할 수 있습니다. 다음 방법으로 개발자 토큰 검색 [manager 계정에 로그인](https://ads.google.com/home/tools/manager-accounts/) 다음 위치로 이동 [!DNL API Center] 페이지를 가리키도록 업데이트하는 중입니다. |
| `refreshToken` | 새로 고침 토큰은 [!DNL OAuth2] 인증. 이 토큰을 사용하면 액세스 토큰이 만료된 후 다시 생성할 수 있습니다. |
| `clientId` | 클라이언트 ID는 클라이언트 암호와 함께 의 일부로 사용됩니다 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 사용하면 Google에 대한 애플리케이션을 식별하여 애플리케이션이 계정을 대신하여 작동할 수 있습니다. |
| `clientSecret` | 클라이언트 암호는 클라이언트 ID와 함께 의 일부로 사용됩니다 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 사용하면 Google에 대한 애플리케이션을 식별하여 애플리케이션이 계정을 대신하여 작동할 수 있습니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. Google 광고의 연결 사양 ID는 다음과 같습니다. `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

다음에 대한 API 개요 문서 읽기 [Google 광고 시작하기에 대한 자세한 정보](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 요청 매개 변수의 일부로 Google Ads 인증 자격 증명을 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 Google Ads에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Google 광고 계정의 클라이언트 고객 ID입니다. |
| `auth.params.loginCustomerID` | Google Ads Manager 계정에 해당하는 로그인 고객 ID입니다. |
| `auth.params.developerToken` | Google Ads 계정의 개발자 토큰. |
| `auth.params.refreshToken` | Google Ads 계정의 새로 고침 토큰입니다. |
| `auth.params.clientID` | Google 광고 계정의 클라이언트 ID입니다. |
| `auth.params.clientSecret` | Google 광고 계정의 클라이언트 암호입니다. |
| `connectionSpec.id` | Google Ads 연결 사양 ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다(`id`). 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 자습서에 따라 를 사용하여 Google Ads 기본 연결을 만들었습니다. [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [를 사용하여 광고 데이터를 플랫폼으로 가져오기 위한 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/advertising.md)
