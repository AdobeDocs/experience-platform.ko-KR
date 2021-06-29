---
keywords: Experience Platform;홈;인기 항목;veva crm;Vevar CRM;Vevar;
solution: Experience Platform
title: Flow Service API를 사용하여 Vec CRM 기본 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Vec CRM에 연결하는 방법을 알아봅니다.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 9bd241d5f986759268edd072cee72d02f40f858f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# (베타) [!DNL Flow Service] API를 사용하여 [!DNL Veeva CRM] 기본 연결을 만듭니다

>[!NOTE]
>
>[!DNL Veeva CRM] 소스가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 를 참조하십시오.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 [!DNL Veeva CRM]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Veeva CRM]에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이 [!DNL Veeva CRM]과 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM] 인스턴스의 URL입니다. |
| `username` | [!DNL Veeva CRM] 계정의 사용자 이름 값입니다. |
| `password` | [!DNL Veeva CRM] 계정의 암호 값입니다. |
| `securityToken` | [!DNL Veeva CRM] 인스턴스에 대한 보안 토큰입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL Veeva CRM]에 대한 연결 사양 ID는 다음과 같습니다.`fcad62f3-09b0-41d3-be11-449d5a621b69`. |

이러한 값에 대한 자세한 내용은 이 [[!DNL Veeva CRM] document](https://developer.veevacrm.com/api/#order-management-rest-api)를 참조하십시오.

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL Veeva CRM] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Veeva CRM]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `name` | [!DNL Veeva CRM] 기본 연결의 이름입니다. 이 이름을 사용하여 [!DNL Veeva CRM] 기본 연결을 조회할 수 있습니다. |
| `description` | [!DNL Veeva CRM] 기본 연결에 대한 선택적 설명입니다. |
| `auth.specName` | 연결에 사용되는 인증 유형입니다. |
| `auth.params.environmentUrl` | [!DNL Veeva CRM] 인스턴스의 URL입니다. |
| `auth.params.username` | [!DNL Veeva CRM] 계정의 사용자 이름 값입니다. |
| `auth.params.password` | [!DNL Veeva CRM] 계정의 암호 값입니다. |
| `auth.params.securityToken` | [!DNL Veeva CRM] 인스턴스에 대한 보안 토큰입니다. |
| `connectionSpec.id` | [!DNL Veeva CRM]에 대한 연결 사양 ID:`fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다. 이 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 자습서에 따르면 [!DNL Flow Service] API를 사용하여 [!DNL Veeva CRM] 기본 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 [흐름 서비스 API](../../explore/crm.md)를 사용하여 CRM 시스템을 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
