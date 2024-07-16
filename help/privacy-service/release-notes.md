---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 릴리스 노트
description: Adobe Experience Platform Privacy Service에 대한 최신 릴리스 정보입니다.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# [!DNL Privacy Service] 릴리스 노트

이 문서에는 Adobe Experience Platform [!DNL Privacy Service]의 새로운 기능과 개선 사항 및 중요 버그 수정에 대한 정보가 포함되어 있습니다.

>[!NOTE]
>
>다른 [!DNL Experience Platform] 서비스에 대한 최신 릴리스 정보는 [여기](../release-notes/latest/latest.md)에서 찾을 수 있습니다.

## 2020년 9월 9일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| LGPD(브라질) 지원 | 이제 브라질의 [!DNL Lei Geral de Proteção de Dados](LGPD) 규정에 따라 개인 정보 보호 작업을 만들 수 있습니다. 이러한 작업은 규정 코드 `lgpd_bra`에 따라 추적됩니다. |

## 2020년 4월 8일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국의 PDPA(개인 정보 보호법)에 따라 [!DNL Privacy]개의 요청을 만들고 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열에서 &quot;pdpa_tha&quot; 값을 허용합니다. |
| UI의 네임스페이스 유형 | 이제 [!DNL Privacy Service] UI의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용 안내서](ui/user-guide.md)를 참조하세요. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

## 2020년 1월 14일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| [!DNL Privacy Service] 리브랜딩 | 서비스가 GDPR 외에 다른 규정을 지원하도록 확장됨에 따라 이전에 &quot;GDPR 서비스&quot;라고 했던 이름이 [!DNL Privacy Service](으)로 새롭게 브랜딩되었습니다. |
| 새 API 엔드포인트 | [!DNL Privacy Service] API의 기본 경로가 `/data/privacy/gdpr`에서 `/data/core/privacy/jobs`(으)로 업데이트되었습니다. |
| 새 필수 `regulation` 속성 | [!DNL Privacy Service] API에서 새 작업을 만들 때 작업을 추적할 규정을 나타내려면 요청 페이로드에 `regulation` 속성을 제공해야 합니다. 허용되는 값은 `gdpr` 및 `ccpa`입니다. 자세한 내용은 [!DNL Privacy Service] API 안내서의 [개인 정보 작업](api/privacy-jobs.md)에 대한 문서를 참조하십시오. |
| Adobe Primetime 인증 지원 | [!DNL Privacy Service]이(가) 이제 `primetimeAuthentication`을(를) 제품 값으로 사용하여 Adobe Primetime 인증에서 액세스/삭제 요청을 수락합니다. 자세한 내용은 [Primetime 인증 설명서](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)를 참조하세요. |

### 개선 사항

* [!DNL Privacy Service] UI 개선 사항:
   * GDPR 및 CCPA 규정에 대한 별도의 작업 추적 페이지입니다.
   * GDPR과 CCPA에 대한 추적 데이터 간을 전환하는 새로운 *규정 유형* 드롭다운입니다.

## 2019년 7월 25일

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| 요청 지표 대시보드 | [!DNL Privacy Service] UI의 새 지표 대시보드는 제출되고 오류가 발생하고 완료된 GDPR 요청에 대한 가시성을 제공합니다. |
| 요청 빌더 | 기술 사용자와 비기술 사용자가 모두 GDPR 요청을 제출하는 서비스 조직의 경우, &quot;요청 만들기&quot; 기능이 UI에 추가되었습니다. JSON 파일 제출 기능은 [!DNL Privacy Service] UI에서 계속 사용할 수 있습니다. |
| GDPR 작업 이벤트 알림 | GDPR 작업 상태에 대한 이벤트 알림은 많은 워크플로우에서 중요한 요소입니다. 이전에는 개별 이메일 알림을 사용하여 알림이 제공되었지만 GDPR 이벤트 알림은 Adobe I/O 이벤트를 활용하는 메시지이며, 이는 작업 요청 자동화를 용이하게 하는 구성된 웹후크로 전송됩니다. [!DNL Privacy Service] UI 사용자는 제품 또는 GDPR 작업이 완료되면 Adobe I/O GDPR 이벤트에 가입하여 업데이트를 받을 수 있습니다. |

## 2019년 4월 18일

### 개선 사항

* [!DNL Privacy Service] UI의 상태 테이블에 대한 기본 범위가 7일 범위로 수정되었습니다.
* 내부 예외 처리가 향상되었습니다.
* 데이터 변경률이 낮은 일반적인 내부 호출에 대한 캐싱을 도입하여 성능이 향상되었습니다.

### 버그 수정

* [!DNL Privacy Service] API에서 `GET /` 끝점에 대해 필터링된 쿼리에 대해 누락된 로깅 정보가 추가되었습니다.

## 2019년 4월 11일

### 개선 사항

* Beta 고객을 위한 새로운 기능을 지원하도록 UI가 업데이트되었습니다
* Beta의 UI 2.0 기능을 지원하는 새로운 지표 API

## 2019년 4월 9일

### 개선 사항

* 모든 조회(GET) API 호출이 기본적으로 30일 전환 확인 범위로 업데이트되었습니다
* 최대 전환 확인 기간이 45일로 제한되어 있는 API 사용

## 2019년 2월 14일

### 개선 사항

* 모든 POST 제출에 `include` 필드를 적용합니다.
* JSON을 업로드할 때 `include` 필드를 적용하십시오.

### 버그 수정

* 고객이 [!DNL Privacy Service] UI를 로드할 수 없는 문제를 해결했습니다.
