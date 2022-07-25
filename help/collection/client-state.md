---
title: 클라이언트 상태 관리
description: Adobe Experience Platform Edge Network에서 클라이언트 상태를 관리하는 방법을 알아봅니다
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 클라이언트;상태;관리;에지;네트워크;게이트웨이;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---

# 클라이언트 상태 관리

에지 네트워크 자체는 상태를 저장하지 않습니다(자체 세션을 유지 관리하지 않음). 그러나 다음과 같이 클라이언트측 상태 지속성을 필요로 하는 특정 사용 사례가 있습니다.

* 일관된 장치 식별( [방문자 식별](visitor-identification.md))
* 사용자 동의 수집 및 적용
* 개인화 세션 ID 유지

Edge Network는 상태 관리 프로토콜을 사용하고 스토리지 측면을 클라이언트/SDK로 위임하며 응답에 상태 항목을 포함합니다. 브라우저의 경우 항목은 쿠키로 저장됩니다.

클라이언트 권한은 모든 후속 요청에 저장하고 포함하는 것입니다. 또한 클라이언트는 게이트웨이가 지시하는 대로 항목에 대한 적절한 만료 처리를 수행해야 합니다. 항목이 쿠키로 저장되면 브라우저가 이 모든 작업을 자동으로 수행합니다.

주 항목에는 항상 일반 항목이 있지만 `String` 값(호출자/SDK에 표시됨)을 어떤 식으로든 이 값을 소비하거나 함부로 조작할 수 없습니다. 값 구조/형식 또는 이름 자체가 언제든지 변경될 수 있으므로 내부적으로 상태를 사용하는 클라이언트에 대해 예기치 않은 동작이 발생할 수 있습니다. 상태는 항상 게이트웨이 자체 또는 기타 에지 서비스에 사용됩니다.

## 클라이언트 상태를 메타데이터로 유지

에 의해 반환된 상태 [!DNL Edge Network] 응답 본문에서 는 `Handle` 유형이 있는 객체 `state:store`.

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
| `maxAge` | 정수 | *선택 사항입니다* 시작 TTL(Time-to-Live)(초). 누락된 항목은 현재 세션에 대해서만 저장해야 합니다. |
| `attrs` | `Map<String, String>` | *선택 사항입니다*. 선택적 항목 속성 목록입니다. 보안 레퍼러 HTTP 헤더를 사용하는 모든 보안 연결에 대해 `SameSite` 속성이 `None`. |


다중 태그 지정을 지원하기 위해(즉, 다른 조직을 참조할 수 있는 동일한 속성의 여러 SDK 인스턴스) 모든 상태 항목에는 자동으로 `kndctr_` 및 URL 안전 조직 ID입니다.

클라이언트 SDK가 `state:store` 응답에서 처리를 수행하려면 다음을 수행해야 합니다.

* 게이트웨이에 제공된 만료 시간을 준수하여 클라이언트 측에 항목을 저장합니다.
* 클라이언트 저장소에서 해당 항목을 로드하고 이후 요청에 만료되지 않은 모든 항목을 포함합니다.

다음은 클라이언트측 저장 상태로 전달되는 요청의 예입니다.

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

브라우저 클라이언트로 작업할 때 Edge Network는 항목을 브라우저 쿠키로 자동으로 유지할 수 있습니다. 이렇게 하면 브라우저가 기본적으로 상태 관리 프로토콜을 준수하므로 투명한 상태 저장소를 지원할 수 있습니다.

활성화 및 지원 시 거의 모든 항목이 자사 쿠키로 구체화되지만(아래 참고 참조), 게이트웨이는 타사 쿠키가 `adobedc.demdex.net` 도메인이 사용됩니다.

항목은 항상 해당 정의에 따라 특정 범위(장치/애플리케이션)에 바인딩되므로 현재 요청 컨텍스트와 호환되는 하위 집합만 Edge Network에 의해 작성됩니다. 기록되지 않은 항목은 `state:store` 핸들.

일반적인 규칙으로, 애플리케이션 범위 항목은 항상 자사 쿠키로 기록되고 장치 범위 항목은 타사 쿠키로 작성됩니다. 이 결정은 호출자에게 완전히 투명하며, 게이트웨이는 호출 컨텍스트에 따라 어떤 항목을 쓸 수 있는지 결정합니다.

호출자는 를 통해 클라이언트 상태를 쿠키로 저장하는 지원을 명시적으로 활성화해야 합니다. `meta.state.cookiesEnabled` 플래그:

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
| `cookiesEnabled` | 부울 | 이 설정되면 쿠키를 지원합니다. 기본값은 `false`입니다. |
| `domain` | 문자열 | 필요한 경우 `cookiesEnabled: true`. 쿠키를 작성해야 하는 최상위 도메인입니다. 에지 네트워크는 이 값을 사용하여 상태를 쿠키로 유지할 수 있는지 여부를 결정합니다. |

쿠키 지원이 를 통해 활성화되는 경우에도 `cookiesEnabled` 플래그를 지정하면, Adobe Experience Platform Edge Network가 요청 최상위 도메인이 `domain` 호출자가 지정합니다. 일치하지 않으면 항목이 `state:store` 핸들.

다음과 같은 경우 자사 쿠키를 쓸 수 없습니다(지원이 활성화된 경우에도).

* 제3자에게 요청이 오고 있습니다 `adobedc.demdex.net` 도메인.
* 그 요청은 일행이 되어 있다 `CNAME` 도메인(의 호출자가 지정한 도메인과 다름) `meta.state.domain`.

## 쿠키 보안

모든 쿠키에는 [보안 플래그](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) 가능하면 항상 활성화되었습니다.

모든 보안 쿠키에는 [SameSite 속성](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) 설정 `None`: 쿠키가 자사 및 원본 간 모든 컨텍스트에서 전송됨을 의미합니다.

* 자사 쿠키의 경우(`kndcrt_*`), `Secure` 플래그는 요청 컨텍스트가 보안(HTTPS)이고 레퍼러([Referer HTTP 헤더](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer))도 HTTPS입니다. 레퍼러가 안전하지 않은 경우(HTTP) `Secure` 웹 SDK에서 플래그를 읽을 수 있도록 하기 위해 플래그가 생략됩니다. 보안 쿠키는 비보안 컨텍스트에서 읽을 수 없습니다.
* 타사 쿠키(demdex)의 경우, `Secure` 플래그는 모든 요청이 HTTPS이므로 요청 컨텍스트는 안전하며 이 쿠키는 JavaScript에서 읽지 않으므로 항상 설정됩니다.

다음 `Secure` 플래그가 없습니다. [쿠키의 메타데이터 표시](#state-as-metadata). 전용 `SameSite` 속성이 포함됩니다. 이 경우 `Secure` 항상 플래그 지정 `SameSite` 속성이 있습니다. 쿠키 `SameSite=None` 또한 `Secure` 속성에는 보안 컨텍스트(HTTPS)가 필요하므로
