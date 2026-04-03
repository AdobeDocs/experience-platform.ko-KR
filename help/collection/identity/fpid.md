---
title: 데이터 수집에서 자사 디바이스 ID 사용
description: Edge Network으로 데이터를 전송하는 웹 구현에서 지속적인 ID를 위해 자사 디바이스 ID(FPID)를 구성합니다.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# 데이터 수집에서 자사 디바이스 ID 사용

Experience Platform Edge Network은 Experience Cloud ID(ECID)를 사용하여 웹 사이트 방문자를 식별합니다. 소유한 속성에 대한 ID 내구성을 향상시키기 위해 자사 디바이스 ID(FPID)라고 하는 고유한 디바이스 식별자를 설정하고 관리할 수 있습니다. Edge Network은 FPID를 사용하여 Adobe 솔루션에서 사용하는 ECID를 시드합니다.

이 페이지에서는 사용자가 ECID 및 `identityMap`에 익숙하다고 가정합니다. 자세한 내용은 [데이터 수집의 ID](./overview.md)를 참조하십시오.

## FPID 사용 시기 {#when-to-use}

브라우저 제한 사항은 Adobe이 재방문자를 인식하는 데 사용하는 쿠키의 수명을 단축할 수 있습니다. 조직이 소유하고 제어하는 사이트에 보다 지속적인 ID가 필요한 경우 FPID를 사용하여 고유한 장치 식별자를 관리하고 이를 사용하여 ECID를 시드할 수 있습니다.

FPID는 Web SDK 태그 확장을 포함하여 Web SDK을 사용하는 웹 구현에 대해 지원됩니다. 이는 조직이 소유하는 도메인에서 ID 지속성을 강화하거나 소유한 웹 속성에서 보고 및 개인화에 대한 연속성을 향상하려는 경우 이상적입니다. 또한 사용자가 제어하는 인프라에서 자사 쿠키를 설정하고 관리할 수 있습니다.

FPID는 앱에서 웹으로의 핸드오프 또는 여러 도메인의 ID 연속성을 주요 목표로 하는 경우 적합한 도구가 아닙니다. 이러한 시나리오에 대해서는 [모바일-웹 ID 공유](./mobile-to-web.md) 및 [도메인 간 공유](./cross-domain-sharing.md)를 참조하십시오.

FPID 사용에 대한 이점은 다음과 같습니다.

* 소유한 속성에 대한 지속성 강화
* 장치 식별자가 생성 및 관리되는 방식에 대한 제어권을 강화합니다.
* 분석 및 개인화를 위한 내구성 있는 기반입니다.

FPID 사용에 대한 장단점은 다음과 같습니다.

* 기본 ID 동작에 의존하는 것보다 구현 책임이 더 큽니다.
* 서버 측 쿠키 논리 및 데이터 수집 구성 간의 조정.
* 식별자를 확인하기 위한 추가 유효성 검사가 예상대로 사용되고 있습니다.

### 높은 수준 설정 경로

1. 제어하는 인프라에서 자사 디바이스 ID를 생성하고 관리합니다.
1. [자사 쿠키](#setting-cookie-datastreams) 또는 [ID 페이로드](#identityMap)에서 해당 ID를 읽도록 구현을 구성하십시오.
1. 재방문자가 소유한 속성에서 시간 경과에 따라 일관된 ID를 유지하는지 확인합니다.

## FPID 작동 방식 {#how-fpids-work}

Adobe Experience Cloud으로 전달된 FPID는 결정론적 알고리즘을 사용하여 ECID로 변환됩니다. 동일한 FPID가 Edge Network으로 전송될 때마다 동일한 ECID가 FPID에서 시드됩니다. FPID를 사용하여 ECID를 시드하면 `identityMap`에서 삭제되고 생성된 ECID로 대체됩니다. FPID는 Adobe Experience Platform 또는 Experience Cloud 솔루션에 저장되지 않습니다.

ECID와 FPID가 모두 있는 경우 ECID는 항상 사용자를 먼저 식별하는 데 사용됩니다. 이 우선 순위는 기존 ECID가 브라우저 쿠키 저장소에 있을 때 기본 식별자로 유지되며 기존 방문자 수가 인플레이션을 위험하지 않도록 합니다. 기존 사용자의 경우 ECID가 만료되거나 브라우저 정책 또는 수동 작업의 결과로 삭제될 때까지 FPID가 기본 ID가 되지 않습니다.

ID는 다음 순서로 우선 순위가 지정됩니다.

1. `identityMap`에 포함된 ECID
1. 쿠키에 저장된 ECID
1. `identityMap`에 포함된 FPID
1. 쿠키에 저장된 FPID

## FPID 쿠키 생성 및 설정 {#set-fpid-cookie}

Edge Network은 [UUIDv4 형식](https://datatracker.ietf.org/doc/html/rfc4122)을 준수하는 ID만 허용합니다. UUIDv4 형식이 아닌 장치 ID가 거부되었습니다.

* UUID는 고유하고 임의적이며 충돌 가능성이 거의 없습니다.
* UUIDv4는 IP 주소 또는 기타 PII(개인 식별 정보)를 사용하여 시드할 수 없습니다.
* UUID를 생성하는 라이브러리는 모든 프로그래밍 언어에 사용할 수 있습니다.

### 서버측 쿠키 설정 {#set-cookie-server}

자체 서버를 통해 쿠키를 설정할 때 다양한 방법을 사용하여 쿠키가 브라우저 정책에 의해 제한되지 않도록 할 수 있습니다.

* 서버측 스크립팅 언어를 사용하여 쿠키 생성
* 사이트의 하위 도메인 또는 다른 끝점에 대한 API 요청에 대한 응답으로 쿠키를 설정합니다.
* 콘텐츠 관리 시스템을 사용하여 쿠키 생성(CMS)
* CDN(콘텐츠 전달 네트워크)을 사용하여 쿠키 생성

자사 쿠키는 DNS [&#x200B; 또는 JavaScript 코드와 반대로 DNS &#x200B;](https://datatracker.ietf.org/doc/html/rfc1035)A 레코드[(IPv4의 경우) 또는 &#x200B;](https://datatracker.ietf.org/doc/html/rfc3596)AAAA 레코드`CNAME`(IPv6의 경우)을 사용하는 서버를 사용하여 설정할 때 가장 효과적입니다.

>[!IMPORTANT]
>
>JavaScript의 `document.cookie` 메서드(태그 메서드 [`cookie.set()`](../tags/cookie.md) 사용 포함)를 사용하여 설정된 쿠키는 쿠키 지속 시간을 제한하는 브라우저 정책으로부터 거의 보호되지 않습니다.

`A` 또는 `AAAA` 레코드는 쿠키 설정 및 추적에 대해서만 지원됩니다. 데이터 수집을 위한 기본 메서드는 DNS `CNAME`을(를) 통해 이루어집니다. FPID는 `A` 또는 `AAAA` 레코드를 사용하여 설정되고 `CNAME`을(를) 사용하여 Adobe으로 전송됩니다. [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko#adobe-managed-certificate-program)을(를) 사용하면 데이터 수집을 위해 `CNAME`을(를) 구성할 수 있습니다.

### 쿠키 설정 시기 {#when-to-set-cookie}

FPID 쿠키는 데이터를 Edge Network에 보내기 전에 이상적으로 설정됩니다. 데이터를 수집하기 전에 동의해야 하는 경우 동의 흐름으로 FPID 쿠키를 조정하는 방법에 대한 지침은 [자사 장치 ID로 동의](./consent.md#consent-with-fpids)를 참조하십시오. 첫 번째 요청에서 ECID를 시드하는 데 FPID를 사용할 수 있는지 확인하면 방문자 인플레이션이 감소합니다. 불가능한 시나리오에서는 여전히 기존 메서드를 사용하여 ECID가 생성되고 쿠키가 존재하는 한 기본 식별자 역할을 합니다. ECID가 더 이상 존재하지 않을 때까지 생성된 FPID가 기본 식별자가 되지 않습니다. ECID가 결국 브라우저 삭제 정책의 영향을 받지만 FPID가 영향을 받지 않는다고 가정할 경우 FPID는 다음 방문에서 기본 식별자가 되고 각 후속 방문에서 ECID를 시드하는 데 사용됩니다.

### 만료 설정 {#set-expiration}

Adobe은 FPID 쿠키의 수명을 신중하게 고려할 것을 권장합니다. 조직의 개인 정보 보호 정책을 조직이 운영되는 국가 또는 지역의 법률 및 정책과 함께 고려해야 합니다. 조직의 설정에 따라 회사 전체의 쿠키 설정 정책 또는 운영하는 각 로케일에서 사용자에 대해 달라지는 정책을 채택할 수 있습니다. 초기 쿠키 만료와 관계없이 새 사이트 방문이 발생할 때마다 만료를 연장하는 논리를 포함해야 합니다.

### 쿠키 플래그 {#cookie-flags}

여러 브라우저에서 쿠키가 처리되는 방식에 영향을 주는 몇 가지 쿠키 플래그가 있습니다.

* **`HTTPOnly`**: `HTTPOnly` 플래그를 사용하여 설정된 쿠키는 클라이언트측 스크립트를 사용하여 액세스할 수 없습니다. 즉, FPID를 설정할 때 `HTTPOnly` 플래그를 설정하는 경우 `identityMap`에 포함할 쿠키 값을 읽으려면 서버측 스크립팅 언어를 사용해야 합니다. Edge Network에서 FPID 쿠키의 값을 읽도록 선택하는 경우 `HTTPOnly` 플래그를 설정하면 클라이언트측 스크립트가 해당 값에 액세스할 수 없지만 Edge Network의 쿠키 읽기 기능에 부정적인 영향을 주지 않습니다. `HTTPOnly` 플래그를 사용해도 쿠키 수명을 제한할 수 있는 쿠키 정책에는 영향을 주지 않습니다. 그러나 FPID의 값을 설정하고 읽으면서 여전히 고려해야 할 사항입니다.
* **`Secure`**: `Secure` 특성이 설정된 쿠키는 HTTPS 프로토콜을 통해 암호화된 요청을 사용하여 서버로만 전송됩니다. 이 플래그를 사용하면 중간자 공격자가 쿠키 값에 쉽게 액세스할 수 없습니다. 가능하면 항상 `Secure` 플래그를 설정하는 것이 좋습니다.
* **`SameSite`**: `SameSite` 특성을 사용하면 서버에서 쿠키가 사이트 간 요청으로 전송되는지 여부를 확인할 수 있습니다. 속성은 크로스 사이트 위조 공격으로부터 일부 보호를 제공합니다. 가능한 값은 `Strict`, `Lax` 및 `None`입니다. 조직에 적합한 설정을 결정하려면 내부 팀에 문의하십시오. `SameSite` 특성이 지정되지 않은 경우 일부 브라우저의 기본 설정은 `SameSite=Lax`입니다.

## Edge Network에 FPID 보내기 {#send-fpid}

다음 두 가지 방법으로 Edge Network에 FPID를 보낼 수 있습니다.

* **[메서드 1](#setting-cookie-datastreams)**: 웹 SDK 호출에 대해 `CNAME`을(를) 구성하고 데이터 스트림 구성에 FPID 쿠키 이름을 포함하십시오.
* **[메서드 2](#identityMap)**: ID 맵에 FPID를 포함합니다.

### 방법 1: `CNAME`을(를) 구성하고 데이터 스트림에서 자사 ID 쿠키를 설정합니다. {#setting-cookie-datastreams}

고유한 도메인에서 FPID 쿠키를 설정하려면 웹 SDK 호출에 대해 고유한 `CNAME`을(를) 구성한 다음 데이터 스트림 구성에서 자사 ID 쿠키 기능을 활성화해야 합니다. DNS의 `CNAME` 레코드를 사용하면 한 도메인 이름에서 다른 도메인 이름으로 별칭을 만들 수 있습니다. 이 별칭은 서드파티 서비스가 자신의 도메인에 속한 것처럼 표시되어 쿠키가 자사 쿠키처럼 보이도록 하는 데 도움이 될 수 있습니다. `CNAME`을(를) 사용하여 자사 데이터 수집을 사용하도록 설정하면 데이터 수집 끝점에 대한 요청 시 도메인에 대한 모든 쿠키가 전송됩니다.

1. Adobe을 사용하여 조직에서 데이터 수집에 사용할 `CNAME` 레코드를 만드십시오. 전체 프로세스를 보려면 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/ko/docs/core-services/interface/data-collection/adobe-managed-cert)을 참조하세요.
1. 데이터 스트림에서 **[!UICONTROL First Party ID Cookie]** 옵션을 사용하도록 설정합니다. 이 설정은 Edge Network에 ID 맵에서 값을 조회하는 대신 자사 디바이스 ID를 조회할 때 지정된 쿠키를 참조하도록 지시합니다. 이 설정을 활성화할 때 FPID가 저장될 쿠키의 이름을 제공해야 합니다. 자세한 내용은 [데이터스트림 만들기 및 구성](/help/datastreams/configure.md#advanced-options)을 참조하십시오.

   ![자사 ID 쿠키 설정을 강조 표시하는 데이터 스트림 구성을 표시하는 플랫폼 UI 이미지](/help/collection/js/assets/first-party-id-datastreams.png)

### 방법 2: `identityMap`에서 FPID 사용 {#identityMap}

FPID를 자체 쿠키에 저장하는 대신 ID 맵을 통해 FPID를 Edge Network으로 보낼 수 있습니다.

다음은 `identityMap`에서 FPID를 설정하는 방법의 예입니다.

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

다른 ID 형식과 마찬가지로 FPID를 `identityMap` 내에 다른 ID와 함께 포함할 수 있습니다. 다음 예에는 인증된 CRM ID가 있는 FPID가 포함되어 있습니다.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

자사 데이터 수집이 활성화된 경우 Edge Network에서 읽는 쿠키에 FPID가 포함된 경우 인증된 CRM ID만 캡처합니다.

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

다음 `identityMap`은(는) FPID에 대한 `primary` 표시기가 없기 때문에 Edge Network에서 오류 응답을 생성합니다. `identityMap`에 있는 ID 중 하나 이상은 `primary`(으)로 표시되어야 합니다.

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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## FPID로 마이그레이션 {#migrating-to-fpid}

이전 구현에서 자사 디바이스 ID로 마이그레이션하는 경우 낮은 수준에서 전환이 어떻게 표시되는지 시각화하기 어려울 수 있습니다. 이 프로세스를 설명하는 데 도움이 되도록 이전에 사이트를 방문한 고객이 포함된 시나리오와 FPID 마이그레이션이 Adobe 솔루션에서 해당 고객을 식별하는 방법에 미칠 영향을 고려하십시오.

![FPID로 마이그레이션한 후 방문 간에 고객의 ID 값이 어떻게 업데이트되는지 보여 주는 다이어그램](/help/collection/js/assets/identity/tracking/visits.png)

| 방문 | 설명 |
| --- | --- |
| 첫 방문 | FPID 쿠키 설정을 아직 시작하지 않았다고 가정합니다. [AMCV 쿠키](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=ko#section-c55af54828dc4cce89f6118655d694c8)에 포함된 ECID는 방문자를 식별하는 데 사용되는 식별자입니다. |
| 두 번째 방문 | FPID 솔루션 롤아웃이 시작되었습니다. 기존 ECID는 여전히 존재하며 방문자 식별을 위한 기본 식별자로 유지됩니다. |
| 세 번째 방문 | 두 번째와 세 번째 방문 사이에 브라우저 정책으로 인해 ECID가 삭제될 만큼 충분한 시간이 경과되었습니다. 그러나 FPID가 DNS `A` 레코드를 사용하여 설정되었으므로 FPID는 유지됩니다. FPID는 이제 기본 ID로 간주되며 최종 사용자 디바이스에 기록되는 ECID를 시드하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션의 새 방문자로 간주됩니다. |
| 네 번째 방문 | 세 번째와 네 번째 방문 사이에 브라우저 정책으로 인해 ECID가 삭제될 만큼 충분한 시간이 경과되었습니다. 이전 방문과 마찬가지로 FPID는 설정된 방식으로 인해 유지됩니다. 이번에는 이전 방문과 동일한 ECID가 생성됩니다. 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션 전체에서 이전 방문과 동일한 사용자로 표시됩니다. |
| 다섯 번째 방문 | 네 번째와 다섯 번째 방문 사이에 최종 사용자는 브라우저의 모든 쿠키를 지웠습니다. 새 FPID가 생성되고 새 ECID 생성을 시드하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션의 새 방문자로 간주됩니다. |
