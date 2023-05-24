---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;
title: 실패한 데이터 흐름 실행 다시 시도
description: 이 자습서에서는 흐름 서비스 API를 사용하여 실패한 데이터 흐름 실행을 다시 시도하는 방법에 대한 단계를 다룹니다
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 실패한 데이터 흐름 실행 다시 시도

>[!IMPORTANT]
>
>실패한 데이터 흐름 실행을 다시 시도하는 기능은 일괄 처리 소스에서 사용할 수 있습니다. 실패한 데이터 흐름 실행만 다시 시도할 수 있습니다.

이 자습서에서는 다음을 사용하여 실패한 데이터 흐름 실행을 다시 시도하는 방법에 대한 단계를 다룹니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../landing/api-guide.md).

## 실패한 데이터 흐름 실행 다시 시도

실패한 데이터 흐름 실행을 다시 시도하려면 다음에 대한 POST 요청을 수행하십시오. `/runs` 데이터 흐름의 실행 ID 및 를 제공하는 동안 엔드포인트 `re-trigger` 작업을 쿼리 매개 변수의 일부로 지정합니다.

**API 형식**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 매개변수 | 설명 |
| --- | --- |
| `{RUN_ID}` | 다시 시도할 데이터 흐름 실행에 해당하는 실행 ID입니다. |
| `op` | 수행할 작업을 결정하는 작업입니다. 실패한 데이터 흐름 실행을 다시 시도하려면 다음을 지정해야 합니다. `re-trigger` 작업. |

**요청**

다음 요청은 실행 ID에 대한 데이터 흐름 실행을 재시도합니다 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

성공적인 응답은 새로 생성된 흐름 실행 ID와 해당 etag 버전을 반환합니다.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
