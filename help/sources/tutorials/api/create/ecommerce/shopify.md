---
keywords: Experience Platform;홈;인기 항목;Shopify;shopify;ecommerce
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Shopify 커넥터 기반 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Shopify를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Shopify] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Shopify]&#x200B;(이하 &quot;[!DNL Shopify]&quot;)에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Sources]](../../../../home.md): [!DNL Experience Platform]을(를) 사용하면 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Shopify]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Shopify]과(와) 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL Shopify] 서버의 끝점입니다. |
| `accessToken` | [!DNL Shopify] 사용자 계정의 액세스 토큰입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Shopify]의 연결 사양 ID는 `4f63aa36-bd48-4e33-bb83-49fbcd11c708`입니다. |

시작에 대한 자세한 내용은 이 [Shopify 인증 문서](https://shopify.dev/concepts/about-apis/authentication)를 참조하십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Shopify] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL Shopify]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Shopify] 서버의 끝점입니다. |
| `auth.params.accessToken` | [!DNL Shopify] 사용자 계정의 액세스 토큰입니다. |
| `connectionSpec.id` | [!DNL Shopify] 연결 사양 ID: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Shopify] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 E-Commerce 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/ecommerce.md)
