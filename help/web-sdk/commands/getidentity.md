---
title: getIdentity
description: 이벤트 데이터를 전송하지 않고 방문자의 ID를 얻습니다.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 5f8a9938eaccfd2eeabc75c56608f11819a81ffa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---

# `getIdentity`

[`sendEvent`](sendevent/overview.md) 명령을 실행하면 웹 SDK에서 방문자의 ID가 없는 경우 자동으로 해당 방문자의 ID를 가져옵니다.

`getIdentity` 명령을 사용하면 이벤트 데이터를 보내지 않고 방문자 ID를 가져올 수 있습니다.

방문자 ID를 생성하고 데이터를 보내기 위해 별도의 호출이 필요한 경우 이 명령을 사용할 수 있습니다.

`getIdentity` 명령은 다음 흐름을 통해 `ECID`을(를) 검색합니다.

1. 웹 SDK을 사용하여 `getIdentity` 또는 [`appendIdentityToUrl`](appendidentitytourl.md)을(를) 호출합니다.
1. 웹 SDK은 동의 정보가 제공될 때까지 기다립니다.
1. 웹 SDK에서 호출에 `ECID` 네임스페이스가 요청되었는지 확인합니다. 기본적으로 `ECID` 네임스페이스는 항상 포함됩니다.
1. Web SDK은 `kndctr` 쿠키를 읽고 해당 값이 있는 경우 `ECID`(으)로 반환합니다. `ECID` 값만 반환하고 `regionId`은(는) 반환하지 않습니다.
1. `kndctr` ID 쿠키가 설정되지 않았거나 `"CORE"` 네임스페이스가 요청되면 Web SDK에서 Edge Network에 요청합니다.
1. Edge Network은 `ECID` 및 `regionId`을(를) 모두 반환합니다(필요한 경우 `CORE ID`).

## 웹 SDK 태그 확장을 사용하여 ID 가져오기

웹 SDK 태그 확장은 태그 확장 UI를 통해 이 명령을 제공하지 않습니다. JavaScript 라이브러리 구문을 사용하여 사용자 지정 코드 편집기를 사용합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 ID 가져오기

웹 SDK의 구성된 인스턴스를 호출할 때 `getIdentity` 명령을 실행합니다. 이 명령을 구성할 때 사용할 수 있는 옵션은 다음과 같습니다.

* **`namespaces`**: 네임스페이스의 배열입니다. 기본값은 `["ECID"]`입니다. 기타 지원되는 값은 다음과 같습니다.
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  [!DNL ECID]과(와) [!DNL CORE ID]을(를) 동시에 요청할 수 있습니다. 예: `"namespaces": ["ECID","CORE"]`.

* **`edgeConfigOverrides`**: [데이터 스트림 구성 재정의 개체](datastream-overrides.md)입니다.

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## 응답 개체

이 명령을 사용하여 [응답을 처리](command-responses.md)하기로 결정하는 경우 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`identity.ECID`**: 방문자의 ECID가 포함된 문자열입니다.
* **`identity.CORE`**: 방문자의 코어 ID가 포함된 문자열입니다.
* **`edge.regionID`**: ID를 가져올 때 브라우저가 히트한 Edge Network 영역을 나타내는 정수입니다. 기존 Audience Manager 위치 힌트와 동일합니다.
