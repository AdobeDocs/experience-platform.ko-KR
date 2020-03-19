---
title: 라이브러리 정보 검색 중
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 라이브러리 정보 검색
description: 웹 사이트에 로드된 라이브러리에 대한 정보를 검색하는 방법 학습
seo-description: Adobe Experience Cloud SDK가 자동으로 수집하여 웹 사이트에 로드된 라이브러리에 대한 정보를 검색하는 방법
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) 라이브러리 정보 검색

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

웹 사이트에 로드한 라이브러리 이면의 일부 세부 정보에 액세스하는 것은 종종 유용합니다. 이렇게 하려면 다음과 같이 `getLibraryInfo` 명령을 실행합니다.

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

현재 제공된 `libraryInfo` 객체에는 다음과 같은 속성이 포함됩니다.

* `version` 로드된 라이브러리의 버전입니다. 예를 들어 로드되는 라이브러리 버전이 1.0.0이면 값이 `1.0.0`됩니다.