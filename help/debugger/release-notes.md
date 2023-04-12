---
title: Adobe Experience Platform Debugger 릴리스 노트
description: Adobe Experience Platform Debugger에 대한 최신 릴리스 정보입니다.
keywords: debugger;experience Platform Debugger 확장 프로그램;chrome;확장 프로그램;릴리스 정보
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 4%

---

# Adobe Experience Platform Debugger 릴리스 노트

## 버전 1.4.0 - 2022년 10월 3일

* 웹 SDK 하이브리드 구현에 대한 AEP Assurance 디버깅 지원이 추가되었습니다.
* 동일한 AEP Assurance 세션 내에 여러 탭에 대한 지원이 추가되었습니다.
* 로그인한 후 사용자가 프로필/조직을 전환할 수 없는 문제가 해결되었습니다.
   * 일부 계정의 경우 조직을 전환하려면 로그아웃하고 다시 로그인해야 합니다.
* Target 추적을 활성화하지 못할 때 오류 메시지가 추가되었습니다.
* 종속성이 업데이트되었습니다.

## 버전 1.3.3 - 2022년 6월 20일

* 네트워크 이벤트 테이블에서 팝업을 열 수 없는 문제를 수정했습니다.
* 온페이지 합금 정보를 로드할 수 없는 문제를 해결했습니다.

## 버전 1.3.2 - 2022년 6월 9일

* 사용자가 로그인하면 기본 아바타가 추가되었습니다.
* 로그의 JSON 개체에 구문 강조를 추가했습니다.

## 버전 1.3.1 - 2022년 5월 24일

* 종속성이 업데이트되었습니다.
* 사후 프로세스 히트를 활성화할 수 없는 Analytics 문제가 해결되었습니다.
* 디버거가 Adobe 로그인 창에 첨부되는 문제가 해결되었습니다.
* 로그 메시지가 디버거에 표시되지 않는 AT.js 문제가 해결되었습니다.

## 버전 1.3.0 - 2022년 1월 28일

* 현재 릴리스 버전 및 노트를 보여주는 정보 링크가 추가되었습니다.
* Analytics 요청에 대해 처리된 후 히트를 보기 위한 전환을 추가했습니다. 토글은 Analytics 섹션에서 사용할 수 있습니다.
* 세션이 디버거 외부에서 닫혔을 때 발생하는 원격 디버깅 세션 문제가 해결되었습니다.
* 웹 SDK Edge 트랜잭션 탭에 표시되는 오류 알림을 수정했습니다.
* 디버거가 _satellite 개체에 액세스할 때 페이지 사용 중단 경고의 Adobe 태그가 수정되었습니다.
* 페이지에서 AppMeasurement 인스턴스를 찾을 수 없는 일부 사례를 수정했습니다.
* 디버거 창을 처음 열 때 발생하는 페이지 연결 문제를 해결했습니다.

## 버전 1.2.0 - 2021년 10월 26일

* 네트워크 보기에 있는 모든 브라우저 탭의 이벤트를 표시합니다. 현재 탭에서 이벤트만 보려면 디버거의 오른쪽 아래 모서리에 있는 잠금 아이콘을 선택하십시오.
* 브랜딩을 업데이트했습니다.

## 버전 1.1.0 - 2021년 10월 5일

* 원격 디버깅 시각화 - 원격 디버깅 이벤트를 Adobe Experience Platform Web SDK > Edge 트랜잭션 섹션에서 시각적 플로우 차트로 구성합니다.
* 새 원격 디버깅 세션을 시작할 때 페이지에서 사용되는 Adobe Experience Platform Web SDK 조직이 로그인한 조직과 일치해야 합니다.
* 연결된 탭에 대한 에지 트랜잭션만 표시합니다. Target 추적 로그는 여전히 로그 > 에지 섹션에서 사용할 수 있습니다.
* 페이지에서 Adobe Experience Platform Web SDK의 각 인스턴스에 대해 별도의 데이터 스트림 ID 구성 무시를 허용합니다. 디버그 추가 사용 전환.
* Adobe Experience Platform Web SDK용 원격 디버깅 세션에서 Adobe Target 추적 토큰이 항상 전송되지 않는 문제를 해결했습니다.

## 버전 1.0.0 2021년 5월 5일

* Experience Platform 디버거의 첫 번째 주 릴리스입니다. Experience Cloud Debugger을 대체하기 위한 것입니다.
