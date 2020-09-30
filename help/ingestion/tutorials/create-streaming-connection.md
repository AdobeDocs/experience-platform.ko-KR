---
keywords: Experience Platform;home;popular topics;streaming connection;create streaming connection;api guide;tutorial;create a streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: API를 사용하여 스트리밍 연결 만들기
topic: tutorial
type: Tutorial
description: 이 자습서는 Adobe Experience Platform 데이터 통합 서비스 API의 일부인 스트리밍 통합 API를 사용하는 데 도움이 됩니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 2%

---


# API를 사용하여 스트리밍 연결 만들기

이 자습서는 Adobe Experience Platform 데이터 API의 일부인 스트리밍 통합 API를 사용하는 데 도움이 [!DNL Ingestion Service] 됩니다.

## 시작하기

Adobe Experience Platform로의 데이터 스트리밍을 시작하려면 스트리밍 연결 등록이 필요합니다. 스트리밍 연결을 등록할 때 스트리밍 데이터 소스와 같은 몇 가지 주요 세부 사항을 제공해야 합니다.

스트리밍 연결을 등록한 후 데이터 프로듀서로서 데이터를 플랫폼으로 스트리밍하는 데 사용할 수 있는 고유한 URL을 갖게 됩니다.

또한 이 자습서에서는 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL 경험 데이터 모델(XDM)]](../../xdm/home.md):경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크
- [[!DNL 실시간 고객 프로필]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.

다음 섹션에서는 스트리밍 통합 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 연결 만들기

연결은 소스를 지정하며 스트리밍 통합 API와 호환되는 흐름을 만드는 데 필요한 정보를 포함합니다.

**API 형식**

```http
POST /flowservice/connections
```

**요청**

>[!NOTE]
>
>스트리밍 통합 `providerId` 을 위한 스트리밍 연결을 만드는 API에 대해 지정하는 API와 같이 나열된 값과 이 값이 예와 같이 사용되어야 `connectionSpec`**** 합니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

**응답**

성공적인 응답은 새로 만든 연결에 대한 세부 사항과 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 연결 `id` 의 이름입니다. 이것은 본 계약서에 명시될 것입니다 `{CONNECTION_ID}`. |
| `etag` | 연결에 할당된 식별자로, 연결 개정을 지정합니다. |

## 데이터 수집 URL 가져오기

이제 연결이 만들어지면 데이터 수집 URL을 검색할 수 있습니다.

**API 형식**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 연결 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 연결에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다. 데이터 수집 URL은 연결과 함께 자동으로 생성되며 이 `inletUrl` 값을 사용하여 검색할 수 있습니다.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## 다음 단계

스트리밍 연결을 만들었으므로 데이터를 스트리밍하거나 시계열 또는 기록할 수 있으므로 데이터 내에서 데이터를 인제스트할 수 있습니다 [!DNL Platform]. 시계열 데이터를 스트리밍하는 방법 [!DNL Platform]을 알려면 [스트리밍 시계열 데이터 자습서로 이동합니다](./streaming-time-series-data.md). 기록 데이터를 스트리밍하는 방법을 [!DNL Platform]알아보려면 [스트리밍 레코드 데이터 자습서로 이동합니다](./streaming-record-data.md).

## 부록

이 섹션에서는 API를 사용하여 스트리밍 연결을 만드는 방법에 대한 보충 정보를 제공합니다.

### 인증된 스트리밍 연결

인증된 데이터 수집을 사용하면 [!DNL Real-time Customer Profile] 및 [!DNL Identity]과 같은 Adobe Experience Platform 서비스가 신뢰할 수 있는 출처의 레코드와 신뢰할 수 없는 출처의 레코드를 구별할 수 있습니다. PII(개인 식별 정보)를 전송하려는 클라이언트는 IMS 액세스 토큰을 POST 요청의 일부로 전송함으로써 이를 수행할 수 있습니다. IMS 토큰이 유효한 경우 레코드는 신뢰할 수 있는 소스에서 수집된 것으로 표시됩니다.

인증된 스트리밍 연결을 만드는 방법에 대한 자세한 내용은 인증된 스트리밍 연결 [만들기 자습서를 참조하십시오](create-authenticated-streaming-connection.md).