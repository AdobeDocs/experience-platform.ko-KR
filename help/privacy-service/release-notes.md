---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service 릴리스 노트
topic: release notes
translation-type: tm+mt
source-git-commit: 580cce74ab7da9547417a9e74e88b5ddab52171f
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Privacy Service 릴리스 노트

이 문서에서는 Adobe Experience Platform Privacy Service의 새로운 기능, 개선 사항 및 중요한 버그 수정 사항에 대한 정보를 제공합니다.

>[!NOTE] 다른 Experience Platform 서비스에 대한 최신 릴리스 노트는 [여기에서 확인할 수 있습니다](../release-notes/latest/latest.md).

## 2020년 4월 8일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국에 있는 개인 정보 보호법(PDPA)에 따라 개인 정보 요청을 생성하고 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열은 &quot;pdpa_tha&quot; 값을 수락합니다. |
| UI의 네임스페이스 유형 | 이제 Privacy Service UI의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용자 가이드](ui/user-guide.md) 를 참조하십시오. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

## 2020년 1월 14일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| Privacy Service 리브랜딩 | 이전에 &quot;GDPR 서비스&quot;로 불렸던 GDPR은 GDPR뿐만 아니라 다른 규정을 지원하도록 서비스가 확대됨에 따라 Privacy Service으로 다시 브랜딩되었습니다. |
| 새 API 끝점 | Privacy Service API의 기본 경로가 에서 로 업데이트되었습니다. `/data/privacy/gdpr` `/data/core/privacy/jobs` |
| 새 필수 `regulation` 속성 | Privacy Service API에서 새 작업을 만들 때 작업 `regulation` 을 추적할 규칙을 나타내기 위해 요청 페이로드에서 속성을 제공해야 합니다. 허용된 값은 `gdpr` 및 `ccpa`입니다. 자세한 내용은 Privacy Service 개발자 안내서의 [개인 정보](api/privacy-jobs.md) 작업에 대한 문서를 참조하십시오. |
| Adobe Primetime 인증 지원 | 이제 Privacy Service은 Adobe Primetime 인증 `primetimeAuthentication` 의 제품 값으로 액세스/삭제 요청을 수락합니다. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### 개선 사항

* Privacy Service UI 개선 사항:
   * GDPR 및 CPA 규정에 대한 별도의 작업 추적 페이지를 참조하십시오.
   * 새로운 _규정 유형_ 드롭다운을 사용하여 GDPR과 CCPA에 대한 추적 데이터 간을 전환할 수 있습니다.

## 2019년 7월 25일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| 지표 요청 대시보드 | Privacy Service UI의 새로운 지표 대시보드는 제출되고, 오류되고, 완료된 GDPR 요청에 대한 가시성을 제공합니다. |
| 요청 빌더 | GDPR 요청을 제출하는 기술 및 비기술 사용자가 모두 있는 서비스 조직에 대해 &quot;요청 만들기&quot; 기능이 UI에 추가되었습니다. JSON 파일 제출 기능은 Privacy Service UI에서 계속 사용하길 원하는 조직의 경우 계속 사용할 수 있습니다. |
| GDPR 작업 이벤트 알림 | GDPR 작업 상태에 대한 이벤트 알림은 많은 워크플로우에서 중요한 요소입니다. 이전에는 개별 이메일 공지를 사용하여 알림을 제공했지만 GDPR 이벤트 알림은 Adobe I/O 이벤트를 활용하는 메시지로서, Adobe I/O 이벤트는 구성된 웹 후크 지원 작업 요청 자동화로 전송됩니다. Privacy Service UI 사용자는 Adobe I/O GDPR 이벤트를 구독하여 제품 또는 GDPR 작업이 완료되면 업데이트를 받을 수 있습니다. |

## 2019년 4월 18일

### 개선 사항

* Privacy Service UI의 상태 테이블에 대한 기본 범위가 7일 범위로 수정되었습니다.
* 향상된 내부 예외 처리
* 데이터 변경 비율이 낮은 일반적인 내부 호출에 캐싱을 도입함으로써 성능이 개선되었습니다.

### 버그 수정

* Privacy Service API에서 종단점에 대한 필터링된 쿼리에 대한 누락된 로깅 정보를 `GET /` 추가했습니다.

## 2019년 4월 11일

### 개선 사항

* 베타 고객을 위한 새로운 기능을 지원하기 위해 업데이트된 UI
* 베타에서 UI 2.0 기능을 지원하는 새로운 지표 API

## 2019년 9월 4일

### 개선 사항

* 모든 조회(GET) API 호출이 기본적으로 30일 조회 범위로 업데이트되었습니다.
* 최대 45일의 룩백 범위를 포함하도록 제한된 API 사용

## 2019년 2월 14일

### 개선 사항

* 모든 POST 제출 시 `include` 필드를 적용합니다.
* JSON을 업로드할 때 필드를 `include` 적용합니다.

### 버그 수정

* 고객이 Privacy Service UI를 로드할 수 없는 문제를 해결했습니다.