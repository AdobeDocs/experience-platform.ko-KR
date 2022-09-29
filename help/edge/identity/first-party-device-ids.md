---
title: Platform Web SDK의 자사 장치 ID
description: Adobe Experience Platform Web SDK에 대한 자사 장치 ID(FPID)를 구성하는 방법을 알아봅니다.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 0%

---

# Platform Web SDK의 자사 장치 ID

Adobe Experience Platform Web SDK가 할당합니다 [Adobe Experience Cloud ID(ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) 사용자 행동을 추적하기 위해 쿠키의 사용을 통해 웹 사이트 방문자에게 문의하십시오. 쿠키 수명 단위에 대한 브라우저 제한을 설명하기 위해 대신 고유한 장치 식별자를 설정 및 관리하도록 선택할 수 있습니다. 이를 자사 장치 ID(FPID)라고 합니다.

>[!NOTE]
>
>자사 장치 ID 지원은 Platform Web SDK를 통해 Platform Edge 네트워크에 데이터를 전송할 때만 사용할 수 있습니다.

이 문서에서는 Platform Web SDK 구현에 대한 자사 장치 ID를 구성하는 방법에 대해 설명합니다.

## 전제 조건

이 안내서에서는 ECID의 역할 및 `identityMap`. 다음 사항에 대한 개요를 참조하십시오. [웹 SDK의 ID 데이터](./overview.md) 추가 정보.

## FPID 사용

FPID는 자사 쿠키를 사용하여 방문자를 추적합니다. 자사 쿠키는 DNS를 활용하는 서버를 사용하여 설정할 때 가장 효과적입니다 [레코드](https://datatracker.ietf.org/doc/html/rfc1035) (IPv4의 경우) 또는 [AAAA 레코드](https://datatracker.ietf.org/doc/html/rfc3596) (IPv6의 경우), DNS CNAME 또는 JavaScript 코드와 반대됩니다.

>[!IMPORTANT]
>
>레코드 또는 AAAA 레코드는 쿠키를 설정하고 추적하는 경우에만 지원됩니다. 데이터 수집에 대한 기본 방법은 DNS CNAME을 통해 입니다. 즉, FPID는 A 레코드 또는 AAAA 레코드를 사용하여 설정되고 CNAME을 사용하여 Adobe으로 전송됩니다.
>
>다음 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) 은 여전히 자사 데이터 수집에 대해 지원됩니다.

FPID 쿠키가 설정되면 이벤트 데이터를 수집하여 Adobe으로 전송할 수 있습니다. 수집된 FPID는 Adobe Experience Cloud 애플리케이션에서 계속 기본 식별자인 ECID를 생성하는 시드로 사용됩니다.

웹 사이트 방문자에 대한 FPID를 Platform Edge Network에 보내려면 FPID를 `identityMap` 해당 방문자에 대한 방문 수입니다. 다음 문서의 뒷부분에서 섹션을 참조하십시오. [에서 FPID 사용 `identityMap`](#identityMap) 추가 정보.

### ID 형식 요구 사항

Platform Edge Network는 [UUIDv4 형식](https://datatracker.ietf.org/doc/html/rfc4122). UUIDv4 형식이 아닌 장치 ID는 거부됩니다.

UUID를 생성하면 거의 항상 고유한 무작위 ID가 생성되며 충돌 발생 가능성이 무시할 수 있습니다. UUIDv4는 IP 주소 또는 기타 PII(개인 식별 정보)를 사용하여 초기 설정할 수 없습니다. UUID는 어디서나 사용할 수 있으며 거의 모든 프로그래밍 언어로 라이브러리를 찾아 생성할 수 있습니다.

## 자체 서버를 사용하여 쿠키 설정

소유한 서버를 사용하여 쿠키를 설정할 때 브라우저 정책으로 인해 쿠키가 제한되지 않도록 하는 데 다양한 방법을 사용할 수 있습니다.

* 서버측 스크립팅 언어를 사용하여 쿠키 생성
* 사이트의 하위 도메인 또는 다른 종단점에 대한 API 요청에 응답으로 쿠키를 설정합니다
* CMS를 사용하여 쿠키 생성
* CDN을 사용하여 쿠키 생성

>[!IMPORTANT]
>
>JavaScript의 `document.cookie` 메서드는 쿠키 지속 시간을 제한하는 브라우저 정책으로부터 거의 보호되지 않습니다.

### 쿠키를 설정하는 경우

FPID 쿠키는 Edge 네트워크에 대한 요청을 수행하기 전에 가장 먼저 설정해야 합니다. 그러나 이 작업이 불가능한 시나리오에서 ECID는 여전히 기존 메서드를 사용하여 생성되며 쿠키가 존재하는 한 기본 식별자로 작동합니다.

ECID가 결국 브라우저 삭제 정책의 영향을 받지만 FPID가 그렇지 않다고 가정할 경우 FPID는 다음 방문의 기본 식별자가 되며 후속 방문마다 ECID를 시딩하는 데 사용됩니다.

### 쿠키에 대한 만료 설정

쿠키의 만료를 설정하는 것은 FPID 기능을 구현할 때 신중하게 고려해야 하는 것입니다. 이러한 결정을 내릴 때, 해당 각 지역의 법률 및 정책과 함께 조직이 운영되는 국가 또는 지역을 고려해야 합니다.

이 결정의 일부로, 회사 차원의 쿠키 설정 정책 또는 운영 중인 각 로케일의 사용자에 따라 달라지는 정책을 채택할 수 있습니다.

쿠키의 초기 만료로 선택하는 설정에 관계없이, 사이트에 대한 새 방문이 발생할 때마다 쿠키의 만료를 확장하는 논리를 포함해야 합니다.

## 쿠키 플래그의 영향

쿠키가 다른 브라우저에서 처리되는 방식에 영향을 주는 다양한 쿠키 플래그가 있습니다.

* [&#39;HTTPOnly&#39;](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

를 사용하여 설정된 쿠키 `HTTPOnly` 클라이언트측 스크립트를 사용하여 플래그에 액세스할 수 없습니다. 즉, `HTTPOnly` fpid를 설정할 때 플래그에 포함할 쿠키 값을 읽으려면 서버측 스크립팅 언어를 사용해야 합니다 `identityMap`.

Platform Edge Network에서 FPID 쿠키의 값을 읽도록 선택하는 경우 `HTTPOnly` 플래그는 클라이언트측 스크립트에서 이 값에 액세스할 수 없지만 Platform Edge 네트워크의 쿠키 읽기 기능에 부정적인 영향을 주지 않습니다.

>[!NOTE]
>
>의 사용 `HTTPOnly` 플래그는 쿠키 라이프타임을 제한할 수 있는 쿠키 정책에 영향을 주지 않습니다. 그러나 FPID의 값을 설정하고 읽을 때 여전히 고려해야 할 사항입니다.

### `Secure` {#secure}

를 사용하여 설정된 쿠키 `Secure` 속성은 HTTPS 프로토콜을 통해 암호화된 요청이 있는 서버에만 전송됩니다. 이 플래그를 사용하면 중간 공격자가 쿠키의 값에 쉽게 액세스할 수 없도록 할 수 있습니다. 가능하면 를 설정하는 것이 좋습니다 `Secure` 플래그.

### `SameSite` {#same-site}

다음 `SameSite` 속성을 사용하면 서버가 사이트 간 요청을 사용하여 쿠키를 전송하는지 여부를 결정할 수 있습니다. 이 속성은 사이트 간 위조 공격으로부터 일부 보호를 제공합니다. 가능한 세 가지 값이 있습니다. `Strict`, `Lax` 및 `None`. 조직에 적합한 설정을 확인하려면 내부 팀에 문의하십시오.

없는 경우 `SameSite` 속성이 지정되면 일부 브라우저에 대한 기본 설정이 `SameSite=Lax`.

## 에서 FPID 사용 `identityMap` {#identityMap}

다음은 FPID를 기본적으로 설정하는 방법의 예입니다 `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

다른 ID 유형과 마찬가지로 내에서 다른 ID와 함께 FPID를 포함할 수 있습니다 `identityMap`. 다음은 인증된 CRM ID에 포함된 FPID의 예입니다.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

자사 데이터 수집이 활성화될 때 Edge Network에서 읽는 쿠키에 FPID가 포함된 경우 인증된 CRM ID만 캡처해야 합니다.

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

다음 `identityMap` 에지 네트워크에서 오류가 발생하여 `primary` FPID에 대한 표시기입니다. 에 있는 ID 중 하나 이상 `identityMap` 을(를) 로 표시해야 합니다. `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

이 경우 Experience Edge에서 반환한 오류 응답은 다음과 비슷합니다.

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID 계층

ECID와 FPID가 모두 있으면 ECID가 사용자를 식별하는 데 우선 순위가 지정됩니다. 이렇게 하면 기존 ECID가 브라우저 쿠키 저장소에 있을 때 기본 식별자가 계속 되고 기존 방문자 수가 영향을 받지 않습니다. 기존 사용자의 경우 FPID는 ECID가 만료되거나 브라우저 정책 또는 수동 프로세스의 결과로 삭제될 때까지 기본 ID가 되지 않습니다.

ID는 다음 순서로 우선 순위가 지정됩니다.

1. 에 포함된 ECID `identityMap`
1. 쿠키에 저장된 ECID
1. 에 포함된 FPID `identityMap`
1. 쿠키에 저장된 FPID

## 자사 장치 ID로 마이그레이션

이전 구현에서 FPID를 사용하여 로 마이그레이션하는 경우 전환이 낮은 수준에서 어떤 모습일지 시각화하기가 어려울 수 있습니다.

이 프로세스를 설명하는 데 도움이 되도록 이전에 사이트를 방문한 고객이 참여하는 시나리오와, FPID 마이그레이션이 Adobe 솔루션에서 해당 고객이 식별되는 방식에 어떤 영향을 미칠 것인지 생각해 보십시오.

![FPID로 마이그레이션한 후 방문 간에 고객의 ID 값이 업데이트되는 방식을 보여주는 다이어그램](../assets/identity/tracking/visits.png)

| 방문 | 설명 |
| --- | --- |
| 첫 번째 방문 | FPID 쿠키 설정을 아직 시작하지 않았다고 가정합니다. 에 포함된 ECID [AMCV 쿠키](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) 은 방문자를 식별하는 데 사용되는 식별자입니다. |
| 두 번째 방문 | 자사 장치 ID 솔루션 롤아웃이 시작되었습니다. 기존 ECID는 여전히 존재하며 방문자 식별의 기본 식별자로 계속 사용됩니다. |
| 세 번째 방문 | 두 번째와 세 번째 방문 사이에 브라우저 정책으로 인해 ECID가 삭제된 충분한 시간이 경과되었습니다. 그러나 FPID가 DNS A-record를 사용하여 설정되었으므로 FPID가 유지됩니다. 이제 FPID를 기본 ID로 간주하여 최종 사용자 장치에 기록된 ECID를 시딩하는 데 사용합니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션에서 새 방문자로 간주됩니다. |
| 네 번째 방문 | 세 번째와 네 번째 방문 사이에 브라우저 정책으로 인해 ECID가 삭제된 충분한 시간이 경과되었습니다. 이전 방문과 마찬가지로 FPID는 설정된 방식 때문에 유지됩니다. 이번에는 이전 방문과 동일한 ECID가 생성됩니다. 사용자가 Experience Platform 및 Experience Cloud 솔루션 전체에서 이전 방문과 동일한 사용자로 표시됩니다. |
| 다섯 번째 방문 | 네 번째와 다섯 번째 방문 사이에 최종 사용자는 브라우저의 모든 쿠키를 지웠습니다. 새 FPID가 생성되어 새 ECID 생성을 시딩하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션에서 새 방문자로 간주됩니다. |

{style=&quot;table-layout:auto&quot;}

## FAQ

다음은 자사 장치 ID에 대해 자주 묻는 질문에 대한 답변 목록입니다.

### ID를 시딩하는 것은 단순히 ID를 생성하는 것과 어떻게 다릅니까?

시드 개념은 Adobe Experience Cloud에 전달된 FPID가 결정론적 알고리즘을 사용하여 ECID로 변환된다는 점에서 독특합니다. 동일한 FPID가 Adobe Experience Platform Edge Network에 전송될 때마다 동일한 ECID가 FPID에서 초기 설정됩니다.

### 자사 장치 ID는 언제 생성되어야 합니까?

잠재적 방문자 인플레이션을 줄이려면 Platform Web SDK를 사용하여 첫 번째 요청을 수행하기 전에 FPID를 생성해야 합니다. 그러나 이 작업을 수행할 수 없는 경우 ECID가 해당 사용자에 대해 계속 생성되며 기본 식별자로 사용됩니다. 생성된 FPID는 ECID가 더 이상 없을 때까지 기본 식별자가 되지 않습니다.

### 자사 장치 ID를 지원하는 데이터 수집 방법은 무엇입니까?

현재 Platform Web SDK만 FPID를 지원합니다.

### FPID가 플랫폼 또는 Experience Cloud 솔루션에 저장됩니까?

FPID를 사용하여 ECID를 시딩하면 `identityMap` 및 는 생성된 ECID로 대체되었습니다. FPID는 Adobe Experience Platform 또는 Experience Cloud 솔루션에 저장되지 않습니다.
