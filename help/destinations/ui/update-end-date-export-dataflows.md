---
title: 데이터 세트 내보내기 데이터 흐름의 종료 날짜 업데이트(2025년 5월 1일까지 필요한 작업)
type: Tutorial
hide: true
hidefromtoc: true
description: 현재 종료 날짜를 2025년 5월 1일로 설정하여 데이터 세트 내보내기 데이터 흐름의 종료 날짜를 업데이트하는 방법을 알아봅니다.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 데이터 세트 내보내기 데이터 흐름의 종료 날짜 업데이트(2025년 5월 1일까지 필요한 작업)

>[!IMPORTANT]
>
>이 페이지의 작업 항목은 조직이 Experience Platform의 2024년 9월 릴리스 이전에 데이터 세트 내보내기 데이터 흐름을 설정한 경우 적용됩니다.

## 현재 상황

Experience Platform의 [2024년 9월 릴리스](/help/release-notes/latest/latest.md#destinations)에서는 데이터 세트 데이터 흐름 내보내기에 대한 `endTime` 날짜를 설정하는 옵션을 도입했습니다. Adobe은 또한 2024년 9월 릴리스 전에 *생성된 모든 데이터 세트 내보내기 데이터 흐름에 대해 기본 종료 날짜를 2025년 5월 1일로 도입했습니다*. 이러한 데이터 흐름은 현재 아래에 표시된 것과 유사한 메시지를 표시합니다.

내보내기 데이터 집합 데이터 흐름의 종료 날짜를 업데이트해야 한다는 UI 알림 ![1&rbrace;](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**작업 항목**: 이러한 데이터 흐름의 경우 만료되기 전에 종료 날짜를 수동으로 업데이트해야 합니다. 그렇지 않으면 내보내기가 중지됩니다. Experience Platform UI를 사용하여 2025년 5월 1일에 중지하도록 설정된 데이터 흐름을 식별합니다.

## 나에게 알림을 보내는 이유

조직은 2025년 5월 1일 종료 날짜가 포함된 활성 데이터 세트 내보내기 데이터 흐름이 있는 것으로 식별되었습니다.

## UI를 사용하여 종료 날짜 업데이트

Experience Platform UI를 사용하여 종료 날짜가 2025년 5월 1일인 데이터 흐름을 식별하고 향후 날짜로 업데이트합니다.

### 업데이트가 필요한 데이터 흐름 찾기

아래와 같이 **대상 > 찾아보기**(으)로 이동하여 **데이터 형식** 열에서 데이터 형식 **데이터 집합**&#x200B;을(를) 찾습니다. 원하는 데이터 흐름을 선택하여 검사합니다.

![데이터 집합 내보내기 데이터 흐름이 찾아보기 탭에서 강조 표시되었습니다.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### 데이터 흐름의 종료 날짜 업데이트

데이터 흐름의 종료 날짜를 업데이트하려면:

1. 이전 단계에서 검사하기 위해 선택한 데이터 흐름에서 **데이터 세트 내보내기**&#x200B;를 선택합니다.
   ![찾아보기 탭에서 강조 표시된 데이터 세트 내보내기 컨트롤입니다.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. 워크플로우에서 **예약** 단계로 진행하고 **일정 편집**&#x200B;을 선택합니다.
   ![예약 단계에서 강조 표시된 예약 컨트롤을 편집합니다.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. 2025년 5월 1일 이후에 원하는 종료 날짜를 선택하고 **저장**&#x200B;을 선택하세요.
   ![예약 단계에서 강조 표시된 종료 날짜 컨트롤을 선택하십시오.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. 워크플로우 끝으로 이동하고 업데이트를 저장합니다.

예약 단계에 대한 자세한 내용은 [데이터 세트 내보내기 UI 자습서](/help/destinations/api/export-datasets.md#scheduling)를 참조하십시오.

## API를 사용하여 종료 날짜 업데이트

### 업데이트가 필요한 데이터 흐름 찾기

### 데이터 흐름의 종료 날짜 업데이트
