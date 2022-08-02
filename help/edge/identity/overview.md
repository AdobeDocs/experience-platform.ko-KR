---
title: Platform Web SDK의 ID 데이터
description: Adobe Experience Platform Web SDK를 사용하여 ECID(Adobe Experience Cloud ID)를 검색하고 관리하는 방법을 알아봅니다.
keywords: ID;자사 ID;ID 서비스;타사 ID;ID 마이그레이션;방문자 ID;타사 ID;타사 ID;MigrationEnabled;getIdentity;ID 동기화;syncIdentity;sendEvent;identityMap;기본;ecid;ID 네임스페이스;네임스페이스 ID;인증 상태;해시Enabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: d6aed404828d06bf223f348dd97960652b05933a
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 1%

---

# Platform Web SDK의 ID 데이터

Adobe Experience Platform 웹 SDK는 다음을 활용합니다 [Adobe Experience Cloud ID(ECID)](../../identity-service/ecid.md) 방문자 행동을 추적하려면 ECID를 사용하면 각 장치에 여러 세션 간에 지속될 수 있는 고유한 식별자가 있는지 확인하여 웹 세션 중 및 여러 세션에서 발생하는 모든 히트를 특정 장치에 연결할 수 있습니다.

이 문서에서는 Platform Web SDK를 사용하여 ECID를 관리하는 방법에 대한 개요를 제공합니다.

## SDK를 사용하여 ECID 추적

Platform Web SDK는 쿠키를 사용하여 ECID를 할당하고 추적하며, 이러한 쿠키를 생성하는 방법을 구성하는 데 사용할 수 있는 여러 가지 방법이 있습니다.

새 사용자가 웹 사이트에 도달하면 Adobe Experience Cloud Identity 서비스는 해당 사용자에 대한 장치 ID 쿠키 설정을 시도합니다. 처음 방문하는 사용자의 경우 ECID가 생성되고 Adobe Experience Platform Edge Network의 첫 번째 응답에서 반환됩니다. 재방문자의 경우 ECID가 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 쿠키 를 추가하고 Edge Network에 의해 페이로드에 추가됩니다.

ECID가 포함된 쿠키가 설정되면 웹 SDK에서 생성한 각 후속 요청에는 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 쿠키 .

장치 식별을 위해 쿠키를 사용하는 경우 Edge Network와 상호 작용하는 두 가지 옵션이 있습니다.

1. Edge Network 도메인에 직접 데이터 전송 `adobedc.net`. 이 메서드를 라고 합니다 [타사 데이터 수집](#third-party).
1. 을 가리키는 고유한 도메인에 CNAME을 만듭니다 `adobedc.net`. 이 메서드를 라고 합니다 [자사 데이터 수집](#first-party).

아래 섹션에 설명된 대로, 사용하도록 선택하는 데이터 수집 방법은 브라우저 전체의 쿠키 라이프타임에 직접적인 영향을 줍니다.

### 타사 데이터 수집 {#third-party}

타사 데이터 수집에는 Edge Network 도메인에 직접 데이터를 전송하는 작업이 포함됩니다 `adobedc.net`.

최근 몇 년간 웹 브라우저는 타사에서 설정한 쿠키를 처리하는 데 점점 더 제한을 받고 있습니다. 일부 브라우저는 기본적으로 타사 쿠키를 차단합니다. 타사 쿠키를 사용하여 사이트 방문자를 식별하는 경우, 해당 쿠키의 수명은 대부분 자사 쿠키를 대신 사용하여 사용할 수 있는 것보다 거의 항상 짧습니다. 경우에 따라 타사 쿠키가 7일 이내에 만료됩니다.

또한 타사 데이터 수집을 사용하는 경우 일부 광고 차단기는 트래픽을 모두 Adobe 데이터 수집 종단점으로 제한합니다.

### 자사 데이터 수집 {#first-party}

자사 데이터 수집에는 을 가리키는 고유한 도메인의 CNAME을 통해 쿠키를 설정하는 작업이 포함됩니다 `adobedc.net`.

브라우저가 사이트 소유 종단점에 의해 설정된 쿠키와 유사한 방식으로 CNAME 종단점에 의해 설정된 쿠키를 오래 처리했지만 브라우저에 의해 구현된 최근 변경 사항은 CNAME 쿠키를 처리하는 방법에 대한 차이를 만들었습니다. 현재 자사 CNAME 쿠키를 기본적으로 차단하는 브라우저는 없지만, 일부 브라우저는 CNAME을 사용하여 설정된 쿠키의 수명을 7일로 제한합니다.

### 쿠키 수명은 Adobe Experience Cloud 애플리케이션에 미치는 영향 {#lifespans}

퍼스트 파티 또는 타사 데이터 수집을 선택하는지 여부에 관계없이 쿠키가 지속될 수 있는 시간은 Adobe Analytics 및 Customer Journey Analytics의 방문자 수에 직접적인 영향을 줍니다. 또한 사이트에서 Adobe Target 또는 Offer decisioning을 사용할 때 최종 사용자는 일관되지 않은 개인화 경험을 경험할 수 있습니다.

예를 들어, 사용자가 지난 7일 동안 3번 본 경우 홈 페이지로 모든 항목을 홍보할 개인화 경험을 만든 경우를 생각해 보겠습니다.

최종 사용자가 일주일에 3회 방문한 다음 7일 동안 사이트를 다시 방문하지 않는 경우, 쿠키를 브라우저 정책에 의해 삭제되었을 수 있으므로 해당 사용은 사이트를 방문할 때 사용한 브라우저에 따라 사이트 재방문 시 새 사용자로 간주될 수 있습니다. 이러한 경우 7일 전에 사이트를 방문한 방문자가 있더라도 Analytics 도구에서 방문자를 새 사용자로 취급합니다. 또한 사용자를 위한 경험을 개인화하기 위한 모든 노력이 다시 시작됩니다.

### 자사 장치 ID

쿠키 수명 효과가 위에 설명된 대로 반영되도록, 대신 고유한 장치 식별자를 설정하고 관리하도록 선택할 수 있습니다. 다음 안내서를 참조하십시오. [자사 장치 ID](./first-party-device-ids.md) 추가 정보.

## 현재 사용자에 대한 ECID 및 지역 검색

현재 방문자에 대한 고유 ECID를 검색하려면 `getIdentity` 명령. ECID가 아직 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다. `getIdentity` 방문자에 대한 지역 ID도 반환합니다.

>[!NOTE]
>
>이 메서드는 일반적으로 를 읽어야 하는 사용자 지정 솔루션에서 사용됩니다 [!DNL Experience Cloud] Adobe Audience Manager에 대한 위치 힌트가 필요합니다. 표준 구현에서는 사용되지 않습니다.

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

XDM 사용 [`identityMap` 필드](../../xdm/schema/composition.md#identityMap), 여러 ID를 사용하여 장치/사용자를 식별하고, 인증 상태를 설정하고, 기본 ID로 간주되는 식별자를 결정할 수 있습니다. 로 설정된 식별자가 없는 경우 `primary`, 기본 기본값은 입니다. `ECID`.

`identityMap` 필드는 `sentEvent` 명령.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

내의 각 속성 `identityMap` 특정 ID에 속하는 ID를 나타냅니다 [id 네임스페이스](../../identity-service/namespaces.md). 속성 이름은 ID 네임스페이스 심벌이어야 합니다. 이 심볼은 &quot; 아래에 Adobe Experience Platform 사용자 인터페이스에 나열된 것을 찾을 수 있습니다.[!UICONTROL ID]&quot;. 속성 값은 해당 ID 네임스페이스와 관련된 ID 배열이어야 합니다.

>[!IMPORTANT]
>
>에서 전달된 네임스페이스 ID입니다 `identityMap` 는 대/소문자를 구분합니다. 불완전한 데이터 수집을 방지하려면 올바른 네임스페이스 ID를 사용해야 합니다.

ID 배열의 각 ID 객체에는 다음 속성이 포함됩니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `id` | 문자열 | **(필수)** 지정된 네임스페이스에 대해 설정할 ID입니다. |
| `authenticationState` | 문자열 | **(필수)** ID의 인증 상태입니다. 가능한 값은 다음과 같습니다 `ambiguous`, `authenticated`, 및 `loggedOut`. |
| `primary` | 부울 | 이 ID를 프로필에서 기본 조각으로 사용해야 하는지 여부를 결정합니다. 기본적으로 ECID는 사용자의 기본 식별자로 설정됩니다. 생략하면 이 값의 기본값은 입니다. `false`. |

## 방문자 API에서 ECID로 마이그레이션

방문자 API를 사용하여에서 마이그레이션할 때 기존 AMCV 쿠키를 마이그레이션할 수도 있습니다. ECID 마이그레이션을 활성화하려면 `idMigrationEnabled` 매개 변수를 구성합니다. ID 마이그레이션을 통해 다음과 같은 사용 사례를 사용할 수 있습니다.

* 도메인의 일부 페이지가 방문자 API를 사용하고 있고 다른 페이지가 이 SDK를 사용하는 경우 이 경우 SDK는 기존 AMCV 쿠키를 읽고 기존 ECID를 사용하여 새 쿠키를 기록합니다. 또한, SDK는 SDK를 사용하여 구현된 페이지에서 ECID를 처음 가져오는 경우 방문자 API를 사용하여 구현된 후속 페이지에 동일한 ECID가 있도록 AMCV 쿠키를 기록합니다.
* 방문자 API도 있는 페이지에서 Adobe Experience Platform Web SDK를 설정할 때. 이 경우 AMCV 쿠키가 설정되지 않은 경우 SDK는 페이지에서 방문자 API를 찾아 ECID를 가져오도록 호출합니다.
* 전체 사이트에서 Adobe Experience Platform Web SDK를 사용하고 방문자 API가 없는 경우 반환 방문자 정보를 보존하도록 ECID를 마이그레이션하는 것이 유용합니다. SDK가 배포되면 `idMigrationEnabled` 대부분의 방문자 쿠키가 마이그레이션되도록 일정 기간 동안 설정을 해제할 수 있습니다.

### 마이그레이션을 위한 트레이트 업데이트

XDM 형식 데이터를 Audience Manager으로 보낼 때 마이그레이션 시 이 데이터를 신호로 변환해야 합니다. XDM에서 제공하는 새 키를 반영하도록 트레이트를 업데이트해야 합니다. 이 프로세스는 [BAAAM 도구](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) 해당 Audience Manager이 생성되었습니다.

## 이벤트 전달에서 사용

현재 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 사용 및 사용 `appmeasurement.js` 및 `visitor.js`로 설정되면 이벤트 전달 기능을 활성화할 수 있으며 이로 인해 문제가 발생하지 않습니다. 백 엔드에서 Adobe은 모든 AAM 세그먼트를 가져와 Analytics 호출에 추가합니다. Analytics에 대한 호출에 이러한 세그먼트가 포함되어 있으면 Analytics는 Audience Manager을 호출하여 데이터를 전달하지 않으므로 이중 데이터 수집은 없습니다. 또한 동일한 세그먼테이션 종단점이 백엔드에서 호출되므로 웹 SDK를 사용할 때 위치 힌트가 필요하지 않습니다.
