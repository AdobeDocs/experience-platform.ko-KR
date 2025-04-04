---
title: API를 사용하여 Google 광고를 Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google 광고에 연결하는 방법을 알아봅니다.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Google Ads]을(를) Experience Platform에 연결

>[!NOTE]
>
>[!DNL Google Ads] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Google Ads] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 자습서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Google Ads]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Google Ads] 원본 개요](../../../../connectors/advertising/ads.md)를 참조하세요.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 Google Ads 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

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
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

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
| `auth.params.clientCustomerID` | [!DNL Google Ads] 계정의 클라이언트 고객 ID. |
| `auth.params.loginCustomerID` | [!DNL Google Ads] 관리자 계정에 해당하는 로그인 고객 ID. |
| `auth.params.developerToken` | [!DNL Google Ads] 계정의 개발자 토큰입니다. |
| `auth.params.refreshToken` | [!DNL Google Ads] 계정의 새로 고침 토큰입니다. |
| `auth.params.clientID` | [!DNL Google Ads] 계정의 클라이언트 ID. |
| `auth.params.clientSecret` | [!DNL Google Ads] 계정의 클라이언트 암호입니다. |
| `auth.params.googleAdsApiVersion` | 사용 중인 [!DNL Google Ads] API 버전입니다. Experience Platform에서 지원되는 최신 버전은 `v17`입니다. |
| `connectionSpec.id` | [!DNL Google Ads] 연결 사양 ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 데이터 흐름을 만들어 광고 데이터 수집

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Google Ads] 기본 연결을 만들고 [!DNL Google Ads] 계정을 Experience Platform에 연결했습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 광고 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/advertising.md)
