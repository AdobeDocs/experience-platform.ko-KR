---
keywords: Experience Platform;홈;인기 항목;google 광고;Google 광고;google 광고;광고
title: Flow Service API를 사용하여 Google Ads 기본 연결 만들기
description: Flow Service API를 사용하여 Adobe Experience Platform을 Google Ads에 연결하는 방법을 알아봅니다.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# 를 사용하여 Google Ads 기본 연결 만들기 [!DNL Flow Service] API

>[!NOTE]
>
>Google 광고 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음을 사용하여 Google Ads용 기본 연결을 만드는 단계를 안내합니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 사용하여 Google 광고에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] Google Ads와 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `clientCustomerId` | 클라이언트 고객 ID는 Google 광고 API를 사용하여 관리하려는 Google Ads 클라이언트 계정에 해당하는 계정 번호입니다. 이 ID는 `123-456-7890`. |
| `developerToken` | 개발자 토큰을 사용하면 Google 광고 API에 액세스할 수 있습니다. 동일한 개발자 토큰을 사용하여 모든 Google 광고 계정에 대해 요청을 수행할 수 있습니다. 다음 방법으로 개발자 토큰을 검색합니다. [manager 계정에 로그인](https://ads.google.com/home/tools/manager-accounts/) 그런 다음 [!DNL API Center] 페이지. |
| `refreshToken` | 새로 고침 토큰은 [!DNL OAuth2] 인증. 이 토큰을 사용하면 액세스 토큰이 만료된 후 다시 생성할 수 있습니다. |
| `clientId` | 클라이언트 ID는 의 일부로 클라이언트 암호와 함께 사용됩니다 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 함께 사용하면 애플리케이션을 Google에 식별하여 계정을 대신하여 애플리케이션이 작동할 수 있습니다. |
| `clientSecret` | 클라이언트 암호는 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 함께 사용하면 애플리케이션을 Google에 식별하여 계정을 대신하여 애플리케이션이 작동할 수 있습니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. Google 광고에 대한 연결 사양 ID는 다음과 같습니다. `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

에 대한 API 개요 문서를 참조하십시오 [Google 광고 시작에 대한 자세한 정보](https://developers.google.com/google-ads/api/docs/first-call/overview).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 요청 매개 변수의 일부로 Google 광고 인증 자격 증명을 제공하는 중 종단점입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 Google 광고에 대한 기본 연결을 만듭니다.

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
| `auth.params.clientCustomerID` | Google 광고 계정의 클라이언트 고객 ID. |
| `auth.params.developerToken` | Google 광고 계정의 개발자 토큰입니다. |
| `auth.params.refreshToken` | Google 광고 계정의 새로 고침 토큰. |
| `auth.params.clientID` | Google 광고 계정의 클라이언트 ID입니다. |
| `auth.params.clientSecret` | Google 광고 계정의 클라이언트 암호입니다. |
| `connectionSpec.id` | Google Ads 연결 사양 ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 사용하여 Google Ads 기본 연결을 만들었습니다 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름 을 만들어 [!DNL Flow Service] API](../../collect/advertising.md)
