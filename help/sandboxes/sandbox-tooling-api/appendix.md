---
title: 샌드박스 도구 API 안내서 부록
description: 이 문서에서는 샌드박스 도구 API 작업과 관련된 추가 정보를 제공합니다.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# 샌드박스 API 안내서 부록

이 문서에서는 [!DNL Sandbox] API 작업과 관련된 추가 정보를 제공합니다.

## 쿼리 매개 변수 사용 {#query}

샌드박스 도구 API는 패키지를 나열할 때 쿼리 매개 변수를 사용하여 페이지를 매기고 결과를 필터링할 수 있도록 지원합니다.

>[!NOTE]
>
>`limit`을(를) 전달하고 개별적으로 시작할 수 있습니다.

| 매개변수 | 설명 |
| --- | --- |
| `limit` | 응답에서 반환할 최대 레코드 수입니다. 기본 제한은 20입니다. |
| `start` | 하위 세트 항목 목록이 시작되어야 하는 시작입니다. |
| `targetSandbox` | 아티팩트를 가져올 샌드박스 이름을 나타냅니다. |
| `jobType` | 작업 유형. 이 값은 `NEW`, `RESUME` 또는 `ROLLBACK`일 수 있습니다. |
| `jobStatus` | 작업의 상태입니다. 이 값은 `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` 또는 `CANCELLED`일 수 있습니다. |
| `requestType` | 요청 유형. 이 값은 `EXPORT`, `IMPORT` 또는 `COPY`일 수 있습니다. |
| `expiryPeriod` | 이 사용자가 지정한 기간은 패키지가 게시된 시점부터 패키지 만료 날짜(일)를 정의합니다. 이 값은 음수가 아니어야 합니다. 기본값은 업데이트 또는 게시 API가 호출된 시점부터 90일입니다. |
| `packageType` | 패키지의 유형입니다. 이 값은 `PARTIAL` 또는 `FULL`일 수 있습니다. |
| `status` | 패키지의 상태입니다. 이 값은 `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` 또는 `PUBLISH_FAILED`일 수 있습니다. |
