---
title: 클라이언트 상태 관리
description: Adobe Experience Platform Edge Network가 클라이언트 상태를 관리하는 방법 알아보기
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 클라이언트;상태;관리;에지;네트워크;게이트웨이;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# 클라이언트 상태 관리

Edge Network 자체는 상태를 저장하지 않습니다(자체 세션을 유지 관리하지 않음). 그러나 다음과 같이 클라이언트측 상태 지속성이 필요한 특정 사용 사례가 있습니다.

* 일관된 디바이스 식별(참조) [방문자 식별](visitor-identification.md))
* 사용자 동의 수집 및 적용
* 개인화 세션 ID 유지

에지 네트워크는 상태 관리 프로토콜을 사용하여 스토리지 측면을 클라이언트/SDK에 위임하고 응답에 상태 항목을 포함합니다. 브라우저의 경우 항목이 쿠키로 저장됩니다.

클라이언트는 이 매개 변수를 저장하고 모든 후속 요청에 포함시킵니다. 또한 클라이언트가 게이트웨이의 지시에 따라 항목에 대한 적절한 만료도 처리해야 합니다. 항목이 쿠키로 저장되면 브라우저는 이 모든 작업을 자동으로 수행합니다.

상태 항목은 항상 일반 값을 갖지만 `String` 값 (호출자/SDK에 표시됨), 어떤 식으로든 값을 사용하거나 변조해서는 안 됩니다. 값 구조/형식 또는 이름 자체가 언제든지 변경될 수 있으며, 이로 인해 내부적으로 상태를 사용하는 클라이언트에 예기치 않은 동작이 발생할 수 있습니다. 상태는 항상 게이트웨이 자체 또는 다른 에지 서비스에 의해 사용되도록 의도된다.

## 클라이언트 상태를 메타데이터로 유지

에 의해 반환된 상태 [!DNL Edge Network] 응답 본문에서 `Handle` 유형이 있는 객체 `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| `key` | 문자열 | **필수 여부**. 항목 이름입니다. |
| `value` | 문자열 | *선택 사항입니다*. 항목 값입니다. |
| `maxAge` | 정수 | *선택 사항* 항목이 만료될 때까지의 시간(초)입니다. 누락된 경우 항목은 현재 세션에 대해서만 저장해야 합니다. |
| `attrs` | `Map<String, String>` | *선택 사항입니다*. 항목 속성의 선택적 목록입니다. 보안 참조 HTTP 헤더가 있는 모든 보안 연결에 대해 `SameSite` 속성이 로 설정되어 있습니다. `None`. |


다중 태그 지정을 지원하기 위해(즉, 동일한 속성에 여러 SDK 인스턴스가 있고, 이는 잠재적으로 서로 다른 조직을 참조할 수 있음) 모든 상태 항목에 접두사가 자동으로 붙습니다 `kndctr_` 및 URL 안전 조직 ID입니다.

클라이언트 SDK가 `state:store` 응답에서 을 처리하려면 다음을 수행해야 합니다.

* 게이트웨이가 제공한 만료 시간을 고려하여 클라이언트측에 항목을 저장합니다.
* 클라이언트 저장소에서 해당 항목을 로드하고 만료되지 않은 모든 항목을 후속 요청에 포함합니다.

다음은 클라이언트측 저장 상태에서 전달되는 요청의 예입니다.

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## 브라우저 쿠키에서 클라이언트 상태 유지

브라우저 클라이언트에서 작업할 때 Edge Network는 항목을 브라우저 쿠키로 자동으로 유지할 수 있습니다. 따라서 브라우저는 기본적으로 상태 관리 프로토콜을 준수하므로 투명한 상태 스토리지 지원이 가능합니다.

거의 모든 항목은 활성화 및 지원될 때 자사 쿠키로 구체화되지만(아래 참고 사항 참조), 게이트웨이는 타사 쿠키가 있을 때 일부 타사 쿠키를 저장할 수도 있습니다 `adobedc.demdex.net` 도메인이 사용됩니다.

항목은 항상 정의에 따라 특정 범위(장치/애플리케이션)에 바인딩되므로 현재 요청 컨텍스트와 호환되는 하위 집합만 Edge Network에 의해 작성됩니다. 작성되지 않은 항목은 `state:store` 핸들.

일반적으로 애플리케이션 범위 항목은 항상 자사 쿠키로 기록되는 반면 디바이스 범위 항목은 타사 쿠키로 기록됩니다. 결정은 호출자에게 완전히 투명하며, 게이트웨이는 호출 컨텍스트에 따라 어떤 엔트리를 쓸 수 있는지를 결정한다.

호출자는 를 통해 클라이언트 상태를 쿠키로 저장하도록 명시적으로 지원해야 합니다. `meta.state.cookiesEnabled` 플래그:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| `cookiesEnabled` | 부울 | 설정되면 은 쿠키에 대한 지원을 활성화합니다. 기본값은 `false`입니다. |
| `domain` | 문자열 | 필요한 경우 `cookiesEnabled: true`. 쿠키를 작성해야 하는 최상위 도메인입니다. Edge Network는 이 값을 사용하여 상태를 쿠키로 유지할 수 있는지 여부를 결정합니다. |

를 통해 쿠키 지원이 활성화된 경우에도 `cookiesEnabled` 플래그에서 Adobe Experience Platform Edge Network는 요청 최상위 도메인이 와 일치하는 경우에만 상태 항목을 기록합니다. `domain` 호출자가 지정합니다. 불일치가 발생하면 항목이 `state:store` 핸들.

다음과 같은 경우에는 자사 쿠키를 작성할 수 없습니다(지원이 활성화된 경우에도).

* 요청이 서드파티에게 오고 있습니다. `adobedc.demdex.net` 도메인.
* 요청은 퍼스트 파티로 전달됩니다. `CNAME` 도메인(의 호출자가 지정한 도메인과 다름) `meta.state.domain`.

## 쿠키 보안

모든 쿠키에는 [보안 플래그](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) 가능하면 활성화되었습니다.

모든 보안 쿠키에는 [SameSite 속성](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) 을 로 설정 `None`는 쿠키가 자사 및 교차 출처의 모든 컨텍스트에서 전송됨을 의미합니다.

* 자사 쿠키의 경우(`kndcrt_*`), `Secure` 플래그는 요청 컨텍스트가 보안(HTTPS)이고 레퍼러()인 경우에만 설정됩니다.[Referer HTTP 헤더](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Referer))도 HTTPS입니다. 레퍼러가 안전하지 않은 경우(HTTP) `Secure` 웹 SDK에서 읽을 수 있도록 허용하기 위해 플래그가 생략됩니다. 비보안 컨텍스트에서는 보안 쿠키를 읽을 수 없습니다.
* 타사 쿠키(demdex)의 경우 `Secure` 모든 요청이 HTTPS이므로 플래그는 항상 설정되므로 요청 컨텍스트는 안전하며 이 쿠키는 JavaScript에서 읽지 않습니다.

다음 `Secure` 플래그가 다음 위치에 없습니다. [쿠키의 메타데이터 표현](#state-as-metadata). 만 `SameSite` 속성이 포함됩니다. 이 경우 를 올바르게 설정하는 것은 클라이언트의 책임입니다. `Secure` 다음 시간마다 플래그 지정 `SameSite` 속성이 있습니다. 이 포함된 쿠키 `SameSite=None` 또한 다음을 지정해야 합니다. `Secure` 보안 컨텍스트(HTTPS)가 필요하므로 속성입니다.
