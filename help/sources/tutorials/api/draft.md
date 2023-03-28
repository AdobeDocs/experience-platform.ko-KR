---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;
title: Flow Service API를 사용하는 초안 데이터 흐름
description: Flow Service API를 사용하여 데이터 흐름을 초안 상태로 설정하는 방법을 알아봅니다.
badge: label="새 기능" type="양수"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Flow Service API를 사용하는 초안 데이터 흐름

Flow Service API를 사용할 때 데이터 흐름을 초안으로 저장 `mode=draft` 흐름 생성 호출 동안 쿼리 매개 변수를 사용하십시오. 초안은 나중에 새 정보로 업데이트한 다음 준비가 되면 게시할 수 있습니다. 이 자습서에서는 Flow Service API를 사용하여 데이터 흐름을 초안 상태로 설정하는 단계를 설명합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 사전 요구 사항

이 자습서에서는 데이터 흐름을 만드는 데 필요한 자산을 이미 생성했어야 합니다. 여기에는 다음 항목이 포함되어 있습니다.

* 인증된 기본 연결
* 소스 연결
* 대상 XDM 스키마
* 대상 데이터 세트
* 타겟 연결
* 매핑

이 값이 아직 없는 경우 [소스 개요의 카탈로그](../../home.md). 그런 다음 해당 소스의 지침에 따라 데이터 흐름을 작성하기 위해 필요한 자산을 생성합니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).

## 데이터 흐름을 초안 상태로 설정

다음 섹션에서는 데이터 흐름을 초안으로 설정하고, 데이터 흐름을 업데이트하고, 데이터 흐름을 게시하고, 결국 데이터 흐름을 삭제하는 프로세스에 대해 설명합니다.

### 데이터 흐름 초안

데이터 흐름을 초안으로 설정하려면 `/flows` 엔드포인트를 추가하는 중 `mode=draft` 을 쿼리 매개 변수로 사용합니다. 이를 통해 데이터 흐름을 만들고 초안으로 저장할 수 있습니다.

**API 형식**

```http
POST /flows?mode=draft
```

| 매개 변수 | 설명 |
| --- | --- |
| `mode` | 데이터 흐름의 상태를 결정하는 사용자가 제공하는 쿼리 매개 변수입니다. 데이터 흐름을 초안으로 설정하려면 `mode` to `draft`. |

**요청**

다음 요청은 초안 데이터 흐름을 만듭니다.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**응답**

성공적인 응답은 `id` 및 `etag` 데이터 흐름

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 데이터 흐름 업데이트

초안을 업데이트하려면 `/flows` 업데이트할 데이터 흐름의 ID를 제공하는 동안 종단점입니다. 이 단계 동안 `If-Match` header 매개 변수 `etag` 업데이트할 데이터 흐름의 일부입니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 초안 데이터 집합에 매핑 변환을 추가합니다.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**응답**

성공적인 응답은 플로우 ID를 반환하고 `etag`. 변경을 확인하려면 `/flows` 흐름 ID를 제공하는 동안 종단점입니다.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 데이터 흐름 게시

초안을 게시할 준비가 되면 POST 요청을 `/flows` 게시할 초안 데이터 흐름의 ID와 게시 작업 작업을 제공하는 동안 종단점입니다.

**API 형식**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 매개 변수 | 설명 |
| --- | --- |
| `op` | 쿼리된 데이터 흐름의 상태를 업데이트하는 작업 작업입니다. 초안 데이터 흐름을 게시하려면 `op` to `publish`. |

**요청**

다음 요청은 초안 데이터 흐름을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 ID 및 해당 값을 반환합니다 `etag` 데이터 흐름

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 데이터 흐름 삭제

데이터 흐름을 삭제하려면 `/flows` 삭제할 데이터 흐름의 ID를 제공하는 동안 종단점입니다. Flow Service API를 사용하여 데이터 흐름을 삭제하는 방법에 대한 자세한 단계는 [API에서 데이터 흐름 삭제](./delete-dataflows.md).