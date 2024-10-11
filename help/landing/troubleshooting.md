---
keywords: Experience Platform;홈;인기 항목;API 오류 코드;API 오류 코드;오류 코드 API;오류 코드 API;API 요청 오류;API 문제 해결;API 오류
solution: Experience Platform
title: Adobe Experience Platform FAQ 및 문제 해결 안내서
description: 자주 묻는 질문에 대한 답변과 Adobe Experience Platform에서 일반적인 오류를 해결하기 위한 안내서를 확인합니다.
landing-page-description: 자주 묻는 질문에 대한 답변과 Adobe Experience Platform에서 일반적인 오류를 해결하기 위한 안내서를 확인합니다.
short-description: 자주 묻는 질문에 대한 답변과 Experience Platform에서 일반적인 오류를 해결하기 위한 안내서를 확인합니다.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 4%

---

# [!DNL Platform] FAQ 및 문제 해결 안내서

이 문서에서는 Adobe Experience Platform에 대해 자주 묻는 질문에 대한 답변과 [!DNL Experience Platform] API에서 발생할 수 있는 일반적인 오류에 대한 높은 수준의 문제 해결 안내서를 제공합니다. 개별 [!DNL Platform] 서비스에 대한 문제 해결 안내서는 아래의 [서비스 문제 해결 디렉터리](#service-troubleshooting-directory)를 참조하십시오.

## FAQ {#faq}

다음은 Adobe Experience Platform에 대한 FAQ 응답 목록입니다.

## [!DNL Experience Platform] API란? {#what-are-experience-platform-apis}

[!DNL Experience Platform]은(는) HTTP 요청을 사용하여 [!DNL Platform] 리소스에 액세스하는 여러 RESTful API를 제공합니다. 이러한 서비스 API는 각각 여러 끝점을 노출하며, 이를 통해 리소스를 나열(GET), 조회(GET), 편집(PUT 및/또는 PATCH), 삭제(DELETE) 작업을 수행할 수 있습니다. 각 서비스에 사용할 수 있는 특정 끝점 및 작업에 대한 자세한 내용은 Adobe I/O에서 [API 참조 설명서](https://www.adobe.com/go/platform-api-reference-en)를 참조하세요.

## API 요청을 포맷하려면 어떻게 합니까? {#how-do-i-format-an-api-request}

요청 형식은 사용 중인 [!DNL Platform] API에 따라 다릅니다. 사용 중인 특정 [!DNL Platform] 서비스에 대한 설명서에 제공된 예제를 따라 API 호출을 구성하는 방법을 알아봅니다.

API 요청 형식에 대한 자세한 내용은 Platform API 시작 안내서 [샘플 API 호출 읽기](./api-guide.md#sample-api) 섹션을 참조하십시오.

## 내 조직이란? {#what-is-my-ims-organization}

조직은 고객을 Adobe으로 표현한 것입니다. 라이센스가 부여된 모든 Adobe 솔루션은 이 고객 조직과 통합됩니다. 조직에서 [!DNL Experience Platform]에 대한 권한이 있는 경우 개발자에게 액세스 권한을 할당할 수 있습니다. 조직 ID(`x-gw-ims-org-id`)는 API 호출을 실행해야 하는 조직을 나타내므로 모든 API 요청에 헤더로 필요합니다. 이 ID는 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)을 통해 찾을 수 있습니다. **통합** 탭에서 특정 통합에 대한 **개요** 섹션으로 이동하여 **클라이언트 자격 증명**&#x200B;에서 ID를 찾으십시오. [!DNL Platform]에 인증하는 방법에 대한 단계별 연습은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오.

## API 키는 어디에서 찾을 수 있습니까? {#where-can-i-find-my-api-key}

API 키는 모든 API 요청의 헤더로 필요합니다. [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)을 통해 찾을 수 있습니다. 콘솔 내의 **통합** 탭에서 특정 통합을 위한 **개요** 섹션으로 이동하면 **클라이언트 자격 증명**&#x200B;에서 키를 찾을 수 있습니다. [!DNL Platform]에 인증하는 방법에 대한 단계별 연습은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오.

## 액세스 토큰을 얻는 방법 {#how-do-i-get-an-access-token}

모든 API 호출의 인증 헤더에 액세스 토큰이 필요합니다. 조직의 통합에 액세스할 수 있는 경우 CURL 명령을 사용하여 생성할 수 있습니다. 액세스 토큰은 24시간 동안만 유효하며, 그 이후에는 API를 계속 사용하려면 새 토큰을 생성해야 합니다. 액세스 토큰 생성에 대한 자세한 내용은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오.

## 쿼리 매개 변수는 어떻게 사용합니까? {#how-do-i-user-query-parameters}

일부 [!DNL Platform] API 끝점은 쿼리 매개 변수를 사용하여 특정 정보를 찾고 응답에서 반환된 결과를 필터링합니다. 쿼리 매개 변수는 `paramName=paramValue` 형식을 사용하여 하나 이상의 쿼리 매개 변수 뒤에 물음표(`?`) 기호가 있는 요청 경로에 추가됩니다. 단일 호출에서 여러 매개 변수를 결합할 경우 앰퍼샌드(`&`)를 사용하여 개별 매개 변수를 분리해야 합니다. 다음 예는 여러 쿼리 매개 변수를 사용하는 요청이 설명서에 표시되는 방법을 보여 줍니다.

일반적으로 사용되는 쿼리 매개 변수의 예는 다음과 같습니다.

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

특정 서비스 또는 끝점에 사용할 수 있는 쿼리 매개 변수에 대한 자세한 내용은 서비스별 설명서를 참조하십시오.

## PATCH 요청에서 업데이트할 JSON 필드를 어떻게 표시합니까? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

[!DNL Platform] API의 많은 PATCH 작업에서 [JSON 포인터](https://tools.ietf.org/html/rfc6901) 문자열을 사용하여 업데이트할 JSON 속성을 나타냅니다. 이는 일반적으로 [JSON 패치](https://tools.ietf.org/html/rfc6902) 형식을 사용하여 요청 페이로드에 포함됩니다. 이러한 기술에 필요한 구문에 대한 자세한 내용은 [API 기본 사항 안내서](api-fundamentals.md)를 참조하십시오.

## Postman을 사용하여 [!DNL Platform] API를 호출할 수 있습니까? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/)은(는) RESTful API에 대한 호출을 시각화하는 데 유용한 도구입니다. [Platform API 시작 안내서](api-guide.md)에는 Postman 컬렉션을 가져오기 위한 비디오와 지침이 포함되어 있습니다. 또한 각 서비스에 대한 Postman 컬렉션 목록이 제공됩니다.

## [!DNL Platform]에 대한 시스템 요구 사항은 무엇입니까? {#what-are-the-system-requirements-for-platform}

UI 또는 API 사용 여부에 따라 다음 시스템 요구 사항이 적용됩니다.

**UI 기반 작업의 경우:**
- 최신 표준 웹 브라우저입니다. 최신 버전의 [!DNL Chrome]이(가) 권장되지만 [!DNL Firefox], [!DNL Internet Explorer] 및 Safari의 현재 및 이전 주요 릴리스도 지원됩니다.
   - 새 주요 버전이 릴리스될 때마다 [!DNL Platform]은(는) 최신 버전을 지원하기 시작하지만 세 번째 최신 버전에 대한 지원은 중단됩니다.
- 모든 브라우저에는 쿠키와 JavaScript이 활성화되어 있어야 합니다.

**API 및 개발자 상호 작용의 경우:**
- REST, 스트리밍 및 Webhook 통합을 위해 개발할 개발 환경입니다.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

다음은 [!DNL Experience Platform] 서비스를 사용할 때 발생할 수 있는 오류 목록입니다. 개별 [!DNL Platform] 서비스에 대한 문제 해결 안내서는 아래의 [서비스 문제 해결 디렉터리](#service-troubleshooting-directory)를 참조하십시오.

## API 상태 코드 {#api-status-codes}

[!DNL Experience Platform] API에서 다음 상태 코드를 찾을 수 있습니다. 각각은 다양한 원인을 가지고 있으므로, 이 절에서 설명하는 내용은 본질적으로 일반적이다. 개별 [!DNL Platform] 서비스의 특정 오류에 대한 자세한 내용은 아래의 [서비스 문제 해결 디렉터리](#service-troubleshooting-directory)를 참조하십시오.

| 상태 코드 | 설명 | 가능한 원인 |
|--- | --- | ---|
| 400 | 잘못된 요청 | 요청이 잘못 구성되었거나, 키 정보가 누락되었거나, 잘못된 구문이 들어 있습니다. |
| 401 | 인증 실패 | 요청이 인증 검사를 통과하지 못했습니다. 액세스 토큰이 누락되었거나 유효하지 않을 수 있습니다. 자세한 내용은 아래의 [OAuth 토큰 오류](#oauth-token-is-missing) 섹션을 참조하십시오. |
| 403 | 금지 | 리소스를 찾았지만 볼 수 있는 자격 증명이 없습니다. <br> 이 오류의 가능한 원인은 리소스에 액세스하거나 편집하는 데 필요한 [액세스 제어 권한](/help/access-control/home.md)이 없기 때문일 수 있습니다. Platform API를 사용하기 위해 [필요한 특성 기반 액세스 제어 권한을 얻는 방법](/help/landing/api-authentication.md#get-abac-permissions)을 읽어 보십시오. </p> |
| 404 | 찾을 수 없음 | 요청한 리소스를 서버에서 찾을 수 없습니다. 리소스가 삭제되었거나 요청한 경로가 잘못 입력되었을 수 있습니다. |
| 500 | 내부 서버 오류 | 서버측 오류입니다. 여러 번 동시에 호출하는 경우 API 제한에 도달하고 결과를 필터링해야 할 수 있습니다. 자세한 내용은 [데이터 필터링](../catalog/api/filter-data.md)에 대한 [!DNL Catalog Service] API 개발자 안내서 하위 가이드를 참조하십시오. 요청을 다시 시도하기 전에 잠시 기다린 후 문제가 지속되면 관리자에게 문의하십시오. |

## 요청 헤더 오류 {#request-header-errors}

[!DNL Platform]의 모든 API 호출에는 특정 요청 헤더가 필요합니다. 개별 서비스에 필요한 헤더를 확인하려면 [API 참조 설명서](https://www.adobe.com/go/platform-api-reference-en)를 참조하십시오. 필요한 인증 헤더의 값을 찾으려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오. API 호출을 수행할 때 이러한 헤더가 누락되거나 유효하지 않은 경우 다음 오류가 발생할 수 있습니다.

### OAuth 토큰이 누락되었습니다 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

API 요청에서 `Authorization` 헤더가 누락된 경우 이 오류 메시지가 표시됩니다. 인증 헤더가 유효한 액세스 토큰에 포함되어 있는지 확인한 후 다시 시도하십시오.

### OAuth 토큰이 잘못되었습니다. {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

이 오류 메시지는 `Authorization` 헤더의 제공된 액세스 토큰이 유효하지 않을 때 표시됩니다. 토큰을 올바르게 입력했는지 확인하거나 Adobe I/O 콘솔에서 [새 토큰을 생성](https://www.adobe.com/go/platform-api-authentication-en)하십시오.

### API 키가 필요합니다. {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

이 오류 메시지는 API 요청에서 API 키 헤더(`x-api-key`)가 누락된 경우 표시됩니다. 헤더가 유효한 API 키에 포함되어 있는지 확인한 후 다시 시도하십시오.

### API 키가 잘못되었습니다. {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

제공된 API 키 헤더(`x-api-key`)의 값이 잘못된 경우 이 오류 메시지가 표시됩니다. 키를 올바르게 입력했는지 확인한 후 다시 시도하십시오. API 키를 모를 경우 [Adobe I/O 콘솔](https://console.adobe.io)에서 찾을 수 있습니다. **통합** 탭에서 특정 통합에 대한 **개요** 섹션으로 이동하여 **클라이언트 자격 증명**&#x200B;에서 API 키를 찾습니다.

### 헤더 누락 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

이 오류 메시지는 API 요청에서 조직 헤더(`x-gw-ims-org-id`)가 누락된 경우 표시됩니다. 헤더가 조직의 ID에 포함되어 있는지 확인한 후 다시 시도하십시오.

### 프로필이 올바르지 않음 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

이 오류 메시지는 사용자 또는 Adobe I/O 통합(`Authorization` 헤더의 [액세스 토큰](#how-do-i-get-an-access-token)(으)로 식별됨)이 `x-gw-ims-org-id` 헤더에 제공된 조직의 [!DNL Experience Platform] API를 호출할 수 없는 경우에 표시됩니다. 헤더에 조직에 대한 올바른 ID를 입력했는지 확인한 후 다시 시도하십시오. 조직 ID를 모를 경우 [Adobe I/O 콘솔](https://console.adobe.io)에서 찾을 수 있습니다. **통합** 탭의 **개요** 섹션으로 이동하여 특정 통합을 위해 **클라이언트 자격 증명**&#x200B;에서 ID를 찾습니다.

### Etag 새로 고침 오류 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

다른 API 호출자가 흐름, 연결, 소스 커넥터 또는 타겟 연결과 같은 소스 또는 대상 엔티티를 변경한 경우 etag 오류가 발생할 수 있습니다. 버전 불일치로 인해 수행하려는 변경 사항이 최신 버전의 엔티티에 적용되지 않습니다.

이 문제를 해결하려면 엔터티를 다시 가져오고 변경 내용이 새 버전의 엔터티와 호환되는지 확인한 다음 `If-Match` 헤더에 새 태그를 배치하고 마지막으로 API를 호출해야 합니다.

### 유효한 콘텐츠 유형이 지정되지 않음 {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

이 오류 메시지는 POST, PUT 또는 PATCH 요청에 잘못되거나 누락된 `Content-Type` 헤더가 있는 경우 표시됩니다. 헤더가 요청에 포함되어 있고 해당 값이 `application/json`인지 확인하십시오.

### 사용자 영역이 누락되었습니다. {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

이 오류 메시지는 아래 두 가지 경우 중 하나에 표시됩니다.
- API 요청에서 잘못되거나 잘못된 조직 ID 헤더(`x-gw-ims-org-id`)가 전달된 경우. 조직의 올바른 ID가 포함되어 있는지 확인한 후 다시 시도하십시오.
- 제공된 인증 자격 증명으로 표시된 계정이 Experience Platform을 위한 제품 프로필과 연결되어 있지 않은 경우. Platform API 인증 자습서에서 [액세스 자격 증명을 생성](./api-authentication.md#authentication-for-each-session)하는 단계에 따라 계정에 플랫폼을 추가하고 그에 따라 인증 자격 증명을 업데이트합니다.

## 서비스 문제 해결 디렉터리 {#service-troubleshooting-directory}

다음은 [!DNL Experience Platform] API에 대한 문제 해결 가이드 및 API 참조 설명서 목록입니다. 각 문제 해결 안내서에서는 FAQ에 대한 답변과 개별 [!DNL Platform] 서비스와 관련된 문제에 대한 해결 방법을 제공합니다. API 참조 문서는 각 서비스에 대해 사용 가능한 모든 끝점에 대한 포괄적인 안내서를 제공하며, 받을 수 있는 샘플 요청 본문, 응답 및 오류 코드를 보여 줍니다.

| 서비스 | API 참조 | 문제 해결 |
| --- | --- | --- |
| 액세스 제어 | [액세스 제어 API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [액세스 제어 문제 해결 가이드](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform 데이터 수집 | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [일괄 처리 수집 문제 해결 안내서](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform 데이터 수집 | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [스트리밍 수집 문제 해결 안내서](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform 데이터 과학 Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 문제 해결 가이드](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform 데이터 거버넌스 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform ID 서비스 | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 문제 해결 가이드](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform 쿼리 서비스 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 문제 해결 가이드](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform 세그멘테이션 | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model](XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] FAQ 및 문제 해결 안내서](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service]([!DNL Sources] 및 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 문제 해결 가이드](../profile/troubleshooting.md) |
| 샌드박스 | [샌드박스 API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [샌드박스 문제 해결 안내서](../sandboxes/troubleshooting-guide.md) |
