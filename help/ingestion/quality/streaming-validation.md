---
keywords: Experience Platform;홈;인기 항목;스트리밍;스트리밍 수집;스트리밍 통합;스트리밍 수집 유효성 검사;유효성 검사;스트리밍 수집 유효성 검사;유효성 검사;동기 유효성 검사;비동기 유효성 검사;비동기 유효성 검사;비동기 유효성 검사;비동기 유효성 검사;
solution: Experience Platform
title: 스트리밍 수집 유효성 검사
topic-legacy: tutorial
type: Tutorial
description: 스트리밍 수집 기능을 사용하면 스트리밍 끝점을 사용하여 실시간으로 Adobe Experience Platform에 데이터를 업로드할 수 있습니다. 스트리밍 수집 API는 동기식과 비동기식의 두 가지 유효성 검사 모드를 지원합니다.
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: beb5d615da6d825678f446eec609a2bb356bb310
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 3%

---

# 스트리밍 수집 유효성 검사

스트리밍 수집 기능을 사용하면 스트리밍 끝점을 사용하여 실시간으로 Adobe Experience Platform에 데이터를 업로드할 수 있습니다. 스트리밍 수집 API는 동기식과 비동기식의 두 가지 유효성 검사 모드를 지원합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크입니다.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): 데이터를 로 보낼 수 있는 방법 중 하나입니다 [!DNL Experience Platform].

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

- 권한 부여: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Schema Registry]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: `application/json`

### 유효성 검사 적용 범위

[!DNL Streaming Validation Service] 에서는 다음 영역에서 유효성 검사를 다룹니다.
- Range
- 현재 상태
- 열거형
- 패턴
- 유형
- 형식

## 동기 유효성 검사

동기 유효성 검사는 수집이 실패한 이유에 대한 즉각적인 피드백을 제공하는 유효성 검사 방법입니다. 그러나 실패 시 유효성 검사가 실패한 레코드는 삭제되고 다운스트림으로 전송되지 않습니다. 따라서 동기 유효성 검사는 개발 프로세스 동안에만 사용해야 합니다. 동기 유효성 검사를 수행할 때 호출자에게 XDM 유효성 검사 결과와 실패 이유를 모두 알려줍니다.

기본적으로 동기 유효성 검사가 설정되지 않습니다. 이를 활성화하려면 API 호출 시 선택적 쿼리 매개 변수 `syncValidation=true`을 전달해야 합니다. 또한 스트림 종단점이 VA7 데이터 센터에 있는 경우에만 동기 유효성 검사를 사용할 수 있습니다.

동기 유효성 검사 중에 메시지가 실패하면 메시지가 출력 큐에 기록되지 않고 사용자에게 즉시 피드백을 제공합니다.

>[!NOTE]
>
>변경 사항이 캐시되므로 스키마 변경 사항을 즉시 사용할 수 없습니다. 캐시를 새로 고치려면 최대 15분을 허용합니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

다음 요청을 제출하여 동기 유효성 검사를 통해 데이터를 데이터 입구로 수집합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 수집할 데이터의 JSON 본문. |

**응답**

동기 유효성 검사가 활성화된 경우, 성공적인 응답에는 해당 페이로드에서 발생한 유효성 검사 오류가 포함됩니다.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

위의 응답에는 발견된 스키마 위반 수 및 위반 내용이 나열됩니다. 예를 들어, 이 응답에는 `workEmail` 키와 `person` 키가 스키마에 정의되어 있지 않으므로 허용되지 않습니다. 또한 스키마에 `string`이 필요하지만 대신 `long`가 삽입되었으므로 `_id`에 대한 값이 잘못된 것으로 플래그를 지정합니다. 5개의 오류가 발생하면 유효성 검사 서비스가 **해당 메시지 처리를 중지합니다**. 그러나 다른 메시지는 계속 구문 분석됩니다.

## 비동기 유효성 검사

비동기 유효성 검사는 즉각적인 피드백을 제공하지 않는 유효성 검사 방법입니다. 대신 데이터가 손실되지 않도록 [!DNL Data Lake]에서 실패한 배치로 데이터가 전송됩니다. 이 실패한 데이터는 나중에 검색하여 추가 분석 및 재생을 수행할 수 있습니다. 이 방법은 프로덕션에 사용해야 합니다. 별도로 요청되지 않는 한 스트리밍 수집은 비동기 유효성 검사 모드에서 작동합니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

비동기 유효성 검사를 사용하여 데이터를 데이터 입구로 수집하려면 다음 요청을 제출하십시오.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 수집할 데이터의 JSON 본문. |

>[!NOTE]
>
>비동기 유효성 검사가 기본적으로 활성화되어 있으므로 추가 쿼리 매개 변수는 필요하지 않습니다.

**응답**

비동기 유효성 검사가 활성화되면 성공적인 응답이 다음을 반환합니다.

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

명시적으로 요청하지 않았기 때문에 동기 유효성 검사를 건너뛴 응답 상태를 확인하십시오.

## 부록

이 섹션에는 데이터 섭취에 대한 응답에 대한 다양한 상태 코드가 의미하는 바에 대한 정보가 포함되어 있습니다.

### 상태 코드

| 상태 코드 | 무슨 의미입니까 |
| ----------- | ------------- |
| 200 | 성공. 동기 유효성 검사의 경우 유효성 검사 검사를 통과했음을 의미합니다. 비동기 유효성 검사의 경우 메시지를 성공적으로 수신했음을 의미합니다. 사용자는 데이터 집합을 관찰하여 최종 메시지 상태를 확인할 수 있습니다. |
| 400 | 오류. 요청에 문제가 있습니다. 스트리밍 유효성 검사 서비스에서 자세한 내용이 포함된 오류 메시지를 받았습니다. |
| 401년 | 오류. 요청이 허가되지 않았습니다. 베어러 토큰으로 요청해야 합니다. 액세스를 요청하는 방법에 대한 자세한 내용은 이 [자습서](https://www.adobe.com/go/platform-api-authentication-en) 또는 이 [블로그 게시물](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)을 확인하십시오. |
| 500 | 오류. 내부 시스템 오류가 있습니다. |
| 501년 | 오류. 즉, 동기 유효성 검사가 이 위치에 대해 지원되지 않는 **입니다.** |
| 503년 | 오류. 현재 서비스를 사용할 수 없습니다. 클라이언트는 지수 백오프 전략을 사용하여 적어도 세 번 다시 시도해야 합니다. |
