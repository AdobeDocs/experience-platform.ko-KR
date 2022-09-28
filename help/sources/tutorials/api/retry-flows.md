---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;
title: 실패한 데이터 흐름 실행 다시 시도
description: 이 자습서에서는 Flow Service API를 사용하여 실패한 데이터 흐름을 다시 시도하는 방법에 대해 설명합니다
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 실패한 데이터 흐름 실행 다시 시도

>[!IMPORTANT]
>
>실패한 데이터 흐름 실행을 다시 시도하는 것에 대한 지원을 배치 소스에서 사용할 수 있습니다. 실패한 데이터 흐름 실행만 다시 시도할 수 있습니다.

이 자습서에서는 다음을 사용하여 실패한 데이터 흐름 실행을 다시 시도하는 방법에 대해 설명합니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).

## 실패한 데이터 흐름 실행 다시 시도

실패한 데이터 흐름을 다시 실행하려면 `/runs` 데이터 흐름의 실행 ID와 `re-trigger` 작업을 쿼리 매개 변수의 일부로 사용합니다.

**API 형식**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RUN_ID}` | 다시 시도할 데이터 흐름 실행에 해당하는 실행 ID입니다. |
| `op` | 수행할 작업을 결정하는 작업입니다. 실패한 데이터 흐름 실행을 다시 시도하려면 다음을 지정해야 합니다 `re-trigger` 를 사용하십시오. |

**요청**

다음 요청은 실행 ID에 대해 데이터 흐름 실행을 다시 시도합니다 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**응답**

성공적인 응답은 새로 만든 흐름 실행 ID 및 해당 태그 버전을 반환합니다.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
