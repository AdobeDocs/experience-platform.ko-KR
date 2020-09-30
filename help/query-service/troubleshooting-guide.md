---
keywords: Experience Platform;home;popular topics;query service;Query service;troubleshooting guide;faq;troubleshooting;
solution: Experience Platform
title: Adobe Experience Platform 쿼리 서비스 문제 해결 가이드
topic: troubleshooting
description: 이 문서에는 사용자가 경험하는 일반적인 오류 코드와 가능한 원인에 대한 정보가 포함되어 있습니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---


# 오류 및 문제 해결

## REST API 오류

| HTTP 상태 코드 | 설명 | 가능한 원인 |
| ---------------- | ----------- | --------------- |
| 400 | 잘못된 요청 | 형식이 잘못되었거나 잘못된 쿼리 |
| 401 | 인증 실패 | 잘못된 인증 토큰 |
| 500 | 내부 서버 오류 | 내부 시스템 오류 |

## PostgreSQL API 오류

| 오류 코드 및 연결 상태 | 설명 | 가능한 원인 |
| ------------------------------- | ----------- | -------------- |
| **28P01** 시작 - 인증 | 잘못된 암호 | 잘못된 인증 토큰 |
| **28000** 시작 - 인증 | 잘못된 인증 유형 | 인증 유형이 잘못되었습니다. 틀림없어 `AuthenticationCleartextPassword`. |
| **42P12** 시작 - 인증 | 테이블을 찾을 수 없음 | 사용할 테이블을 찾을 수 없습니다. |
| **42601** 쿼리 | 구문 오류 | 명령 또는 구문 오류가 잘못되었습니다. |
| **58000** 쿼리 | 시스템 오류 | 내부 시스템 오류 |
| **42P01** 쿼리 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다. |
| **42P07** 쿼리 | 테이블이 있습니다. | 이름이 같은 테이블이 이미 있습니다(테이블 만들기). |
| **53400** 쿼리 | LIMIT가 최대값을 초과합니다. | 사용자가 100,000보다 높은 LIMIT 절을 지정했습니다. |
| **53400** 쿼리 | 문 시간 초과 | 제출된 실시간 진술은 최대 10분 이상 소요되었습니다. |
| **08P01** 해당 사항 없음 | 지원되지 않는 메시지 유형 | 지원되지 않는 메시지 유형 |
