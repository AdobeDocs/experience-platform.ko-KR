---
title: Reactor API의 암호
description: 이벤트 전달에서 사용할 Reactor API에서 암호를 구성하는 방법에 대한 기본 사항을 알아봅니다.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 24e79c14268b9eab0e8286eb8cd1352c1dfcd1b6
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Reactor API의 암호

Reactor API에서 암호는 인증 자격 증명을 나타내는 리소스입니다. 보안 데이터 교환을 위해 다른 시스템을 인증하기 위해 이벤트 전달에 기밀이 사용됩니다. 따라서 이벤트 전달 속성(속성이 `platform` 속성이 `edge`).

현재 다음과 같이 표시되는 세 가지 지원되는 암호 유형이 있습니다 `type_of` attribute:

| 암호 유형 | 설명 |
| --- | --- |
| `token` | 두 시스템에서 모두 알고 이해할 수 있는 인증 토큰 값을 나타내는 단일 문자열입니다. |
| `simple-http` | 사용자 이름과 암호로 각각 두 개의 문자열 속성을 포함합니다. |
| `oauth2-client_credentials` | 을(를) 지원하는 여러 특성을 포함합니다 [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 인증 사양입니다. 이벤트 전달에서 필요한 정보를 요청한 다음 지정된 간격으로 이러한 토큰의 갱신을 처리합니다. |

{style=&quot;table-layout:auto&quot;}

이 안내서에서는 이벤트 전달에 사용할 암호를 구성하는 방법에 대한 높은 수준의 개요를 제공합니다. 암호 구조의 JSON 예를 포함하여 Reactor API에서 암호를 관리하는 방법에 대한 자세한 지침은 다음을 참조하십시오. [비밀 끝점 안내서](../endpoints/secrets.md).

## 자격 증명

각 암호에는 `credentials` 각 자격 증명 값을 가지는 속성입니다. When [api에서 암호 만들기](../endpoints/secrets.md#create)의 경우, 각 유형의 비밀에는 아래 섹션에 표시된 대로 필요한 속성이 다릅니다.

* [`토큰`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

비밀과 `type_of` 값 `token` 에는 단일 속성만 필요합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `token` | 문자열 | 대상 시스템에서 인식하는 비밀 토큰. |

{style=&quot;table-layout:auto&quot;}

토큰은 정적 값으로 저장되므로 암호는 `expires_at` 및 `refresh_at` 속성이 `null` 비밀이 만들어지면

### `simple-http` {#simple-http}

비밀과 `type_of` 값 `simple-http` 에 다음 속성이 필요합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `username` | 문자열 | 사용자 이름. |
| `password` | 문자열 | 암호. 이 값은 API 응답에 포함되지 않습니다. |

{style=&quot;table-layout:auto&quot;}

암호가 만들어지면 두 속성이 BASE64 인코딩과 교환됩니다 `username:password`. 교환 후, 비밀은 `expires_at` 및 `refresh_at` 속성이 `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

비밀과 `type_of` 값 `oauth2-client_credentials` 에 다음 속성이 필요합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `client_id` | 문자열 | OAuth 통합을 위한 클라이언트 ID입니다. |
| `client_secret` | 문자열 | OAuth 통합을 위한 클라이언트 암호입니다. 이 값은 API 응답에 포함되지 않습니다. |
| `token_url` | 문자열 | OAuth 통합을 위한 인증 URL입니다. |
| `refresh_offset` | 정수 | *(선택 사항)* 새로 고침 작업을 오프셋할 값(초)입니다. 암호를 만들 때 이 속성을 생략하면 값이 `14400` (4시간) 기본적으로 제공됩니다. |
| `options` | 오브젝트 | *(선택 사항)* OAuth 통합을 위한 추가 옵션을 지정합니다.<ul><li>`scope`: 를 나타내는 문자열입니다 [OAuth 2.0 범위](https://oauth.net/2/scope/) 참조하십시오.</li><li>`audience`: 를 나타내는 문자열입니다 [Auth0 액세스 토큰](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

다음 경우에 `oauth2-client_credentials` 비밀번호가 만들어지거나 업데이트되고 `client_id` 및 `client_secret` 그리고 `options`)은 를 POST 요청에서 `token_url`를 설정하는 것이 좋습니다.

>[!NOTE]
>
>인증 서비스 응답 본문은 OAuth 프로토콜과 호환됩니다.

인증 서비스가 `200 OK` 및 JSON 응답 본문을 구문 분석하고 `access_token` 은 에지 환경에 푸시되고 `expires_in` 는 를 계산하는 데 사용됩니다 `expires_at` 및 `refresh_at` 비밀의 속성입니다. 그 비밀에는 환경관계가 없으면 `access_token` 이 삭제됩니다.

자격 증명 교환은 다음 조건에 따라 성공한 것으로 간주됩니다.

* `expires_in` 보다 큼 `28800` (8시간)
* `refresh_offset` 다음보다 작음 `expires_in` 빼기 `14400` (4시간). 예를 들어 `expires_in` is `36000` (10시간) 및 `refresh_offset` is `28800` (8시간), `28800` 보다 큼 `36000` - `14400` (`21600`).

교환이 성공하면 비밀의 상태 속성이 `succeeded` 및 값 `expires_at` 및 `refresh_at` 설정됨:

* `expires_at` 는 현재 UTC 시간과 다음 값을 더한 값입니다 `expires_in`.
* `refresh_at` 는 현재 UTC 시간과 다음 값을 더한 값입니다 `expires_in`에서 값을 뺀 값입니다. `refresh_offset`. 예를 들어 `expires_in` is `43200` (12시간) 및 `refresh_offset` is `14400` (4시간), `refresh_at` 속성이 `28800` (8시간) 현재 UTC 시간 이후

어떤 이유로든 교환이 실패하면 `status_details` 의 속성 `meta` 관련 정보로 객체를 업데이트합니다.

#### 새로 고침 `oauth2-client_credentials` 비밀

다음과 같은 경우 `oauth2-client_credentials` 비밀이 환경에 할당되어 있으며 해당 상태는 `succeeded` (자격 증명이 교환되었습니다) 새 교환이 자동으로 수행됩니다 `refresh_at`.

교환이 성공하면 `refresh_status` 의 속성 `meta` 개체가 `succeeded` while `expires_at`, `refresh_at`, 및 `activated_at` 그에 따라 업데이트됩니다.

교환이 실패하면 액세스 토큰이 만료되기 2시간 전까지 마지막 시도에서 3번 더 시도합니다. 모든 시도가 실패하면 `refresh_status_details` 속성 `meta` 개체 업데이트 관련 세부 사항

### `oauth2-google` {#oauth2-google}

비밀과 `type_of` 값 `oauth2-google` 에는 다음 속성이 필요합니다. `credentials`:

| 자격 증명 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `scopes` | 어레이 | 인증에 대한 Google 제품 범위를 나열합니다. 지원되는 범위는 다음과 같습니다.<ul><li>[Google 광고](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

만들기 후 `oauth2-google` 비밀, 응답에는 `meta.authorization_url` 속성을 사용합니다. Google 인증 흐름을 완료하려면 이 URL을 브라우저에 복사하여 붙여넣어야 합니다.

#### 권한 재인증 `oauth2-google` 비밀

에 대한 인증 URL `oauth2-google` 비밀이 만들어지면 1시간 후에 만료됩니다. `meta.authorization_url_expires_at`). 이 시간이 지나면 인증 프로세스를 갱신하려면 암호를 재승인해야 합니다.

자세한 내용은 [비밀 끝점 안내서](../endpoints/secrets.md#reauthorize) 재인증 방법에 대한 자세한 내용 `oauth2-google` secret으로 사용하십시오.

## 환경 관계

암호를 만들 때는 [환경](../endpoints/environments.md) 이 URL이 존재할 경우 비밀이 생성된 환경에 즉시 배포됩니다.

암호는 한 환경에서만 연결할 수 있습니다. 비밀과 환경 사이의 관계가 설정되면 그 비밀이 환경에서 제거될 수 없고, 그 비밀이 다른 환경과 연결될 수 없습니다.

>[!NOTE]
>
>이 규칙의 유일한 예외는 해당 환경이 삭제된 경우입니다. 이 경우 관계가 지워지고 비밀이 다른 환경에 할당될 수 있습니다.

비밀의 자격 증명이 성공적으로 교환된 후 환경에 연결할 비밀과 Exchange 아티팩트(에 대한 토큰 문자열) `token`: Base64로 인코딩된 문자열입니다 `simple-http`또는 액세스 토큰에 대해 `oauth2-client_credentials`)가 환경에 안전하게 저장됩니다.

Exchange 아티팩트가 환경에 성공적으로 저장되면 비밀의 `activated_at` 속성이 현재 UTC 시간으로 설정되며 이제 데이터 요소를 사용하여 참조할 수 있습니다. 자세한 내용은 [다음 섹션](#referencing-secrets) 비밀 참조에 대한 자세한 정보.

## 참조 암호 {#referencing-secrets}

암호를 참조하려면 &quot; 유형의 데이터 요소를 만들어야 합니다[!UICONTROL 비밀]&quot;(에서 제공) [[!UICONTROL 코어] 확장](../../extensions/web/core/overview.md)) 내의 아무 곳에나 삽입할 수 있습니다. 이 데이터 요소를 구성할 때 각 환경에 사용할 암호를 입력하라는 메시지가 표시됩니다. 그런 다음 HTTP 호출을 위한 헤더 내에서 등의 비밀 데이터 요소를 참조하는 규칙을 만들 수 있습니다.

![비밀 데이터 요소](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>라이브러리에 비밀 데이터 요소를 추가하려면 하나 이상의 항목이 있어야 합니다 `succeeded` 라이브러리가 빌드되는 환경과 연결된 암호입니다. 예를 들어 라이브러리에 다음이 없는 비밀 데이터 요소가 있는 경우 `succeeded` 에 대해 구성된 암호 [!UICONTROL 스태이징 암호] 섹션, 스테이징 환경에서 해당 라이브러리를 빌드하려고 하면 오류가 발생합니다.

런타임 시 비밀 데이터 요소는 환경에 저장된 해당 비밀 교환 아티팩트로 대체됩니다.

## 다음 단계

이 안내서에서는 Reactor API에서 기밀 작업을 수행하는 기본 사항을 다룹니다. API 호출을 사용하여 암호를 관리하는 방법에 대한 자세한 내용은 [비밀 끝점 안내서](../endpoints/secrets.md).
