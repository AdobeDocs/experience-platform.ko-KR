---
title: 오류 처리
description: Adobe Experience Platform Edge Network Server API에 대한 API 요청을 수행할 때 발생할 수 있는 오류에 대해 알아봅니다.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---

# 오류 처리

## 개요 {#overview}

Adobe Experience Platform Edge Network Server API의 API 오류는 내부(Edge Network 자체) 또는 외부(입력, 구성 또는 업스트림 관련) 등 다양한 원인이 있을 수 있습니다.

## 오류 유형 {#error-types}

| 오류 | 유형 | 설명 | 상태 코드 |
| --- | --- | --- | --- |
| `RequestProcessingError` | 내부 | 예기치 않은 상황에서 Adobe Experience Platform Edge Network에서 일반 목적 오류가 발생했습니다. | `500` |
| `InputError` | 외부 | 잘못된 입력으로 인한 오류와 엔티티 유효성 검사 오류를 포함합니다. | `4xx` |
| `ConfigurationError` | 외부 | 서버측 구성 오류입니다. | `422` |
| `UpstreamError` | 외부 | 업스트림 서비스와의 통신 오류. | `207 Multi-Status` |

## 심각도

서버 API 오류는 심각도로 분할할 수도 있습니다.

* **치명적인 오류** 디스패치 파이프라인이 중단됩니다.
* **치명적이지 않은 오류** 은(는) 요청 처리를 계속할 수 있도록 하는 동안 부분 처리를 시그널링할 수 있습니다.
   * 이 경우 요청의 전체 상태 코드가 다음으로 변경됩니다. `207 Multi-Status`.

| 오류 | 유형 | 비고 |
| --- | --- | --- |
| `RequestProcessingError` | 치명 | 요청 처리 중 언제든지 발생할 수 있습니다. |
| `InputError` | 치명 | 업스트림에 디스패치하기 전에 요청을 수락할 때 발생합니다. |
| `ConfigurationError` | 치명 | 업스트림에 디스패치하기 전에 요청을 수락할 때 발생합니다. |
| `UpstreamError` | 비치명적 | 업스트림 서비스와의 통신 오류. |

### 치명적인 오류 {#fatal-errors}

치명적인 오류로 인해 요청 처리가 중지되고 2xx 이외의 응답 상태가 반환됩니다. 다음을 확인하십시오. [오류 유형](#error-types) 섹션에 각 오류 유형에 해당하는 예상 상태 코드를 표시합니다.

오류에는 오류 개체가 포함된 응답 본문이 함께 표시됩니다. 이 경우 응답 본문에 정의된 문제 세부 정보가 포함됩니다. [RFC 7807 HTTP API에 대한 문제 세부 정보](https://tools.ietf.org/html/rfc7807).

반환된 콘텐츠 유형은 다음과 같습니다. `application/problem+json` 미디어 유형. 존재하는 경우 이 응답에는 오류와 관련하여 기계가 읽을 수 있는 세부 정보가 포함됩니다. 문제 세부 정보에 URI 유형이 포함됩니다.

모든 오류 개체에는 `type`, `status`, `title`, `detail` 및 `report` api 클라이언트가 문제가 무엇인지 알 수 있도록 메시지 속성.

| 속성 | 유형 | 설명 |
| -------- | ------ | ----------- |
| `type` | 문자열 | 형식에 따라 문제 유형을 식별하는 URI 참조(RFC3986) `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | 숫자 | 이 문제 발생에 대해 서버에서 생성된 HTTP 상태 코드입니다. |
| `title` | 문자열 | 사람이 인식할 수 있는 문제 유형에 대한 간략한 요약입니다. |
| `detail` | 문자열 | 사람이 인식할 수 있는 문제 유형에 대한 간략한 설명입니다. |
| `report` | 오브젝트 | 요청 ID 또는 조직 ID와 같이 디버깅에 도움이 되는 추가 속성의 맵입니다. 경우에 따라 유효성 검사 오류 목록과 같이, 해당 오류와 관련된 데이터가 포함될 수 있습니다. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### 치명적이지 않은 오류 {#non-fatal-errors}

치명적이지 않은 오류는 다음으로 분류될 수 있습니다.

* 오류: 요청을 처리하는 동안 발생했지만 전체 요청이 거부되지 않은 문제(예: 중요하지 않은 업스트림 실패).
* 경고: 요청의 일부 처리가 발생했음을 알릴 수 있는 업스트림 서비스의 메시지.

치명적이지 않은 오류(경고 제외)가 발생하면 [!DNL Server API] 응답 상태를 다음으로 변경 `207 Multi-Status`.

반면 경고는 일반적으로 요청에 완전히 영향을 주지 않는 일시적인 상태를 나타내므로 대부분 정보입니다. 여기 한 가지 예는 세그먼테이션 엔진에서 읽은 부분 프로필이며, 이 경우 정확도는 어느 정도 영향을 받지만 기능은 계속 전달됩니다.

치명적이지 않은 오류는 _문제 세부 정보_ 형식을 지정하지만, 유형이 인 Edge Gateway의 표준 응답에 직접 포함됩니다. `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## 처리 `4xx` 및 `5xx` 응답


| 오류 코드 | 설명 |
|---|---|
| `4xx Bad Request` | 가장 `4xx` 400, 403, 404와 같은 오류는 클라이언트를 대신하여 재시도하면 안 됩니다. 단, `429`. 이는 클라이언트 오류이며 성공하지 못합니다. 클라이언트는 요청을 다시 시도하기 전에 오류를 해결해야 합니다. |
| `429 Too Many Requests` | `429` HTTP 응답 코드는 Adobe Experience Platform Edge Network 또는 업스트림 서비스가 요청을 제한하고 있음을 나타냅니다. 이 경우 이러한 시나리오에서는 호출자가 다음을 준수해야 합니다. `Retry-After` 응답 헤더. 뒤로 흐르는 모든 응답은 도메인별 오류 코드와 함께 HTTP 응답 코드를 전달해야 합니다. |
| `500 Internal Server Error` | `500` 오류는 일반적인 catch-all 오류입니다. `500` 오류는 재시도하지 않아야 합니다. 단, `502` 및 `503`. 중개인은 다음으로 응답해야 함: `500` 일반적인 오류 코드/메시지 또는 더 많은 도메인별 오류 코드/메시지로 응답할 수 있습니다. |
| `502 Bad Gateway` | Adobe Experience Platform 에지 네트워크가 업스트림 서버에서 잘못된 응답을 받았음을 나타냅니다. 이 문제는 서버 간 네트워크 문제로 인해 발생할 수 있습니다. 임시 네트워크 문제가 해결될 수 있으므로 다시 시도하면 문제가 해결될 수 있으므로 수신자는 `502` 잠시 후 오류가 요청을 다시 시도할 수 있습니다. |
| `503 Service Unavailable` | 이 오류 코드는 서비스를 일시적으로 사용할 수 없음을 나타냅니다. 이 문제는 유지 관리 기간 동안 발생할 수 있습니다. 수신자 `503` 오류는 요청을 다시 시도할 수 있지만 은(는) 다음을 준수해야 합니다. `Retry-After` 머리글입니다. |
| `504 Gateway Timeout` | 업스트림 서버에 대한 Adobe Experience Platform Edge Network 요청이 시간 초과되었음을 나타냅니다. 이 문제는 서버 간 네트워크 문제, DNS 문제 또는 기타 네트워크 문제로 인해 발생할 수 있습니다. 일시적인 네트워크 문제는 잠시 후에 해결될 수 있으며, 다시 시도하면 문제가 해결될 수 있습니다. |
