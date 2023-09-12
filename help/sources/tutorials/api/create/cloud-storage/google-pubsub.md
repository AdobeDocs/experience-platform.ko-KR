---
title: 흐름 서비스 API를 사용하여 Google PubSub 소스 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google PubSub 계정에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b157b9147d8ea8100bcaedca272b303a3c04e71a
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# 만들기 [!DNL Google PubSub] 흐름 서비스 API를 사용한 소스 연결

>[!IMPORTANT]
>
>다음 [!DNL Google PubSub] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

이 자습서에서는 연결하는 단계를 안내합니다 [!DNL Google PubSub] (이하 &quot;라고 한다)[!DNL PubSub]&quot;) Experience Platform 대상, 사용 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션은 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL PubSub] 를 사용하여 플랫폼으로 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 에 연결하려면 [!DNL PubSub], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `projectId` | 인증에 필요한 프로젝트 ID [!DNL PubSub]. |
| `credentials` | 인증에 필요한 자격 증명 [!DNL PubSub]. 자격 증명에서 공백을 제거한 후 전체 JSON 파일을 넣었는지 확인해야 합니다. |
| `topicName` | 메시지 피드를 나타내는 리소스의 이름입니다. 의 특정 데이터 스트림에 대한 액세스 권한을 제공하려면 항목 이름을 지정해야 합니다 [!DNL PubSub] 소스. 주제 이름 형식은 다음과 같습니다. `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | 의 이름 [!DNL PubSub] 구독. 위치 [!DNL PubSub]가입을 사용하면 메시지가 게시된 주제를 구독하여 메시지를 받을 수 있습니다. **참고**: 단일 [!DNL PubSub] 구독은 하나의 데이터 흐름에만 사용할 수 있습니다. 여러 데이터 흐름을 만들려면 구독이 여러 개 있어야 합니다. 구독 이름 형식은 다음과 같습니다. `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 대상 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 다음 [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

이러한 값에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL PubSub] 인증](https://cloud.google.com/pubsub/docs/authentication) 문서. 서비스 계정 기반 인증을 사용하려면 다음을 참조하십시오 [[!DNL PubSub] 서비스 계정 만들기에 대한 안내서](https://cloud.google.com/docs/authentication/production#create_service_account) 자격 증명을 생성하는 방법에 대한 단계입니다.

>[!TIP]
>
>서비스 계정 기반 인증을 사용하는 경우 자격 증명을 복사하고 붙여넣을 때 서비스 계정에 대한 충분한 사용자 액세스 권한을 부여했는지 그리고 JSON에 추가 공백이 없는지 확인하십시오.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

소스 연결을 만드는 첫 번째 단계는 [!DNL PubSub] 소스 및 기본 연결 ID 생성. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL PubSub] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

다음 [!DNL PubSub] 소스를 사용하면 인증 중에 허용할 액세스 유형을 지정할 수 있습니다. 루트 액세스를 갖도록 계정을 설정하거나 특정 항목에 대한 액세스를 제한할 수 있습니다 [!DNL PubSub] 주제 및 구독.

>[!NOTE]
>
>에 할당된 사용자(역할) [!DNL PubSub] 프로젝트는 내에서 생성된 모든 주제 및 구독에서 상속됩니다. [!DNL PubSub] 프로젝트. 주도자(역할)가 특정 주제에 액세스할 수 있도록 하려면 해당 주도자(역할)도 주제의 해당 구독에 추가해야 합니다. 자세한 내용은 [[!DNL PubSub] 액세스 제어에 대한 설명서](<https://cloud.google.com/pubsub/docs/access-control>).

**API 형식**

```http
POST /connections
```

**요청**

>[!BEGINTABS]

>[!TAB 프로젝트 기반 인증]

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
          "specName": "Project Based Authentication",
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
| `auth.params.projectId` | 인증에 필요한 프로젝트 ID [!DNL PubSub]. |
| `auth.params.credentials` | 인증에 필요한 자격 증명 또는 키 [!DNL PubSub]. |
| `connectionSpec.id` | 다음 [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB 주제 및 구독 기반 인증]

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
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | 인증에 필요한 자격 증명 또는 키 [!DNL PubSub]. |
| `auth.params.topicName` | 에 대한 프로젝트 ID 및 주제 ID 쌍 [!DNL PubSub] 액세스 권한을 제공하려는 소스. |
| `auth.params.subscriptionName` | 에 대한 프로젝트 ID 및 구독 ID 쌍 [!DNL PubSub] 액세스 권한을 제공하려는 소스. |
| `connectionSpec.id` | 다음 [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다(`id`). 다음 단계에서 소스 연결을 만들려면 이 기본 연결 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 소스 연결 만들기 {#source}

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 소스, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

POST 소스 연결을 만들려면 `/sourceConnections` 의 엔드포인트 [!DNL Flow Service] API.

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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 포함하도록 제공할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 의 기본 연결 ID [!DNL PubSub] 이전 단계에서 생성된 소스. |
| `connectionSpec.id` | 의 고정 연결 사양 ID [!DNL PubSub]. 이 ID는 `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 형식 [!DNL PubSub] 수집할 데이터. 현재 지원되는 데이터 형식은 `json`. |
| `params.topicName` | 의 이름 [!DNL PubSub] 주제. 위치 [!DNL PubSub]: 주제는 메시지 피드를 나타내는 명명된 리소스입니다. |
| `params.subscriptionName` | 특정 주제에 해당하는 구독 이름. 위치 [!DNL PubSub], 구독을 통해 주제에서 메시지를 읽을 수 있습니다. 한 개의 주제에 하나 이상의 구독을 할당할 수 있습니다. |
| `params.dataType` | 이 매개 변수는 수집되는 데이터의 유형을 정의합니다. 지원되는 데이터 유형은 다음과 같습니다. `raw` 및 `xdm`. |

**응답**

성공적인 응답은 고유 식별자()를 반환합니다.`id`)을 참조하십시오. 데이터 흐름을 만들려면 다음 자습서에서 이 ID가 필요합니다.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL PubSub] 를 사용한 소스 연결 [!DNL Flow Service] API. 다음 자습서에서 이 소스 연결 ID를 사용하여 다음을 수행할 수 있습니다. [다음을 사용하여 스트리밍 데이터 흐름 만들기 [!DNL Flow Service] API](../../collect/streaming.md).
