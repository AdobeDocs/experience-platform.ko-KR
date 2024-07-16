---
title: getLibraryInfo
description: 현재 웹 SDK 라이브러리 버전에 대한 정보를 검색합니다.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

`getLibraryInfo` 명령은 현재 사용 중인 웹 SDK 라이브러리 버전에 대한 정보를 제공합니다. 이 명령을 사용하여 다른 웹 속성에 배포하는 웹 SDK 버전을 추적할 수 있습니다.

## 웹 SDK 태그 확장을 사용한 라이브러리 정보

태그 확장은 이 명령을 전송하는 인터페이스를 제공하지 않습니다. JavaScript 라이브러리 구문 다음에 나오는 사용자 지정 코드 편집기를 사용하십시오.

태그 확장을 사용하여 이 명령을 실행하면 태그 확장 버전과 라이브러리 버전이 모두 포함되어 `+` 기호와 연결됩니다. 웹 SDK 라이브러리 버전이 먼저 나열되고 그 뒤에 태그 확장 버전이 나열됩니다.

## 웹 SDK JavaScript 라이브러리를 사용한 라이브러리 정보

웹 SDK의 구성된 인스턴스를 호출할 때 `getLibraryInfo` 명령을 실행합니다. 이 명령은 일반적으로 채우는 개체를 검색할 수 있도록 해 주는 JavaScript 약속과 쌍을 이룹니다.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## 응답 개체

이 명령을 사용하여 [응답을 처리](command-responses.md)하기로 결정하는 경우 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`libraryInfo.commands`**: 이 버전의 웹 SDK에서 지원하는 명령 배열.
* **`libraryInfo.configs`**: 이 버전의 웹 SDK에서 지원하는 구성 설정의 배열입니다.
* **`libraryInfo.version`**: 웹 SDK 라이브러리의 버전입니다.
