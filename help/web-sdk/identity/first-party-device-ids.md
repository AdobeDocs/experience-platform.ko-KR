---
title: 웹 SDK에서 자사 디바이스 ID 사용
description: Adobe Experience Platform Web SDK에서 자사 디바이스 ID(FPID)를 구성하는 방법에 대해 알아봅니다.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: c7be2fff2cd94677b745e6ed095454bc46f8a37b
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 0%

---


# 웹 SDK에서 자사 디바이스 ID 사용

Adobe Experience Platform Web SDK은 쿠키를 사용하여 웹 사이트 방문자에게 [Adobe Experience Cloud ID(ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=ko)를 할당하여 사용자 행동을 추적합니다. 쿠키 수명에 대한 브라우저 제한을 해결하기 위해 자사 디바이스 ID(FPID)라고 하는 디바이스 식별자를 설정하고 관리할 수 있습니다.

>[!NOTE]
>
>자사 장치 ID 지원은 웹 SDK을 통해 Experience Platform Edge Network에 데이터를 전송할 때만 사용할 수 있습니다.

>[!IMPORTANT]
>
>자사 장치 ID는 Web SDK의 [타사 쿠키](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) 기능과 호환되지 않습니다. 자사 디바이스 ID 또는 타사 쿠키를 동시에 사용할 수는 없습니다.

## 전제 조건 {#prerequisites}

시작하기 전에 ECID 및 `identityMap`을(를) 포함하여 웹 SDK에서 ID 데이터가 작동하는 방식을 잘 알고 있는지 확인하십시오. 자세한 내용은 웹 SDK의 [ID 데이터에 대한 개요](./overview.md)를 참조하십시오.

## 자사 디바이스 ID 형식 요구 사항 {#formatting-requirements}

Edge Network은 [UUIDv4 형식](https://datatracker.ietf.org/doc/html/rfc4122)을 준수하는 ID만 허용합니다. UUIDv4 형식이 아닌 장치 ID는 거부됩니다.

* [!DNL UUIDs]은(는) 고유하고 임의적이며 충돌 가능성이 거의 없습니다.
* IP 주소 또는 기타 PII(개인 식별 정보)를 사용하여 [!DNL UUIDv4]을(를) 시드할 수 없습니다.
* [!DNL UUIDs]을(를) 생성할 라이브러리는 모든 프로그래밍 언어에 사용할 수 있습니다.

## 고유한 서버를 사용하여 [!DNL FPID] 쿠키 설정 {#set-cookie-server}

자체 서버를 통해 쿠키를 설정할 때 브라우저 정책으로 인해 쿠키가 제한되지 않도록 다양한 방법을 사용할 수 있습니다.

* 서버측 스크립팅 언어를 사용하여 쿠키 생성
* 사이트의 하위 도메인 또는 다른 끝점에 대한 API 요청에 대한 응답으로 쿠키를 설정합니다.
* [!DNL CMS]을(를) 사용하여 쿠키 생성
* [!DNL CDN]을(를) 사용하여 쿠키 생성

또한 항상 도메인의 `A` 레코드 아래에 FPID 쿠키를 설정해야 합니다.

>[!IMPORTANT]
>
>JavaScript의 `document.cookie` 메서드를 사용하여 설정된 쿠키는 쿠키 지속 시간을 제한하는 브라우저 정책으로부터 거의 보호되지 않습니다.

### 쿠키 설정 시기 {#when-to-set-cookie}

Edge Network에 요청하기 전에 [!DNL FPID] 쿠키를 설정하는 것이 좋습니다. 그러나 불가능한 시나리오에서는 여전히 기존 메서드를 사용하여 [!DNL ECID]이(가) 생성되고 쿠키가 존재하는 한 기본 식별자 역할을 합니다.

[!DNL ECID]이(가) 결국 브라우저 삭제 정책의 영향을 받지만 [!DNL FPID]은(는) 영향을 받지 않는다고 가정할 경우 [!DNL FPID]은(는) 다음 방문에서 기본 식별자가 되고 후속 방문마다 [!DNL ECID]을(를) 시드하는 데 사용됩니다.

### 쿠키 만료 설정 {#set-expiration}

[!DNL FPID] 기능을 구현할 때 쿠키의 만료를 설정하는 것은 신중하게 고려해야 합니다. 이를 결정할 때는 각 지역의 법률 및 정책과 함께 조직이 운영되는 국가 또는 지역을 고려해야 합니다.

이 결정의 일부로 회사 전체의 쿠키 설정 정책 또는 운영하는 각 로케일에서 사용자에 따라 달라지는 정책을 채택할 수 있습니다.

쿠키의 초기 만료에 대해 선택하는 설정에 관계없이 사이트를 새로 방문할 때마다 쿠키 만료를 확장하는 논리를 포함해야 합니다.

## 쿠키 플래그의 영향 {#cookie-flag-impact}

다양한 브라우저에서 쿠키가 처리되는 방식에 영향을 주는 다양한 쿠키 플래그가 있습니다.

* [&#39;HTTPOnly&#39;](#http-only)
* [&#39;보안&#39;](#secure)
* [&#39;SameSite&#39;](#same-site)

### `HTTPOnly` {#http-only}

`HTTPOnly` 플래그를 사용하여 설정된 쿠키는 클라이언트측 스크립트를 사용하여 액세스할 수 없습니다. 즉, [!DNL FPID]을(를) 설정할 때 `HTTPOnly` 플래그를 설정하는 경우 `identityMap`에 포함할 쿠키 값을 읽으려면 서버측 스크립팅 언어를 사용해야 합니다.

Edge Network에서 [!DNL FPID] 쿠키의 값을 읽도록 선택하는 경우 `HTTPOnly` 플래그를 설정하면 클라이언트측 스크립트가 해당 값에 액세스할 수 없지만 Edge Network의 쿠키 읽기 기능에 부정적인 영향을 주지 않습니다.

>[!NOTE]
>
>`HTTPOnly` 플래그를 사용하면 쿠키 수명을 제한할 수 있는 쿠키 정책에 영향을 주지 않습니다. 그러나 [!DNL FPID]의 값을 설정하고 읽을 때는 여전히 고려해야 할 사항입니다.

### `Secure` {#secure}

`Secure` 특성으로 설정된 쿠키는 [!DNL HTTPS] 프로토콜을 통해 암호화된 요청으로 서버로만 전송됩니다. 이 플래그를 사용하면 중간자 공격자가 쿠키의 값에 쉽게 액세스할 수 없게 됩니다. 가능하면 항상 `Secure` 플래그를 설정하는 것이 좋습니다.

### `SameSite` {#same-site}

`SameSite` 특성을 사용하면 서버가 사이트 간 요청을 통해 쿠키를 전송하는지 여부를 확인할 수 있습니다. 속성은 크로스 사이트 위조 공격으로부터 일부 보호를 제공합니다. 가능한 값은 `Strict`, `Lax` 및 `None`입니다. 조직에 적합한 설정을 결정하려면 내부 팀에 문의하십시오.

`SameSite` 특성이 지정되지 않은 경우 일부 브라우저의 기본 설정은 이제 `SameSite=Lax`입니다.

## 계층 {#id-hierarchy}

[!DNL ECID]과(와) [!DNL FPID]이(가) 모두 있으면 [!DNL ECID]이(가) 사용자를 식별하는 우선 순위를 갖습니다. 이렇게 하면 기존 [!DNL ECID]이(가) 브라우저 쿠키 저장소에 있는 경우 기본 식별자로 유지되며 기존 방문자 수가 영향을 받지 않습니다. 기존 사용자의 경우 [!DNL ECID]이(가) 만료되거나 브라우저 정책 또는 수동 프로세스의 결과로 삭제될 때까지 [!DNL FPID]이(가) 기본 ID가 되지 않습니다.

ID는 다음 순서로 우선 순위가 지정됩니다.

1. `identityMap`에 포함된 [!DNL ECID]
1. [!DNL ECID]이(가) 쿠키에 저장됨
1. `identityMap`에 포함된 [!DNL FPID]
1. [!DNL FPID]이(가) 쿠키에 저장됨


## 자사 디바이스 ID로 마이그레이션 {#migrating-to-fpid}

이전 구현에서 자사 디바이스 ID로 마이그레이션하는 경우 낮은 수준에서 전환이 어떻게 보이는지 시각화하기 어려울 수 있습니다.

이 프로세스를 설명하는 데 도움이 되도록 이전에 사이트를 방문한 고객이 포함된 시나리오와 [!DNL FPID] 마이그레이션이 Adobe 솔루션에서 해당 고객을 식별하는 방법에 미칠 영향을 고려하십시오.

![FPID로 마이그레이션한 후 방문 간에 고객의 ID 값이 어떻게 업데이트되는지 보여 주는 다이어그램](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>`ECID` 쿠키는 항상 `FPID`보다 우선 순위가 지정됩니다.

| ‍ | 설명 |
| --- | --- |
| 첫 방문 | [!DNL FPID] 쿠키 설정을 아직 시작하지 않았다고 가정해 보십시오. [AMCV 쿠키](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=ko#section-c55af54828dc4cce89f6118655d694c8)에 포함된 [!DNL ECID]은(는) 방문자를 식별하는 데 사용되는 식별자입니다. |
| 두 번째 방문 | [!DNL FPID] 솔루션의 롤아웃이 시작되었습니다. 기존 [!DNL ECID]이(가) 여전히 있으며 방문자 식별을 위한 기본 식별자로 유지됩니다. |
| 세 번째 방문 | 두 번째와 세 번째 방문 사이에 브라우저 정책으로 인해 [!DNL ECID]이(가) 삭제될 만큼 충분한 시간이 경과되었습니다. 그러나 [!DNL FPID]이(가) [!DNL DNS] [!DNL A] 레코드를 사용하여 설정되었으므로 [!DNL FPID]이(가) 유지됩니다. [!DNL FPID]은(는) 이제 기본 ID로 간주되며 최종 사용자 장치에 기록된 [!DNL ECID]을(를) 시드하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션의 새 방문자로 간주됩니다. |
| 네 번째 방문 | 세 번째와 네 번째 방문 사이에 브라우저 정책으로 인해 [!DNL ECID]이(가) 삭제될 만큼 충분한 시간이 경과되었습니다. 이전 방문과 마찬가지로 [!DNL FPID]은(는) 설정된 방식으로 인해 유지됩니다. 이번에는 이전 방문과 동일한 [!DNL ECID]이(가) 생성됩니다. 사용자는 Experience Platform 및 Experience Cloud 솔루션 전체에서 이전 방문과 동일한 사용자로 표시됩니다. |
| 다섯 번째 방문 | 네 번째와 다섯 번째 방문 사이에 최종 사용자는 브라우저의 모든 쿠키를 지웠습니다. 새 [!DNL FPID]이(가) 생성되고 새 [!DNL ECID] 만들기를 시드하는 데 사용됩니다. 이제 사용자는 Adobe Experience Platform 및 Experience Cloud 솔루션의 새 방문자로 간주됩니다. |

{style="table-layout:auto"}

## 자사 디바이스 ID(FPID) 사용 {#using-fpid}

자사 장치 ID([!DNL FPIDs])는 자사 쿠키를 사용하여 방문자를 추적합니다. 자사 쿠키는 DNS [!DNL CNAME] 또는 [!DNL JavaScript] 코드와 반대로 DNS [A 레코드](https://datatracker.ietf.org/doc/html/rfc1035)&#x200B;(IPv4의 경우) 또는 [AAAA 레코드](https://datatracker.ietf.org/doc/html/rfc3596)&#x200B;(IPv6의 경우)을 사용하는 서버를 사용하여 설정할 때 가장 효과적입니다.

>[!IMPORTANT]
>
>[!DNL A] 또는 [!DNL AAAA] 레코드는 쿠키 설정 및 추적에 대해서만 지원됩니다. 데이터 수집을 위한 기본 메서드는 [!DNL DNS CNAME]을(를) 통해 수행됩니다. [!DNL FPIDs]은(는) [!DNL A] 또는 [!DNL AAAA] 레코드를 사용하여 설정되었으며 [!DNL CNAME]을(를) 사용하여 Adobe으로 전송됩니다.
>
>[Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko#adobe-managed-certificate-program)도 자사 데이터 수집에 대해 지원됩니다.

[!DNL FPID] 쿠키가 설정되면 해당 값을 가져와 이벤트 데이터가 수집될 때 Adobe으로 보낼 수 있습니다. 수집된 [!DNL FPIDs]은(는) Adobe Experience Cloud 애플리케이션에서 기본 식별자인 [!DNL ECIDs]을(를) 생성하는 데 사용됩니다.

다음 두 가지 방법으로 [!DNL FPIDs]을(를) 사용할 수 있습니다.

* **[메서드 1](#setting-cookie-datastreams)**: 웹 SDK 호출에 대해 [!DNL CNAME]을(를) 구성하고 데이터 스트림 구성에 [!DNL FPID] 쿠키의 이름을 포함하십시오.
* **[메서드 2](#identityMap)**: ID 맵에 [!DNL FPID]을(를) 포함합니다. 자세한 내용은 이 문서의 아래쪽에서 `identityMap`[&#128279;](#identityMap)에서 FPID 사용 에 대한 섹션을 참조하십시오.

### 방법 1: 웹 SDK 호출에 대한 CNAME을 구성하고 데이터 스트림에서 자사 ID 쿠키를 설정합니다 {#setting-cookie-datastreams}

도메인에서 [!DNL FPID] 쿠키를 설정하려면 웹 SDK 호출에 대해 고유한 [!DNL CNAME]&#x200B;(표준 이름)을 구성한 다음 데이터 스트림 구성에서 [!DNL First Party ID Cookie] 기능을 활성화해야 합니다.

**1단계. 웹 SDK 배포 도메인에 대한 CNAME 구성**

DNS의 [!DNL CNAME] 레코드를 사용하면 한 도메인 이름에서 다른 도메인 이름으로 별칭을 만들 수 있습니다. 이렇게 하면 서드파티 서비스가 사용자 도메인의 일부인 것처럼 표시되어 쿠키를 자사 쿠키처럼 보이게 할 수 있습니다.

**예**

웹 사이트 `mywebsite.com`에서 Web SDK을 구현하는 것이 좋습니다. 웹 SDK이 데이터를 Edge Network으로 `edge.adobedc.net` 도메인으로 보냅니다.

| [!DNL CNAME] 없이 | [!DNL CNAME] 사용 |
|---------|----------|
| <ul><li>웹 사이트 `mywebsite.com`은(는) 웹 SDK 도메인 `edge.adobedc.net`을(를) 사용하여 Edge Network에 데이터를 보냅니다.</li><li>`edge.adobedc.net`에서 설정한 쿠키는 `mywebsite.com` 도메인에서 가져오지 않으므로 타사 쿠키로 간주됩니다. 사용자 브라우저에 따라 서드파티 쿠키가 차단될 수 있으며, 귀하의 데이터가 Edge Network에 도달하지 않습니다.</li></ul> | <ul><li>`metrics.mywebsite.com`과(와) 같이 웹 SDK을 배포하는 하위 도메인을 만듭니다.</li><li>`metrics.mywebsite.com`이(가) `edge.adobedc.net`을(를) 가리키도록 DNS 시스템에서 [!DNL CNAME] 레코드를 설정했습니다.</li><li>웹 사이트에서 `metrics.mywebsite.com`을(를) 통해 브라우저에 쿠키를 설정하면 `edge.adobedc.net`(타사) 대신 `mywebsite.com`(자사)에서 쿠키가 제공되는 것으로 표시됩니다. 이렇게 하면 자사 ID 쿠키가 차단될 가능성이 줄어들어 보다 정확한 데이터 수집이 보장됩니다.</li></ul> |

[!DNL CNAME]을(를) 사용하여 자사 데이터 수집을 사용하도록 설정하면 데이터 수집 끝점에 대한 요청 시 도메인에 대한 모든 쿠키가 전송됩니다.

이 기능을 사용하려면 특정 하위 도메인 대신 도메인의 최상위 수준에서 [!DNL FPID] 쿠키를 설정해야 합니다. 하위 도메인에서 설정하면 쿠키 값이 Edge Network으로 전송되지 않으며 [!DNL FPID] 솔루션이 의도한 대로 작동하지 않습니다.

>[!IMPORTANT]
>
>이 기능을 사용하려면 [자사 데이터 수집](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko)을 사용하도록 설정해야 합니다.

**2단계. 데이터 스트림에 대해**&#x200B;[!UICONTROL &#x200B;자사 ID 쿠키&#x200B;]&#x200B;**기능을 사용하도록 설정**

CNAME을 구성한 후에는 데이터 스트림에 대해 **[!UICONTROL 자사 ID 쿠키]** 옵션을 활성화해야 합니다. 이 설정은 Edge Network에 [ID 맵](#identityMap)에서 이 값을 조회하는 대신 자사 장치 ID를 조회할 때 지정된 쿠키를 참조하도록 지시합니다.

데이터스트림을 설정하는 방법에 대한 자세한 내용은 [데이터스트림 구성 설명서](../../datastreams/configure.md#advanced-options)를 참조하세요.

Adobe Experience Cloud 사용 방법에 대한 자세한 내용은 [자사 쿠키](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko-KR)에 대한 설명서를 참조하십시오.

![자사 ID 쿠키 설정을 강조 표시하는 데이터 스트림 구성을 표시하는 플랫폼 UI 이미지](../assets/first-party-id-datastreams.png)

이 설정을 활성화할 때 [!DNL FPID]이(가) 저장될 쿠키의 이름을 제공해야 합니다.

>[!NOTE]
>
>자사 ID를 사용하는 경우 타사 ID 동기화를 수행할 수 없습니다. 타사 ID 동기화는 [!DNL Visitor ID] 서비스와 해당 서비스에서 생성한 `UUID`을(를) 사용합니다. 자사 ID 기능을 사용하는 경우 [!DNL Visitor ID] 서비스를 사용하지 않고 [!DNL ECID]이(가) 생성되므로 타사 ID를 동기화할 수 없습니다.
><br> 자사 ID를 사용하는 경우 Audience Manager 파트너 ID 동기화가 대부분 `UUIDs` 또는 `DIDs`을(를) 기반으로 하는 경우 파트너 플랫폼에서 활성화되도록 타깃팅된 [Audience Manager](https://experienceleague.adobe.com/ko/docs/audience-manager) 기능이 지원되지 않습니다. 자사 ID에서 파생된 [!DNL ECID]이(가) `UUID`에 연결되어 있지 않으므로 주소를 지정할 수 없습니다.

## 방법 2: `identityMap`에서 FPID 사용 {#identityMap}

[!DNL FPID]을(를) 자신의 쿠키에 저장하는 대신 ID 맵을 통해 [!DNL FPID]을(를) Edge Network으로 보낼 수 있습니다.

다음은 `identityMap`에서 [!DNL FPID]을(를) 설정하는 방법의 예입니다.

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

다른 ID 형식과 마찬가지로 `identityMap` 내에 다른 ID와 함께 [!DNL FPID]을(를) 포함할 수 있습니다. 다음은 인증된 [!DNL CRM ID]에 포함된 [!DNL FPID]의 예입니다.

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
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

자사 데이터 수집이 활성화될 때 Edge Network에서 읽는 쿠키에 [!DNL FPID]이(가) 포함되어 있으면 인증된 [!DNL CRM ID]만 캡처해야 합니다.

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

다음 `identityMap`은(는) [!DNL FPID]에 대한 `primary` 표시기가 없으므로 Edge Network에서 오류 응답을 생성합니다. `identityMap`에 있는 ID 중 적어도 하나는 `primary`(으)로 표시되어야 합니다.

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

## FAQ {#faq}

다음은 자사 디바이스 ID에 대한 FAQ 응답 목록입니다.

### ID 시드는 단순히 ID를 생성하는 것과 어떻게 다릅니까?

시드의 개념은 Adobe Experience Cloud으로 전달된 [!DNL FPID]이(가) 결정론적 알고리즘을 사용하여 [!DNL ECID]&#x200B;(으)로 변환된다는 점에서 독특합니다. 동일한 [!DNL FPID]이(가) Edge Network으로 전송될 때마다 동일한 [!DNL ECID]이(가) [!DNL FPID]에서 시드됩니다.

### 자사 디바이스 ID는 언제 생성해야 합니까?

잠재적인 방문자 인플레이션을 줄이려면 웹 SDK을 사용하여 첫 번째 요청을 수행하기 전에 [!DNL FPID]을(를) 생성해야 합니다. 그러나 이렇게 할 수 없는 경우 해당 사용자에 대해 [!DNL ECID]이(가) 계속 생성되며 기본 식별자로 사용됩니다. 생성된 [!DNL FPID]은(는) [!DNL ECID]이(가) 더 이상 존재하지 않을 때까지 기본 식별자가 되지 않습니다.

### 자사 디바이스 ID를 지원하는 데이터 수집 방법

현재 Web SDK만 자사 디바이스 ID를 지원합니다.

### 자사 디바이스 ID가 플랫폼 또는 Experience Cloud 솔루션에 저장됩니까?

[!DNL FPID]을(를) 사용하여 [!DNL ECID]을(를) 시드하면 `identityMap`에서 삭제되고 생성된 [!DNL ECID]&#x200B;(으)로 대체됩니다. [!DNL FPID]이(가) Adobe Experience Platform 또는 Experience Cloud 솔루션에 저장되지 않았습니다.
