---
title: 자동으로 수집된 정보
seo-title: Adobe Experience Platform 웹 SDK에서 자동으로 수집한 정보
description: Adobe Experience Cloud SDK가 자동으로 수집하는 각 정보에 대한 설명
seo-description: Adobe Experience Cloud SDK가 자동으로 수집하는 각 정보에 대한 설명
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 5%

---


# 자동으로 수집된 정보

Adobe Experience Cloud SDK는 특별한 구성 없이 다양한 정보를 자동으로 수집합니다. 그러나 필요한 경우 명령의 옵션을 사용하여 이 정보 `context` 를 비활성화할 수 `configure` 있습니다. [SDK 구성을 참조하십시오](../fundamentals/configuring-the-sdk.md). 아래는 그러한 정보의 목록입니다. 괄호 안의 이름은 컨텍스트를 구성할 때 사용할 문자열을 나타냅니다.

## 장치 (`device`)

장치에 대한 정보입니다. 사용자 에이전트 문자열에서 서버측을 조회할 수 있는 데이터는 포함되지 않습니다.

### 화면 높이

| **페이로드의 경로:** | **예:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

화면의 높이(픽셀)입니다.

### 화면 방향

| **페이로드의 경로:** | **가능한 값:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 또는 `portrait` |

화면의 방향.

### 화면 너비

| **페이로드의 경로:** | **예:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

화면의 너비(픽셀 단위)입니다.

## 환경 (`environment`)

브라우저 환경에 대한 세부 정보입니다.

### 환경 유형

브라우저

| **페이로드의 경로:** | **예:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

그 경험이 표면화된 환경의 유형. JavaScript용 Adobe Experience Platform SDK는 항상 설정됩니다 `browser`.

### 뷰포트 높이

| **페이로드의 경로:** | **예:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

브라우저 컨텐츠 영역의 높이(픽셀 단위).

### 뷰포트 너비

| **페이로드의 경로:** | **예:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

브라우저 컨텐츠 영역의 너비(픽셀 단위).

## 구현 세부 정보

이벤트를 수집하는 데 사용되는 SDK에 대한 정보입니다.

### 이름

| **페이로드의 경로:** | **예:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

SDK(소프트웨어 개발 키트) 식별자입니다.  이 필드는 URI를 사용하여 다른 소프트웨어 라이브러리에서 제공하는 식별자 간의 고유성을 향상시킵니다.

### 버전

| **페이로드의 경로:** | **예:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

## 배치 컨텍스트(`placeContext`)

최종 사용자의 위치에 대한 정보입니다.

### 현지 시간

| **페이로드의 경로:** | **예:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

간소화된 확장 ISO 형식 [ISO 8601의 최종 사용자를 위한 로컬 타임스탬프](https://tools.ietf.org/html/rfc3339#section-5.6).

### 로컬 시간대 오프셋

| **페이로드의 경로:** | **예:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

사용자가 GMT에서 옵트되는 시간(분).

## 타임스탬프

| **페이로드의 경로:** | **예:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

이벤트의 타임스탬프입니다.  이 컨텍스트 부분은 제거할 수 없습니다.

단순화된 확장 ISO 형식 [ISO 8601의 최종 사용자에 대한 UTC 타임스탬프](https://tools.ietf.org/html/rfc3339#section-5.6).

## 웹 세부 사항(`web`)

사용자가 있는 페이지에 대한 세부 사항.

### 현재 페이지 URL

| **페이로드의 경로:** | **예:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

현재 페이지의 URL.

### 레퍼러 URL

| **페이로드의 경로:** | **예:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

방문한 이전 페이지의 URL.
