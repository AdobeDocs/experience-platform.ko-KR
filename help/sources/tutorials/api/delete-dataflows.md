---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: Flow Service API를 사용하여 데이터 흐름 삭제
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 데이터 흐름 삭제를 위한 단계를 설명합니다.
translation-type: tm+mt
source-git-commit: ae3e64a5f9a82c0efe3cffeb6d4d425ae2e72bda
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# Flow Service API를 사용하여 데이터 흐름 삭제

이 자습서에서는 을 사용하여 일괄 처리 및 스트리밍 소스로 구성된 데이터 흐름을 삭제하는 단계를 설명합니다 [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 시작하기

이 자습서에서는 올바른 흐름 ID가 있어야 합니다. 유효한 플로우 ID가 없는 경우 [소스 개요에서](../../home.md) 선택한 커넥터를 선택하고 이 튜토리얼을 시작하기 전에 설명한 단계를 따르십시오.

또한 이 자습서에서는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 데이터 흐름을 성공적으로 삭제하려면 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 흐름 삭제

기존 흐름 ID를 사용하면 API에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제할 수 [!DNL Flow Service] 있습니다.

**API 형식**

```http
DELETE /flows/{FLOW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 삭제할 데이터 프롤에 대한 고유한 `id` 값입니다. |

**요청**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다. 데이터 흐름(데이터 흐름)에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. API가 HTTP 404(찾을 수 없음) 오류를 반환하여 데이터 흐름 삭제되었음을 나타냅니다.

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 기존 데이터 흐름을 [!DNL Flow Service] 삭제했습니다.

사용자 인터페이스를 사용하여 이러한 작업을 수행하는 방법에 대한 자세한 내용은 UI에서 데이터 흐름 [삭제에 대한 자습서를 참조하십시오](../../tutorials/ui/delete.md)
