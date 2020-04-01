---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스트리밍 통합 유효성 검사
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# 스트리밍 통합 유효성 검사

스트리밍 통합 기능을 사용하면 스트리밍 끝점을 사용하여 실시간으로 Adobe Experience Platform에 데이터를 업로드할 수 있습니다. 스트리밍 통합 API는 동기식 및 비동기식 두 가지 인증 모드를 지원합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [XDM(Experience Data Model) 시스템](../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [스트리밍 통합](../streaming-ingestion/overview.md):Experience Platform으로 데이터를 전송할 수 있는 방법 중 하나입니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

스키마 레지스트리에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: `application/json`

### 유효성 검사 적용 범위

Streaming Validation Service는 다음 영역의 유효성 검사를 다룹니다.
- 범위
- 현재 상태
- 열거형
- 패턴
- 유형
- 형식

## 동기 유효성 검사

동기 유효성 검사는 통합 실패 이유에 대한 즉각적인 피드백을 제공하는 유효성 검사 방법입니다. 하지만 실패 시 유효성 검사에 실패한 레코드는 삭제되고 다운스트림으로 전송되지 않습니다. 따라서 동기 유효성 검사는 개발 프로세스 동안에만 사용해야 합니다. 동기 유효성 검사를 수행할 때 호출자에게 XDM 유효성 검사 결과와 실패 이유를 모두 알려 줍니다.

기본적으로 동기 유효성 검사가 설정되지 않습니다. 이를 활성화하려면 API 호출을 수행할 `synchronousValidation=true` 때 선택적 쿼리 매개 변수를 전달해야 합니다. 또한 현재 스트림 끝점이 VA7 데이터 센터에 있는 경우에만 동기식 유효성 검사를 사용할 수 있습니다.

동기 유효성 검사 중에 메시지가 실패하면 메시지가 출력 대기열에 기록되지 않고 사용자에게 즉각적인 피드백을 제공합니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

동기 유효성 검사를 통해 데이터를 데이터 입력부로 인제스트하려면 다음 요청을 제출하십시오.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 인제스트할 데이터의 JSON 본문입니다. |

**응답**

동기 유효성 검사가 활성화되면 성공한 응답에는 페이로드에서 발생한 유효성 검사 오류가 포함됩니다.

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

위의 응답에는 검색된 스키마 위반 수와 위반 사항이 나열됩니다. 예를 들어, 이 응답에는 키가 스키마에서 정의되지 `workEmail` 않았으며 `person` 따라서 허용되지 않는다고 표시됩니다. 스키마에는 `_id` 잘못된 값이 `string``long` 예상되었지만 대신 삽입된 것이므로 잘못된 값으로 플래그합니다. 5개의 오류가 발생하면 해당 메시지 처리가 **중지됩니다** . 그러나 다른 메시지는 계속 구문 분석됩니다.

## 비동기 유효성 검사

비동기 유효성 검사는 즉각적인 피드백을 제공하지 않는 유효성 검사 방법입니다. 대신 데이터가 데이터 손실을 방지하기 위해 Data Lake에서 실패한 묶음으로 전송됩니다. 나중에 이 실패한 데이터를 검색하여 다시 재생할 수 있습니다. 이 방법은 생산에 사용되어야 한다. 별도로 요청되지 않는 한 스트리밍 통합 기능은 비동기 유효성 검사 모드에서 작동합니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

비동기 유효성 검사를 통해 데이터를 데이터 입력부로 인제스트하려면 다음 요청을 제출합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 인제스트할 데이터의 JSON 본문입니다. |

>[!NOTE] 비동기 유효성 검사가 기본적으로 활성화되어 있으므로 추가 쿼리 매개 변수가 필요하지 않습니다.

**응답**

비동기 유효성 검사가 활성화되면 성공적인 응답은 다음을 반환합니다.

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

동기 유효성 검사가 명시적으로 요청되지 않았기 때문에 응답을 건너뛰는 방법을 확인하십시오.

## 부록

이 섹션에는 데이터 인제스트 응답에 대한 다양한 상태 코드가 의미하는 사항에 대한 정보가 포함되어 있습니다.

### 상태 코드

| 상태 코드 | What it means |
| ----------- | ------------- |
| 200 | 성공. 동기 유효성 확인의 경우 유효성 검사를 통과했음을 의미합니다. 비동기 유효성 검사의 경우, 메시지를 수신한 것만을 의미합니다. 사용자는 데이터 세트를 관찰하여 최종 메시지 상태를 확인할 수 있습니다. |
| 400 | 오류. 귀하의 요청에 문제가 있습니다. 자세한 내용이 포함된 오류 메시지가 스트리밍 유효성 검사 서비스로부터 수신됩니다. |
| 401 | 오류. 요청이 인증되지 않았습니다. 베어러 토큰을 요청해야 합니다. 액세스 권한을 요청하는 방법에 대한 자세한 내용은 이 [자습서](../../tutorials/authentication.md) 또는 이 [블로그 게시물을](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)참조하십시오. |
| 500 | 오류. 내부 시스템 오류가 있습니다. |
| 501 | 오류. 즉, 이 위치에 대해 동기 유효성 검사가 **지원되지** 않습니다. |
| 503 | 오류. 서비스를 현재 사용할 수 없습니다. 클라이언트는 기하급수적인 백오프 전략을 사용하여 최소 3번 재시도해야 합니다. |