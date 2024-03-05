---
title: Web SDK의 자사 디바이스 ID
description: Adobe Experience Platform Web SDK에 대한 자사 디바이스 ID(FPID)를 구성하는 방법에 대해 알아봅니다.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# Web SDK의 자사 디바이스 ID

Adobe Experience Platform Web SDK는 [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) 쿠키를 사용하여 웹 사이트 방문자에게 알리고 사용자 행동을 추적합니다. 쿠키 수명에 대한 브라우저 제한 사항을 고려하기 위해 대신 고유한 장치 식별자를 설정하고 관리하도록 선택할 수 있습니다. 이를 자사 디바이스 ID(FPID)라고 합니다.

>[!NOTE]
>
>자사 디바이스 ID 지원은 Platform Web SDK를 통해 Platform Edge Network로 데이터를 전송할 때만 사용할 수 있습니다.

>[!IMPORTANT]
>
>자사 디바이스 ID가 [타사 쿠키](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) Web SDK의 기능입니다.
>자사 디바이스 ID를 사용하거나 서드파티 쿠키를 사용할 수 있지만 두 기능을 동시에 사용할 수는 없습니다.

이 문서에서는 Platform Web SDK 구현을 위한 자사 디바이스 ID를 구성하는 방법을 다룹니다.

## 전제 조건

이 안내서에서는 사용자가 ECID 및 의 역할을 포함하여 Platform Web SDK에 대해 ID 데이터가 작동하는 방식을 잘 알고 있다고 가정합니다. `identityMap`. 의 개요 보기 [웹 SDK의 ID 데이터](./overview.md) 추가 정보.

## FPID 사용

FPID는 자사 쿠키를 사용하여 방문자를 추적합니다. 자사 쿠키는 DNS를 사용하는 서버를 사용하여 설정할 때 가장 효과적입니다 [레코드](https://datatracker.ietf.org/doc/html/rfc1035) (IPv4의 경우) 또는 [AAAA 레코드](https://datatracker.ietf.org/doc/html/rfc3596) DNS CNAME 또는 JavaScript 코드가 아닌 IPv6의 경우.

>[!IMPORTANT]
>
>`A` 또는 `AAAA` 레코드는 쿠키 설정 및 추적에 대해서만 지원됩니다. 데이터 수집을 위한 기본 방법은 DNS CNAME을 통하는 것입니다. 즉, FPID는 A 레코드나 AAAA 레코드를 사용하여 설정되고 CNAME을 사용하여 Adobe으로 전송됩니다.
>
>다음 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) 는 자사 데이터 수집에 대해서도 계속 지원됩니다.

FPID 쿠키가 설정되면 해당 값을 가져와 이벤트 데이터가 수집될 때 Adobe으로 보낼 수 있습니다. 수집된 FPID는 시드로 사용되어 ECID를 생성하는데, 이 ECID는 Adobe Experience Cloud 애플리케이션에서 계속 기본 식별자가 됩니다.

웹 사이트 방문자에 대한 FPID를 Platform Edge Network로 보내려면 `identityMap` 해당 방문자에 대해. 이 문서의 뒷부분에서 섹션 참조 [에서 FPID 사용 `identityMap`](#identityMap) 추가 정보.

### ID 형식 요구 사항

Platform Edge Network는 [UUIDv4 형식](https://datatracker.ietf.org/doc/html/rfc4122). UUIDv4 형식이 아닌 장치 ID는 거부됩니다.

UUID를 생성하면 거의 항상 고유한 임의 ID가 생성되며 충돌이 발생할 확률은 무시할 수 있습니다. UUIDv4는 IP 주소 또는 기타 PII(개인 식별 정보)를 사용하여 시드할 수 없습니다. UUID는 어디에나 존재하며 거의 모든 프로그래밍 언어에 대해 라이브러리를 찾아 생성할 수 있습니다.

## 자체 서버를 사용하여 쿠키 설정

소유한 서버를 사용하여 쿠키를 설정할 때 브라우저 정책으로 인해 쿠키가 제한되지 않도록 하기 위해 다양한 방법을 사용할 수 있습니다.

* 서버측 스크립팅 언어를 사용하여 쿠키 생성
* 사이트의 하위 도메인 또는 다른 끝점에 대한 API 요청에 대한 응답으로 쿠키를 설정합니다.
* CMS를 사용하여 쿠키 생성
* CDN을 사용하여 쿠키 생성

>[!IMPORTANT]
>
>JavaScript를 사용하여 설정된 쿠키 `document.cookie` 메서드는 쿠키 지속 시간을 제한하는 브라우저 정책으로부터 거의 보호되지 않습니다.

### 쿠키 설정 시기

FPID 쿠키는 Edge Network에 요청하기 전에 이상적으로 설정해야 합니다. 단, 그럴 수 없는 시나리오에서는 기존 메서드를 사용하여 ECID가 여전히 생성되고 쿠키가 존재하는 한 기본 식별자 역할을 합니다.

ECID가 결국 브라우저 삭제 정책의 영향을 받지만 FPID가 영향을 받지 않는다고 가정할 경우 FPID는 다음 방문에서 기본 식별자가 되고 각 후속 방문에서 ECID를 시드하는 데 사용됩니다.

### 쿠키 만료 설정

쿠키의 만료를 설정하는 것은 FPID 기능을 구현할 때 신중하게 고려해야 하는 사항입니다. 이를 결정할 때는 각 지역의 법률 및 정책과 함께 조직이 운영되는 국가 또는 지역을 고려해야 합니다.

이 결정의 일부로 회사 전체의 쿠키 설정 정책 또는 운영하는 각 로케일에서 사용자에 따라 달라지는 정책을 채택할 수 있습니다.

쿠키의 초기 만료에 대해 선택하는 설정에 관계없이 사이트를 새로 방문할 때마다 쿠키 만료를 확장하는 논리를 포함해야 합니다.

## 쿠키 플래그의 영향

다양한 브라우저에서 쿠키가 처리되는 방식에 영향을 주는 다양한 쿠키 플래그가 있습니다.

* [&#39;HTTPOnly&#39;](#http-only)
* [&#39;보안&#39;](#secure)
* [&#39;SameSite&#39;](#same-site)

### `HTTPOnly` {#http-only}

를 사용하여 설정된 쿠키 `HTTPOnly` 클라이언트측 스크립트를 사용하여 플래그에 액세스할 수 없습니다. 즉, 다음을 설정하면 `HTTPOnly` flag fpid를 설정할 때 를 포함할 쿠키 값을 읽으려면 서버측 스크립팅 언어를 사용해야 합니다 `identityMap`.

Platform Edge Network가 FPID 쿠키의 값을 읽도록 선택한 경우 `HTTPOnly` 플래그를 사용하면 클라이언트측 스크립트가 해당 값에 액세스할 수 없지만 Platform Edge Network의 쿠키 읽기 기능에 부정적인 영향을 주지 않습니다.

>[!NOTE]
>
>사용 `HTTPOnly` 플래그는 쿠키 수명을 제한할 수 있는 쿠키 정책에 영향을 주지 않습니다. 그러나 FPID의 값을 설정하고 읽으면서 여전히 고려해야 할 사항입니다.

### `Secure` {#secure}

로 설정된 쿠키 `Secure` 속성은 HTTPS 프로토콜을 통해 암호화된 요청을 통해 서버로만 전송됩니다. 이 플래그를 사용하면 중간자 공격자가 쿠키의 값에 쉽게 액세스할 수 없게 됩니다. 가능하면 항상 를 설정하는 것이 좋습니다. `Secure` 플래그.

### `SameSite` {#same-site}

다음 `SameSite` 속성을 사용하면 서버에서 쿠키가 사이트 간 요청으로 전송되는지 여부를 확인할 수 있습니다. 속성은 크로스 사이트 위조 공격으로부터 일부 보호를 제공합니다. 세 가지 가능한 값이 있습니다. `Strict`, `Lax`, 및 `None`. 조직에 적합한 설정을 결정하려면 내부 팀에 문의하십시오.

없는 경우 `SameSite` 속성을 지정했습니다. 이제 일부 브라우저의 기본 설정이 `SameSite=Lax`.

## 에서 FPID 사용 `identityMap` {#identityMap}

아래는에서 FPID를 설정하는 방법의 예입니다. `identityMap`:

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

다른 ID 유형과 마찬가지로 FPID를 다른 ID와 함께 포함할 수 있습니다 `identityMap`. 다음은 인증된 CRM ID에 포함된 FPID의 예입니다.

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

자사 데이터 수집이 활성화될 때 Edge Network에서 읽는 쿠키에 FPID가 포함되어 있으면 인증된 CRM ID만 캡처해야 합니다.

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

다음 `identityMap` 가 누락되면 Edge Network에서 오류 응답이 발생합니다. `primary` FPID에 대한 표시기. 에 있는 ID 중 하나 이상 `identityMap` 은(는) (으)로 표시되어야 합니다. `primary`.

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

이 경우 Edge Network에서 반환하는 오류 응답은 다음과 비슷합니다.

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

## 계층

ECID와 FPID가 모두 존재하는 경우, ECID는 사용자를 식별하는 데 우선 순위가 지정됩니다. 이렇게 하면 기존 ECID가 브라우저 쿠키 저장소에 있을 때 기본 식별자로 유지되며 기존 방문자 수가 영향을 받지 않습니다. 기존 사용자의 경우 FPID는 ECID가 만료되거나 브라우저 정책 또는 수동 프로세스의 결과로 삭제될 때까지 기본 ID가 되지 않습니다.

ID는 다음 순서로 우선 순위가 지정됩니다.

1. 에 포함된 ECID `identityMap`
1. 쿠키에 저장된 ECID
1. 에 포함된 FPID `identityMap`
1. 쿠키에 저장된 FPID

## 자사 디바이스 ID로 마이그레이션

이전 구현에서 FPID를 사용하여 마이그레이션하는 경우 낮은 수준에서 전환이 어떻게 보이는지 시각화하기 어려울 수 있습니다.

이 프로세스를 설명하는 데 도움이 되도록 이전에 사이트를 방문한 고객이 포함된 시나리오와 FPID 마이그레이션이 Adobe 솔루션에서 해당 고객을 식별하는 방법에 미칠 영향을 고려하십시오.

![FPID로 마이그레이션한 후 방문 간에 고객의 ID 값이 어떻게 업데이트되는지 보여 주는 다이어그램](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>다음 `ECID` 쿠키는 항상 다음보다 우선합니다. `FPID`.

| 방문 | 설명 |
| --- | --- |
| 첫 번째 방문 | FPID 쿠키 설정을 아직 시작하지 않았다고 가정합니다. 에 포함된 ECID [AMCV 쿠키](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) 은 방문자를 식별하는 데 사용되는 식별자입니다. |
| 두 번째 방문 | 자사 디바이스 ID 솔루션 롤아웃이 시작되었습니다. 기존 ECID는 여전히 존재하며 방문자 식별을 위한 기본 식별자로 유지됩니다. |
| 세 번째 방문 | 두 번째와 세 번째 방문 사이에 브라우저 정책으로 인해 ECID가 삭제될 만큼 충분한 시간이 경과되었습니다. 그러나 FPID가 DNS A-record를 사용하여 설정되었기 때문에 FPID는 유지됩니다. 이제 FPID가 기본 ID로 간주되어 최종 사용자 디바이스에 기록되는 ECID를 시드하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션에서 새 방문자로 간주됩니다. |
| 네 번째 방문 | 세 번째와 네 번째 방문 사이에 브라우저 정책으로 인해 ECID가 삭제될 만큼 충분한 시간이 경과되었습니다. 이전 방문과 마찬가지로 FPID는 설정된 방식으로 인해 유지됩니다. 이번에는 이전 방문과 동일한 ECID가 생성됩니다. 사용자는 Experience Platform 및 Experience Cloud 솔루션 전체에서 이전 방문과 동일한 사용자로 표시됩니다. |
| 다섯 번째 방문 | 네 번째와 다섯 번째 방문 사이에 최종 사용자는 브라우저의 모든 쿠키를 지웠습니다. 새 FPID가 생성되고 새 ECID 생성을 시드하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션에서 새 방문자로 간주됩니다. |

{style="table-layout:auto"}

## FAQ

다음은 자사 디바이스 ID에 대한 FAQ 응답 목록입니다.

### ID 시드는 단순히 ID를 생성하는 것과 어떻게 다릅니까?

시드의 개념은 Adobe Experience Cloud에 전달된 FPID가 결정론적 알고리즘을 사용하여 ECID로 변환된다는 점에서 독특합니다. 동일한 FPID가 Adobe Experience Platform Edge Network로 전송될 때마다 동일한 ECID가 FPID에서 시드됩니다.

### 자사 디바이스 ID는 언제 생성해야 합니까?

잠재적 방문자 인플레이션을 줄이려면 Web SDK를 사용하여 첫 번째 요청을 수행하기 전에 FPID를 생성해야 합니다. 그러나 이렇게 할 수 없는 경우 해당 사용자에 대한 ECID가 계속 생성되고 기본 식별자로 사용됩니다. 생성된 FPID는 ECID가 더 이상 존재하지 않을 때까지 기본 식별자가 되지 않습니다.

### 자사 디바이스 ID를 지원하는 데이터 수집 방법

현재 Web SDK만 FPID를 지원합니다.

### FPID가 플랫폼 또는 Experience Cloud 솔루션에 저장됩니까?

FPID를 사용하여 ECID를 시드하면 `identityMap` 및 가 생성된 ECID로 대체되었습니다. FPID는 Adobe Experience Platform 또는 Experience Cloud 솔루션에 저장되지 않습니다.
