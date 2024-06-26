---
keywords: Experience Platform;홈;인기 항목;사각형;사각형
title: 흐름 서비스 API를 사용하여 사각형 기반 연결 만들기
description: 흐름 서비스 API를 사용하여 Square를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 만들기 [!DNL Square] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Square] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Square] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Square], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `host` | 의 URL [!DNL Square] 인스턴스. |
| `clientId` | 와 연결된 클라이언트 ID [!DNL Square] 계정입니다. |
| `clientSecret` | 와(과) 연결된 클라이언트 암호 [!DNL Square] 계정입니다. |
| `accessToken` | 액세스 토큰은 다음을 인증하는 데 사용됩니다. [!DNL Square] OAuth 2.0 인증을 사용하는 계정입니다. 액세스 토큰은에서 가져올 수 있습니다. [!DNL Square]. |
| `refreshToken` | 새로 고침 토큰은 현재 액세스 토큰이 만료되면 새 액세스 토큰을 생성하는 데 사용됩니다. 새로 고침 토큰은에서 가져올 수 있습니다. [!DNL Square]. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Square] 은(는) `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

이러한 자격 증명과 자격 증명을 얻는 방법에 대한 자세한 내용은 [[!DNL Square] oauth에 대한 설명서](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Square] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.host` | 의 URL [!DNL Square] 인스턴스. |
| `auth.params.clientId` | 와 연결된 클라이언트 ID [!DNL Square] 계정입니다. |
| `auth.params.clientSecret` | 와(과) 연결된 클라이언트 암호 [!DNL Square] 계정입니다. |
| `auth.params.accessToken` | 액세스 토큰은 다음을 인증하는 데 사용됩니다. [!DNL Square] OAuth 2.0 인증을 사용하는 계정입니다. 액세스 토큰은에서 가져올 수 있습니다. [!DNL Square]. |
| `auth.params.refreshToken` | 새로 고침 토큰은 현재 액세스 토큰이 만료되면 새 액세스 토큰을 생성하는 데 사용됩니다. 새로 고침 토큰은에서 가져올 수 있습니다. [!DNL Square]. |
| `connectionSpec.id` | 다음 [!DNL Square] 연결 사양 ID: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**응답**

성공한 응답은 고유 연결 식별자( )를 포함하여 새로 생성된 연결을 반환합니다.`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Square] 을 사용한 연결 [!DNL Flow Service] API이며 연결의 고유 ID 값을 가져왔습니다. 다음 자습서에서 이 ID를 사용하여 다음 방법을 배울 수 있습니다 [흐름 서비스 API를 사용하여 결제 애플리케이션 탐색](../../explore/payments.md).
