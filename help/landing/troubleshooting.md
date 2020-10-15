---
keywords: Experience Platform;home;popular topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Adobe Experience Platform FAQ 및 문제 해결 안내서
description: 자주 묻는 질문에 대한 답변과 Experience Platform에서 일반적인 오류를 해결하기 위한 안내서를 확인하십시오.
topic: getting started
type: Documentation
user-guide-description: 자주 묻는 질문에 대한 답변과 Experience Platform에서 일반적인 오류를 해결하기 위한 안내서를 확인하십시오.
translation-type: tm+mt
source-git-commit: bc7c0a5d59c666ba80fac81a859b5ecf4dd37412
workflow-type: tm+mt
source-wordcount: '1956'
ht-degree: 5%

---


# [!DNL Platform] FAQ 및 문제 해결 가이드

이 문서에서는 Adobe Experience Platform에 대한 FAQ와 모든 API에서 발생할 수 있는 일반적인 오류에 대한 고급 문제 해결 안내서를 제공합니다 [!DNL Experience Platform] . 개별 [!DNL Platform] 서비스에 대한 문제 해결 가이드는 아래의 [서비스 문제 해결 디렉토리를 참조하십시오](#service-troubleshooting-directory) .

## FAQ {#faq}

다음은 Adobe Experience Platform에 대한 FAQ의 목록입니다.

## API란 [!DNL Experience Platform] 무엇입니까? {#what-are-experience-platform-apis}

[!DNL Experience Platform] 은 리소스에 액세스하기 위해 HTTP 요청을 사용하는 여러 개의 RESTful API를 [!DNL Platform] 제공합니다. 이러한 서비스 API는 각각 여러 끝점을 노출하며, 목록(GET), 조회(GET), 편집(PUT 및/또는 PATCH), 삭제(DELETE) 등의 작업을 수행할 수 있도록 해줍니다. 각 서비스에 사용할 수 있는 특정 끝점과 작업에 대한 자세한 내용은 Adobe I/O에 대한 [API 참조 설명서를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) 참조하십시오.

## API 요청의 포맷은 어떻게 됩니까? {#how-do-i-format-an-api-request}

요청 형식은 사용되는 API에 따라 [!DNL Platform] 다릅니다. API 호출을 구성하는 방법을 배우는 가장 좋은 방법은 사용 중인 특정 서비스에 대한 설명서에 나와 있는 예제와 함께 따르는 것입니다 [!DNL Platform] .

### 예제 API 호출 읽기

이 설명서는 두 가지 방법으로 API 호출 예를 보여 줍니다. [!DNL Experience Platform] 첫째, 호출은 해당 **API 형식**, 작업(GET, POST, PUT, PATCH, DELETE) 및 사용 중인 종단점만 표시하는 템플릿 표현(예: `/global/classes`) 일부 템플릿에는 다음과 같이 호출을 공식화하는 방법을 보여주는 데 도움이 되는 변수의 위치가 표시됩니다 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

그러면 호출은 API와 성공적으로 상호 작용하기 위해 필요한 헤더와 전체 &quot;기본 경로&quot;를 포함하는 **요청**&#x200B;시 cURL 명령으로 표시됩니다. 기본 경로는 모든 끝점에 미리 펜드되어야 합니다. 예를 들어 앞서 언급한 종점이 `/global/classes` 됩니다 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. 설명서 전체에서 API 형식/요청 패턴을 볼 수 있으며 플랫폼 API를 직접 호출할 때 요청 예제에 표시된 전체 경로를 사용할 수 있습니다.

### API 요청 예

다음은 설명서에서 보게 될 형식을 보여주는 예제 API 요청입니다.

**API 형식**

API 형식은 사용 중인 작업(GET)과 끝점을 보여줍니다. 변수는 중괄호로 `{CONTAINER_ID}`표시됩니다(이 경우).

```http
GET /{CONTAINER_ID}/classes
```

**요청**

이 예제 요청에서 API 형식의 변수는 요청 경로에 실제 값이 주어집니다. 모든 필수 헤더도 표시되며, 샘플 헤더 값 또는 민감한 정보(보안 토큰 및 액세스 ID 등)가 포함되어야 하는 변수도 표시됩니다.

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

응답은 전송된 요청을 기준으로 API에 대한 성공적인 호출 후 수신될 내용을 보여줍니다. 경우에 따라 응답이 공간에 대해 잘리는 경우가 있습니다. 즉, 샘플에 표시되는 추가 정보나 정보를 볼 수 있습니다.

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

플랫폼 API의 필수 헤더 및 요청 본문을 포함하여 특정 끝점에 대한 자세한 내용은 [API 참조 설명서를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html).

## IMS 조직이란 무엇입니까? {#what-is-my-ims-organization}

IMS 조직은 고객의 Adobe입니다. 모든 라이센스 Adobe 솔루션은 이 고객 조직과 통합됩니다. IMS 조직에서 권한을 부여받으면 개발자에게 액세스 권한 [!DNL Experience Platform]을 할당할 수 있습니다. IMS 조직 ID(`x-gw-ims-org-id`)는 API 호출이 실행되어야 하는 조직을 나타내며, 따라서 모든 API 요청의 헤더로 필요합니다. 이 ID는 [Adobe 개발자 콘솔을 통해 찾을 수 있습니다](https://www.adobe.com/go/devs_console_ui).통합 **** 탭에서 **특정 통합에 대한** 개요 **섹션으로 이동하여 클라이언트 자격 증명 아래에서 ID를**&#x200B;찾습니다. 인증 방법에 대한 단계별 연습은 [!DNL Platform]인증 자습서 [](../tutorials/authentication.md)를 참조하십시오.

## API 키는 어디에서 찾을 수 있습니까? {#where-can-i-find-my-api-key}

API 키는 모든 API 요청의 헤더로 필요합니다. Adobe 개발자 콘솔을 통해 찾을 수 [있습니다](https://www.adobe.com/go/devs_console_ui). 콘솔 내의 **통합** 탭에서 특정 통합에 대한 **개요** 섹션으로 이동하여 클라이언트 자격 증명 **에 있는 키를**&#x200B;찾습니다. 인증 방법에 대한 단계별 연습은 [!DNL Platform]인증 자습서 [](../tutorials/authentication.md)를 참조하십시오.

## 액세스 토큰을 어떻게 얻을 수 있습니까? {#how-do-i-get-an-access-token}

액세스 토큰은 모든 API 호출의 인증 헤더에 필요합니다. IMS 조직에 대한 통합에 액세스할 수 있는 경우 `curl` 명령을 사용하여 생성할 수 있습니다. 액세스 토큰은 24시간 동안만 유효하며 그 이후부터는 API를 계속 사용하려면 새 토큰을 생성해야 합니다. 액세스 토큰 생성에 대한 자세한 내용은 [인증 자습서를 참조하십시오](../tutorials/authentication.md).

## 쿼리 매개 변수는 어떻게 사용합니까? {#how-do-i-user-query-parameters}

일부 [!DNL Platform] API 끝점은 쿼리 매개 변수를 승인하여 특정 정보를 찾고 응답으로 반환된 결과를 필터링합니다. 쿼리 매개 변수는 요청 경로에 물음표(`?`) 기호를 추가하고 형식을 사용하여 하나 이상의 쿼리 매개 변수를 추가합니다 `paramName=paramValue`. 단일 호출에서 여러 매개 변수를 결합할 때는 앰퍼샌드(`&`)를 사용하여 개별 매개 변수를 구분해야 합니다. 다음 예에서는 여러 쿼리 매개 변수를 사용하는 요청이 설명서에서 어떻게 표시되는지 보여줍니다.

일반적으로 사용되는 쿼리 매개 변수의 예는 다음과 같습니다.

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

특정 서비스 또는 종단점에 사용할 수 있는 쿼리 매개 변수에 대한 자세한 내용은 서비스 관련 설명서를 참조하십시오.

## PATCH 요청에서 업데이트할 JSON 필드를 어떻게 표시합니까? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

API의 많은 PATCH 작업 [!DNL Platform] 은 업데이트할 [JSON 속성을 나타내기 위해 JSON 포인터](https://tools.ietf.org/html/rfc6901) 문자열을 사용합니다. 이러한 내용은 일반적으로 [JSON 패치](https://tools.ietf.org/html/rfc6902) 형식을 사용하여 요청 페이로드에 포함됩니다. 이러한 기술에 필요한 구문에 대한 자세한 내용은 [API 기본 사항 가이드를](api-fundamentals.md) 참조하십시오.

## Postman을 사용하여 API를 호출할 수 [!DNL Platform] 있습니까? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 은 RESTful API에 대한 호출을 시각화하는 데 유용한 도구입니다. 이 [중간 게시물은](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) 사용자가 Postman을 설정하여 자동으로 인증을 수행하고 이를 사용하여 API를 사용하는 방법에 대해 [!DNL Experience Platform] 설명합니다.

## 시스템 요구 사항은 무엇입니까 [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

UI 또는 API 사용 여부에 따라 다음 시스템 요구 사항이 적용됩니다.

**UI 기반 작업의 경우:**
- 최신 표준 웹 브라우저입니다. 최신 버전 [!DNL Chrome] 이 권장되지만, 현재 및 이전 주요 릴리스 [!DNL Firefox]와 Safari [!DNL Internet Explorer]도 지원됩니다.
   - 새로운 주요 버전이 출시될 때마다 최신 버전을 지원하는 동시에 세 번째 최신 버전에 대한 지원이 [!DNL Platform] 삭제됩니다.
- 모든 브라우저에는 쿠키와 JavaScript가 활성화되어 있어야 합니다.

**API 및 개발자 인터랙션의 경우**
- REST, 스트리밍 및 웹후크 통합을 위한 개발 환경입니다.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

다음은 [!DNL Experience Platform] 서비스를 사용할 때 발생할 수 있는 오류 목록입니다. 개별 [!DNL Platform] 서비스에 대한 문제 해결 가이드는 아래의 [서비스 문제 해결 디렉토리를 참조하십시오](#service-troubleshooting-directory) .

## API 상태 코드 {#api-status-codes}

모든 [!DNL Experience Platform] API에서 다음 상태 코드가 나타날 수 있습니다. 각각 다양한 이유가 있기 때문에, 이 부분에 설명되는 것은 일반적으로 일반적이다. 개별 [!DNL Platform] 서비스의 특정 오류에 대한 자세한 내용은 아래 [서비스 문제 해결 디렉토리를 참조하십시오](#service-troubleshooting-directory) .

| 상태 코드 | 설명 | 가능한 원인 |
--- | --- | ---
| 400 | 잘못된 요청 | 요청이 잘못 구성되었거나 키 정보가 누락되었으며/또는 잘못된 구문이 포함되어 있습니다. |
| 401 | 인증 실패 | 요청이 인증 검사를 통과하지 못했습니다. 액세스 토큰이 없거나 잘못되었습니다. 자세한 내용은 아래 [OAuth 토큰 오류](#oauth-token-is-missing) 섹션을 참조하십시오. |
| 403 | 금지 | 리소스를 찾았지만 볼 수 있는 자격 증명이 없습니다. |
| 404 | 찾을 수 없음 | 요청한 리소스를 서버에서 찾을 수 없습니다. 리소스가 삭제되었거나 요청한 경로가 잘못 입력되었을 수 있습니다. |
| 500 | 내부 서버 오류 | 서버측 오류입니다. 동시에 여러 호출을 하는 경우 API 제한에 도달하고 결과를 필터링해야 할 수 있습니다. 자세한 내용은 데이터 [!DNL Catalog Service] 필터링 [](../catalog/api/filter-data.md) 관련 API 개발자 가이드 하위 가이드를 참조하십시오. 요청을 다시 시도하기 전에 잠시 기다린 후 문제가 계속되면 관리자에게 문의하십시오. |

## 요청 헤더 오류 {#request-header-errors}

모든 API 호출에는 특정 요청 헤더가 [!DNL Platform] 필요합니다. 개별 서비스에 필요한 헤더를 확인하려면 [API 참조 설명서를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html). 필요한 인증 헤더의 값을 찾으려면 [인증 자습서를 참조하십시오](../tutorials/authentication.md). API 호출 시 이러한 헤더 중 하나가 누락되거나 잘못된 경우 다음 오류가 발생할 수 있습니다.

### OAuth 토큰이 없습니다. {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

이 오류 메시지는 API 요청에서 `Authorization` 헤더가 누락되면 표시됩니다. 인증 헤더가 올바른 액세스 토큰에 포함되어 있는지 확인한 후 다시 시도하십시오.

### OAuth 토큰이 잘못되었습니다.

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

헤더에 제공된 액세스 토큰이 유효하지 않을 때 이 오류 메시지가 `Authorization` 표시됩니다. 토큰이 올바르게 입력되었는지 [확인하거나 Adobe I/O 콘솔에서 새 토큰을](../tutorials/authentication.md) 생성합니다.

### API 키가 필요합니다.

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

이 오류 메시지는 API 요청에 API 키 헤더(`x-api-key`)가 누락된 경우 표시됩니다. 헤더를 유효한 API 키에 포함하고 있는지 확인한 후 다시 시도하십시오.

### API 키가 잘못되었습니다.

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

이 오류 메시지는 제공된 API 키 헤더(`x-api-key`)의 값이 잘못된 경우에 표시됩니다. 다시 시도하기 전에 키를 올바르게 입력했는지 확인하십시오. API 키를 모르는 경우 [Adobe I/O 콘솔에서 찾을 수 있습니다](https://console.adobe.io).통합 **** 탭에서 **개요** 섹션으로 이동하여 **클라이언트 자격 증명**&#x200B;아래에서 API 키를찾습니다.


### 헤더 누락

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

이 오류 메시지는 API 요청에서 IMS 조직 헤더(`x-gw-ims-org-id`)가 누락된 경우 표시됩니다. 헤더가 IMS 조직의 ID에 포함되어 있는지 확인한 후 다시 시도하십시오.

### 프로필이 잘못되었습니다.

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

이 오류 메시지는 사용자 또는 Adobe I/O 통합(헤더에서 [액세스 토큰으로](#how-do-i-get-an-access-token) 식별됨)이 `Authorization` 헤더에 제공된 IMS 조직에 대한 [!DNL Experience Platform] API를 호출할 권한이 없는 경우 `x-gw-ims-org-id` 표시됩니다. 헤더에서 IMS 조직에 대해 올바른 ID를 제공한 후 다시 시도하십시오. 조직 ID를 모르는 경우 [Adobe I/O 콘솔에서 찾을 수 있습니다](https://console.adobe.io).통합 **** 탭에서 **개요** 섹션으로 이동하여 클라이언트 자격 증명 ****&#x200B;아래에서 ID를찾습니다.

### 올바른 콘텐츠 형식이 지정되지 않았습니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

이 오류 메시지는 POST, PUT 또는 PATCH 요청에 잘못된 헤더가 있거나 누락된 경우 `Content-Type` 표시됩니다. 헤더가 요청에 포함되고 해당 값이 포함되었는지 확인합니다 `application/json`.


## 서비스 문제 해결 디렉터리 {#service-troubleshooting-directory}

다음은 API에 대한 문제 해결 가이드 및 API 참조 설명서 [!DNL Experience Platform] 목록입니다. 각 문제 해결 가이드는 개별 [!DNL Platform] 서비스와 관련된 문제에 대한 질문과 해결 방법을 제공합니다. API 참조 문서는 각 서비스에 대해 사용 가능한 모든 끝점에 대한 포괄적인 안내서를 제공하고 사용자가 받을 수 있는 샘플 요청 본문, 응답 및 오류 코드를 보여줍니다.

| 서비스 | API 참조 | 문제 해결 |
| --- | --- | --- |
| 액세스 제어 | [액세스 제어 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [액세스 제어 문제 해결 가이드](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform 데이터 수집 | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [일괄 처리 문제 해결](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[안내스트리밍 통합 문제 해결 가이드](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform 데이터 과학 작업 공간 | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 문제 해결 안내서](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform 데이터 거버넌스 | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform ID 서비스 | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] 문제 해결 안내서](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform 쿼리 서비스 | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] 문제 해결 안내서](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform 세분화 | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] FAQ 및 문제 해결 가이드](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 및 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] 문제 해결 안내서](../profile/troubleshooting.md) |
| 샌드 박스 | [샌드박스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [샌드박스 문제 해결 가이드](../sandboxes/troubleshooting-guide.md) |

