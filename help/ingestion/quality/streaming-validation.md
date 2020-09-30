---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestion;streaming ingestion validation;validation;Streaming ingestion validation;validate;Synchronous validation;synchronous validation;Asynchronous validation;asynchronous validation;
solution: Experience Platform
title: 스트리밍 통합 유효성 검사
topic: tutorial
type: Tutorial
description: 스트리밍 통합 기능을 사용하면 스트리밍 끝점을 실시간으로 사용하여 데이터를 Adobe Experience Platform에 업로드할 수 있습니다. 스트리밍 통합 API는 동기식 및 비동기식 두 가지 인증 모드를 지원합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 3%

---


# 스트리밍 통합 유효성 검사

스트리밍 통합 기능을 사용하면 스트리밍 끝점을 실시간으로 사용하여 데이터를 Adobe Experience Platform에 업로드할 수 있습니다. 스트리밍 통합 API는 동기식 및 비동기식 두 가지 인증 모드를 지원합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

- [[!DNL 경험 데이터 모델(XDM) 시스템]](../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
- [[!DNL 스트리밍 통합]](../streaming-ingestion/overview.md):데이터를 보낼 수 있는 방법 중 하나입니다 [!DNL Experience Platform].

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Schema Registry]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: `application/json`

### 유효성 검사 적용 범위

[!DNL Streaming Validation Service] 는 다음 영역의 유효성 검사를 포함합니다.
- 범위
- 현재 상태
- 열거형
- 패턴
- 유형
- 형식

## 동기 유효성 검사

동기 유효성 검사는 통합 실패 이유에 대한 즉각적인 피드백을 제공하는 유효성 검사 방법입니다. 하지만 실패 시 유효성 검사에 실패한 레코드가 삭제되고 다운스트림으로 전송되지 않습니다. 따라서 동기 유효성 검사는 개발 과정에서만 사용해야 합니다. 동기 유효성 검사를 수행할 때 호출자에게 XDM 유효성 검사 결과와 실패 이유를 모두 알려 줍니다.

기본적으로 동기 유효성 검사가 켜져 있지 않습니다. 이를 활성화하려면 API 호출 시 선택적 쿼리 매개 변수 `synchronousValidation=true` 를 전달해야 합니다. 또한 현재 스트림 끝점이 VA7 데이터 센터에 있는 경우에만 동기식 유효성 검사를 사용할 수 있습니다.

동기 유효성 검사 중에 메시지가 실패하면 출력 대기열에 메시지가 기록되지 않으므로 사용자에게 즉각적인 피드백을 제공합니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

동기 유효성 검사를 통해 데이터 입구로 데이터를 인제스트하려면 다음 요청을 제출하십시오.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 인제스트할 데이터의 JSON 본문. |

**응답**

동기 유효성 검사가 활성화된 경우 성공한 응답에는 페이로드에서 발생한 모든 유효성 검사 오류가 포함됩니다.

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

위의 응답에는 검색된 스키마 위반 수와 위반 사항이 나열됩니다. 예를 들어, 이 응답에는 스키마에서 키와 키 `workEmail` 가 정의되지 `person` 않았으므로 허용되지 않는다고 표시됩니다. 또한 스키마가 예상되었지만 대신 `_id` 가 삽입되었으므로 에 대한 값 `string`에 잘못된 플래그를 `long` 지정합니다. 5개의 오류가 발생하면 유효성 검사 서비스가 해당 메시지 처리를 **중지합니다** . 하지만 다른 메시지는 계속 구문 분석됩니다.

## 비동기 유효성 검사

비동기 유효성 검사는 즉각적인 피드백을 제공하지 않는 유효성 검사 방법입니다. 대신 데이터 손실을 방지하기 위해 데이터가 실패한 일괄 처리 [!DNL Data Lake] 로 전송됩니다. 나중에 이 실패한 데이터를 검색하여 다시 볼 수 있습니다. 이 방법은 제조업에 사용해야 한다. 별도로 요청되지 않는 한 스트리밍 통합 기능은 비동기 유효성 검사 모드에서 작동합니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

비동기 유효성 검사를 통해 데이터 입구로 데이터를 인제스트하려면 다음 요청을 제출합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 인제스트할 데이터의 JSON 본문. |

>[!NOTE]
>
>비동기 유효성 검사가 기본적으로 활성화되므로 추가 쿼리 매개 변수가 필요하지 않습니다.

**응답**

비동기 유효성 검사가 활성화된 경우 성공적인 응답으로 다음을 반환합니다.

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

동기 유효성 검사가 명시적으로 요청되지 않았기 때문에 응답에서 건너뛴 방법을 확인하십시오.

## 부록

이 섹션에는 데이터 인제스트 응답에 대한 다양한 상태 코드가 의미하는 사항에 대한 정보가 포함되어 있습니다.

### 상태 코드

| 상태 코드 | 무엇을 의미합니까 |
| ----------- | ------------- |
| 200 | 성공. 동기 유효성 검사의 경우 유효성 검사를 통과했음을 의미합니다. 비동기 유효성 검사의 경우, 메시지를 성공적으로 수신했음을 의미합니다. 사용자는 데이터 세트를 관찰하여 최종 메시지 상태를 확인할 수 있습니다. |
| 400 | 오류. 당신 요청에 문제가 있습니다. 자세한 내용이 포함된 오류 메시지가 스트리밍 유효성 검사 서비스로부터 수신됩니다. |
| 401 | 오류. 요청이 인증되지 않았습니다. 무기명 토큰을 통해 요청해야 합니다. 액세스를 요청하는 방법에 대한 자세한 내용은 이 [자습서](../../tutorials/authentication.md) 또는 이 [블로그 게시물을 참조하십시오](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | 오류. 내부 시스템 오류가 있습니다. |
| 501 | 오류. 즉, 이 위치에 대해 동기 유효성 검사가 **지원되지** 않습니다. |
| 503 | 오류. 현재 서비스를 사용할 수 없습니다. 클라이언트는 기하급수적인 백오프 전략을 사용하여 최소 3번 재시도해야 합니다. |