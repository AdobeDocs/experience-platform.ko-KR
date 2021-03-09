---
title: Adobe Experience Platform 웹 SDK를 사용하여 Experience Cloud ID 검색
description: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Experience Cloud ID(ECID)를 검색하는 방법을 알아봅니다.
seo-description: Adobe Experience Cloud ID를 가져오는 방법에 대해 알아봅니다.
keywords: ID;퍼스트 파티 ID;ID 서비스;3번째 파티 ID;ID 마이그레이션;방문자 ID;3자 ID;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;동기화 ID;syncIdentity;sendEvent;idMap;기본;ID;네임스페이스 id;authenticationState hashEnabled;
translation-type: tm+mt
source-git-commit: 882bcd2f9aa7a104270865783eed82089862dea3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---


# Adobe Experience Cloud ID 검색

Adobe Experience Platform 웹 SDK는 [Adobe ID 서비스](../../identity-service/ecid.md)를 활용합니다. 이렇게 하면 각 장치에 페이지 간 활동을 함께 연결할 수 있도록 장치에 지속되는 고유 식별자가 있습니다.

## 자사 ID

[!DNL Identity Service]은 자사 도메인의 쿠키에 ID를 저장합니다. [!DNL Identity Service]은(는) 도메인의 HTTP 헤더를 사용하여 쿠키를 설정하려고 시도합니다. 그렇지 않으면 [!DNL Identity Service]은 Javascript를 통해 쿠키를 설정하는 것으로 돌아갑니다. Adobe은 쿠키가 클라이언트측 ITP 제한에 의해 제한되지 않도록 CNAME을 설정하는 것이 좋습니다.

## 타사 ID

[!DNL Identity Service]은(는) ID를 타사 도메인(demdex.net)과 동기화하여 사이트 전체에서 추적을 활성화할 수 있습니다. 이 옵션이 활성화되면 방문자에 대한 첫 번째 요청(예: ECID가 없는 사람)이 demdex.net으로 수행됩니다. 이 작업은 크롬과 같이 이를 허용하는 브라우저에서만 수행되며 구성의 `thirdPartyCookiesEnabled` 매개 변수로 제어됩니다. 이 기능을 모두 비활성화하려면 `thirdPartyCookiesEnabled`을(를) false로 설정합니다.

## ID 마이그레이션

방문자 API를 사용하여 마이그레이션할 때 기존 AMCV 쿠키를 마이그레이션할 수도 있습니다. ECID 마이그레이션을 활성화하려면 구성에서 `idMigrationEnabled` 매개 변수를 설정합니다. ID 마이그레이션은 다음 사용 사례를 활성화합니다.

* 도메인의 일부 페이지가 방문자 API를 사용하고 다른 페이지가 이 SDK를 사용하는 경우 이 경우를 지원하기 위해 SDK는 기존 AMCV 쿠키를 읽고 기존 ECID를 사용하여 새 쿠키를 기록합니다. 또한 SDK는 SDK로 구현된 페이지에서 ECID를 먼저 얻는 경우 방문자 API로 구현된 후속 페이지에 동일한 ECID가 있도록 AMCV 쿠키를 기록합니다.
* 방문자 API도 있는 페이지에 Adobe Experience Platform 웹 SDK가 설정되어 있을 때. 이 경우를 지원하기 위해 AMCV 쿠키가 설정되지 않은 경우 SDK는 페이지에서 방문자 API를 찾아 ECID를 가져오도록 호출합니다.
* 전체 사이트가 Adobe Experience Platform 웹 SDK를 사용하고 있고 방문자 API가 없는 경우 재방문자 정보가 보존되도록 ECID를 마이그레이션하는 것이 유용합니다. 대부분의 방문자 쿠키가 마이그레이션되도록 일정 기간 동안 SDK가 `idMigrationEnabled`과(와) 함께 배포된 후 설정을 해제할 수 있습니다.

## 마이그레이션 트레이트 업데이트

XDM 형식 데이터를 Audience Manager으로 보낼 때 데이터를 마이그레이션할 때 신호로 변환해야 합니다. XDM에서 제공하는 새 키를 반영하려면 트레이트를 업데이트해야 합니다. 이 프로세스는 Audience Manager이 만든 [BAAAM 도구](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)를 사용하여 더 쉬워집니다.

## 서버 측 전달

현재 서버 측 전달이 활성화되어 있고 `appmeasurement.js`을(를) 사용하고 있는 경우 및 `visitor.js` 서버 측 전달 기능을 사용하도록 설정할 수 있으며 이로 인해 문제가 발생하지 않습니다. 백엔드에서 Adobe은 모든 AAM 세그먼트를 가져오고 Analytics에 대한 호출에 추가합니다. Analytics 호출에 이러한 세그먼트가 포함되어 있으면 Analytics는 Audience Manager을 호출하지 않고 데이터를 전달하므로 이중 데이터 수집은 없습니다. 또한 동일한 세그멘테이션 끝점이 백엔드에서 호출되므로 웹 SDK를 사용할 때는 위치 힌트가 필요하지 않습니다.

## 방문자 ID 및 지역 ID 검색

고유 방문자 ID를 사용하려면 `getIdentity` 명령을 사용합니다. `getIdentity` 현재 방문자에 대한 기존 ECID를 반환합니다. 아직 ECID가 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다. `getIdentity` 방문자의 지역 ID도 반환합니다. 자세한 내용은 [Adobe Audience Manager 사용 안내서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html)를 참조하십시오.

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
>해시 기능 외에 `syncIdentity` 메서드는 버전 2.1.0에서 제거되었습니다. 버전 2.1.0+을 사용하고 있고 ID를 동기화하려는 경우 `sendEvent` 명령의 `xdm` 옵션(`identityMap` 필드 아래)에서 직접 보낼 수 있습니다.

또한 [!DNL Identity Service]에서는 `syncIdentity` 명령을 사용하여 자신의 식별자를 ECID와 동기화할 수 있습니다.

>[!NOTE]
>
>모든 `sendEvent` 명령에 사용 가능한 모든 ID를 전달하는 것이 좋습니다. 이를 통해 개인화를 비롯한 다양한 사용 사례를 해결합니다. 이제 이러한 ID를 `sendEvent` 명령에 전달할 수 있으므로 DataLayer에 직접 배치할 수 있습니다.

ID 동기화를 사용하면 여러 ID를 사용하는 장치/사용자를 식별하고 인증 상태를 설정하고 기본 ID로 간주되는 식별자를 결정할 수 있습니다. 식별자가 `primary`으로 설정되지 않은 경우 기본 기본값은 `ECID`입니다.

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

`identityMap` 내의 각 속성은 특정 [identity 네임스페이스](../../identity-service/namespaces.md)에 속하는 ID를 나타냅니다. 속성 이름은 ID 네임스페이스 심볼이어야 합니다. 이 심볼은 &quot;[!UICONTROL ID]&quot; 아래의 Adobe Experience Platform 사용자 인터페이스에 나열될 수 있습니다. 속성 값은 해당 ID 네임스페이스와 관련된 ID 배열이어야 합니다.

ID 배열의 각 ID 객체는 다음과 같이 구성됩니다.

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

이 ID를 통합 프로필의 기본 조각으로 사용할지 여부를 결정합니다. 기본적으로 ECID는 사용자의 기본 식별자로 설정됩니다.
