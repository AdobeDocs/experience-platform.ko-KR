---
title: Adobe Target 확장 기능 릴리스 노트
description: Adobe Experience Platform의 Adobe Target 태그 확장 기능에 대한 최신 릴리스 정보입니다.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 70%

---

# Adobe Target 릴리스 노트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

## 2021년 9월 16일

### Adobe Target 확장 0.11.4

* at.js v1.8.3으로 업데이트됨
* 쿠키를 설정할 때 `SameSite=None` 및 `Secure` 특성이 추가됨

## 2020년 7월 24일

### Adobe Target 확장 0.11.3

* 스크립트나 코드가 `default` 속성을 `window` 또는 `document`에 추가할 때 확장에 실패하는 경우 버그를 수정했습니다

## 2020년 6월 15일

### Adobe Target 확장 0.11.2

* at.js 1.x에서 서버 도메인을 잘못 만들어 Target 요청이 실패하는 CNAME 및 Edge Override를 사용할 때 발생하는 문제가 해결되었습니다.

## 2020년 3월 25일

### Adobe Target 확장 0.11.1

* at.js가 v1.8.1로 업데이트되었습니다
* 매개 변수 및 페이지 로드 매개 변수가 올바르게 처리되지 않는 문제가 해결되었습니다.

## 2019년 10월 10일

### Adobe Target 확장 0.11.0

* at.js가 v1.8로 업데이트되었습니다.
* ECID(Experience Cloud ID 라이브러리) v4.4와 at.js 1.8 간의 통합을 위해 성능이 향상되었습니다.
* 이전에는 at.js가 경험을 가져오기 전에 ECID 라이브러리가 두 개의 차단 호출을 생성했습니다. 이는 단일 호출로 감소하여 성능이 크게 향상되었습니다.

>[!NOTE]
>Adobe Experience Platform용 ECID 태그 확장을 v4.4.1로 업그레이드하여 향상된 성능을 이용해 보십시오.

## 2019년 7월 31일

### Adobe Target 확장 0.10.1

* Adobe Target용 태그 확장을 처리하는 매개 변수에 대한 핫픽스

## 2019년 5월 4일

### Adobe Target 확장 0.10.0

* 최신 Google Chrome 변경으로 인해 발생한 데이터 요소 문제가 해결되었습니다.

## 2019년 3월 14일

### Adobe Target 확장 0.9.3

* at.js 1.7.1을 사용할 확장 버전이 업데이트되었습니다.

## 2019년 2월 20일

### Adobe Target 확장 0.9.2

* Target과 Analytics 확장 간의 경합 상태가 수정되었습니다.

## 2019년 2월 12일

### Adobe Target 확장 0.9.1

#### **기능**

* 태그를 통해 옵트인 개인 정보 보호 기능이 지원되는 at.js 1.7.0을 사용하여 Target 태그가 실행되는 방법과 시기를 제어할 수 있도록 확장이 업데이트되었습니다. 옵트인 구현 설정 방법에 대한 태그 설명서를 확인하십시오. 빈 값이 있는 mbox 매개 변수를 Target으로 보내야 하는지 여부를 사용자 지정할 수 있는 가능성이 추가되었습니다.

## 2019년 1월 23일

### Adobe Target 확장 0.8.4

* at.js가 버전 1.6.4로 업데이트되었습니다.
* 확장 UI가 Adobe Spectrum으로 마이그레이션되었습니다.

## 2018년 11월 15일

### Adobe Target 확장 0.8.2

* at.js가 버전 1.6.3으로 업데이트되었습니다.

## 2018년 10월 24일

### Adobe Target 확장 0.8.1

* at.js가 버전 1.6.2로 업데이트되었습니다.

## 2018년 8월 23일

### Adobe Target 확장 0.8.0

* at.js가 버전 1.6.0으로 업데이트되었습니다.

## 2018년 8월 10일

### Adobe Target 확장 0.7.2

* 부분 변경 사항
* `extension.json` 파일에서 `exchangeUrl` 속성이 업데이트되었습니다.

## 2018년 8월 1일

### Adobe Target 확장 0.7.1

* 사소한 수정 사항

## 2018년 6월 18일

### Adobe Target 확장 0.7.0

* at.js 버전이 1.5.0으로 업데이트되었습니다.
* IE 11의 Media Optimizer에서 null 참조 오류가 발생한 문제가 해결되었습니다.

## 2018년 6월 15일

### Adobe Target 확장 0.6.0

#### **기능**

* Target 확장이at.js v1.3.1을 사용하도록 업데이트되었습니다. Analytics와 함께 Target을 배포할 때 이제 모든 Target 호출이 확인될 때까지(리디렉션 오퍼 포함) 기다렸다가 Analytics가 실행되므로 이전에 존재했던 경합 상태가 해결됩니다.

## 2018년 2월 22일

### Adobe Target 확장 0.4.1

#### **기능**

* Adobe Exchange 목록이 extension.json에 추가되었습니다.
* Target이 비활성화되고 Authoring이 활성화되어 있는지에 대한 확인이 추가되었습니다.

#### **버그 수정**

* 태그를 통해 배포될 때 시각적 경험 작성기가 페이지 숨김을 취소하지 못하는 Adobe Target 확장 의 오류를 수정했습니다.

## 2018년 2월 8일

### Adobe Target 확장 0.4.0

#### **기능**

* 확장 구성 화면에서 보기가 업데이트되었습니다.
* at.js가 버전 1.2.3으로 업데이트되었습니다(JSON 오퍼에 대한 지원 추가).
