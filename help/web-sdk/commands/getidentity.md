---
title: getIdentity
description: 이벤트 데이터를 전송하지 않고 방문자의 ID를 얻습니다.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

다음 `getIdentity` 명령을 사용하면 이벤트 데이터를 전송하지 않고 방문자 ID를 얻을 수 있습니다. 를 실행할 때 `sendEvent` 명령을 실행하면 웹 SDK는 방문자의 ID가 없는 경우 자동으로 해당 방문자의 ID를 가져옵니다.

방문자 ID를 생성하고 데이터를 보내기 위해 별도의 호출이 필요한 경우 이 명령을 사용할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 ID 가져오기

웹 SDK 태그 확장은 태그 확장 UI를 통해 이 명령을 제공하지 않습니다. JavaScript 라이브러리 구문을 사용하여 사용자 지정 코드 편집기를 사용합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 ID 가져오기

실행 `getIdentity` 명령을 사용하여 웹 SDK의 구성된 인스턴스를 호출할 수 있습니다. 이 명령을 구성할 때 사용할 수 있는 옵션은 다음과 같습니다.

* **`namespaces`**: 네임스페이스의 배열입니다. 기본값은 `["ECID"]`입니다. 유효한 값은 다음과 같습니다 `["ECID"]`, `null`, 또는 `undefined`.
* **`edgeConfigOverrides`**: 안 [데이터 스트림 구성 재정의 개체](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## 응답 개체

다음을 결정하시면 [응답 처리](command-responses.md) 이 명령을 사용하면 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`identity.ECID`**: 방문자의 ECID를 포함하는 문자열입니다.
* **`edge.regionID`**: ID를 가져올 때 브라우저가 히트한 에지 네트워크 영역을 나타내는 정수입니다. 기존 Audience Manager 위치 힌트와 동일합니다.
