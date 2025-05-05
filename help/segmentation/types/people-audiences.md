---
solution: Experience Platform
title: 사용자 대상
description: 사용자 대상을 사용하여 사용자를 타깃팅하는 방법에 대해 알아봅니다.
source-git-commit: d73f8c47f9eedff05446688f0c798c322e51aa5d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# People 대상 안내서

Adobe Experience Platform에서 사용자 기반 대상을 사용하면 마케팅 캠페인에 대한 특정 사용자 그룹을 타깃팅할 수 있습니다.

사용자 대상은 고객 프로필 데이터를 사용하여 특정 시장을 타깃팅하므로 광고하려는 특정 인구 통계를 더 잘 타깃팅할 수 있습니다.

## 용어 {#terminology}

인물 대상을 시작하기 전에 다양한 대상 유형 간의 차이점을 검토하십시오.

- **계정 대상**: 계정 대상은 **계정** 프로필 데이터를 사용하여 만든 대상입니다. 계정 프로필 데이터를 사용하여 다운스트림 계정 내에서 사용자를 타겟팅하는 대상을 만들 수 있습니다. 계정 대상에 대한 자세한 내용은 [계정 대상 개요](./account-audiences.md)를 참조하십시오.
- **사용자 대상**: 사용자 대상은 **고객** 프로필 데이터를 사용하여 만든 대상입니다. 고객 프로필 데이터를 사용하여 비즈니스 고객을 타겟팅하는 대상을 만들 수 있습니다.
- **잠재 고객 대상**: 잠재 고객은 **잠재 고객** 프로필 데이터를 사용하여 만든 대상입니다. Prospect 프로필 데이터를 사용하여 인증되지 않은 사용자로부터 대상을 만들 수 있습니다. 잠재 고객에 대한 자세한 내용은 [잠재 고객 개요](./prospect-audiences.md)를 참조하십시오.

## 액세스 {#access}

인물 대상에 액세스하려면 **[!UICONTROL 고객]** 섹션에서 **[!UICONTROL 대상]**&#x200B;을(를) 선택하십시오.

![고객 섹션에서 대상자 탭이 강조 표시되어 있습니다.](../images/types/people/select-audiences.png)

대상 포털이 표시되고 조직에 대한 모든 사람 대상 목록이 표시됩니다.

![사람 대상의 대상 포털이 표시됩니다.](../images/types/people/people-audiences.png)

이 보기에는 이름, 프로필 수, 원본, 라이프사이클 상태, 만든 날짜 및 마지막으로 업데이트한 날짜 등 대상에 대한 정보가 나열됩니다.

또한 검색 및 필터링 기능을 사용하여 특정 계정 대상을 신속하게 검색하고 정렬할 수 있습니다. 이 기능에 대한 자세한 내용은 [Audience Portal 개요](../ui/audience-portal.md#manage-audiences)를 참조하십시오.

## 대상자 세부 정보 {#details}

특정 인물 대상에 대한 세부 정보를 보려면 대상자 포털에서 대상을 선택하십시오.

![지정된 대상이 Audience Portal에서 강조 표시됩니다.](../images/types/people/select-audience.png)

대상자 세부 사항 페이지가 표시됩니다. 설명, 원본 및 라이프사이클 상태를 포함한 정보가 표시됩니다.

![대상 세부 정보 페이지가 표시되어 사람 대상에 대한 정보를 표시합니다.](../images/types/people/audience-details.png)

대상 세부 정보 페이지에 대한 자세한 내용은 Audience Portal 개요[&#128279;](../ui/audience-portal.md#audience-details)의 대상 세부 정보 섹션을 참조하십시오.

## 대상자 만들기 {#create}

대상 작성기 또는 세그먼트 빌더를 사용하여 사람 대상을 만들 수 있습니다. 대상자 만들기를 시작하려면 대상자 포털에서 대상자 만들기를 선택합니다.

![대상자 만들기 단추가 강조 표시됩니다.](../images/types/people/select-create-audience.png)

대상자를 작성할지 규칙을 작성할지 선택할 수 있는 팝오버가 표시됩니다.

![작성 및 대상자와 작성 규칙 중에서 선택할 수 있는 팝오버가 표시됩니다.](../images/types/people/create-audience-popover.png)

대상자 만들기에 대한 자세한 내용은 [대상자 포털 개요](../ui/audience-portal.md#create-audience)를 참조하십시오.

## 대상자 활성화 {#activate}

사용자 대상을 만든 후 이 대상을 다른 다운스트림 서비스로 활성화할 수 있습니다.

활성화할 대상을 선택한 다음 **[!UICONTROL 대상에 활성화]**&#x200B;를 선택합니다.

![빠른 작업 메뉴 아래에 [대상에 활성화] 단추가 강조 표시되어 있습니다.](../images/types/people/activate-to-destination.png)

대상의 업데이트 빈도에 따라 사용 가능한 대상 목록이 포함된 [!UICONTROL 대상 활성화] 페이지가 나타납니다. 활성화 프로세스에 대한 자세한 내용은 [활성화 개요](../../destinations/ui/activation-overview.md)를 참조하십시오.

## 다음 단계

이 안내서를 읽고 나면 Adobe Experience Platform에서 사용자 대상을 만들고 관리하는 방법을 이해할 수 있습니다. 다양한 대상자 유형에 대해 알아보려면 [대상자 유형 개요](./overview.md)를 읽어 보십시오.
