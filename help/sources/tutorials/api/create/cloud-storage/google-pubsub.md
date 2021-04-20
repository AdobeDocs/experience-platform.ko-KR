---
keywords: Experience Platform;홈;인기 항목;Google PubSub;google pubsub
solution: Experience Platform
title: Flow Service API를 사용하여 Google PubSub 소스 연결 만들기
topic: overview
type: Tutorial
description: Flow Service API를 사용하여 Google PubSub 계정에 Adobe Experience Platform을 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---


# Flow Service API를 사용하여 [!DNL Google PubSub] 소스 연결 만들기

>[!NOTE]
>
>[!DNL Google PubSub] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)을 사용하여 [!DNL Google PubSub](이하 &quot;[!DNL PubSub]&quot;라 함)을 Adobe Experience Platform에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL PubSub] 소스 연결을 성공적으로 만들기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL PubSub]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `projectId` | [!DNL PubSub] 인증에 필요한 프로젝트 ID. |
| `credentials` | [!DNL PubSub] 인증에 필요한 자격 증명 또는 키 |

이러한 값에 대한 자세한 내용은 다음 [PubSub 인증](https://cloud.google.com/pubsub/docs/authentication) 문서를 참조하십시오. 서비스 계정 기반 인증을 사용하는 경우 자격 증명을 생성하는 방법에 대한 자세한 내용은 다음 [PubSub 안내서](https://cloud.google.com/docs/authentication/production#create_service_account)를 참조하십시오.

>[!TIP]
>
>서비스 계정 기반 인증을 사용하는 경우 자격 증명을 복사하고 붙여넣을 때 서비스 계정에 충분한 사용자 액세스 권한을 부여했는지, JSON에 추가 공백이 없는지 확인하십시오.

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

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 데이터 흐름을 만드는 데 사용할 수 있으므로 [!DNL PubSub] 계정당 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL PubSub] 연결을 만들려면 공급자 ID 및 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. 공급자 ID는 `521eee4d-8cbe-4906-bb48-fb6bd4450033`이고 연결 사양 ID는 `70116022-a743-464a-bbfe-e226a7f8210c`입니다.

**API 형식**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.projectId` | [!DNL PubSub] 인증에 필요한 프로젝트 ID. |
| `auth.params.credentials` | [!DNL PubSub] 인증에 필요한 자격 증명 또는 키 |
| `connectionSpec.id` | [!DNL PubSub] 연결 사양 ID:`70116022-a743-464a-bbfe-e226a7f8210c`. |

**응답**

성공적으로 응답하면 새로 만든 [!DNL PubSub] 연결의 연결 ID가 반환됩니다. 다음 튜토리얼에서 클라우드 스토리지 데이터를 살펴보려면 이 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL PubSub] 연결을 만들고 고유한 연결 ID를 얻었습니다. 이 연결 ID를 사용하여 Flow Service API](../../collect/streaming.md)를 사용하여 스트리밍 데이터를 수집할 수 있습니다.[
