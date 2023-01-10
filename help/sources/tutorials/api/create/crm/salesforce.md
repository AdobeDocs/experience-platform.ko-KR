---
keywords: Experience Platform;홈;인기 항목;Salesforce;salesforce
solution: Experience Platform
title: Flow Service API를 사용하여 Salesforce 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Salesforce 계정에 연결하는 방법을 알아봅니다.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# 만들기 [!DNL Salesforce] 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Salesforce] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Platform] 변환 후 [!DNL Salesforce] 계정을 사용하여 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 에 연결 [!DNL Salesforce]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `environmentUrl` | 의 URL입니다 [!DNL Salesforce] 소스 인스턴스. |
| `username` | 사용자 이름 [!DNL Salesforce] 사용자 계정. |
| `password` | 의 암호 [!DNL Salesforce] 사용자 계정. |
| `securityToken` | 에 대한 보안 토큰 [!DNL Salesforce] 사용자 계정. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL AdWords] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

시작하는 방법에 대한 자세한 내용은 [이 Salesforce 문서](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Salesforce] 요청 매개 변수의 일부로 인증 자격 증명.


**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Salesforce]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.username` | 사용자 이름과 연결된 사용자 이름 [!DNL Salesforce] 계정이 필요합니다. |
| `auth.params.password` | 와 연결된 암호 [!DNL Salesforce] 계정이 필요합니다. |
| `auth.params.securityToken` | 와 연결된 보안 토큰 [!DNL Salesforce] 계정이 필요합니다. |
| `connectionSpec.id` | 다음 [!DNL Salesforce] 연결 사양 ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**응답**

성공적인 응답은 해당 고유 식별자( )를 포함하여 새로 생성된 연결을 반환합니다`id`). 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Salesforce] 기본 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름 을 만들어 [!DNL Flow Service] API](../../collect/crm.md)
