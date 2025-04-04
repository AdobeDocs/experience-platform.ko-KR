---
keywords: Experience Platform;홈;인기 항목;hubspot;Hubspot
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 HubSpot Base 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 HubSpot에 연결하는 방법에 대해 알아봅니다.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 [!DNL HubSpot] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL HubSpot]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL HubSpot]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL HubSpot]과(와) 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `clientId` | [!DNL HubSpot] 응용 프로그램과 연결된 클라이언트 ID입니다. |
| `clientSecret` | [!DNL HubSpot] 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `accessToken` | OAuth 통합을 처음 인증할 때 얻은 액세스 토큰입니다. |
| `refreshToken` | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL HubSpot]의 연결 사양 ID는 `cc6a4487-9e91-433e-a3a3-9cf6626c1806`입니다. |

시작에 대한 자세한 내용은 이 [HubSpot 문서](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)를 참조하세요.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL HubSpot] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL HubSpot]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.clientId` | [!DNL HubSpot] 응용 프로그램과 연결된 클라이언트 ID입니다. |
| `auth.params.clientSecret` | [!DNL HubSpot] 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `auth.params.accessToken` | OAuth 통합을 처음 인증할 때 얻은 액세스 토큰입니다. |
| `auth.params.refreshToken` | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰. |
| `connectionSpec.id` | [!DNL HubSpot] 연결 사양 ID: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL HubSpot] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 마케팅 자동화 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/marketing-automation.md)
