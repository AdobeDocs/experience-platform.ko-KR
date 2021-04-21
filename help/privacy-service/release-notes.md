---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: Privacy Service 릴리스 노트
topic-legacy: release notes
description: Adobe Experience Platform Privacy Service의 최신 릴리스 노트입니다.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# [!DNL Privacy Service] 릴리스 노트

이 문서에는 Adobe Experience Platform [!DNL Privacy Service]의 새로운 기능에 대한 정보와 개선 사항 및 중요한 버그 수정 사항이 포함되어 있습니다.

>[!NOTE]
>
>다른 [!DNL Experience Platform] 서비스에 대한 최신 릴리스 노트는 [여기](../release-notes/latest/latest.md)에서 찾을 수 있습니다.

## 2020년 9월 9일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| LGPD 지원(브라질) | 이제 브라질의 [!DNL Lei Geral de Proteção de Dados](LGPD) 규정에 따라 개인 정보 일자리를 만들 수 있습니다. 이러한 작업은 규정 코드 `lgpd_bra`에 따라 추적됩니다. |

## 2020년 4월 8일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | [!DNL Privacy] 요청은 이제 태국에 있는 개인 데이터 보호 법(PDPA)에 따라 생성 및 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열은 값 &quot;pdpa_tha&quot;를 수락합니다. |
| UI의 네임스페이스 유형 | 이제 [!DNL Privacy Service] UI의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용자 안내서](ui/user-guide.md)를 참조하십시오. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

## 2020년 1월 14일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| [!DNL Privacy Service] 재브랜딩 | 이전에 &quot;GDPR 서비스&quot;라고 이름 붙여진 이 서비스는 GDPR 외에도 다른 규정을 지원하도록 성장하여 [!DNL Privacy Service](으)로 다시 브랜딩되었습니다. |
| 새 API 끝점 | [!DNL Privacy Service] API의 기본 경로가 `/data/privacy/gdpr`에서 `/data/core/privacy/jobs`(으)로 업데이트되었습니다. |
| 새로 필요한 `regulation` 속성 | [!DNL Privacy Service] API에서 새 작업을 만들 때 작업을 추적할 규칙을 나타내려면 요청 페이로드에 `regulation` 속성을 제공해야 합니다. 허용된 값은 `gdpr` 및 `ccpa`입니다. 자세한 내용은 [!DNL Privacy Service] 개발자 안내서의 [개인 정보 작업](api/privacy-jobs.md)에 있는 문서를 참조하십시오. |
| Adobe Primetime 인증 지원 | [!DNL Privacy Service] 이제 제품 값으로 Adobe Primetime 인증의 액세스/삭제 요청 `primetimeAuthentication` 을 허용합니다. 자세한 내용은 [Primetime 인증 설명서](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)을 참조하십시오. |

### 개선 사항

* [!DNL Privacy Service] 향상된 UI:
   * GDPR 및 CPA 규정에 대한 작업 추적 페이지를 따로 분류합니다.
   * GDPR과 CCPA에 대한 추적 데이터 간을 전환하도록 새 *규정 유형* 드롭다운을 사용합니다.

## 2019년 7월 25일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| 요청 지표 대시보드 | [!DNL Privacy Service] UI의 새 지표 대시보드는 제출, 오류 발생 및 완료된 GDPR 요청에 대한 가시성을 제공합니다. |
| 요청 빌더 | GDPR 요청을 제출하는 기술 사용자와 기술 지식이 없는 사용자를 모두 보유한 서비스 조직에 &quot;요청 만들기&quot; 기능이 UI에 추가되었습니다. JSON 파일 제출 기능은 계속 사용하길 원하는 조직의 경우 [!DNL Privacy Service] UI에서 계속 사용할 수 있습니다. |
| GDPR 작업 이벤트 알림 | GDPR 작업 상태에 대한 이벤트 알림은 많은 워크플로우에서 중요한 요소입니다. 개별 이메일 알림을 사용하여 이전에 알림을 제공했지만 GDPR 이벤트 알림은 Adobe I/O 이벤트를 활용하는 메시지입니다. 이 알림은 이벤트를 구성된 웹후크로 전송되어 작업 요청 자동화를 촉진합니다. [!DNL Privacy Service] UI 사용자는 Adobe I/O GDPR 이벤트를 구독하여 제품 또는 GDPR 작업이 완료되면 업데이트를 받을 수 있습니다. |

## 2019년 4월 18일

### 개선 사항

* [!DNL Privacy Service] UI의 상태 테이블에 대한 기본 범위가 7일 범위로 수정되었습니다.
* 내부 예외 처리가 개선되었습니다.
* 데이터 변경 비율이 낮은 일반적인 내부 호출에 캐싱을 도입함으로써 성능이 개선되었습니다.

### 버그 수정

* [!DNL Privacy Service] API에서 `GET /` 끝점에 대한 필터링된 쿼리에 대해 누락된 로깅 정보를 추가했습니다.

## 2019년 4월 11일

### 개선 사항

* 베타 고객을 위한 새로운 기능을 지원하도록 UI 업데이트
* 베타에서 UI 2.0 기능을 지원하기 위한 새로운 지표 API

## 2019년 4월 9일

### 개선 사항

* 모든 조회(GET) API 호출을 기본적으로 30일 조회 범위로 업데이트했습니다.
* 최대 전환 범위를 45일로 제한하는 제한된 API 사용

## 2019년 2월 14일

### 개선 사항

* 모든 POST 제출에서 `include` 필드를 적용합니다.
* JSON을 업로드할 때 `include` 필드를 적용합니다.

### 버그 수정

* 고객이 [!DNL Privacy Service] UI를 로드할 수 없는 문제가 해결되었습니다.
