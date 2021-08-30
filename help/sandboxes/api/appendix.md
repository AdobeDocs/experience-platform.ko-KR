---
keywords: Experience Platform;홈;인기 항목;api;API;샌드박스;샌드박스;샌드박스
solution: Experience Platform
title: 샌드박스 API 안내서 부록
description: 이 문서에서는 Sandbox API 작업과 관련된 추가 정보를 제공합니다.
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# 샌드박스 API 안내서 부록

이 문서에서는 [!DNL Sandbox] API 작업과 관련된 추가 정보를 제공합니다.

## 쿼리 매개 변수 사용 {#query}

[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)에서는 샌드박스를 나열할 때 쿼리 매개 변수를 페이지 및 필터 결과에 사용할 수 있습니다.

>[!NOTE]
>
>`limit` 및 `offset` 쿼리 매개 변수를 함께 지정해야 합니다. 하나만 지정하면 API에 오류가 반환됩니다. 없음을 지정하면 기본 제한은 50이고 오프셋은 0입니다.

| 매개 변수 | 설명 |
| --- | --- |
| `limit` | 응답에서 반환될 최대 레코드 수입니다. |
| `offset` | 응답 목록을 시작(오프셋)할 첫 번째 레코드의 엔티티 수입니다. |
