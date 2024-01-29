---
title: 흐름 서비스 API를 사용하여 Salesforce Marketing Cloud 기반 연결 만들기
description: 흐름 서비스 API를 사용하여 Experience Platform에 대해 Salesforce Marketing Cloud 계정을 인증하는 방법을 알아봅니다.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 5bb95c2823ce7baa09cbc84c2f1ccf70a0796549
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 4%

---

# 만들기 [!DNL Salesforce Marketing Cloud] 를 사용한 기본 연결 [!DNL Flow Service] API

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 소스 통합.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Salesforce Marketing Cloud] 사용 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Salesforce Marketing Cloud] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Salesforce Marketing Cloud], 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 응용 프로그램의 호스트 서버입니다. 이는 종종 하위 도메인입니다. **참고:** 을(를) 입력할 때 `host` 값, 다음을 지정해야 합니다. `{subdomain}.rest.marketingcloudapis.com`. 예를 들어 호스트 URL이 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`를 선택한 다음 입력하기만 하면 됩니다. `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` 을 호스트 값으로 사용하십시오. |
| `clientId` | 와 연결된 클라이언트 ID [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `clientSecret` | 와(과) 연결된 클라이언트 암호 [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Salesforce Marketing Cloud] 은(는) `ea1c2a08-b722-11eb-8529-0242ac130003`. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Salesforce Marketing Cloud] 문서](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Salesforce Marketing Cloud] 요청 본문의 일부인 인증 자격 증명입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.clientId` | 와 연결된 클라이언트 ID [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `auth.params.clientSecret` | 와(과) 연결된 클라이언트 암호 [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `connectionSpec.id` | 다음 [!DNL Salesforce Marketing Cloud] 연결 사양 ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**응답**

성공한 응답은 고유 연결 식별자( )를 포함하여 새로 생성된 연결을 반환합니다.`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Salesforce Marketing Cloud] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 마케팅 자동화 데이터를 플랫폼으로 가져오기 위한 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/marketing-automation.md)
