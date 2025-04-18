---
keywords: Experience Platform;홈;인기 항목;servicenow;ServiceNow
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 ServiceNow Base 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 ServiceNow 서버에 연결하는 방법을 알아봅니다.
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 [!DNL ServiceNow] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Google ServiceNow]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL ServiceNow] 서버에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL ServiceNow]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow] 서버의 끝점입니다. |
| `username` | 인증을 위해 [!DNL ServiceNow] 서버에 연결하는 데 사용되는 사용자 이름입니다. |
| `password` | 인증을 위해 [!DNL ServiceNow] 서버에 연결할 암호입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL ServiceNow]의 연결 사양 ID는 `eb13cb25-47ab-407f-ba89-c0125281c563`입니다. |

시작하는 방법에 대한 자세한 내용은 [이 ServiceNow 문서](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)를 참조하세요.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL ServiceNow] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL ServiceNow]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `auth.params.server` | [!DNL ServiceNow] 서버의 끝점입니다. |
| `auth.params.username` | 인증을 위해 [!DNL ServiceNow] 서버에 연결하는 데 사용되는 사용자 이름입니다. |
| `auth.params.password` | 인증을 위해 [!DNL ServiceNow] 서버에 연결할 암호입니다. |
| `connectionSpec.id` | [!DNL ServiceNow] 연결 사양 ID: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결이 반환됩니다. 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL ServiceNow] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 고객 성공 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/customer-success.md)
