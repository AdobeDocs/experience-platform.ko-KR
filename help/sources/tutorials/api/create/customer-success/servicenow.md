---
keywords: Experience Platform;홈;인기 항목;servicenow;ServiceNow
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 ServiceNow Base 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 ServiceNow 서버에 연결하는 방법을 알아봅니다.
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 만들기 [!DNL ServiceNow] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Google ServiceNow] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL ServiceNow] 를 사용하는 서버 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 에 연결하려면 [!DNL ServiceNow], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `endpoint` | 의 엔드포인트 [!DNL ServiceNow] 서버입니다. |
| `username` | 에 연결하는 데 사용된 사용자 이름 [!DNL ServiceNow] 인증용 서버입니다. |
| `password` | 에 연결할 암호 [!DNL ServiceNow] 인증용 서버입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL ServiceNow] 은(는) `eb13cb25-47ab-407f-ba89-c0125281c563`. |

시작하기에 대한 자세한 내용은 을(를) 참조하십시오. [이 ServiceNow 문서](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL ServiceNow] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL ServiceNow]:

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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.server` | 의 엔드포인트 [!DNL ServiceNow] 서버입니다. |
| `auth.params.username` | 에 연결하는 데 사용된 사용자 이름 [!DNL ServiceNow] 인증용 서버입니다. |
| `auth.params.password` | 에 연결할 암호 [!DNL ServiceNow] 인증용 서버입니다. |
| `connectionSpec.id` | 다음 [!DNL ServiceNow] 연결 사양 ID: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**응답**

응답이 성공하면 고유 식별자를 포함하여 새로 만든 연결이 반환됩니다(`id`). 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL ServiceNow] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 다음을 사용하여 고객 성공 데이터를 Platform으로 가져오기 [!DNL Flow Service] API](../../collect/customer-success.md)
