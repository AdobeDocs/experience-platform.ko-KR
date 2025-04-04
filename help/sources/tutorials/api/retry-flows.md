---
title: 실패한 데이터 흐름 실행 다시 시도
description: 흐름 서비스 API를 사용하여 실패한 데이터 흐름 실행을 다시 시도하는 방법을 알아봅니다.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# 실패한 데이터 흐름 실행 다시 시도

>[!IMPORTANT]
>
>실패한 데이터 흐름 실행을 다시 시도하는 기능은 일괄 처리 소스에서 사용할 수 있습니다. 실패한 데이터 흐름 실행만 다시 시도할 수 있습니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 실패한 데이터 흐름 실행을 다시 시도하는 방법에 대한 단계를 다룹니다.

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 실패한 데이터 흐름 실행 다시 시도

실패한 데이터 흐름 실행을 다시 시도하려면 쿼리 매개 변수의 일부로 데이터 흐름의 실행 ID 및 `re-trigger` 작업을 제공하는 동안 `/runs` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 매개변수 | 설명 |
| --- | --- |
| `{RUN_ID}` | 다시 시도할 데이터 흐름 실행에 해당하는 실행 ID입니다. |
| `op` | 수행할 작업을 결정하는 작업입니다. 실패한 데이터 흐름 실행을 다시 시도하려면 `re-trigger`을(를) 작업으로 지정해야 합니다. |

**요청**

>[!NOTE]
>
>데이터 흐름 실행에 수집된 레코드가 0개인 경우 `re-trigger` 작업을 사용하여 성공한 데이터 흐름 실행을 다시 시도할 수도 있습니다.

다음 요청은 실행 ID `4fb0418e-1804-45d6-8d56-dd51f05c0baf`에 대한 데이터 흐름 실행을 다시 시도합니다.

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
