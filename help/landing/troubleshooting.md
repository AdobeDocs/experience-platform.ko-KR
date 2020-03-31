---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform FAQ 및 문제 해결 가이드
topic: getting started
translation-type: tm+mt
source-git-commit: 260eddee41d337f25b90ab365a76ab2ffd3dedef

---


# 플랫폼 FAQ 및 문제 해결 가이드

이 문서에서는 Adobe Experience Platform에 대한 FAQ와 Adobe Experience Platform API에서 발생할 수 있는 일반적인 오류에 대한 고급 문제 해결 안내서를 제공합니다. 개별 플랫폼 서비스에 대한 문제 해결 가이드를 보려면 아래 [서비스 문제 해결 디렉토리를](#service-troubleshooting-directory) 참조하십시오.

## FAQ {#faq}

다음은 Adobe Experience Platform에 대한 FAQ에 대한 답변 목록입니다.

## Experience Platform API란 무엇입니까? {#what-are-experience-platform-apis}

Experience Platform은 플랫폼 리소스에 액세스하기 위해 HTTP 요청을 사용하는 여러 RESTful API를 제공합니다. 이러한 서비스 API는 여러 끝점을 노출하며, 목록(GET), 조회(GET), 편집(PUT 및/또는 PATCH), 삭제(DELETE) 리소스 작업을 수행할 수 있도록 해줍니다. 각 서비스에 사용할 수 있는 특정 끝점 및 작업에 대한 자세한 내용은 Adobe I/O에 [대한 API 참조 설명서를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) 참조하십시오.

## API 요청의 포맷은 어떻게 됩니까? {#how-do-i-format-an-api-request}

요청 형식은 사용되는 플랫폼 API에 따라 다릅니다. API 호출을 구성하는 방법을 학습하는 가장 좋은 방법은 사용 중인 특정 플랫폼 서비스에 대한 설명서에 나와 있는 예제를 따르는 것입니다.

### 예제 API 호출 읽기

경험 플랫폼의 설명서에는 두 가지 방법으로 API 호출 예를 보여줍니다. 먼저 호출은 API 형식 ****, 작업(GET, POST, PUT, PATCH, DELETE)과 사용되는 끝점(예: `/global/classes`)만 표시하는 템플릿 표현으로 제공됩니다. 일부 템플릿은 호출을 구성하는 방법을 설명하는 데 도움이 되는 변수의 위치를 보여줍니다(예: `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`).

그런 다음 호출은 API와 성공적으로 상호 작용하는 데 **필요한**&#x200B;헤더와 전체 &quot;기본 경로&quot;를 포함하는 요청에 cURL 명령으로 표시됩니다. 기본 경로는 모든 끝점에 미리 포함되어야 합니다. 예를 들어 앞서 언급한 `/global/classes` 종점이 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`됩니다. 설명서 전체에서 API 형식/요청 패턴을 볼 수 있으며 플랫폼 API를 직접 호출할 때 요청 예제에 표시된 전체 경로를 사용할 수 있습니다.

### API 요청 예

다음은 설명서에서 보게 될 형식을 보여 주는 API 요청의 예입니다.

**API 형식**

API 형식은 사용 중인 작업(GET 파섹) 및 끝점을 표시합니다. 변수는 중괄호로 표시됩니다(이 경우, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**요청**

이 예제 요청에서 API 형식의 변수는 요청 경로에서 실제 값을 받습니다. 모든 필수 헤더뿐만 아니라 샘플 헤더 값 또는 중요한 정보(예: 보안 토큰 및 액세스 ID)가 포함되어야 하는 변수도 표시됩니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답은 전송된 요청을 기준으로 API에 대한 성공적인 호출 후 받을 내용을 보여줍니다. 경우에 따라 대수가 잘려서 샘플에 표시되는 추가 정보나 추가 정보를 볼 수 있습니다.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

필수 헤더 및 요청 본문을 포함하여 플랫폼 API의 특정 끝점에 대한 자세한 내용은 API [참조 설명서를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)참조하십시오.

## IMS 조직이란 무엇입니까? {#what-is-my-ims-organization}

IMS 조직은 고객의 Adobe 대표입니다. 라이선스가 부여된 모든 Adobe 솔루션은 이 고객 조직과 통합됩니다. IMS 조직에서 경험 플랫폼을 이용할 수 있는 경우 개발자에게 액세스 권한을 할당할 수 있습니다. IMS 조직 ID(`x-gw-ims-org-id`)는 API 호출이 실행되어야 하는 조직을 나타내며, 따라서 모든 API 요청의 헤더로 필요합니다. 이 ID는 Adobe I/O 콘솔을 통해 [찾을 수 있습니다](https://console.adobe.io/).통합 **탭에서** 특정 **통합에 대한** 개요 섹션으로 이동하여 클라이언트 자격 증명에서 ID를 **찾습니다**. 플랫폼에 대한 인증 방법에 대한 단계별 연습은 [인증 자습서를](../tutorials/authentication.md)참조하십시오.

## API 키는 어디에서 찾을 수 있습니까? {#where-can-i-find-my-api-key}

API 키는 모든 API 요청의 헤더로 필요합니다. Adobe I/O 콘솔을 통해 [확인할 수 있습니다](https://console.adobe.io/). 콘솔 내의 통합 **탭에서** 특정 **통합에** 대한 개요 섹션으로 이동하면 클라이언트 자격 증명에 있는 키가 **표시됩니다**. 플랫폼에 대한 인증 방법에 대한 단계별 연습은 [인증 자습서를](../tutorials/authentication.md)참조하십시오.

## 액세스 토큰은 어떻게 받습니까? {#how-do-i-get-an-access-token}

액세스 토큰은 모든 API 호출의 인증 헤더에 필요합니다. IMS 조직에 대한 통합에 액세스할 수 있는 경우 `curl` 명령을 사용하여 생성할 수 있습니다. 액세스 토큰은 24시간 동안만 유효하며, 이후에는 API를 계속 사용하려면 새 토큰을 생성해야 합니다. 액세스 토큰 생성에 대한 자세한 내용은 [인증 자습서를](../tutorials/authentication.md)참조하십시오.

## 쿼리 매개 변수는 어떻게 사용합니까? {#how-do-i-user-query-parameters}

일부 플랫폼 API 끝점은 쿼리 매개 변수를 사용하여 특정 정보를 찾고 응답에서 반환된 결과를 필터링합니다. 쿼리 매개 변수는 요청 경로에 물음표(`?`) 기호가 추가되고 형식을 사용하여 하나 이상의 쿼리 매개 변수가 추가됩니다 `paramName=paramValue`. 단일 호출에서 여러 매개 변수를 결합할 때는 앰퍼샌드(`&`)를 사용하여 개별 매개 변수를 구분해야 합니다. 다음 예에서는 여러 쿼리 매개 변수를 사용하는 요청이 설명서에서 어떻게 표시되는지 보여줍니다.

일반적으로 사용되는 쿼리 매개 변수의 예는 다음과 같습니다.

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

특정 서비스 또는 종단점에 사용할 수 있는 쿼리 매개 변수에 대한 자세한 내용은 서비스별 설명서를 참조하십시오.

## PATCH 요청에서 업데이트할 JSON 필드를 어떻게 나타냅니까? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

플랫폼 API의 많은 PATCH 작업에서는 JSON [포인터](https://tools.ietf.org/html/rfc6901) 문자열을 사용하여 업데이트할 JSON 속성을 나타냅니다. 이러한 항목은 일반적으로 JSON 패치 [형식을 사용하여 요청 페이로드에](https://tools.ietf.org/html/rfc6902) 포함됩니다. 이러한 [기술에 필요한 구문에 대한 자세한 내용은 API 기본 가이드](api-fundamentals.md) 를 참조하십시오.

## Postman을 사용하여 플랫폼 API를 호출할 수 있습니까? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) 은 RESTful API에 대한 호출을 시각화하는 데 유용한 도구입니다. 이 [중간 게시물은](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Postman을 설정하여 자동으로 인증을 수행하고 이를 사용하여 Experience Platform API를 사용하는 방법에 대해 설명합니다.

## 플랫폼의 시스템 요구 사항은 무엇입니까? {#what-are-the-system-requirements-for-platform}

UI 또는 API를 사용 중인지 여부에 따라 다음 시스템 요구 사항이 적용됩니다.

**UI 기반 작업의 경우:**
- 최신 표준 웹 브라우저 최신 버전의 Chrome이 권장되지만 Firefox, Internet Explorer 및 Safari의 최신 및 이전 주요 릴리스가 지원됩니다.
   - 새로운 주요 버전이 출시될 때마다 Platform은 최신 버전을 지원하는 동시에 세 번째 최신 버전에 대한 지원이 중단됩니다.
- 모든 브라우저에는 쿠키와 JavaScript가 활성화되어 있어야 합니다.

**API 및 개발자 인터랙션의 경우**
- REST, 스트리밍 및 웹후크 통합을 위한 개발 환경입니다.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

다음은 Experience Platform 서비스를 사용할 때 발생할 수 있는 오류 목록입니다. 개별 플랫폼 서비스에 대한 문제 해결 가이드를 보려면 아래 [서비스 문제 해결 디렉토리를](#service-troubleshooting-directory) 참조하십시오.

## API 상태 코드 {#api-status-codes}

Experience Platform API에서 다음 상태 코드가 나타날 수 있습니다. 각각 다양한 원인이 있으므로 이 섹션에서 제공하는 설명은 일반적으로 자연적입니다. 개별 플랫폼 서비스의 특정 오류에 대한 자세한 내용은 아래 [서비스 문제 해결 디렉토리를](#service-troubleshooting-directory) 참조하십시오.

| 상태 코드 | 설명 | 가능한 원인 |
--- | --- | ---
| 400 | 잘못된 요청 | 요청이 잘못 구성되었거나, 키 정보가 누락되었거나, 잘못된 구문이 포함되어 있습니다. |
| 401 | 인증 실패 | 요청이 인증 검사를 통과하지 못했습니다. 액세스 토큰이 없거나 유효하지 않을 수 있습니다. 자세한 내용은 [아래 OAuth 토큰 오류](#oauth-token-is-missing) 섹션을 참조하십시오. |
| 403 | 금지 | 리소스를 찾았지만 볼 수 있는 자격 증명이 없습니다. |
| 404 | 찾을 수 없음 | 요청한 리소스를 서버에서 찾을 수 없습니다. 리소스가 삭제되었거나 요청된 경로가 잘못 입력되었을 수 있습니다. |
| 500 | 내부 서버 오류 | 서버 측 오류입니다. 여러 개의 동시 호출을 수행하는 경우 API 제한에 도달하고 결과를 필터링해야 할 수 있습니다. (자세한 내용은 [데이터](../catalog/api/filter-data.md) 필터링에 대한 자세한 내용은 카탈로그 서비스 API 개발자 가이드 하위 안내서를 참조하십시오.) 요청을 다시 시도하기 전에 잠시 기다린 후 문제가 계속되면 관리자에게 문의하십시오. |

## 요청 헤더 오류 {#request-header-errors}

플랫폼의 모든 API 호출에는 특정 요청 헤더가 필요합니다. 개별 서비스에 필요한 헤더는 API 참조 [설명서를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)참조하십시오. 필요한 인증 헤더의 값을 찾으려면 인증 [자습서를](../tutorials/authentication.md)참조하십시오. API 호출을 할 때 이러한 헤더가 누락되었거나 잘못된 경우 다음 오류가 발생할 수 있습니다.

### OAuth 토큰이 없습니다. {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

API 요청에서 `Authorization` 헤더가 누락되면 이 오류 메시지가 표시됩니다. 다시 시도하기 전에 권한 부여 헤더가 올바른 액세스 토큰에 포함되어 있는지 확인합니다.

### OAuth 토큰이 잘못되었습니다.

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

이 오류 메시지는 `Authorization` 헤더에 제공된 액세스 토큰이 유효하지 않을 때 표시됩니다. 토큰이 올바르게 입력되었는지 확인하거나 Adobe I/O 콘솔에서 새 토큰을 [](../tutorials/authentication.md) 생성합니다.

### API 키가 필요합니다.

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

이 오류 메시지는 API 키 헤더(`x-api-key`)가 API 요청에서 누락된 경우 표시됩니다. 헤더가 올바른 API 키에 포함되어 있는지 확인한 후 다시 시도하십시오.

### API 키가 잘못되었습니다.

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

제공된 API 키 헤더(`x-api-key`)의 값이 잘못된 경우 이 오류 메시지가 표시됩니다. 다시 시도하기 전에 키를 올바르게 입력했는지 확인하십시오. API 키를 모르는 경우 Adobe I/O 콘솔에서 찾을 수 [있습니다](https://console.adobe.io).통합 **탭에서** 특정 **통합에 대한** 개요 섹션으로 이동하여 클라이언트 자격 증명에서 API 키를 **찾습니다**.


### 헤더 누락

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

이 오류 메시지는 API 요청에서 IMS 조직 헤더(`x-gw-ims-org-id`)가 누락된 경우 표시됩니다. 다시 시도하기 전에 헤더가 IMS 조직의 ID에 포함되어 있는지 확인합니다.

### 프로필이 잘못되었습니다.

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

이 오류 메시지는 사용자 또는 Adobe I/O 통합(헤더에서 [액세스 토큰으로](#how-do-i-get-an-access-token) 식별됨)이 `Authorization` `x-gw-ims-org-id` 헤더에 제공된 IMS 조직에 대해 Experience Platform API를 호출할 권한이 없는 경우에 표시됩니다. 헤더에서 IMS 조직에 대해 올바른 ID를 제공한 후 다시 시도하십시오. 조직 ID를 모르는 경우 Adobe I/O 콘솔에서 찾을 수 [있습니다](https://console.adobe.io).통합 **탭에서** 특정 **통합에 대한** 개요 섹션으로 이동하여 클라이언트 자격 증명에서 ID를 **찾습니다**.

### 올바른 콘텐츠 형식을 지정하지 않았습니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

이 오류 메시지는 POST, PUT 또는 PATCH 요청에 잘못되었거나 누락된 `Content-Type` 헤더가 있을 때 표시됩니다. 헤더가 요청에 포함되고 해당 값이 `application/json`올바른지 확인합니다.


## 서비스 문제 해결 디렉토리 {#service-troubleshooting-directory}

다음은 Experience Platform API에 대한 문제 해결 가이드 및 API 참조 설명서 목록입니다. 각 문제 해결 가이드는 개별 플랫폼 서비스별 문제에 대한 질문과 해결 방법에 대한 답변을 제공합니다. API 참조 문서는 각 서비스에 대해 사용 가능한 모든 끝점에 대한 포괄적인 안내서를 제공하고 사용자가 수신할 수 있는 샘플 요청 본문, 응답 및 오류 코드를 보여줍니다.

| 서비스 | API 참조 | 문제 해결 |
--- | --- | ---
| 액세스 제어 | [액세스 제어 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [액세스 제어 문제 해결 가이드](../access-control/troubleshooting-guide.md) |
| 카탈로그 | [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| 데이터 통합(일괄 처리) | [데이터 통합 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [일괄 처리 문제 해결 가이드](../ingestion/batch-ingestion/troubleshooting.md) |
| 데이터 통합(스트리밍) | [데이터 통합 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [스트리밍 통합 문제 해결 가이드](../ingestion/streaming-ingestion/troubleshooting.md) |
| 데이터 과학 작업 영역 | [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [데이터 과학 작업 공간 문제 해결 가이드](../data-science-workspace/troubleshooting-guide.md) |
| 데이터 사용 레이블 지정 및 실행(DULE) | [DULE 정책 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| XDM(Experience Data Model) | [스키마 레지스트리 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [XDM 시스템 FAQ 및 문제 해결 가이드](../xdm/troubleshooting-guide.md) |
| ID 서비스 | [ID 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [ID 서비스 문제 해결 가이드](../identity-service/troubleshooting-guide.md) |
| 쿼리 서비스 | [쿼리 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [쿼리 서비스 문제 해결 가이드](../query-service/troubleshooting-guide.md) |
| 실시간 고객 프로필 | [실시간 고객 프로필 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| 샌드박스 | [샌드박스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [샌드박스 문제 해결 가이드](../sandboxes/troubleshooting-guide.md) |