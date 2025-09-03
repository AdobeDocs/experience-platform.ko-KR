---
title: Adobe Content Analytics 확장 기능 릴리스 노트
description: Adobe Experience Platform의 Content Analytics 태그 확장 기능에 대한 최신 릴리스 정보입니다.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 77d19ab813f881cd3c48c27ed4a9ac02e268e23f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Adobe Content Analytics 확장 릴리스 노트

다음은 Content Analytics 태그 확장에 대한 릴리스 노트 목록입니다.

| 버전 | Date | 문제 해결 |
|---|---|---|
| 1.0.48 | 2025년 8월 25일 | <ul><li>문서의 그림자 루트 DOM 요소 내에 자산 추적에 대한 지원을 추가합니다.</li></ul> |
| 1.0.47 | 2025년 7월 23일 | <ul><li>경험이 활성화되지 않아 경험에 대한 정규 표현식 검사가 실패하는 경우 발생하는 버그를 수정했습니다. 이 문제로 인해 Content Analytics 데이터가 수집되지 않았습니다.</li><li>Experience Cloud에 기본 언어가 설정되지 않은 일부 사용자에 대해 태그 UI가 표시되지 않는 기본 언어 설정 문제를 해결했습니다.</li></ul> |
| 1.0.46 | 2025년 6월 18일 | <ul><li>프로덕션 데이터 스트림이 없는 경우 확장 구성을 저장하려고 할 때 알림 메시지가 추가되었습니다.</li><li>대신 문자화된 페이로드 콘텐츠를 콘솔에 배치하여 Content Analytics 페이로드의 가시성 문제를 일시적으로 해결했습니다.</li><li>확장 UI에 현지화 지원이 추가되었습니다.</li><li>확장 UI 콘텐츠 주위에 추가 패딩이 발생하는 CSS 문제를 부분적으로 수정했습니다.</li></ul> |
| 1.0.45 | 2025년 4월 14일 | <ul><li>페이지 보기 이벤트를 기다리는 동안 Content Analytics 이벤트 유지와 관련된 구성 설정에서 여러 버그가 해결되었습니다. 이제 Content Analytics은 기본적으로 첫 번째 페이지 보기 이벤트가 발생할 때까지 이벤트 실행을 기다립니다.</li></ul> |
| 1.0.44 | 2025년 3월 31일 | <ul><li>AppMeasurement 통합의 첫 번째 반복.</li><li>이 버전은 아직 특정 요청(예: 페이지 보기 수) 필터링을 지원하지 않지만, 향후 업데이트에서 이 기능을 추가할 수 있습니다. 현재 페이지에 있는 첫 번째 AppMeasurement 인스턴스를 사용합니다.</li></ul> |
| 1.0.43 | 2025년 3월 10일 | <ul><li>초기 확장 릴리스.</li></ul> |
