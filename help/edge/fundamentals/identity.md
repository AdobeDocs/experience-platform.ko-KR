---
title: Experience Cloud ID 검색 중
seo-title: Adobe Experience Platform 웹 SDK Experience Cloud ID 검색
description: Adobe Experience Cloud ID를 얻는 방법을 알아봅니다.
seo-description: Adobe Experience Cloud ID를 얻는 방법을 알아봅니다.
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 5%

---


# ID - Experience Cloud ID 검색

Adobe Experience Platform [!DNL Web SDK] 는 [Adobe 아이덴티티 서비스를 활용합니다](../../identity-service/ecid.md). 이렇게 하면 각 장치에 페이지 간의 활동을 함께 연결할 수 있도록 장치에서 지속되는 고유한 식별자가 있습니다.

## 자사 ID

이 [!DNL Identity Service] 는 자사 도메인에 있는 쿠키의 ID를 저장합니다. 이 [!DNL Identity Service] 는 도메인에서 HTTP 헤더를 사용하여 쿠키를 설정하려고 시도합니다. 그렇지 않으면 Javascript를 통해 쿠키 설정으로 [!DNL Identity Service] 돌아갑니다. Adobe은 쿠키가 클라이언트측 ITP 제한에 의해 제한되지 않도록 CNAME을 설정하는 것이 좋습니다.

## 타사 ID

ID를 타사 도메인(demdex.net)과 동기화하여 사이트 간 추적을 활성화할 수 [!DNL Identity Service] 있습니다. 이 옵션이 활성화되면 방문자(예: ECID가 없는 사람)에 대한 첫 번째 요청이 demdex.net으로 수행됩니다. 이 작업은 이를 허용하는 브라우저(예: 크롬)에서만 수행되며 구성의 매개 `thirdPartyCookiesEnabled` 변수에 의해 제어됩니다. 이 기능을 모두 비활성화하려면 false `thirdPartyCookiesEnabled` 로 설정합니다.

## ID 마이그레이션

방문자 API를 사용하여 마이그레이션할 때 기존 AMCV 쿠키를 마이그레이션할 수도 있습니다. ECID 마이그레이션을 활성화하려면 구성에서 매개 `idMigrationEnabled` 변수를 설정합니다. 일부 사용 사례를 사용하도록 id 마이그레이션이 설정되었습니다.

* 도메인의 일부 페이지가 방문자 API를 사용하고 다른 페이지가 이 SDK를 사용하는 경우 이 경우를 지원하기 위해 SDK는 기존 AMCV 쿠키를 읽고 기존 ECID를 사용하여 새 쿠키를 기록합니다. 또한, SDK는 AEP 웹 SDK로 구현된 페이지에서 ECID를 먼저 얻는 경우 방문자 API를 사용하여 구현된 후속 페이지의 ECID가 동일하도록 AMCV 쿠키를 기록합니다.
* 방문자 API가 있는 페이지에서 AEP 웹 SDK가 설정되면 이 경우를 지원하기 위해 AMCV 쿠키가 설정되지 않은 경우 SDK는 페이지에서 방문자 API를 찾아 ECID를 얻기 위해 호출합니다.
* 전체 사이트가 AEP 웹 SDK를 사용하고 있고 방문자 API가 없는 경우 ECID를 마이그레이션하여 재방문자 정보를 유지하는 것이 유용합니다. SDK가 일정 기간 `idMigrationEnabled` 에 배포되어 대부분의 방문자 쿠키가 마이그레이션되면 설정을 해제할 수 있습니다.

## 방문자 ID 검색

이 고유 ID를 사용하려면 `getIdentity` 명령을 사용하십시오. `getIdentity` 현재 방문자에 대한 기존 ECID를 반환합니다. 아직 ECID가 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다.

>[!NOTE]
>
>이 메서드는 일반적으로 [!DNL Experience Cloud] ID를 읽어야 하는 사용자 지정 솔루션에서 사용됩니다. 표준 구현에서는 사용되지 않습니다.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## ID 동기화

>[!NOTE]
>
>해싱 기능 외에 버전 2.1.0에서 이 `syncIdentity` 방법이 제거되었습니다. 버전 2.1.0+을 사용하고 있고 ID를 동기화하려는 경우 필드 아래에 있는 명령 `xdm` 옵션 `sendEvent` 에서 직접 전송할 수 `identityMap` 있습니다.

또한, [!DNL Identity Service] 명령을 사용하여 자체 식별자를 ECID와 동기화할 수 `syncIdentity` 있습니다.

>[!NOTE]
>
>모든 `sendEvent` 명령에 사용 가능한 모든 ID를 전달하는 것이 좋습니다. 이를 통해 개인화를 비롯한 다양한 사용 사례를 해결할 수 있습니다. 이러한 ID를 `sendEvent` 명령에 전달할 수 있으므로 DataLayer에 직접 삽입할 수 있습니다.

ID를 동기화하면 여러 ID를 사용하는 장치/사용자를 식별하고 인증 상태를 설정하고 기본 ID로 간주되는 식별자를 결정할 수 있습니다. 식별자를 다음으로 설정하지 않은 경우 기본 기본값은 `primary`입니다 `ECID`.

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
})
```


### ID 동기화 옵션

#### ID 네임스페이스 기호

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | 없음 |

개체의 키는 ID 네임스페이스 [](../../identity-service/namespaces.md) 기호입니다. 이 목록은 Adobe Experience Platform 사용자 인터페이스에서 &quot;ID&quot;[!UICONTROL 에서 확인할 수 있습니다].

#### `id`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | 없음 |

지정된 네임스페이스에 대해 동기화할 ID입니다.

#### `authenticationState`

| **유형** | **필수 여부** | **기본값** | **가능한 값** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 문자열 | 예 | 모호해 | 모호함, 인증됨 및 로그아웃됨 |

ID의 인증 상태입니다.

#### `primary`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 옵션 | false |

이 ID를 통합 프로필의 기본 조각으로 사용할지 여부를 결정합니다. 기본적으로 ECID는 사용자의 기본 식별자로 설정됩니다.

#### `hashEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 옵션 | false |

활성화하면 SHA256 해싱을 사용하여 ID를 해시합니다.
