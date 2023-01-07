---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 릴리스 노트
description: Adobe Experience Platform Privacy Service에 대한 최신 릴리스 노트입니다.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] 릴리스 노트

이 문서에는 Adobe Experience Platform의 새로운 기능에 대한 정보가 포함되어 있습니다 [!DNL Privacy Service], 향상된 기능 및 중요한 버그 수정.

>[!NOTE]
>
>다른 사용자에 대한 최신 릴리스 노트 [!DNL Experience Platform] 서비스를 찾을 수 있습니다. [여기](../release-notes/latest/latest.md).

## 2020년 9월 9일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| LGPD 지원(브라질) | 이제 브라질이 개인 정보 보호 작업을 만들 수 있습니다 [!DNL Lei Geral de Proteção de Dados] (LGPD) 규정. 이러한 직업은 규정 규정에 따라 추적된다 `lgpd_bra`. |

## 2020년 4월 8일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | [!DNL Privacy] 이제 태국 내 개인 정보 보호법(PDPA)에 따라 요청을 만들고 추적할 수 있습니다. API에서 개인 정보 요청을 수행할 때 `regulation` array는 &quot;pdpa_tha&quot; 값을 허용합니다. |
| UI의 네임스페이스 유형 | 이제 [!DNL Privacy Service] UI. 자세한 내용은 [사용 안내서](ui/user-guide.md) 추가 정보. |
| 이전 끝점 사용 중단 | 이전 API 엔드포인트(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

## 2020년 1월 14일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| [!DNL Privacy Service] 리브랜딩 | 이전에 &quot;GDPR Service&quot;라고 이름이 변경된 사용자가 [!DNL Privacy Service] 서비스는 GDPR 외에도 다른 규정을 지원하도록 성장했습니다. |
| 새 API 엔드포인트 | 의 기본 경로 [!DNL Privacy Service] API가 `/data/privacy/gdpr` to `/data/core/privacy/jobs` |
| 새로운 필수 `regulation` 속성 | 에서 새 작업을 만들 때 [!DNL Privacy Service] API, a `regulation` 작업을 추적할 규칙을 나타내려면 요청 페이로드에서 속성을 제공해야 합니다. 허용되는 값은 다음과 같습니다 `gdpr` 및 `ccpa`. 다음 문서를 참조하십시오. [개인 정보 보호 작업](api/privacy-jobs.md) 에서 [!DNL Privacy Service] 자세한 내용은 API 안내서 를 참조하십시오. |
| Adobe Primetime 인증 지원 | [!DNL Privacy Service] 이제 에서는 다음 방법으로 Adobe Primetime 인증에서 액세스/삭제 요청을 허용합니다 `primetimeAuthentication` 를 제품 값으로 채우는 방법을 설명합니다. 자세한 내용은 [Primetime 인증 설명서](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) 추가 정보. |

### 개선 사항

* [!DNL Privacy Service] UI 개선 사항:
   * GDPR 및 CCPA 규정에 대한 별도의 작업 추적 페이지.
   * 새로 만들기 *규정 유형* 드롭다운을 사용하여 GDPR과 CCPA에 대한 추적 데이터 간을 전환할 수 있습니다.

## 2019년 7월 25일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| 요청 지표 대시보드 | 의 새 지표 대시보드 [!DNL Privacy Service] UI는 제출, 오류 발생 및 완료된 GDPR 요청에 대한 가시성을 제공합니다. |
| 요청 빌더 | GDPR 요청을 제출하는 기술 및 비기술 사용자를 모두 보유한 조직을 서비스하기 위해 UI에 &quot;요청 만들기&quot; 기능이 추가되었습니다. JSON 파일 제출 기능은 여전히 [!DNL Privacy Service] UI를 계속 사용하길 원하는 조직의 경우 |
| GDPR 작업 이벤트 알림 | GDPR 작업 상태에 대한 이벤트 알림은 많은 워크플로우에 중요한 요소입니다. 개별 전자 메일 알림을 사용하여 이전에 알림을 제공했지만 GDPR 이벤트 알림은 Adobe I/O 이벤트를 활용하는 메시지이며, 이 알림은 작업 요청 자동화를 위해 구성된 웹 후크에 전송됩니다. [!DNL Privacy Service] UI 사용자는 Adobe I/O GDPR 이벤트에 가입하여 제품 또는 GDPR 작업이 완료되면 업데이트를 받을 수 있습니다. |

## 2019년 4월 18일

### 개선 사항

* 의 상태 테이블에 대한 기본 범위 [!DNL Privacy Service] UI가 7일 범위로 수정되었습니다.
* 내부 예외 처리가 향상되었습니다.
* 데이터 변경률이 낮은 일반적인 내부 호출에 캐싱을 도입하여 성능이 향상되었습니다.

### 버그 수정

* 에 대한 필터링된 쿼리에 대한 누락된 로깅 정보를 추가했습니다. `GET /` 의 엔드포인트 [!DNL Privacy Service] API.

## 2019년 4월 11일

### 개선 사항

* 베타 고객을 위한 새로운 기능을 지원하도록 UI가 업데이트되었습니다
* 베타에서 UI 2.0 기능을 지원하는 새로운 지표 API

## 2019년 4월 9일

### 개선 사항

* 모든 조회(GET) API 호출이 기본적으로 30일 전환 확인 범위로 업데이트되었습니다
* 최대 전환 확인 범위를 갖도록 제한된 API 사용

## 2019년 2월 14일

### 개선 사항

* 를 `include` 모든 POST 제출의 필드.
* 를 `include` JSON을 업로드할 때 필드를 생성합니다.

### 버그 수정

* 고객이 를 로드할 수 없는 문제가 해결되었습니다. [!DNL Privacy Service] UI.
