---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Flow Service API를 사용하여 Microsoft Dynamics 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 플랫폼을 Microsoft Dynamics 계정에 연결하는 방법을 알아봅니다.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Microsoft Dynamics] 소스 연결 만들기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 [!DNL Flow Service] API를 사용하여 Flow Service API를 사용하여 [!DNL Microsoft Dynamics](이하 &quot;Dynamics&quot;) 계정에 플랫폼을 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 플랫폼을 Dynamics 계정에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Dynamics]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics] 인스턴스의 서비스 URL입니다. |
| `username` | [!DNL Dynamics] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Dynamics] 계정의 암호입니다. |
| `servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID. 이 ID는 서비스 주체와 키 기반 인증을 사용할 때 필요합니다. |
| `servicePrincipalKey` | 서비스 주체 비밀 키입니다. 이 자격 증명은 서비스 주체 및 키 기반 인증을 사용하는 경우에 필요합니다. |

시작하는 방법에 대한 자세한 내용은 [이 [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)를 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 데이터 흐름을 만드는 데 사용할 수 있으므로 [!DNL Dynamics] 계정당 하나의 연결만 필요합니다.

### 기본 인증을 사용하여 [!DNL Dynamics] 연결 만들기

기본 인증을 사용하여 [!DNL Dynamics] 연결을 만들려면 `serviceUri`, `username` 및 `password` 연결에 대한 값을 제공하면서 [!DNL Flow Service] API에 POST 요청을 하십시오.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL Dynamics] 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. [!DNL Dynamics]에 대한 연결 사양 ID는 `38ad80fe-8b06-4938-94f4-d4ee80266b07`입니다.

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
| `auth.params.password` | [!DNL Dynamics] 계정과 연결된 암호입니다. |
| `connectionSpec.id` | 이전 단계에서 검색된 [!DNL Dynamics] 계정의 연결 사양 `id`입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 서비스 주체 키 기반 인증을 사용하여 [!DNL Dynamics] 연결 만들기

서비스 주체 키 기반 인증을 사용하여 [!DNL Dynamics] 연결을 만들려면 [!DNL Flow Service] API에 POST 요청을 하고 연결의 `serviceUri`, `servicePrincipalId` 및 `servicePrincipalKey`에 대한 값을 제공합니다.

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
| `auth.params.servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID. 이 ID는 서비스 주체와 키 기반 인증을 사용할 때 필요합니다. |
| `auth.params.servicePrincipalKey` | 서비스 주체 비밀 키입니다. 이 자격 증명은 서비스 주체 및 키 기반 인증을 사용하는 경우에 필요합니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL Dynamics] 연결을 만들고 연결의 고유 ID 값을 받았습니다. 이 ID는 다음 튜토리얼에서 Flow Service API](../../explore/crm.md)를 사용하여 [CRM 시스템을 탐색하는 방법을 학습할 때 사용할 수 있습니다.
