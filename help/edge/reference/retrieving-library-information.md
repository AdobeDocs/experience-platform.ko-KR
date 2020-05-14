---
title: 라이브러리 정보 검색 중
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 라이브러리 정보 검색
description: 웹 사이트에 로드된 라이브러리에 대한 정보를 검색하는 방법을 알아봅니다.
seo-description: Adobe Experience Cloud SDK가 자동으로 수집하여 웹 사이트에 로드된 라이브러리에 대한 정보를 검색하는 방법을 알아봅니다
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 라이브러리 정보 검색 중

웹 사이트에 로드한 라이브러리 이면의 일부 세부 정보에 액세스하는 것은 종종 유용합니다. 이렇게 하려면 다음과 같이 `getLibraryInfo` 명령을 실행합니다.

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

현재 제공된 개체에는 다음 속성이 `libraryInfo` 포함되어 있습니다.

* `version` 로드된 라이브러리의 버전입니다. 예를 들어 로드되는 라이브러리 버전이 1.0.0이면 값이 됩니다 `1.0.0`.