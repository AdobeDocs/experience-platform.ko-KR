---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics;Dynamics
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Microsoft Dynamics 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Platform을 Microsoft Dynamics 계정에 연결하는 방법을 알아봅니다.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 4%

---

# 만들기 [!DNL Microsoft Dynamics] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Microsoft Dynamics] (이하 &quot;라고 한다)[!DNL Dynamics]&quot;) 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 다음을 사용하여 Platform을 Dynamics 계정에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 에 연결하려면 [!DNL Dynamics], 다음 연결 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `serviceUri` | 의 서비스 URL [!DNL Dynamics] 인스턴스. |
| `username` | 의 사용자 이름 [!DNL Dynamics] 사용자 계정입니다. |
| `password` | 에 대한 암호 [!DNL Dynamics] 계정입니다. |

>[!TAB 서비스 주체 및 키 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `servicePrincipalId` | 에 대한 클라이언트 ID [!DNL Dynamics] 계정입니다. 서비스 주체 및 키 기반 인증을 사용할 때 이 ID가 필요합니다. |
| `servicePrincipalKey` | 서비스 주체 비밀 키. 서비스 주체 및 키 기반 인증을 사용할 때 이 자격 증명이 필요합니다. |

>[!ENDTABS]

시작하기에 대한 자세한 내용은 [이 [!DNL Dynamics] 문서](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결을 만듭니다

>[!TIP]
>
>만든 후에는 의 인증 유형을 변경할 수 없습니다. [!DNL Dynamics] 기본 연결. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Dynamics] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

### 만들기 [!DNL Dynamics] 기본 연결

>[!TIP]
>
>만든 후에는 의 인증 유형을 변경할 수 없습니다. [!DNL Dynamics] 기본 연결. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

소스 연결을 만드는 첫 번째 단계는 [!DNL Dynamics] 소스 및 기본 연결 ID 생성. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Dynamics] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 기본 인증]

을(를) 만들려면 [!DNL Dynamics] 기본 인증을 사용하여 기본 연결, POST 요청 [!DNL Flow Service] 연결에 대한 값을 제공하는 동안 API `serviceUri`, `username`, 및 `password`.

+++요청

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | 와(과) 연결된 서비스 URI [!DNL Dynamics] 인스턴스. |
| `auth.params.username` | 와(과) 연계된 사용자 이름 [!DNL Dynamics] 계정입니다. |
| `auth.params.password` | 과(와) 연계된 암호 [!DNL Dynamics] 계정입니다. |
| `connectionSpec.id` | 다음 [!DNL Dynamics] 연결 사양 ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++응답

응답이 성공하면 고유 식별자를 포함하여 새로 만든 연결이 반환됩니다(`id`). 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 서비스 주체 키 기반 인증]

을(를) 만들려면 [!DNL Dynamics] POST 서비스 주체 키 기반 인증을 사용하는 기본 연결에서 [!DNL Flow Service] 연결에 대한 값을 제공하는 동안 API `serviceUri`, `servicePrincipalId`, 및 `servicePrincipalKey`.

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | 와(과) 연결된 서비스 URI [!DNL Dynamics] 인스턴스. |
| `auth.params.servicePrincipalId` | 에 대한 클라이언트 ID [!DNL Dynamics] 계정입니다. 서비스 주체 및 키 기반 인증을 사용할 때 이 ID가 필요합니다. |
| `auth.params.servicePrincipalKey` | 서비스 주체 비밀 키. 서비스 주체 및 키 기반 인증을 사용할 때 이 자격 증명이 필요합니다. |
| `connectionSpec.id` | 다음 [!DNL Dynamics] 연결 사양 ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++응답

응답이 성공하면 고유 식별자를 포함하여 새로 만든 연결이 반환됩니다(`id`). 이 ID는 다음 단계에서 CRM 시스템을 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## 다음 단계

이 자습서를 따라 [!DNL Microsoft Dynamics] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 CRM 데이터를 플랫폼으로 가져오는 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/crm.md)
