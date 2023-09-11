---
title: 자동으로 수집된 정보
description: Adobe Experience Platform Web SDK에서 자동으로 수집하는 데이터에 대한 개요입니다.
source-git-commit: 89b981104e3cbe597d1556484f4365866bf2a11d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 3%

---

# 자동으로 수집된 정보

Adobe Experience Platform Web SDK는 즉시 사용할 수 있는 몇 가지 정보를 자동으로 수집합니다. 조직에서 이 데이터를 자동으로 수집하지 않으려는 경우 `context` 의 옵션 [`configure` 명령](../fundamentals/configuring-the-sdk.md).

다음에서 제외된 키워드 `context` 배열이 데이터 수집에 포함되지 않습니다. 다음과 같은 경우 `context` 배열이 다음에 없습니다. `configure` 아래 표의 모든 데이터는 자동으로 수집됩니다.

| 이름 | 설명 | `context` array 키워드 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- | --- |
| 화면 높이 | 화면의 픽셀 단위 높이입니다. | `device` | `events[].xdm.device.screenHeight` | `900` |
| 화면 너비 | 화면의 픽셀 단위 폭입니다. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| 화면 방향 | 화면의 방향입니다. | `device` | `events[].xdm.device.screenOrientation` | `landscape` 또는 `portrait` |
| 환경 유형 | 경험이 표시되는 환경의 유형입니다. Adobe Experience Platform Web SDK는 항상 이 필드를 다음으로 설정합니다. `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| 뷰포트 높이 | 브라우저 컨텐츠 영역의 픽셀 단위 높이입니다. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| 뷰포트 폭 | 브라우저 컨텐츠 영역의 픽셀 단위 폭입니다. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| SDK 이름 | SDK 식별자. 이 필드는 URI를 사용하여 다른 소프트웨어 라이브러리에서 제공하는 식별자 간의 고유성을 개선합니다. 독립형 라이브러리를 사용하는 경우 값은 입니다. `https://ns.adobe.com/experience/alloy`. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 입니다. `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| SDK 버전 | 독립형 라이브러리를 사용하는 경우 값은 라이브러리 버전입니다. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 라이브러리 버전과 태그 확장 버전의 연결입니다. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| 환경 | 데이터가 수집된 환경입니다. Adobe Experience Platform Web SDK는 항상 이 필드를 다음으로 설정합니다. `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| 현지 시간 | 간소화된 확장 ISO 형식의 최종 사용자에 대한 로컬 타임스탬프 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 로컬 시간대 오프셋 | 사용자가 GMT에서 오프셋된 시간(분 수)입니다. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| 타임스탬프 | 간소화된 확장 ISO 형식의 최종 사용자에 대한 UTC 타임스탬프 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | 항상 포함됨 | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| 현재 페이지 URL | 현재 페이지의 URL. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 레퍼러 URL | 방문한 이전 페이지의 URL입니다. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
