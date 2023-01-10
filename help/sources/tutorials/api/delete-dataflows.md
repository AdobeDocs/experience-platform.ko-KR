---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;API;api;삭제;데이터 흐름 삭제
solution: Experience Platform
title: Flow Service API를 사용하여 데이터 흐름 삭제
type: Tutorial
description: Flow Service API를 사용하여 일괄 처리 및 스트리밍 데이터 흐름을 삭제하는 방법을 알아봅니다.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# Flow Service API를 사용하여 데이터 흐름 삭제

오류가 있거나 를 사용하여 더 이상 사용되지 않는 일괄 처리 및 스트리밍 데이터 흐름을 삭제할 수 있습니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

이 자습서에서는 을 사용하여 일괄 처리 및 스트리밍 소스로 만든 데이터 흐름을 삭제하는 단계를 설명합니다 [!DNL Flow Service].

## 시작하기

이 자습서에서는 유효한 흐름 ID가 있어야 합니다. 유효한 흐름 ID가 없는 경우, [소스 개요](../../home.md) 및 이 자습서를 시도하기 전에 설명된 단계를 따릅니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).

## 데이터 흐름 삭제

기존 흐름 ID를 사용하는 경우, [!DNL Flow Service] API.

**API 형식**

```http
DELETE /flows/{FLOW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 고유 `id` 삭제할 데이터 흐름 값입니다. |

**요청**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다. 데이터 플로우에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. API가 HTTP 404(찾을 수 없음) 오류를 반환하여 데이터 흐름이 삭제되었음을 나타냅니다.

## 다음 단계

이 자습서를 따라 다음을 성공적으로 사용했습니다. [!DNL Flow Service] 기존 데이터 흐름을 삭제할 API입니다.

사용자 인터페이스를 사용하여 이러한 작업을 수행하는 방법에 대한 단계는 [UI에서 데이터 흐름 삭제](../../tutorials/ui/delete.md)
