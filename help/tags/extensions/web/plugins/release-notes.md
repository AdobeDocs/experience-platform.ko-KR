---
title: 일반 Analytics 플러그인 확장 프로그램에 대한 릴리스 노트
description: Adobe Experience Platform의 일반 Analytics 플러그인 태그 확장에 대한 최신 릴리스 노트입니다.
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 1be361f9cd70b0424542af64a994da0b21d6b5dc
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 56%

---

# 일반 Analytics 플러그인 릴리스 노트

## 2022년 6월 03일

### 일반 Analytics 플러그인 확장 프로그램 3.0.7

#### 기능

쿠키를 설정하는 플러그인은 이제 보안 플래그를 사용합니다

## 2021년 6월 23일

### 일반 Analytics 플러그인 확장 프로그램 3.0.6

#### 버그 수정

* 특수 문자를 사용할 때 getPercentPageViewed가 중단되는 문제가 해결되었습니다.

## 2021년 5월 20일

### 일반 Analytics 플러그인 확장 프로그램 3.0.5

#### 버그 수정

* 일반 초기화 작업을 사용할 때 getTimeParting이 올바르게 초기화되지 않는 문제가 해결되었습니다.

## 2021년 3월 26일

### 일반 Analytics 플러그인 확장 프로그램 3.0.4

#### 버그 수정

* 창 개체에서 getPageLoadTime이 변수를 잘못 설정하는 문제가 해결되었습니다.
* queryParam가 쿼리 문자열에 없는 경우 getQueryParam이 &quot;&quot; 대신 undefined를 반환하는 문제가 수정되었습니다
* 초기화 작업에서 잘못된 버전 번호가 표시되는 문제가 해결되었습니다.

## 2021년 3월 19일

### 일반 Analytics 플러그인 확장 프로그램 3.0.2

#### 기능

* 버전 정보를 컨텍스트 데이터로 자동으로 포함하도록 업데이트된 모든 플러그인
* getPercentPageViewed 플러그인을 추가했습니다.
* 다음 플러그인에 대한 데이터 요소가 추가되었습니다
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* 업데이트된 스타일

## 2020년 4월 9일

### 일반 Analytics 플러그인 확장 프로그램 2.2.0

#### 버그 수정

* 확장 프로그램 보기의 문구가 수정되었습니다.

#### 기능

* 초기화 작업에서 설명서가 업데이트되었습니다.

## 2019년 12월 5일

### 일반 Analytics 플러그인 확장 프로그램 2.1.1

#### 버그 수정

* 이전 버전 2.0.X와 호환되지 않는 문제가 해결되었습니다.
* 설명서 링크가 잘못된 설명서를 가리켰던 문제가 해결되었습니다.
* 초기화 작업에서 `getTimeSinceLastVisit`가 두 번 표시되는 문제가 해결되었습니다.

## 2019년 11월 15일

### 일반 Analytics 플러그인 확장 프로그램 2.1.0

#### 버그 수정

* 이전 버전과의 호환성을 지원하기 위해 개별 플러그인 작업이 다시 도입되었습니다.
* `cleanStr` 플러그인의 문제가 해결되었습니다.
* `getResponsiveLayout` 플러그인의 문제가 해결되었습니다.
* `getPageName` 플러그인의 문제가 해결되었습니다.

#### 기능

* `getTimeParting` 버전 업데이트
* `numberSuite` 버전 업데이트
* `getNewRepeat` 버전 업데이트
* 모든 플러그인에 대한 설명서가 업데이트되었습니다.

## 2019년 10월 30일

### 일반 Analytics 플러그인 확장 프로그램 2.0.3

#### 버그 수정

* 설명서 링크가 끊어진 문제가 해결되었습니다.

## 2019년 10월 11일

### 일반 Analytics 플러그인 확장 프로그램 2.0.2

#### 기능

* 확장 프로그램에 15개의 플러그인이 추가되었습니다.
* 더욱 편리해진 구현을 지원하기 위해 새로운 초기화 작업이 만들어졌습니다.

## 2019년 7월 11일

### 일반 Analytics 플러그인 확장 프로그램 1.0.4

#### 기능

* 확장 프로그램 7개의 플러그인과 함께 릴리스되었습니다.
* 각 플러그인을 초기화하는 개별 작업
