---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 릴리스 정보
description: Adobe Experience Platform Privacy Service에 대한 최신 릴리스 정보입니다.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# [!DNL Privacy Service] 릴리스 정보

이 문서에는 Adobe Experience Platform [!DNL Privacy Service]의 새로운 기능에 대한 정보와 개선 사항, 중요한 버그 수정 사항이 포함되어 있습니다.

>[!NOTE]
>
>기타 [!DNL Experience Platform] 서비스에 대한 최신 릴리스 정보는 [여기](../release-notes/latest/latest.md)에서 확인할 수 있습니다.

## 2020년 9월 9일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| LGPD 지원 (브라질) | 이제 브라질 [!DNL Lei Geral de Proteção de Dados] (LGPD) 규정에 따라 개인정보 보호 관련 작업을 만들 수 있습니다. 이러한 작업은 규정 코드 `lgpd_bra`에 따라 추적됩니다. |

## 2020년 4월 8일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국의 개인정보 보호법(PDPA)에 따라 [!DNL Privacy] 요청을 생성하고 추적할 수 있습니다. API에서 개인정보 보호 요청을 할 때 `regulation` 배열은 “pdpa_tha” 값을 허용합니다. |
| UI의 네임스페이스 유형 | 이제 [!DNL Privacy Service] UI의 Request Builder에서 다양한 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용 안내서](ui/user-guide.md)를 확인하십시오. |
| 이전 엔드포인트 사용 중단 | 이전 API 엔드포인트(`data/privacy/gdpr`)는 더 이상 사용되지 않습니다. |

## 2020년 1월 14일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| [!DNL Privacy Service] 리브랜딩 | 이전 명칭인 “GDPR 서비스”는 GDPR 외에도 다른 규정을 지원하도록 서비스가 확대됨에 따라 [!DNL Privacy Service]로 이름이 변경되었습니다. |
| 새로운 API 엔드포인트 | [!DNL Privacy Service] API의 기본 경로가 `/data/privacy/gdpr`에서 `/data/core/privacy/jobs`로 업데이트되었습니다. |
| 새로운 필수 `regulation` 속성 | [!DNL Privacy Service] API에서 새로운 작업을 만들 때 요청 페이로드에 작업을 추적할 규정을 나타내는 `regulation` 속성을 제공해야 합니다. 허용되는 값은 `gdpr` 및 `ccpa`입니다. 자세한 내용은 [!DNL Privacy Service] API 안내서의 [개인정보 보호 작업](api/privacy-jobs.md)에 대한 문서를 참조하십시오. |
| Adobe Primetime 인증 지원 | 이제 [!DNL Privacy Service]는 Adobe Primetime 인증에서 `primetimeAuthentication`을 제품 값으로 사용하여 액세스/삭제 요청을 수락합니다. 자세한 내용은 [Primetime 인증 설명서](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)를 참조하십시오. |

### 개선 사항

* [!DNL Privacy Service] UI 개선 사항:
   * GDPR 및 CCPA 규정에 따른 별도의 작업 추적 페이지를 추가했습니다.
   * GDPR과 CCPA에 대한 추적 데이터를 전환할 수 있는 새로운 *규정 유형* 드롭다운을 추가했습니다.

## 2019년 7월 25일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| 요청 지표 대시보드 | [!DNL Privacy Service] UI의 새로운 지표 대시보드는 제출된 GDPR 요청, 오류가 발생한 GDPR 요청 및 완료된 GDPR 요청에 대한 가시성을 제공합니다. |
| Request Builder | 기술 전문가인 사용자와 기술 전문가가 아닌 사용자 모두 GDPR 요청을 제출하는 조직에 서비스를 제공하기 위해 UI에 “요청 만들기” 기능이 추가되었습니다. JSON 파일 제출 기능을 계속 사용하고자 하는 조직은 [!DNL Privacy Service] UI에서 사용할 수 있습니다. |
| GDPR 작업 이벤트 알림 | GDPR 작업 상태에 대한 이벤트 알림은 많은 워크플로에 중요한 요소입니다. 이전에는 개별 이메일 알림을 통해 알림이 제공된 반면 GDPR 이벤트 알림은 Adobe I/O 이벤트를 활용한 메시지로, 작업 요청 자동화를 용이하게 하는 구성된 웹 후크로 전송됩니다. [!DNL Privacy Service] UI 사용자는 Adobe I/O GDPR 이벤트를 구독하면 제품이나 GDPR 작업이 완료될 때 업데이트를 받을 수 있습니다. |

## 2019년 4월 18일

### 개선 사항

* [!DNL Privacy Service] UI의 상태 테이블에 대한 기본 범위를 7일로 수정했습니다.
* 내부 예외 처리를 개선했습니다.
* 데이터 변경 속도가 느린 일반적인 내부 호출에 캐싱을 도입하여 성능을 개선했습니다.

### 버그 수정

* [!DNL Privacy Service] API의 `GET /` 엔드포인트에 대한 필터링된 쿼리에 대해 누락된 로깅 정보를 추가했습니다.

## 2019년 4월 11일

### 개선 사항

* Beta 고객을 위한 새로운 기능을 지원하기 위해 UI를 업데이트했습니다.
* Beta에서 UI 2.0 기능을 지원하기 위한 새로운 지표 API를 추가했습니다.

## 2019년 4월 9일

### 개선 사항

* 모든 조회(GET) API 호출의 전환 기간 기본값을 30일로 업데이트했습니다.
* 최대 전환 기간 범위가 45일이 되도록 API 사용을 제한했습니다.

## 2019년 2월 14일

### 개선 사항

* 모든 POST 제출에 `include` 필드를 적용합니다.
* JSON 업로드 시 `include` 필드를 적용합니다.

### 버그 수정

* 고객이 [!DNL Privacy Service] UI를 로드할 수 없는 문제를 해결했습니다.
