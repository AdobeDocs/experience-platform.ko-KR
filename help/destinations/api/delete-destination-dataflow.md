---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;API;api;삭제;대상 데이터 흐름 삭제
solution: Experience Platform
title: Flow Service API를 사용하여 대상 데이터 흐름 삭제
type: Tutorial
description: Flow Service API를 사용하여 데이터 흐름을 일괄 처리 및 스트리밍 대상으로 삭제하는 방법을 알아봅니다.
source-git-commit: df89f8ce8050b26068e0ab7aa01f1c964f5d2422
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# Flow Service API를 사용하여 대상 데이터 흐름 삭제

오류가 있거나 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

이 자습서에서는 을 사용하여 데이터 흐름을 일괄 처리 및 스트리밍 대상으로 삭제하는 단계를 설명합니다 [!DNL Flow Service].

## 시작하기 {#get-started}

이 자습서에서는 유효한 흐름 ID가 있어야 합니다. 유효한 흐름 ID가 없는 경우, [대상 카탈로그](../catalog/overview.md) 및 다음에 요약된 단계를 따릅니다. [대상에 연결](../ui/connect-destination.md) 및 [데이터 활성화](../ui/activation-overview.md) 이 자습서를 시작하기 전에

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): [!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 사용하여 데이터 흐름을 성공적으로 삭제하려면 알아야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다 {#gather-values-for-required-headers}

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Flow Service]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>만약 `x-sandbox-name` 헤더를 지정하지 않으면 요청이 `prod` 샌드박스

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 대상 데이터 흐름 삭제 {#delete-destination-dataflow}

기존 흐름 ID를 사용하면 [!DNL Flow Service] API.

**API 형식**

```http
DELETE /flows/{FLOW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 고유 `id` 삭제할 대상 데이터 흐름의 값입니다. |

**요청**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 202(컨텐츠 없음) 및 빈 본문을 반환합니다. 데이터 플로우에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. API가 HTTP 404(찾을 수 없음) 오류를 반환하여 데이터 흐름이 삭제되었음을 나타냅니다.

## API 오류 처리 {#api-error-handling}

이 자습서의 API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서를 따라 다음을 성공적으로 사용했습니다. [!DNL Flow Service] 기존 데이터 흐름을 대상으로 삭제할 API입니다.

사용자 인터페이스를 사용하여 이러한 작업을 수행하는 방법에 대한 단계는 [UI에서 데이터 흐름 삭제](../ui/delete-destinations.md).
