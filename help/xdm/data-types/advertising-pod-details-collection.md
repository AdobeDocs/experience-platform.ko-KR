---
title: Advertising Pod 세부 정보 수집 데이터 유형
description: Advertising Pod Details Collection XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Advertising Pod 세부 정보] 컬렉션 데이터 형식

[!UICONTROL Advertising Pod Details] 컬렉션은 표준 XDM(Experience Data Model) 데이터 형식입니다. 일반적으로 콘텐츠 브레이크 중에 연속적으로 재생되는 광고 시퀀스 또는 그룹을 정의합니다. [!UICONTROL Advertising Pod Details] 컬렉션 데이터 형식을 사용하여 광고 브레이크 ID, 광고 브레이크에 대한 친숙한 이름, 브레이크 내의 광고 인덱스 및 콘텐츠의 타임라인 내에서 광고 브레이크의 오프셋(초) 등의 세부 정보를 캡처합니다.

![Advertising Pod 세부 정보 수집 데이터 형식의 다이어그램입니다.](../images/data-types/advertising-pod-details-collection.png)

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Pod의 광고 위치] | `index` | 정수 | 예 | 상위 광고 브레이크 시작 내에 있는 광고의 색인입니다. |
| [!UICONTROL Pod 알기 쉬운 이름] | `friendlyName` | 문자열 | 아니요 | 쉽게 이해할 수 있는 광고 브레이크 이름입니다. |
| [!UICONTROL Pod 오프셋] | `offset` | 정수 | 예 | 콘텐츠 내부의 광고 브레이크 오프셋(초). |
