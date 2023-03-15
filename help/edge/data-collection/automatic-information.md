---
title: Adobe Experience Platform 웹 SDK에서 자동으로 수집된 정보
description: Adobe Experience Platform SDK에서 자동으로 수집하는 각 정보에 대한 개요입니다.
keywords: 정보 수집;컨텍스트;구성;장치;screenHeight;화면 높이;screenOrientation;화면 방향;screenWidth;화면 너비;환경;뷰포트 높이;뷰포트 너비;뷰포트 너비;crowserDetails;브라우저 세부 정보;구현 세부 정보;구현 세부 정보;이름;버전;placeContext;localTime;로컬 시간;localTimezoneOffset;로컬 시간대 오프셋;타임스탬프;웹;url;webPageDetails;웹 페이지 세부 정보;webReferrer;웹 레퍼러;가로;세로;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# 자동으로 수집된 정보

Adobe Experience Platform 웹 SDK는 특별한 구성 없이 자동으로 많은 정보를 수집합니다. 그러나 필요한 경우 를 사용하여 이 정보를 비활성화할 수 있습니다 `context` 의 옵션 `configure` 명령입니다. [SDK 구성 을 참조하십시오](../fundamentals/configuring-the-sdk.md). 다음은 이러한 정보 목록입니다. 괄호로 묶인 이름은 컨텍스트를 구성할 때 사용할 문자열을 나타냅니다.

## 장치 (`device`)

장치에 대한 정보. 사용자 에이전트 문자열에서 서버측에서 조회할 수 있는 데이터는 여기에 포함되지 않습니다.

### 화면 높이

| **페이로드의 경로:** | **예:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

화면의 높이(픽셀 단위)입니다.

### 화면 방향

| **페이로드의 경로:** | **가능한 값:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 또는 `portrait` |

화면의 방향입니다.

### 화면 너비

| **페이로드의 경로:** | **예:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

화면의 너비(픽셀 단위)입니다.

## 환경 (`environment`)

브라우저 환경에 대한 세부 정보.

### 환경 유형

브라우저

| **페이로드의 경로:** | **예:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

경험이 표시되는 환경의 유형입니다. Adobe Experience Platform Web SDK는 항상 이 설정을 로 설정합니다. `browser`.

### 뷰포트 높이

| **페이로드의 경로:** | **예:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

브라우저의 콘텐츠 영역 높이(픽셀 단위)입니다.

### 뷰포트 폭

| **페이로드의 경로:** | **예:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

브라우저의 콘텐츠 영역 너비(픽셀 단위)입니다.

## 구현 세부 사항

이벤트를 수집하는 데 사용되는 SDK에 대한 정보입니다.

### 이름

| **페이로드의 경로:** | **예:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

소프트웨어 개발 키트(SDK) 식별자.  이 필드는 URI를 사용하여 다른 소프트웨어 라이브러리에서 제공하는 식별자 간의 고유성을 개선합니다. 독립형 라이브러리를 사용하는 경우 값은 입니다. `https://ns.adobe.com/experience/alloy`. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 입니다. `https://ns.adobe.com/experience/alloy+reactor`.

### 버전

| **페이로드의 경로:** | **예:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

독립형 라이브러리를 사용하는 경우 값은 단순히 라이브러리 버전입니다. 라이브러리를 태그 확장의 일부로 사용하는 경우 이것이 라이브러리 버전 및 &quot;+&quot;와 연결된 태그 확장 버전입니다. 예를 들어 라이브러리 버전이 2.1.0이고 태그 확장 버전이 2.1.3인 경우 값은 다음과 같습니다. `2.1.0+2.1.3`.

### 환경

| **페이로드의 경로:** | **예:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

데이터가 수집된 환경입니다. 항상 (으)로 설정됩니다. `browser`.

## 위치 컨텍스트(`placeContext`)

최종 사용자의 위치에 대한 정보입니다.

### 현지 시간

| **페이로드의 경로:** | **예:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

간소화된 확장 ISO 형식의 최종 사용자에 대한 로컬 타임스탬프 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### 로컬 시간대 오프셋

| **페이로드의 경로:** | **예:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

사용자가 GMT에서 오프셋된 시간(분 수)

## 타임스탬프

| **페이로드의 경로:** | **예:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

이벤트의 타임스탬프.  컨텍스트의 이 부분은 제거할 수 없습니다.

간소화된 확장 ISO 형식의 최종 사용자에 대한 UTC 타임스탬프 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## 웹 세부 정보(`web`)

사용자가 있는 페이지에 대한 세부 정보.

### 현재 페이지 URL

| **페이로드의 경로:** | **예:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

현재 페이지의 URL.

### 레퍼러 URL

| **페이로드의 경로:** | **예:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

방문한 이전 페이지의 URL입니다.
