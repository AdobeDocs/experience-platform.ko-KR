---
description: 이 페이지에서는 /authoring/testing/template/render 종단점을 사용하여 대상 구성에 정의된 템플릿 지정된 고객 데이터 필드가 어떻게 표시되는지 시각화하는 방법에 대해 설명합니다.
title: 템플릿화된 고객 필드의 유효성 검사
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 템플릿화된 고객 필드의 유효성 검사

## 개요 {#overview}

다음 `/authoring/testing/template/render` 엔드포인트는 템플릿을 시각화하는 데 도움이 됩니다 [고객 데이터 필드](file-based-destination-configuration.md#customer-data-fields) 대상 구성에 정의된 모양은 다음과 같습니다.

종단점은 고객 데이터 필드에 대한 임의 값을 생성하여 응답에서 반환합니다. 이렇게 하면 버킷 이름 또는 폴더 경로와 같은 고객 데이터 필드의 의미 체계 구조를 확인할 수 있습니다.

## 시작하기 {#getting-started}

계속하기 전에 [시작 안내서](./getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 전제 조건 {#prerequisites}

를 사용하기 전에 `/template/render` endpoint, 다음 조건을 충족하는지 확인하십시오.

* Destination SDK을 통해 만든 기존 파일 기반 대상이 있으며 [대상 카탈로그](../ui/destinations-workspace.md).
* API 요청을 성공적으로 수행하려면 테스트할 대상 인스턴스에 해당하는 대상 인스턴스 ID가 필요합니다. Platform UI에서 대상과의 연결을 검색할 때 URL에서 API 호출에 사용해야 하는 대상 인스턴스 ID를 가져옵니다.

   ![URL에서 대상 인스턴스 ID를 가져오는 방법을 보여주는 UI 이미지입니다.](assets/get-destination-instance-id.png)

## 템플릿 지정 고객 필드 렌더링 {#render-customer-fields}

**API 형식**

```http
POST /authoring/testing/template/render/destination
```

이 API 종단점의 동작을 보여주기 위해 다음 고객 데이터 필드 구성을 사용하여 파일 기반 대상을 고려해 보겠습니다.

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

아래 요청은 를 호출합니다 `/authoring/testing/template/render` 위에 언급된 두 고객 데이터 필드에 대해 임의로 생성된 값이 있는 응답을 반환하는 끝점입니다.

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
| `destinationId` | 의 ID입니다 [대상 구성](file-based-destination-configuration.md) 테스트 중입니다. |
| `templates` | 다음에 정의된 템플릿 필드 이름 [대상 서버 구성](server-and-file-configuration.md). |

**응답**

성공적인 응답은 `HTTP 200 OK` 상태 및 본문은 템플릿 필드에 대해 임의로 생성된 값을 포함합니다.

이 응답을 통해 버킷 이름 또는 폴더 경로와 같은 고객 데이터 필드의 올바른 구조를 확인할 수 있습니다.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계 {#next-steps}

이제 이 문서를 읽은 후에는 [대상 서버](server-and-file-configuration.md).
