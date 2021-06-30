---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Flow Service API를 사용하여 Microsoft Dynamics Base 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Platform을 Microsoft Dynamics 계정에 연결하는 방법을 알아봅니다.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 8035539321f5016521208aa110a4ee2881cb5d1e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Microsoft Dynamics] 기본 연결을 만듭니다

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 [!DNL Microsoft Dynamics](이하 &quot;[!DNL Dynamics]&quot;라 함)에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 Dynamics 계정에 Platform을 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이 [!DNL Dynamics]에 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics] 인스턴스의 서비스 URL입니다. |
| `username` | [!DNL Dynamics] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Dynamics] 계정의 암호입니다. |
| `servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID입니다. 이 ID는 서비스 보안 주체 및 키 기반 인증을 사용할 때 필요합니다. |
| `servicePrincipalKey` | 서비스 주 비밀 키입니다. 이 자격 증명은 서비스 주 및 키 기반 인증을 사용할 때 필요합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL Dynamics]에 대한 연결 사양 ID는 다음과 같습니다.`38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

시작하는 방법에 대한 자세한 내용은 [이 [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)를 참조하십시오.

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL Dynamics] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

### 기본 인증을 사용하여 [!DNL Dynamics] 기본 연결 만들기

기본 인증을 사용하여 [!DNL Dynamics] 기본 연결을 만들려면 연결의 `serviceUri`, `username` 및 `password` 값을 제공하는 동안 [!DNL Flow Service] API에 POST 요청을 수행하십시오.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.serviceUri` | [!DNL Dynamics] 인스턴스와 연결된 서비스 URI입니다. |
| `auth.params.username` | [!DNL Dynamics] 계정과 연결된 사용자 이름입니다. |
| `auth.params.password` | [!DNL Dynamics] 계정에 연결된 암호입니다. |
| `connectionSpec.id` | [!DNL Dynamics] 연결 사양 ID:`38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결을 반환합니다. 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 서비스 사용자 키 기반 인증을 사용하여 [!DNL Dynamics] 기본 연결을 만듭니다

서비스 사용자 키 기반 인증을 사용하여 [!DNL Dynamics] 기본 연결을 만들려면 연결의 `serviceUri`, `servicePrincipalId` 및 `servicePrincipalKey` 값을 제공하는 동안 [!DNL Flow Service] API에 POST 요청을 수행하십시오.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.serviceUri` | [!DNL Dynamics] 인스턴스와 연결된 서비스 URI입니다. |
| `auth.params.servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID입니다. 이 ID는 서비스 보안 주체 및 키 기반 인증을 사용할 때 필요합니다. |
| `auth.params.servicePrincipalKey` | 서비스 주 비밀 키입니다. 이 자격 증명은 서비스 주 및 키 기반 인증을 사용할 때 필요합니다. |
| `connectionSpec.id` | [!DNL Dynamics] 연결 사양 ID:`38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결을 반환합니다. 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL Dynamics] 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 [흐름 서비스 API](../../explore/crm.md)를 사용하여 CRM 시스템을 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
