---
title: Platform Web SDK의 ID 데이터
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Experience Cloud ID(ECID)를 검색하고 관리하는 방법에 대해 알아봅니다.
keywords: ID;자사 ID;ID 서비스;타사 ID;ID 마이그레이션;방문자 ID;타사 ID;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;동기화 ID;syncIdentity;sendEvent;identityMap;primary;ecid;ID 네임스페이스;네임스페이스 ID;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 1%

---

# Platform Web SDK의 ID 데이터

Adobe Experience Platform Web SDK는 [Adobe Experience Cloud ID (ECID)](../../identity-service/ecid.md) 방문자 행동을 추적합니다. ECID를 사용하면 각 디바이스에 여러 세션에서 지속될 수 있는 고유 식별자가 있는지 확인하여 웹 세션 도중 및 여러 세션에서 발생한 모든 히트를 특정 디바이스에 연결할 수 있습니다.

이 문서에서는 Platform Web SDK를 사용하여 ECID를 관리하는 방법에 대한 개요를 제공합니다.

## SDK를 사용한 ECID 추적

Platform Web SDK는 쿠키를 사용하여 ECID를 할당하고 추적하며, 이러한 쿠키가 생성되는 방식을 구성하는 데 사용 가능한 여러 메서드를 사용합니다.

새 사용자가 웹 사이트에 도달하면 Adobe Experience Cloud Identity Service에서 해당 사용자에 대한 장치 ID 쿠키 설정을 시도합니다. 처음 방문하는 사용자의 경우 ECID가 생성되고 Adobe Experience Platform Edge Network의 첫 번째 응답에서 반환됩니다. 반복 방문자의 경우 ECID가에서 검색됩니다. `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie를 반환하고 Edge Network에서 페이로드에 추가했습니다.

ECID가 포함된 쿠키가 설정되면 Web SDK에서 생성된 각 후속 요청에에 인코딩된 ECID가 포함됩니다. `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 쿠키.

디바이스 식별을 위해 쿠키를 사용하는 경우 Edge Network와 상호 작용하는 두 가지 옵션이 있습니다.

1. Edge Network 도메인으로 직접 데이터 보내기 `adobedc.net`. 이 메서드를 라고 합니다. [타사 데이터 수집](#third-party).
1. 을(를) 가리키는 자체 도메인에 CNAME을 만듭니다 `adobedc.net`. 이 메서드를 라고 합니다. [자사 데이터 수집](#first-party).

아래 섹션에 설명된 대로 사용하도록 선택하는 데이터 수집 방법은 전체 브라우저에서 쿠키 수명에 직접적인 영향을 줍니다.

### 서드파티 데이터 수집 {#third-party}

타사 데이터 수집에는 Edge Network 도메인으로 직접 데이터를 전송하는 작업이 포함됩니다 `adobedc.net`.

최근 몇 년 동안 웹 브라우저는 제3자가 설정한 쿠키를 처리하는 데 점점 더 제한을 받고 있습니다. 일부 브라우저는 기본적으로 서드파티 쿠키를 차단합니다. 서드파티 쿠키를 사용하여 사이트 방문자를 식별하는 경우, 이러한 쿠키의 수명은 거의 항상 자사 쿠키를 대신 사용하여 사용할 수 있는 수명보다 짧습니다. 경우에 따라 서드파티 쿠키가 7일 안에 만료됩니다.

또한 서드파티 데이터 수집을 사용하는 경우 일부 광고 차단기는 트래픽을 제한하여 데이터 수집 엔드포인트를 완전히 Adobe 합니다.

### 자사 데이터 수집 {#first-party}

자사 데이터 수집에는 를 가리키는 자체 도메인에서 CNAME을 통해 쿠키를 설정하는 작업이 포함됩니다 `adobedc.net`.

브라우저는 오랫동안 사이트 소유 엔드포인트에서 설정한 쿠키와 유사한 방식으로 CNAME 엔드포인트에서 설정한 쿠키를 처리했지만, 브라우저에 의해 구현된 최근 변경 사항은 CNAME 쿠키가 처리되는 방법에서 차이를 만들었습니다. 현재 기본적으로 자사 CNAME 쿠키를 차단하는 브라우저는 없지만, 일부 브라우저에서는 CNAME을 사용하여 설정된 쿠키 수명을 7일로 제한합니다.

### 쿠키 수명이 Adobe Experience Cloud 애플리케이션에 미치는 영향 {#lifespans}

자사 데이터 수집 또는 타사 데이터 수집 선택 여부에 관계없이 쿠키가 지속될 수 있는 시간은 Adobe Analytics 및 Customer Journey Analytics의 방문자 수에 직접적인 영향을 줍니다. 또한 사이트에서 Adobe Target 또는 Offer decisioning을 사용할 때 최종 사용자가 일관되지 않은 개인화 경험을 경험할 수 있습니다.

예를 들어 사용자가 지난 7일 동안 항목을 3번 본 경우 항목을 홈 페이지로 홍보하는 개인화 경험을 만든 상황을 생각해 보겠습니다.

최종 사용자가 일주일에 세 번 사이트를 방문한 다음 7일 동안 사이트로 돌아오지 않는 경우, 해당 쿠키가 브라우저 정책(사이트를 방문했을 때 사용 중인 브라우저에 따라)에 의해 삭제되었을 수 있으므로 해당 사용자는 사이트로 돌아올 때 새 사용자로 간주될 수 있습니다. 이 경우 Analytics 도구는 방문자가 7일 조금 전에 사이트를 방문했더라도 새로운 사용자로 취급합니다. 또한 사용자를 위해 경험을 개인화하려는 모든 노력이 다시 시작됩니다.

### 자사 디바이스 ID

위에 설명된 대로 쿠키 수명의 효과를 고려하기 위해 대신 자체 디바이스 식별자를 설정하고 관리하도록 선택할 수 있습니다. 다음 안내서를 참조하십시오 [자사 디바이스 ID](./first-party-device-ids.md) 추가 정보.

## 현재 사용자의 ECID 및 영역 검색

현재 방문자에 대한 고유한 ECID를 검색하려면 `getIdentity` 명령입니다. 아직 ECID가 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다. `getIdentity` 은 방문자에 대한 지역 ID도 반환합니다.

>[!NOTE]
>
>이 메서드는 일반적으로 를 읽어야 하는 사용자 지정 솔루션에 사용됩니다. [!DNL Experience Cloud] ID 또는 Adobe Audience Manager에 대한 위치 힌트가 필요합니다. 표준 구현에서는 사용되지 않습니다.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## 사용 `identityMap`

XDM 사용 [`identityMap` 필드](../../xdm/schema/composition.md#identityMap), 여러 id를 사용하여 장치/사용자를 식별하고, 인증 상태를 설정하고, 기본 id로 간주되는 식별자를 결정할 수 있습니다. 로 설정된 식별자가 없는 경우 `primary`, 기본 기본값은 입니다. `ECID`.

`identityMap` 필드는 다음을 사용하여 업데이트됩니다 `sentEvent` 명령입니다.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe은 다음과 같이 개인을 나타내는 네임스페이스를 보낼 것을 권장합니다. `CRMID`를 기본 ID로 사용하십시오.


내의 각 속성 `identityMap` 특정 항목에 속한 id를 나타냅니다. [id 네임스페이스](../../identity-service/namespaces.md). 속성 이름은 ID 네임스페이스 기호여야 하며 아래 Adobe Experience Platform 사용자 인터페이스에 나열되어 있습니다.[!UICONTROL ID]&quot;. 속성 값은 해당 ID 네임스페이스와 관련된 ID 배열이어야 합니다.

>[!IMPORTANT]
>
>에 전달된 네임스페이스 ID `identityMap` 대/소문자를 구분합니다. 데이터 수집이 불완전하지 않도록 올바른 네임스페이스 ID를 사용해야 합니다.

ID 배열의 각 ID 개체에는 다음 속성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `id` | 문자열 | **(필수)** 해당 네임스페이스에 대해 설정할 ID입니다. |
| `authenticationState` | 문자열 | **(필수)** ID의 인증 상태입니다. 가능한 값은 다음과 같습니다 `ambiguous`, `authenticated`, 및 `loggedOut`. |
| `primary` | 부울 | 이 ID를 프로필의 기본 조각으로 사용할지 여부를 결정합니다. 기본적으로 ECID는 사용자의 기본 식별자로 설정됩니다. 생략하면 이 값의 기본값은 입니다. `false`. |

사용 `identityMap` 디바이스 또는 사용자를 식별하는 필드는 을 사용하는 것과 동일한 결과로 이어집니다. [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=ko-KR) 메서드의 [!DNL ID Service API]. 다음을 참조하십시오. [ID 서비스 API 설명서](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) 을 참조하십시오.

## 방문자 API에서 ECID로 마이그레이션

방문자 API를 사용하여에서 마이그레이션할 때 기존 AMCV 쿠키를 마이그레이션할 수도 있습니다. ECID 마이그레이션을 사용하려면 `idMigrationEnabled` 매개 변수를 채우는 방법을 설명합니다. ID 마이그레이션을 통해 다음과 같은 사용 사례를 사용할 수 있습니다.

* 도메인의 일부 페이지가 방문자 API를 사용하고 다른 페이지가 이 SDK를 사용하는 경우. 이 경우를 지원하기 위해 SDK는 기존 AMCV 쿠키를 읽고 기존 ECID로 새 쿠키를 기록합니다. 또한 SDK는 AMCV 쿠키를 기록하여 SDK로 계측된 페이지에서 ECID를 먼저 획득하는 경우 방문자 API로 계측된 후속 페이지가 동일한 ECID를 갖도록 합니다.
* 방문자 API가 있는 페이지에서 Adobe Experience Platform Web SDK가 설정된 경우. 이 경우를 지원하기 위해 AMCV 쿠키가 설정되지 않은 경우 SDK는 페이지에서 방문자 API를 찾아 호출하여 ECID를 가져옵니다.
* 전체 사이트에서 Adobe Experience Platform Web SDK를 사용하고 있고 방문자 API가 없는 경우, 반환 방문자 정보가 유지되도록 ECID를 마이그레이션하는 것이 유용합니다. SDK가 로 배포된 후 `idMigrationEnabled` 일정 기간 동안 대부분의 방문자 쿠키가 마이그레이션되도록 설정을 끌 수 있습니다.

### 마이그레이션할 트레이트 업데이트

XDM 형식의 데이터를 Audience Manager으로 전송하면 마이그레이션할 때 이 데이터를 신호로 변환해야 합니다. XDM에서 제공하는 새 키를 반영하도록 트레이트를 업데이트해야 합니다. 이 프로세스는 를 사용하여 쉽게 만들 수 있습니다. [BAAAM 도구](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) 해당 Audience Manager이 생성되었습니다.

## 이벤트 전달에 사용

현재 다음을 보유한 경우: [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 활성화되었으며 사용 중 `appmeasurement.js` 및 `visitor.js`, 이벤트 전달 기능을 활성화 상태로 둘 수 있으며, 이렇게 해도 문제가 발생하지 않습니다. 백 엔드에서 Adobe은 모든 AAM 세그먼트를 가져와 Analytics 호출에 추가합니다. Analytics에 대한 호출에 이러한 세그먼트가 포함되어 있는 경우 Analytics는 Audience Manager을 호출하여 데이터를 전달하지 않으므로 이중 데이터 수집은 없습니다. 동일한 세그멘테이션 종단점이 백엔드에서 호출되므로 Web SDK를 사용할 때도 위치 힌트가 필요하지 않습니다.
