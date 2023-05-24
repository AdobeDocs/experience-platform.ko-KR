---
description: 이 페이지에서는 /authoring/testing/template/render 끝점을 사용하여 대상 구성에 정의된 템플릿화된 고객 데이터 필드의 모양을 시각화하는 방법에 대해 설명합니다.
title: 템플릿화된 고객 필드의 유효성 검사
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 템플릿화된 고객 필드의 유효성 검사

## 개요 {#overview}

다음 `/authoring/testing/template/render` 엔드포인트는 템플릿화 방법을 시각화하는 데 도움이 됩니다 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 대상 구성에 정의되어 있으면 다음과 같은 모습입니다.

끝점은 고객 데이터 필드에 대한 무작위 값을 생성하고 응답에서 반환합니다. 버킷 이름 또는 폴더 경로와 같은 고객 데이터 필드의 의미 체계 구조를 확인하는 데 도움이 됩니다.

## 시작하기 {#getting-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 사전 요구 사항 {#prerequisites}

을(를) 사용하기 전에 `/template/render` 엔드포인트입니다. 다음 조건을 충족하는지 확인하십시오.

* Destination SDK을 통해 생성된 기존 파일 기반 대상이 있으며 [대상 카탈로그](../../../ui/destinations-workspace.md).
* API 요청을 성공적으로 수행하려면 테스트할 대상 인스턴스에 해당하는 대상 인스턴스 ID가 필요합니다. Platform UI에서 대상과의 연결을 검색할 때 API 호출에 사용해야 하는 대상 인스턴스 ID를 URL에서 가져옵니다.

   ![URL에서 대상 인스턴스 ID를 가져오는 방법을 보여 주는 UI 이미지입니다.](../../assets/testing-api/get-destination-instance-id.png)

## 템플릿화된 고객 필드 렌더링 {#render-customer-fields}

**API 형식**

```http
POST /authoring/testing/template/render/destination
```

이 API 끝점의 동작을 설명하기 위해 다음 고객 데이터 필드 구성이 있는 파일 기반 대상을 생각해 보겠습니다.

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**요청**

아래 요청은 `/authoring/testing/template/render` endpoint - 위에 언급된 두 고객 데이터 필드에 대해 임의로 생성된 값이 있는 응답을 반환합니다.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `destinationId` | 의 ID [대상 구성](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 테스트하고 있습니다. |
| `templates` | 에 정의된 템플릿화된 필드 이름 [대상 서버 구성](../../authoring-api/destination-server/create-destination-server.md). |

**응답**

성공적인 응답은 다음을 반환합니다. `HTTP 200 OK` 상태이며 본문에는 템플릿화된 필드에 대해 임의로 생성된 값이 포함됩니다.

이 응답은 버킷 이름 또는 폴더 경로와 같은 고객 데이터 필드의 올바른 구조를 확인하는 데 도움이 됩니다.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제에서 정의한 고객 데이터 필드 구성을 확인하는 방법을 이해할 수 있습니다. [대상 서버](../../authoring-api/destination-server/create-destination-server.md).
