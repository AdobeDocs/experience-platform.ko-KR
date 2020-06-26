---
title: Experience Cloud ID 검색 중
seo-title: Adobe Experience Platform 웹 SDK Experience Cloud ID 검색
description: Adobe Experience Cloud ID를 가져오는 방법을 알아봅니다.
seo-description: Adobe Experience Cloud ID를 가져오는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 9%

---


# ID - Experience Cloud ID 검색

Adobe Experience Platform 웹 SDK는 [Adobe Identity Service를 활용합니다](../../identity-service/ecid.md). 이렇게 하면 각 장치에 페이지 간의 활동을 함께 연결할 수 있도록 장치에서 지속되는 고유한 식별자가 있습니다.

## 자사 ID

이 [!DNL Identity Service] 는 자사 도메인에 있는 쿠키의 ID를 저장합니다. 이 [!DNL Identity Service] 는 도메인에서 HTTP 헤더를 사용하여 쿠키를 설정하려고 시도합니다. 그렇지 않으면 Javascript를 통해 쿠키 설정으로 [!DNL Identity Service] 돌아갑니다. Adobe에서는 쿠키가 클라이언트측 ITP 제한 사항에 의해 제한되지 않도록 CNAME을 설정하는 것이 좋습니다.

## 타사 ID

ID를 타사 도메인(demdex.net)과 동기화하여 사이트 간 추적을 활성화할 수 [!DNL Identity Service] 있습니다. 이 옵션이 활성화되면 방문자(예: ECID가 없는 사람)에 대한 첫 번째 요청이 demdex.net으로 수행됩니다. 이 작업은 이를 허용하는 브라우저(예: 크롬)에서만 수행되며 구성의 매개 `thirdPartyCookiesEnabled` 변수에 의해 제어됩니다. 이 기능을 모두 비활성화하려면 false `thirdPartyCookiesEnabled` 로 설정합니다.

## 방문자 ID 검색

이 고유 ID를 사용하려면 `getIdentity` 명령을 사용하십시오. `getIdentity` 현재 방문자에 대한 기존 ECID를 반환합니다. 아직 ECID가 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다.

>[!NOTE]
>
>이 메서드는 일반적으로 Experience Cloud ID를 읽어야 하는 사용자 지정 솔루션에서 사용됩니다. 표준 구현에서는 사용되지 않습니다.

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

또한, [!DNL Identity Service] 명령을 사용하여 자체 식별자를 ECID와 동기화할 수 `syncIdentity` 있습니다.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### ID 동기화 옵션

#### ID 네임스페이스 기호

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | none |

개체의 키는 ID 네임스페이스 [](../../identity-service/namespaces.md) 기호입니다. ID 아래의 Adobe Experience Platform 사용자 인터페이스에 나와 있는 [!UICONTROL ID를 확인할 수 있습니다].

#### `id`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | none |

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
