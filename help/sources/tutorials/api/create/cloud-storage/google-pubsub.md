---
title: 흐름 서비스 API를 사용하여 Google PubSub Source 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google PubSub 계정에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 2%

---

# 흐름 서비스 API를 사용하여 [!DNL Google PubSub] Source 연결 만들기

>[!IMPORTANT]
>
>[!DNL Google PubSub] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

이 자습서에서는 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)를 사용하여 [!DNL Google PubSub]&#x200B;(이하 &quot;[!DNL PubSub]&quot;)을(를) Experience Platform에 연결하는 단계를 안내합니다.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL PubSub]을(를) Experience Platform에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL PubSub] 계정을 [!DNL Flow Service]에 연결하려면 아래에 설명된 연결 속성에 대한 값을 제공해야 합니다. 인증 및 필수 구성 요소 설정에 대한 자세한 내용은 [[!DNL PubSub source] 개요](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites)를 참조하세요.

>[!BEGINTABS]

>[!TAB 프로젝트 기반 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `projectId` | [!DNL PubSub]을(를) 인증하는 데 필요한 프로젝트 ID입니다. |
| `credentials` | [!DNL PubSub]을(를) 인증하는 데 필요한 자격 증명입니다. 자격 증명에서 공백을 제거한 후 전체 JSON 파일을 넣었는지 확인해야 합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 대상 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB 주제 및 구독 기반 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `credentials` | [!DNL PubSub]을(를) 인증하는 데 필요한 자격 증명입니다. 자격 증명에서 공백을 제거한 후 전체 JSON 파일을 넣었는지 확인해야 합니다. |
| `topicName` | 메시지 피드를 나타내는 리소스의 이름입니다. [!DNL PubSub] 원본의 특정 데이터 스트림에 대한 액세스 권한을 제공하려면 항목 이름을 지정해야 합니다. 항목 이름 형식은 `projects/{PROJECT_ID}/topics/{TOPIC_ID}`입니다. |
| `subscriptionName` | [!DNL PubSub] 구독 이름. [!DNL PubSub]에서 구독을 사용하면 메시지가 게시된 주제를 구독하여 메시지를 받을 수 있습니다. **참고**: 단일 [!DNL PubSub] 구독은 하나의 데이터 흐름에만 사용할 수 있습니다. 여러 데이터 흐름을 만들려면 구독이 여러 개 있어야 합니다. 구독 이름 형식은 `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 대상 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

이러한 값에 대한 자세한 내용은 이 [[!DNL PubSub] 인증](https://cloud.google.com/pubsub/docs/authentication) 문서를 참조하십시오. 서비스 계정 기반 인증을 사용하려면 자격 증명을 생성하는 방법에 대한 단계를 보려면 이 [[!DNL PubSub] 서비스 계정 만들기에 대한 안내서](https://cloud.google.com/docs/authentication/production#create_service_account)를 읽어 보십시오.

>[!TIP]
>
>서비스 계정 기반 인증을 사용하는 경우 자격 증명을 복사하고 붙여넣을 때 서비스 계정에 대한 충분한 사용자 액세스 권한을 부여했는지 그리고 JSON에 추가 공백이 없는지 확인하십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

>[!TIP]
>
>만든 후에는 [!DNL Google PubSub] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

원본 연결을 만드는 첫 번째 단계는 [!DNL PubSub] 원본을 인증하고 기본 연결 ID를 생성하는 것입니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL PubSub] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

[!DNL PubSub] 원본에서 인증 중에 허용할 액세스 형식을 지정할 수 있습니다. 루트 액세스를 갖도록 계정을 설정하거나 특정 [!DNL PubSub] 주제 및 구독에 대한 액세스를 제한할 수 있습니다.

>[!NOTE]
>
>[!DNL PubSub] 프로젝트에 할당된 사용자(역할)는 [!DNL PubSub] 프로젝트 내에서 만든 모든 주제 및 구독에서 상속됩니다. 주도자(역할)가 특정 주제에 액세스할 수 있도록 하려면 해당 주도자(역할)도 주제의 해당 구독에 추가해야 합니다. 자세한 내용은 액세스 제어에 대한 [[!DNL PubSub] 설명서를 읽어보세요](<https://cloud.google.com/pubsub/docs/access-control>).

**API 형식**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 프로젝트 기반 인증]

프로젝트 기반 인증으로 기본 연결을 만들려면 `/connections` 끝점에 대한 POST 요청을 만들고 요청 본문에 `projectId` 및 `credentials`을(를) 제공하십시오.

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
| `auth.params.projectId` | [!DNL PubSub]을(를) 인증하는 데 필요한 프로젝트 ID입니다. |
| `auth.params.credentials` | [!DNL PubSub]을(를) 인증하는 데 필요한 자격 증명 또는 키입니다. |
| `connectionSpec.id` | [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++응답

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 다음 단계에서 소스 연결을 만들려면 이 기본 연결 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB 주제 및 구독 기반 인증]

주제 및 구독 기반 인증을 사용하여 기본 연결을 만들려면 `/connections` 끝점에 대한 POST 요청을 만들고 요청 본문에 `credentials`, `topicName` 및 `subscriptionName`을(를) 제공하십시오.

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
| `auth.params.credentials` | [!DNL PubSub]을(를) 인증하는 데 필요한 자격 증명 또는 키입니다. |
| `auth.params.topicName` | 액세스 권한을 제공하려는 [!DNL PubSub] 소스의 프로젝트 ID 및 항목 ID 쌍입니다. |
| `auth.params.subscriptionName` | 액세스를 제공할 [!DNL PubSub] 소스의 프로젝트 ID 및 구독 ID 쌍입니다. |
| `connectionSpec.id` | [!DNL PubSub] 연결 사양 ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++응답

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 다음 단계에서 소스 연결을 만들려면 이 기본 연결 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## 소스 연결 만들기 {#source}

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 소스, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

소스 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 끝점에 대한 POST 요청을 만듭니다.

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
| `baseConnectionId` | 이전 단계에서 생성된 [!DNL PubSub] 소스의 기본 연결 ID입니다. |
| `connectionSpec.id` | [!DNL PubSub]에 대한 고정 연결 사양 ID입니다. 이 ID: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 수집할 [!DNL PubSub] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |
| `params.topicName` | [!DNL PubSub] 주제의 이름입니다. [!DNL PubSub]에서 주제는 메시지 피드를 나타내는 명명된 리소스입니다. |
| `params.subscriptionName` | 특정 주제에 해당하는 구독 이름. [!DNL PubSub]에서 구독을 통해 주제의 메시지를 읽을 수 있습니다. 한 개의 주제에 하나 이상의 구독을 할당할 수 있습니다. |
| `params.dataType` | 이 매개 변수는 수집되는 데이터의 유형을 정의합니다. 지원되는 데이터 형식은 `raw` 및 `xdm`입니다. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 데이터 흐름을 만들려면 다음 자습서에서 이 ID가 필요합니다.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>스트리밍 데이터 흐름을 만들거나 업데이트한 후 데이터 손실 또는 데이터 감소의 잠재적 인스턴스를 방지하기 위해 데이터 수집에서 5분 정도의 짧은 일시 중지가 필요합니다.

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL PubSub] 소스 연결을 만들었습니다. 다음 자습서에서 이 원본 연결 ID를 사용하여 [API를 사용하여 스트리밍 데이터 흐름을 만들 [!DNL Flow Service] 수 있습니다](../../collect/streaming.md).
