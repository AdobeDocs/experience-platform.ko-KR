---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개인정보 보호 서비스 릴리스 노트
topic: release notes
translation-type: tm+mt
source-git-commit: d7aa1b4e3e697a504964d6eb485f536065c6718a

---


# 개인정보 보호 서비스 릴리스 노트

이 문서에는 Adobe Experience Platform Privacy Service의 새로운 기능, 향상된 기능 및 중요한 버그 수정에 대한 정보가 포함되어 있습니다.

## 2020년 1월 14일

### 새로운 기능

| 기능 | 설명 |
--- | ---
| 개인정보 보호 서비스 리브랜딩 | 이전에 &quot;GDPR 서비스&quot;라고 명명한 이 서비스는 GDPR뿐만 아니라 다른 규정을 지원하도록 기능이 강화되어 개인 정보 보호 서비스로 다시 브랜딩되었습니다. |
| 새 API 끝점 | 개인 정보 서비스 API의 기본 경로가 에서 `/data/privacy/gdpr` 로 업데이트되었습니다. `/data/core/privacy/jobs` |
| 새로운 필수 `regulation` 속성 | Privacy Service API에서 새 작업을 만들 때, 작업을 추적할 규칙을 나타내려면 요청 페이로드에 속성을 제공해야 `regulation` 합니다. 허용된 값은 `gdpr` 및 `ccpa`입니다. 자세한 내용은 [개인정보 보호 서비스 개발자 안내서의 개인정보 보호 작업에](api/privacy-jobs.md) 대한 문서를 참조하십시오. |
| Adobe Primetime 인증 지원 | 이제 개인 정보 보호 서비스는 Adobe Primetime 인증의 액세스/삭제 요청을 `primetimeAuthentication` 제품 값으로 허용합니다. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### 개선 사항

* 개인정보 보호 서비스 UI 개선 사항:
   * GDPR 및 CPA 규정을 위한 작업 추적 페이지를 별도로 관리할 수 있습니다.
   * 새로운 _규제 유형_ 드롭다운을 사용하여 GDPR과 CCPA에 대한 추적 데이터 간을 전환합니다.

## 2019년 7월 25일

### 새로운 기능

| 기능 | 설명 |
--- | ---
| 지표 요청 대시보드 | 개인 정보 서비스 UI의 새로운 지표 대시보드에서는 제출, 오류 발생 및 완료된 GDPR 요청에 대한 가시성을 제공합니다. |
| 요청 빌더 | GDPR 요청을 제출하는 기술 사용자와 기술 지식이 없는 사용자를 모두 갖춘 서비스 조직에 대해 &quot;요청 만들기&quot; 기능이 UI에 추가되었습니다. JSON 파일 제출 기능은 개인 정보 서비스 UI에서 계속 사용하길 원하는 조직의 경우 계속 사용할 수 있습니다. |
| GDPR 작업 이벤트 알림 | GDPR 작업 상태에 대한 이벤트 알림은 많은 워크플로우에서 중요한 요소입니다. 이전에는 개별 이메일 알림을 사용하여 알림을 제공했지만 GDPR 이벤트 알림은 Adobe I/O 이벤트를 활용하는 메시지입니다. 이 알림은 작업 요청 자동화를 위해 구성된 웹후크로 전송됩니다. 개인 정보 서비스 UI 사용자는 Adobe I/O GDPR 이벤트를 구독하여 제품 또는 GDPR 작업이 완료되면 업데이트를 받을 수 있습니다. |

## 2019년 4월 18일

### 개선 사항

* 개인 정보 서비스 UI의 상태 테이블에 대한 기본 범위가 7일 범위로 수정되었습니다.
* 향상된 내부 예외 처리.
* 데이터 변경률이 낮은 일반적인 내부 호출에 캐싱을 도입하여 성능이 개선되었습니다.

### 버그 수정

* 개인정보 보호 서비스 API에서 종단점에 대한 필터링된 쿼리에 대한 누락된 로깅 정보가 추가되었습니다. `GET /`

## 2019년 4월 11일

### 개선 사항

* 베타 고객을 위한 새로운 기능을 지원하도록 UI 업데이트
* 베타에서 UI 2.0 기능을 지원하는 새로운 지표 API

## 2019년 9월 4일

### 개선 사항

* 모든 조회(GET) API 호출을 기본적으로 30일 조회 범위로 업데이트했습니다.
* 제한된 API 사용이 최대 45일 조회 범위를 포함하도록 제한됨

## 2019년 2월 14일

### 개선 사항

* 모든 POST 제출 시 필드를 `include` 적용합니다.
* JSON을 업로드할 때 필드를 `include` 적용합니다.

### 버그 수정

* 고객이 개인 정보 서비스 UI를 로드할 수 없던 문제를 수정했습니다.