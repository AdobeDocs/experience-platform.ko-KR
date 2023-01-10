---
keywords: Experience Platform;홈;인기 항목;Google PubSub;google pubsub
solution: Experience Platform
title: Flow Service API를 사용하여 Google PubSub Source 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Google PubSub 계정에 연결하는 방법을 알아봅니다.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# 만들기 [!DNL Google PubSub] Flow Service API를 사용한 소스 연결

이 자습서에서는 연결하는 단계를 안내합니다 [!DNL Google PubSub] (이하 &quot;라 한다)[!DNL PubSub]&quot;)를 사용하여 Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL PubSub] 를 사용하여 플랫폼 구현 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 에 연결 [!DNL PubSub]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `projectId` | 인증하는 데 필요한 프로젝트 ID [!DNL PubSub]. |
| `credentials` | 인증에 필요한 자격 증명 또는 키 [!DNL PubSub]. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 타겟 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 다음 [!DNL PubSub] 연결 사양 ID는 다음과 같습니다. `70116022-a743-464a-bbfe-e226a7f8210c`. |

이러한 값에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL PubSub] 인증](https://cloud.google.com/pubsub/docs/authentication) 문서. 서비스 계정 기반 인증을 사용하려면 다음을 참조하십시오 [[!DNL PubSub] 서비스 계정 생성 가이드](https://cloud.google.com/docs/authentication/production#create_service_account) 을 참조하십시오.

>[!TIP]
>
>서비스 계정 기반 인증을 사용 중인 경우, 자격 증명을 복사하여 붙여넣을 때 서비스 계정에 대한 충분한 사용자 액세스 권한을 부여했는지 및 JSON에 추가 공백이 없는지 확인하십시오.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

소스 연결을 만드는 첫 번째 단계는 [!DNL PubSub] 소스 및 기본 연결 ID를 생성합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고, 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL PubSub] 요청 매개 변수의 일부로 인증 자격 증명.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
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
| `auth.params.projectId` | 인증하는 데 필요한 프로젝트 ID [!DNL PubSub]. |
| `auth.params.credentials` | 인증에 필요한 자격 증명 또는 키 [!DNL PubSub]. |
| `connectionSpec.id` | 다음 [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다`id`). 이 기본 연결 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 소스 연결 만들기 {#source}

소스 연결은 데이터를 수집하는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 흐름을 만드는 데 필요한 데이터 소스, 데이터 형식 및 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 IMS 조직에 따라 다릅니다.

소스 연결을 만들려면 `/sourceConnections` 의 끝점 [!DNL Flow Service] API.

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 포함하도록 제공할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 사용자의 기본 연결 ID입니다 [!DNL PubSub] 이전 단계에서 생성된 소스. |
| `connectionSpec.id` | 에 대한 고정 연결 사양 ID [!DNL PubSub]. 이 ID는 다음과 같습니다. `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 의 형식 [!DNL PubSub] 수집할 데이터입니다. 현재 지원되는 데이터 형식은 `json`. |
| `params.topicId` | 항목 ID는 게시자가 메시지를 보내는 특정 명명된 리소스를 정의합니다 |
| `params.subscriptionId` | 구독 ID는 구독 애플리케이션에 전달될 단일 특정 항목의 메시지 스트림을 나타내는 특정 명명된 리소스를 정의합니다. |
| `params.dataType` | 이 매개 변수는 수집할 데이터의 유형을 정의합니다. 지원되는 데이터 유형은 다음과 같습니다. `raw` 및 `xdm`. |

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 데이터 흐름을 만들려면 다음 자습서에서 필요합니다.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL PubSub] 소스 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 소스 연결 ID를 사용하여 다음을 수행할 수 있습니다 [를 사용하여 스트리밍 데이터 흐름 만들기 [!DNL Flow Service] API](../../collect/streaming.md).
