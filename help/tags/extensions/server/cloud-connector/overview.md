---
title: Cloud Connector 확장 개요
description: Adobe Experience Platform의 Cloud Connector 이벤트 전달 확장에 대해 알아봅니다.
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 83%

---

# Cloud Connector 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Cloud Connector 이벤트 전달 확장을 사용하면 데이터를 대상에 보내거나 대상에서 데이터를 검색하는 사용자 지정 HTTP 요청을 만들 수 있습니다. Cloud Connector 확장은 Adobe Experience Platform Edge Network에 우편배달부가 있는 것과 비슷하며 전용 확장이 아직 없는 엔드포인트로 데이터를 보내는 데 사용할 수 있습니다.

이 확장을 사용하여 규칙을 작성할 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

## Cloud Connector 확장 작업 유형

이 섹션에서는 Adobe Experience Platform Cloud Connector 확장 시 사용할 수 있는 데이터 전송 작업 유형에 대해 설명합니다.

### 요청 유형

엔드포인트에 필요한 요청 유형을 선택하려면 [!UICONTROL 요청 유형] 드롭다운 아래에서 해당 유형을 선택합니다.

| 메서드 | 설명 |
|---|---|
| [GET](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/GET) | 지정된 리소스의 표현을 요청합니다. GET을 사용하는 요청은 데이터만 검색해야 합니다. |
| [POST](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/POST) | 지정된 리소스에 엔티티를 제출합니다. 이로 인해 종종 서버의 상태가 변경되거나 부작용이 발생합니다. |
| [PUT](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/PUT) | 대상 리소스의 현재 표현을 모두 요청 페이로드로 바꿉니다. |
| [PATCH](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/PATCH) | 리소스에 부분 수정을 적용합니다. |
| [DELETE](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/DELETE) | 지정된 리소스를 삭제합니다. |

### 엔드포인트 URL

요청 유형 드롭다운 메뉴 옆의 텍스트 필드에 데이터를 보내는 엔드포인트의 URL을 입력합니다.

### 쿼리 매개 변수, 헤더 및 본문 구성

각 탭(쿼리 매개 변수, 헤더 및 본문 데이터 요소)을 사용하여 지정된 엔드포인트로 보낼 데이터를 제어합니다.

#### 쿼리 매개 변수

쿼리 문자열 매개 변수로 전송할 각 키-값 쌍에 대한 키와 값을 정의합니다. 데이터 요소를 수동으로 입력하려면 이벤트 전달을 위해 중괄호 데이터 요소 토큰화를 사용합니다. “siteSection”이라는 데이터 요소의 값을 키 또는 값으로 참조하려면 `{{siteSection}}`을 입력합니다. 또는 드롭다운 메뉴에서 이전에 만든 데이터 요소를 선택합니다.

쿼리 매개 변수를 더 추가하려면 **[!UICONTROL 다른 매개 변수 추가]**&#x200B;를 선택하십시오.

#### 헤더

헤더로 전송할 각 키-값 쌍의 키와 값을 정의합니다. 데이터 요소를 수동으로 입력하려면 이벤트 전달을 위해 중괄호 데이터 요소 토큰화를 사용합니다. “pageName”이라는 데이터 요소의 값을 키 또는 값으로 참조하려면 `{{pageName}}`을 입력합니다. 또는 드롭다운 메뉴에서 이전에 만든 데이터 요소를 선택하여 선택합니다.

헤더를 더 추가하려면 **[!UICONTROL 다른 헤더 추가]**&#x200B;를 선택하십시오.

다음 표는 사전 정의된 헤더를 나열합니다. 이러한 헤더에만 제한되지 않으며 필요한 경우 사용자 지정 헤더를 추가할 수 있지만 편의를 위해 제공되었습니다.

>[!NOTE]
>
>이러한 헤더에 대한 자세한 내용은 [https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers)를 참조하십시오.

| Header | 설명 |
|---|---|
| [A-IM](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Accept) | |
| [Accept](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Accept) | |
| [Accept-Charset](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Accept-Charset) | |
| [Accept-Encoding](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Accept-Encoding) | |
| [Accept-Language](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Accept-Language) | |
| [Accept-Datetime](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Accept) | 사용자 에이전트가 원래 리소스의 이전 상태에 액세스하려고 함을 나타내기 위해 전송됩니다. 이를 위해서 `Accept-Datetime` 헤더는 원래 리소스의 TimeGate에 대해 실행된 HTTP 요청에 전달되고, 이 값은 원래 리소스의 원하는 이전 상태에 대한 날짜/시간을 나타냅니다. |
| Access-Control-Request-Headers | [Preflight 요청](https://developer.mozilla.org/ko-KR/docs/Glossary/preflight_request)을 실행할 때 브라우저에서 사용하며, 실제 요청이 이루어질 때 클라이언트에서 전송할 [HTTP 헤더](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers)를 서버에 알립니다. |
| Access-Control-Request-Method | [Preflight 요청](https://developer.mozilla.org/ko-KR/docs/Glossary/preflight_request)을 실행할 때 브라우저에서 실제 요청이 수행될 때 사용할 [HTTP 메서드](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods)를 서버에 알려주는 데 사용합니다. Preflight 요청은 항상 [선택사항](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/OPTIONS)이고 실제 요청과 동일한 메서드를 사용하지 않으므로 이 헤더가 필요합니다. |
| Authorization | 서버에 사용자 에이전트를 인증하기 위한 자격 증명을 포함합니다. |
| [Cache-Control](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Cache-Control) | 요청과 응답 모두에서 메커니즘을 캐싱하기 위한 지시문입니다. |
| [Connection](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Connection) | 현재 트랜잭션이 완료된 후 네트워크 연결이 열려 있는지 여부를 제어합니다. |
| [Content-Length](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Content-Length) | 리소스의 크기(바이트 수)입니다. |
| [Content-Type](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Content-Type) | 리소스의 미디어 유형을 나타냅니다. |
| Cookie | 이전에 서버에서 [`Set-Cookie`](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Set-Cookie) 헤더를 사용해 전송한 저장된 [HTTP 쿠키](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Cookies)가 포함됩니다. |
| Date | 일반 HTTP 헤더에는 메시지가 시작된 날짜와 시간이 포함됩니다. |
| [DNT](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/DNT) | 사용자의 추적 환경 설정을 표시합니다. |
| Expect | 요청을 제대로 처리하기 위해 서버에서 이행해야 하는 기대를 나타냅니다. |
| Forwarded | 프록시가 요청 경로에 관련되어 있을 때 변경되거나 손실되는 [역방향 프록시 서버](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling)의 정보를 포함합니다. |
| From | 요청한 사용자 에이전트를 제어하는 사람의 인터넷 이메일 주소를 포함합니다. |
| Host | 요청을 전송할 서버의 호스트 및 포트 번호를 지정합니다. |
| If-Match | |
| If-Modified-Since | |
| [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) | |
| [If-Range](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/If-Range) | |
| [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) | |
| [Max-Forwards](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) | |
| [Origin](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Origin) | |
| [Pragma](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Pragma) | 요청 응답 체인을 따라 어디서나 다양한 영향을 줄 수 있는 구현별 헤더입니다. Cache-Control 헤더가 아직 없는 HTTP/1.0 캐시와의 이전 버전 호환성을 위해 사용됩니다. | |
| [Proxy-Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Range](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Range) | 서버에서 반환할 문서의 일부를 나타냅니다. | |
| [Referer](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Referer) | 현재 요청된 페이지에 대한 링크가 뒤에 이어지는 이전 웹 페이지의 주소입니다. | |
| TE | 사용자 에이전트에서 수락할 전송 인코딩을 지정합니다. (비공식적으로 `Accept-Transfer-Encoding`(좀 더 직관적인)이라고 할 수 있습니다.) |
| Upgrade | [`Upgrade` 헤더 필드에 대한 관련 RFC 문서는 RFC 7230, 섹션 6.7](https://tools.ietf.org/html/rfc7230#section-6.7)입니다. 이 표준은 현재 클라이언트, 서버, 전송 프로토콜 연결에서 다른 프로토콜로 업그레이드하거나 변경하는 규칙을 설정합니다. 예를 들어, 서버에서 `Upgrade` 헤더 필드를 인식하고 구현하기로 결정한다고 가정할 때 이 헤더 표준을 사용하면 클라이언트를 HTTP 1.1에서 HTTP 2.0으로 변경할 수 있습니다. 양 당사자 모두 `Upgrade` 헤더 필드에 지정된 용어를 수락하지 않아도 됩니다. 클라이언트와 서버 헤더 모두에서 사용할 수 있습니다. `Upgrade` 헤더 필드가 지정된 경우, 발신자는 `upgrade` 옵션이 지정된 `Connection` 헤더 필드도 보내야 합니다. | |
| [User-Agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) | 네트워크 프로토콜 피어가 요청한 소프트웨어 사용자 에이전트의 애플리케이션 유형, 운영 체제, 소프트웨어 공급업체 또는 소프트웨어 버전을 식별할 수 있도록 해주는 특성 문자열이 들어 있습니다. |
| [Via](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Via) | 프록시 및 역방향 프록시에 의해 추가되고 요청 헤더와 응답 헤더에 표시될 수 있습니다. |
| [Warning](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | 발생 가능한 문제에 대한 일반적인 경고 정보입니다. |
| X-CSRF-Token | |
| X-Requested-With | |

#### JSON 본문

요청 본문에 보낼 각 키-값 쌍에 대한 키와 값을 정의합니다. 데이터 요소를 수동으로 입력하려면 이벤트 전달을 위해 중괄호 데이터 요소 토큰화를 사용합니다. “appSection”이라는 데이터 요소의 값을 키 또는 값으로 참조하려면 `{{appSection}}`을(를) 입력합니다. 또는 드롭다운 메뉴에서 이전에 만든 데이터 요소를 선택합니다.

키-값 쌍을 더 추가하려면 **[!UICONTROL 다른 키-값 쌍 추가]**&#x200B;를 선택하십시오.

#### Raw 본문

요청 본문에 보낼 각 키-값 쌍에 대한 키와 값을 정의합니다. 데이터 요소를 수동으로 입력하려면 이벤트 전달을 위해 중괄호 데이터 요소 토큰화를 사용합니다. “appSection”이라는 데이터 요소의 값을 키 또는 값으로 참조하려면 `{{appSection}}`을(를) 입력합니다. 또는 드롭다운 메뉴에서 이전에 만든 데이터 요소를 선택하여 선택합니다. 하나 이상의 데이터 요소를 추가할 수 있습니다.

### 고급

이벤트 전달의 규칙 내 작업은 순차적으로 실행됩니다. 클라이언트로부터 들어오는 이벤트에는 표시되지 않는 외부 소스에서 데이터를 검색한 다음 이 응답을 가져와서 단일 규칙 내의 후속 작업에서 이 데이터를 변환하거나 최종 대상으로 보내는 경우가 있을 수 있습니다. 고급 섹션의 “요청 응답 저장”을 사용하면 이 기능을 사용할 수 있습니다.

끝점에서 응답 본문을 저장하려면 **[!UICONTROL 요청 응답 저장]** 상자를 선택하고 텍스트 필드에 응답 키를 정의하십시오.

응답 키를 `productDetails`로 정의한 경우, 데이터 요소에서 이 데이터를 참조한 다음 동일한 규칙 내의 후속 작업에서 이 데이터 요소를 참조합니다. `productDetail`을 참조하는 데이터 요소를 만들려면 `path` 유형의 데이터 요소를 만들고 다음 경로를 입력합니다.

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```
