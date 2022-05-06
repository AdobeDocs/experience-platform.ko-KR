---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;대상 계정 삭제;삭제;api
solution: Experience Platform
title: Flow Service API를 사용하여 대상 계정을 삭제합니다
type: Tutorial
description: Flow Service API를 사용하여 대상 계정을 삭제하는 방법을 알아봅니다.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Flow Service API를 사용하여 대상 계정을 삭제합니다

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

데이터를 활성화하기 전에 먼저 대상 계정을 설정하여 대상에 연결해야 합니다. 이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>대상 계정을 삭제하는 것은 현재 Flow Service API에서만 지원됩니다. 대상 계정은 Experience Platform UI를 사용하여 삭제할 수 없습니다.

## 시작하기 {#get-started}

이 자습서에서는 올바른 연결 ID가 있어야 합니다. 연결 ID는 대상에 대한 계정 연결을 나타냅니다. 올바른 연결 ID가 없는 경우, [대상 카탈로그](../catalog/overview.md) 및 다음에 요약된 단계를 따릅니다. [대상에 연결](../ui/connect-destination.md) 이 자습서를 시작하기 전에

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): [!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 사용하여 대상 계정을 성공적으로 삭제하려면 알아야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다 {#gather-values-for-required-headers}

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Flow Service]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>만약 `x-sandbox-name` 헤더를 지정하지 않으면 요청이 `prod` 샌드박스

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 삭제할 대상 계정의 연결 ID를 찾습니다 {#find-connection-id}

>[!NOTE]
>이 자습서에서는 [비행선 목적지](../catalog/mobile-engagement/airship-attributes.md) 예를 들어, 요약된 단계는 [사용 가능한 대상](../catalog/overview.md).

대상 계정을 삭제하는 첫 번째 단계는 삭제하려는 대상 계정에 해당하는 연결 ID를 확인하는 것입니다.

Experience Platform UI에서 **[!UICONTROL 대상]** > **[!UICONTROL 계정]** 삭제할 계정을 선택하고 **[!UICONTROL 대상]** 열.

![삭제할 대상 계정 선택](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

다음으로, 브라우저의 URL에서 대상 계정의 연결 ID를 검색할 수 있습니다.

![URL에서 연결 ID 검색](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## 연결 삭제 {#delete-connection}

>[!IMPORTANT]
>
>대상 계정을 삭제하기 전에 기존 데이터 흐름을 대상 계정으로 삭제해야 합니다.
>기존 데이터 흐름을 삭제하려면 아래 페이지를 참조하십시오.
>* [Experience Platform UI 사용](../ui/delete-destinations.md) 기존 데이터 흐름을 삭제하려면
>* [Flow Service API 사용](delete-destination-dataflow.md) 기존 데이터 흐름을 삭제하려면 다음을 수행하십시오.


연결 ID가 있고 대상 계정에 데이터 흐름이 없도록 확인한 후에는 다음 항목에 DELETE 요청을 수행하십시오 [!DNL Flow Service] API.

**API 형식**

```http
DELETE /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 고유 `id` 삭제할 연결의 값입니다. |

**요청**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다. 연결에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. API가 대상 계정이 삭제되었음을 나타내는 HTTP 404(찾을 수 없음) 오류를 반환합니다.

## API 오류 처리 {#api-error-handling}

이 자습서의 API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이 자습서를 따라 다음을 성공적으로 사용했습니다. [!DNL Flow Service] 기존 대상 계정을 삭제하는 API입니다. 대상 사용에 대한 자세한 내용은 [대상 개요](/help/destinations/home.md).