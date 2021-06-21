---
title: Adobe Experience Platform Web SDK를 사용하여 Experience Cloud ID 검색
description: Adobe Experience Platform Web SDK를 사용하여 ECID(Adobe Experience Cloud ID)를 검색하는 방법을 알아봅니다.
seo-description: Adobe Experience Cloud ID를 가져오는 방법을 알아봅니다.
keywords: ID;자사 ID;ID 서비스;타사 ID;ID 마이그레이션;방문자 ID;타사 ID;타사 ID;MigrationEnabled;getIdentity;ID 동기화;syncIdentity;sendEvent;identityMap;기본;ecid;ID 네임스페이스;네임스페이스 ID;인증 상태;해시Enabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: d753cfca6f518dfe2cafa1cb30ad26bd0b591c54
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 6%

---

# Adobe Experience Cloud ID

Adobe Experience Platform 웹 SDK는 [Adobe ID 서비스](../../identity-service/ecid.md)를 활용합니다. 이렇게 하면 각 장치에 페이지 간 활동을 함께 연결할 수 있도록 장치에서 지속되는 고유 식별자가 있습니다.

## 자사 ID

[!DNL Identity Service]은(는) 자사 도메인의 쿠키에 ID를 저장합니다. [!DNL Identity Service] 은 도메인에서 HTTP 헤더를 사용하여 쿠키를 설정하려고 시도합니다. 실패하면 [!DNL Identity Service]이(가) JavaScript를 사용하여 쿠키를 설정하는 것으로 돌아갑니다. [Edge 도메인 구성](../fundamentals/configuring-the-sdk.md#edgeConfigId)에 대한 CNAME을 설정하는 것이 좋습니다.

Platform Web SDK에서 오는 모든 히트에는 Edge 네트워크의 ID 서비스에 의해 추가된 ECID가 있습니다. 처음 방문하는 사용자의 경우 ECID가 생성되고 페이로드에 추가됩니다. 반복 방문자의 경우 ECID가 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 쿠키에서 검색되고 페이로드에 추가됩니다.

ECID는 `xdm`의 `identityMap` 필드 아래에 추가됩니다. 브라우저의 개발 도구를 사용하여 유형이 있는 페이로드 아래의 응답에서 ECID를 볼 수 있습니다.`identity:result` 이지만 요청에 ECID가 표시되지 않습니다.

CNAME 구현을 통해 내 도메인과 일치시킬 수 있도록 Adobe가 사용하는 컬렉션 도메인을 맞춤화할 수 있습니다. 이를 통해 Adobe는 JavaScript를 사용하는 클라이언트측 대신 서버측에서 자사 쿠키를 설정할 수 있습니다. 이전에는 이러한 서버측 자사 쿠키가 Safari 브라우저에서 Apple의 ITP(Intelligent Tracking Prevention) 정책에 따라 적용되는 제한을 받지 않았습니다. 그러나 2020년 11월에 Apple은 이러한 제한 사항이 CNAME을 통해 설정된 쿠키에도 적용되도록 정책을 업데이트했습니다. 현재, CNAME으로 서버 측에 설정된 쿠키와 JavaScript로 클라이언트측에 설정된 쿠키는 모두 ITP에서 7일 또는 24시간 만료로 제한됩니다. ITP 정책에 대한 자세한 내용은 [추적 방지](https://webkit.org/tracking-prevention/#intelligent-tracking-prevention-itp)에 있는 이 Apple 문서를 참조하십시오.

CNAME 구현은 쿠키 수명 측면에서 이점이 없지만 광고 차단기 및 덜 일반적인 브라우저로 데이터가 추적기로 분류되는 도메인으로 전송되지 않도록 하는 다른 이점이 있습니다. 이러한 경우 CNAME을 사용하면 이러한 도구를 사용하는 사용자에게 데이터 수집이 중단되지 않을 수 있습니다.

## 타사 ID

[!DNL Identity Service]은(는) ID를 타사 도메인(demdex.net)과 동기화하여 사이트 간에 추적을 활성화할 수 있습니다. 이 기능이 활성화되면 방문자에 대한 첫 번째 요청(예: ECID가 없는 사람)이 demdex.net에 수행됩니다. 이 작업은 Chrome과 같이 이 기능을 허용하는 브라우저에서만 수행되며 구성의 `thirdPartyCookiesEnabled` 매개 변수로 제어됩니다. 이 기능을 모두 비활성화하려면 `thirdPartyCookiesEnabled`을 false로 설정하십시오.

## ID 마이그레이션

방문자 API를 사용하여에서 마이그레이션할 때 기존 AMCV 쿠키를 마이그레이션할 수도 있습니다. ECID 마이그레이션을 활성화하려면 구성에서 `idMigrationEnabled` 매개 변수를 설정합니다. ID 마이그레이션을 통해 다음과 같은 사용 사례를 사용할 수 있습니다.

* 도메인의 일부 페이지가 방문자 API를 사용하고 있고 다른 페이지가 이 SDK를 사용하는 경우 이 경우 SDK는 기존 AMCV 쿠키를 읽고 기존 ECID를 사용하여 새 쿠키를 기록합니다. 또한, SDK는 SDK를 사용하여 구현된 페이지에서 ECID를 처음 가져오는 경우 방문자 API를 사용하여 구현된 후속 페이지에 동일한 ECID가 있도록 AMCV 쿠키를 기록합니다.
* 방문자 API도 있는 페이지에서 Adobe Experience Platform Web SDK를 설정할 때. 이 경우 AMCV 쿠키가 설정되지 않은 경우 SDK는 페이지에서 방문자 API를 찾아 ECID를 가져오도록 호출합니다.
* 전체 사이트에서 Adobe Experience Platform Web SDK를 사용하고 방문자 API가 없는 경우 반환 방문자 정보를 보존하도록 ECID를 마이그레이션하는 것이 유용합니다. SDK가 일정 기간 `idMigrationEnabled`과 함께 배포되어 대부분의 방문자 쿠키가 마이그레이션되면 설정을 해제할 수 있습니다.

## 마이그레이션을 위한 트레이트 업데이트

XDM 형식 데이터를 Audience Manager으로 보낼 때 마이그레이션 시 이 데이터를 신호로 변환해야 합니다. XDM에서 제공하는 새 키를 반영하도록 트레이트를 업데이트해야 합니다. 이 프로세스는 Audience Manager이 만든 [BAAAM 도구](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)를 사용하여 보다 쉽게 수행할 수 있습니다.

## 서버 측 전달

현재 서버 측 전달을 활성화하고 `appmeasurement.js`을 사용 중인 경우. 및 `visitor.js` 서버 측 전달 기능을 활성화한 상태로 둘 수 있으며 이로 인해 문제가 발생하지 않습니다. 백엔드에서 Adobe은 모든 AAM 세그먼트를 가져와 Analytics 호출에 추가합니다. Analytics에 대한 호출에 이러한 세그먼트가 포함되어 있으면 Analytics는 Audience Manager을 호출하여 데이터를 전달하지 않으므로 이중 데이터 수집은 없습니다. 또한 동일한 세그먼테이션 종단점이 백엔드에서 호출되므로 웹 SDK를 사용할 때 위치 힌트가 필요하지 않습니다.

## 방문자 ID 및 지역 ID 검색

고유 방문자 ID를 사용하려면 `getIdentity` 명령을 사용하십시오. `getIdentity` 현재 방문자에 대한 기존 ECID를 반환합니다. ECID가 아직 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다. `getIdentity` 방문자에 대한 지역 ID도 반환합니다. 자세한 내용은 [Adobe Audience Manager 사용 안내서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html)를 참조하십시오.

>[!NOTE]
>
>이 메서드는 일반적으로 [!DNL Experience Cloud] ID를 읽어야 하거나 Adobe Audience Manager 위치 힌트가 필요한 사용자 지정 솔루션에서 사용됩니다. 표준 구현에서는 사용되지 않습니다.

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

## ID 동기화

>[!NOTE]
>
>`syncIdentity` 메서드는 해싱 기능 외에 버전 2.1.0에서 제거되었습니다. 버전 2.1.0+를 사용하고 있고 ID를 동기화하려는 경우 `identityMap` 필드 아래의 `sendEvent` 명령의 `xdm` 옵션에서 직접 보낼 수 있습니다.

또한 [!DNL Identity Service] 에서는 `syncIdentity` 명령을 사용하여 자체 식별자를 ECID와 동기화할 수 있습니다.

>[!NOTE]
>
>모든 `sendEvent` 명령에 사용 가능한 모든 ID를 전달하는 것이 좋습니다. 이렇게 하면 개인화를 포함한 다양한 사용 사례 잠금이 해제됩니다. 이제 `sendEvent` 명령에 이러한 ID를 전달할 수 있으므로 DataLayer에 직접 배치할 수 있습니다.

ID 동기화를 사용하면 여러 ID를 사용하여 장치/사용자를 식별하고, 인증 상태를 설정하고, 기본 ID로 간주되는 식별자를 결정할 수 있습니다. ID가 `primary`(으)로 설정되지 않은 경우 기본 기본값은 `ECID`입니다.

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

`identityMap` 내의 각 속성은 특정 [id 네임스페이스](../../identity-service/namespaces.md)에 속하는 ID를 나타냅니다. 속성 이름은 &quot;[!UICONTROL Identities]&quot; 아래에 Adobe Experience Platform 사용자 인터페이스에 나열된 ID 네임스페이스 심벌이어야 합니다. 속성 값은 해당 ID 네임스페이스와 관련된 ID 배열이어야 합니다.

ID 배열의 각 ID 개체는 다음과 같이 구조화됩니다.

### `id`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | 없음 |

지정된 네임스페이스에 대해 동기화할 ID입니다.

### `authenticationState`

| **유형** | **필수 여부** | **기본값** | **가능한 값** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 문자열 | 예 | 모호하 | 모호함, 인증됨 및 로그아웃됨 |

ID의 인증 상태입니다.

### `primary`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 옵션 | false |

이 ID를 통합 프로필에서 기본 조각으로 사용해야 하는지 여부를 결정합니다. 기본적으로 ECID는 사용자의 기본 식별자로 설정됩니다.
