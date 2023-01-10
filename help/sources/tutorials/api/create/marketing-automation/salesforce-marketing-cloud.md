---
keywords: Experience Platform;홈;인기 항목;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Flow Service API를 사용하여 Salesforce Marketing Cloud 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Salesforce Marketing Cloud에 연결하는 방법을 알아봅니다.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# 만들기 [!DNL Salesforce Marketing Cloud] 기본 연결 [!DNL Flow Service] API

>[!NOTE]
>
>다음 [!DNL Salesforce Marketing Cloud] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Salesforce Marketing Cloud] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 데이터를 다양한 소스에서 수집할 수 있으며 를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공할 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 파티션으로 분할하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

다음 섹션에서는 다음에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Salesforce Marketing Cloud] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Salesforce Marketing Cloud], 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 애플리케이션의 호스트 서버입니다. 종종 하위 도메인입니다. **참고:** 을 입력할 때 `host` 값은 전체 URL이 아니라 하위 도메인만 지정해야 합니다. 예를 들어 호스트 URL이 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`를 입력한 다음 을(를) 입력하기만 하면 됩니다 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 를 호스트 값으로 사용할 수 있습니다. |
| `clientId` | 와 연결된 클라이언트 ID [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `clientSecret` | 와 연결된 클라이언트 암호입니다. [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Salesforce Marketing Cloud] is: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

시작하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Salesforce Marketing Cloud] 문서](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Salesforce Marketing Cloud] 요청 본문의 일부로 인증 자격 증명.

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
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
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
| `auth.params.clientSecret` | 와 연결된 클라이언트 암호입니다. [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `connectionSpec.id` | 다음 [!DNL Salesforce Marketing Cloud] 연결 사양 ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**응답**

성공적인 응답은 해당 고유 연결 식별자(`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Salesforce Marketing Cloud] 기본 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 다음을 사용하여 마케팅 자동화 데이터를 Platform으로 가져오기 [!DNL Flow Service] API](../../collect/marketing-automation.md)
