---
keywords: Experience Platform;홈;인기 항목;Zoho CRM;Zoho CRM;Zoho;Zoho
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Zoho CRM 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Zoho CRM에 연결하는 방법을 알아봅니다.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# 만들기 [!DNL Zoho CRM] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Zoho CRM] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Zoho CRM] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Zoho CRM], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `endpoint` | 의 엔드포인트 [!DNL Zoho CRM] 요청을 수행하는 서버입니다. |
| `accountsUrl` | 계정 URL은 액세스 및 새로 고침 토큰을 생성하는 데 사용됩니다. URL은 도메인별 URL이어야 합니다. |
| `clientId` | 에 해당하는 클라이언트 ID [!DNL Zoho CRM] 사용자 계정입니다. |
| `clientSecret` | 에 해당하는 클라이언트 암호 [!DNL Zoho CRM] 사용자 계정입니다. |
| `accessToken` | 액세스 토큰은 보안 및 임시 액세스 권한을 부여합니다. [!DNL Zoho CRM] 계정입니다. |
| `refreshToken` | 새로 고침 토큰은 액세스 토큰이 만료된 후 새 액세스 토큰을 생성하는 데 사용되는 토큰입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Zoho CRM] 은(는) `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

이러한 자격 증명에 대한 자세한 내용은 [[!DNL Zoho CRM] 인증](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Zoho CRM] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```https
POST /connections
```

**요청**

>[!TIP]
>
>계정 URL 도메인은 적절한 도메인 위치와 일치해야 합니다. 다음은 다양한 도메인과 해당 계정 URL입니다.<ul><li>미국: https://accounts.zoho.com</li><li>오스트레일리아: https://accounts.zoho.com.au</li><li>유럽: https://accounts.zoho.eu</li><li>인도: https://accounts.zoho.in</li><li>중국: https://accounts.zoho.com.cn</li></ul>

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| 매개변수 | 설명 |
| --- | --- |
| `name` | 의 이름 [!DNL Zoho CRM] 기본 연결. 이 이름을 사용하여 [!DNL Zoho CRM] 기본 연결. |
| `description` | 다음에 대한 선택적 설명 [!DNL Zoho CRM] 기본 연결. |
| `auth.specName` | 연결에 사용되는 인증 유형입니다. |
| `auth.params.endpoint` | 의 엔드포인트 [!DNL Zoho CRM] 요청을 수행하는 서버입니다. |
| `auth.params.accountsUrl` | 계정 URL은 액세스 및 새로 고침 토큰을 생성하는 데 사용됩니다. URL은 도메인별 URL이어야 합니다. |
| `auth.params.clientId` | 에 해당하는 클라이언트 ID [!DNL Zoho CRM] 사용자 계정입니다. |
| `auth.params.clientSecret` | 에 해당하는 클라이언트 암호 [!DNL Zoho CRM] 사용자 계정입니다. |
| `auth.params.accessToken` | 액세스 토큰은 보안 및 임시 액세스 권한을 부여합니다. [!DNL Zoho CRM] 계정입니다. |
| `auth.params.refreshToken` | 새로 고침 토큰은 액세스 토큰이 만료된 후 새 액세스 토큰을 생성하는 데 사용되는 토큰입니다. |
| `connectionSpec.id` | 에 대한 연결 사양 ID [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다(`id`). 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Zoho] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 CRM 데이터를 플랫폼으로 가져오는 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/crm.md)
