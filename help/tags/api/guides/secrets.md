---
title: Reactor API의 비밀
description: 이벤트 전달에 사용할 Reactor API에서 비밀을 구성하는 방법의 기본 사항에 대해 알아봅니다.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 1%

---

# Reactor API의 비밀

Reactor API에서 암호는 인증 자격 증명을 나타내는 리소스입니다. 보안은 안전한 데이터 교환을 위해 다른 시스템에 인증하기 위해 이벤트 전달에 사용됩니다. 따라서 비밀은 이벤트 전달 속성(의 속성) 내에서만 만들 수 있습니다. `platform` 속성이 로 설정되어 있습니다. `edge`).

현재 에는 세 가지 지원되는 암호 유형이 표시됩니다. `type_of` 특성:

| 암호 유형 | 설명 |
| --- | --- |
| `token` | 두 시스템에서 알려지고 이해하는 인증 토큰 값을 나타내는 단일 문자 문자열입니다. |
| `simple-http` | 사용자 이름과 암호에 대해 각각 두 개의 문자열 속성을 포함합니다. |
| `oauth2-client_credentials` | 을(를) 지원하기 위한 몇 가지 속성을 포함합니다. [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 인증 사양입니다. 이벤트 전달에서 필요한 정보를 요청한 다음 지정된 간격에 따라 이러한 토큰의 갱신을 처리합니다. |

{style="table-layout:auto"}

이 안내서에서는 이벤트 전달에 사용할 비밀을 구성하는 방법에 대한 높은 수준의 개요를 제공합니다. 비밀 구조의 JSON 예를 포함하여 Reactor API의 비밀을 관리하는 방법에 대한 자세한 지침은 [secrets endpoint 안내서](../endpoints/secrets.md).

## 자격 증명

각 비밀에는 `credentials` 해당 자격 증명 값을 보유하는 속성입니다. 날짜 [api에서 암호 만들기](../endpoints/secrets.md#create), 각 유형의 암호에는 아래 섹션과 같이 서로 다른 필수 속성이 있습니다.

* [`토큰`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

이 있는 비밀 `type_of` 값 `token` 에는 단일 속성만 필요합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `token` | 문자열 | 대상 시스템에서 인식하는 비밀 토큰입니다. |

{style="table-layout:auto"}

토큰은 정적 값으로 저장되므로 `expires_at` 및 `refresh_at` 속성이 다음으로 설정됨 `null` 암호가 만들어지는 시간.

### `simple-http` {#simple-http}

이 있는 비밀 `type_of` 값 `simple-http` 다음 속성을 필요로 합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `username` | 문자열 | 사용자 이름. |
| `password` | 문자열 | 암호. 이 값은 API 응답에 포함되지 않습니다. |

{style="table-layout:auto"}

암호가 만들어지면 두 특성이 의 BASE64 인코딩과 교환됩니다. `username:password`. 교환 후, 비밀은 `expires_at` 및 `refresh_at` 속성이 다음으로 설정됨 `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

이 있는 비밀 `type_of` 값 `oauth2-client_credentials` 다음 속성을 필요로 합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `client_id` | 문자열 | OAuth 통합을 위한 클라이언트 ID입니다. |
| `client_secret` | 문자열 | OAuth 통합을 위한 클라이언트 암호입니다. 이 값은 API 응답에 포함되지 않습니다. |
| `token_url` | 문자열 | OAuth 통합을 위한 인증 URL입니다. |
| `refresh_offset` | 정수 | *(선택 사항)* 새로 고침 작업을 오프셋할 값(초)입니다. 암호를 만들 때 이 특성을 생략하면 값이 로 설정됩니다. `14400` (4시간) 기본적으로 제공됩니다. |
| `options` | 오브젝트 | *(선택 사항)* OAuth 통합을 위한 추가 옵션을 지정합니다.<ul><li>`scope`: 를 나타내는 문자열 [OAuth 2.0 범위](https://oauth.net/2/scope/) 자격 증명용.</li><li>`audience`: 다음을 나타내는 문자열 [Auth0 액세스 토큰](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

다음의 경우 `oauth2-client_credentials` 암호가 생성되거나 업데이트됩니다. `client_id` 및 `client_secret` (그리고 아마도 `options`)은 (으)로 POST 요청에서 교환됩니다 `token_url`에 따라 OAuth 프로토콜의 클라이언트 자격 증명 플로우가 적용됩니다.

>[!NOTE]
>
>인증 서비스 응답 본문은 OAuth 프로토콜과 호환됩니다.

인증 서비스가 다음으로 응답하는 경우 `200 OK` 및 JSON 응답 본문이며 본문이 구문 분석되고 `access_token` 가 에지 환경으로 푸시되고 `expires_in` 를 계산하는 데 사용됩니다. `expires_at` 및 `refresh_at` 암호에 대한 속성입니다. 비밀에 대해 환경 연관성이 없다면, `access_token` 이(가) 무시됩니다.

자격 증명 교환은 다음 조건에 따라 성공한 것으로 간주됩니다.

* `expires_in` 다음보다 큼 `28800` (8시간).
* `refresh_offset` 이(가) 의 값보다 작습니다. `expires_in` 빼기 `14400` (4시간) 예를 들어 다음과 같습니다. `expires_in` 은(는) `36000` (10시간) 및 `refresh_offset` 은(는) `28800` (8시간), 다음 이유로 교환이 실패한 것으로 간주됩니다. `28800` 다음보다 큼 `36000` - `14400` (`21600`).

교환이 성공하면 비밀의 상태 속성이 로 설정됩니다. `succeeded` 및 값 `expires_at` 및 `refresh_at` 다음과 같이 설정됩니다.

* `expires_at` 은 현재 UTC 시간에 다음 값을 더한 값입니다. `expires_in`.
* `refresh_at` 은 현재 UTC 시간에 다음 값을 더한 값입니다. `expires_in`, 값 빼기 `refresh_offset`. 예를 들어 다음과 같습니다. `expires_in` 은(는) `43200` (12시간) 및 `refresh_offset` 은(는) `14400` (4시간), `refresh_at` 속성이 로 설정됩니다. `28800` (8시간) 현재 UTC 시간 후.

어떤 이유로든 교환이 실패하는 경우 `status_details` 의 속성 `meta` 관련 정보로 개체가 업데이트됩니다.

#### 새로 고침 `oauth2-client_credentials` 비밀

다음과 같은 경우 `oauth2-client_credentials` 암호가 환경에 할당되었으며 상태는 입니다. `succeeded` (자격 증명이 정상적으로 교환됨) 새 교환이 다음에서 자동으로 수행됩니다. `refresh_at`.

교환이 성공하면 `refresh_status` 의 속성 `meta` 개체가 로 설정되어 있습니다. `succeeded` while `expires_at`, `refresh_at`, 및 `activated_at` 에 따라 업데이트됩니다.

교환이 실패하면 액세스 토큰이 만료되기 2시간 전에 마지막 시도와 함께 작업을 세 번 더 시도합니다. 모든 시도가 실패하면 `refresh_status_details` 속성 위치: `meta` 관련 세부 정보가 포함된 오브젝트가 업데이트됩니다.

### `oauth2-google` {#oauth2-google}

이 있는 비밀 `type_of` 값 `oauth2-google` 에는 다음 속성이 필요합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `scopes` | 배열 | 인증을 위한 Google 제품 범위를 나열합니다. 지원되는 범위는 다음과 같습니다.<ul><li>[Google 광고](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

를 만든 후 `oauth2-google` 비밀, 응답에는 다음이 포함됩니다. `meta.authorization_url` 속성. Google 인증 플로우를 완료하려면 이 URL을 복사하여 브라우저에 붙여넣어야 합니다.

#### 권한 재인증 `oauth2-google` 비밀

인증용 URL `oauth2-google` 비밀은 비밀이 생성된 후 1시간 후에 만료됩니다( 로 표시). `meta.authorization_url_expires_at`). 이 시간이 지나면 인증 프로세스를 갱신하려면 암호를 다시 승인해야 합니다.

다음을 참조하십시오. [secrets endpoint 안내서](../endpoints/secrets.md#reauthorize) 을(를) 재승인하는 방법에 대한 자세한 내용 `oauth2-google` Reactor API에 PATCH 요청을 하여 보안을 유지합니다.

## 환경 관계

암호를 만들 때 [환경](../endpoints/environments.md) 이 항목이 존재하는 위치. 비밀은 작성된 환경에 즉시 배포됩니다.

암호는 하나의 환경에만 연결할 수 있습니다. 일단 비밀과 환경의 관계가 성립되면 환경에서 비밀을 지울 수 없고 비밀은 다른 환경과 연관될 수 없다.

>[!NOTE]
>
>이 규칙에 대한 유일한 예외는 해당 환경이 삭제되는 경우입니다. 이 경우 관계가 지워지고 비밀이 다른 환경에 할당될 수 있습니다.

암호의 자격 증명이 성공적으로 교환된 후 환경과 연결할 암호에 대한 교환 아티팩트(의 토큰 문자열) `token`, 다음에 대한 Base64 인코딩 문자열 `simple-http`또는 의 액세스 토큰 `oauth2-client_credentials`)은 환경에 안전하게 저장됩니다.

Exchange 아티팩트가 환경에 성공적으로 저장되면 `activated_at` 속성은 현재 UTC 시간으로 설정되며 이제 데이터 요소를 사용하여 참조할 수 있습니다. 다음을 참조하십시오. [다음 섹션](#referencing-secrets) 비밀 참조에 대한 자세한 내용을 보려면.

## 참조 암호 {#referencing-secrets}

암호를 참조하려면 &quot; 유형의 데이터 요소를 만들어야 합니다.[!UICONTROL 암호]&quot; (에 의해 제공됨) [[!UICONTROL 코어] 확장](../../extensions/client/core/overview.md))을 클릭하여 제품에서 사용할 수 있습니다. 이 데이터 요소를 구성할 때 각 환경에 사용할 암호를 묻는 메시지가 표시됩니다. 그런 다음 HTTP 호출의 헤더 내와 같이 비밀 데이터 요소를 참조하는 규칙을 만들 수 있습니다.

![비밀 데이터 요소](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>라이브러리에 비밀 데이터 요소를 추가하려면 하나 이상의 보안 데이터 요소가 있어야 합니다 `succeeded` 라이브러리가 구축되는 환경과 연계된 암호. 예를 들어 라이브러리에 가 없는 비밀 데이터 요소가 있는 경우 `succeeded` 다음에 대해 구성된 암호 [!UICONTROL 스테이징 암호] 섹션에서 스테이징 환경에 해당 라이브러리를 빌드하려고 하면 오류가 발생합니다.

런타임 시 비밀 데이터 요소는 환경에 저장된 해당 비밀 교환 아티팩트로 대체됩니다.

## 다음 단계

이 안내서에서는 Reactor API의 비밀을 사용하여 작업하는 기본 사항에 대해 다룹니다. API 호출을 사용하여 비밀을 관리하는 방법에 대한 자세한 내용은 [secrets endpoint 안내서](../endpoints/secrets.md).
