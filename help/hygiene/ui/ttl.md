---
title: 데이터 집합 TTL 관리
description: Adobe Experience Platform UI에서 데이터 세트에 대한 TTL(Time to Live)을 예약하는 방법을 알아봅니다.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 데이터 집합 TTL 관리

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 Healthcare Shield를 구입한 조직에서만 사용할 수 있습니다.

다음 [[!UICONTROL 데이터 위생] 작업 영역](./overview.md) Adobe Experience Platform UI에서 데이터 세트에 대한 TTL(Time to Live)을 예약할 수 있습니다.

이 문서에서는 Platform UI에서 데이터 세트 TTL을 예약하고 관리하는 방법을 다룹니다.

## TTL 예약

새 요청을 만들려면 **[!UICONTROL 요청 만들기]** 작업 공간의 기본 페이지에서 을 참조하십시오.

![이미지를 보여주는 이미지 [!UICONTROL 요청 만들기] 선택한 단추](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### 날짜 및 데이터 세트 선택

요청 만들기 대화 상자가 나타납니다. 아래에 **[!UICONTROL 작업]** 섹션에서 데이터 세트를 삭제할 날짜를 선택합니다. 수동으로 날짜를 입력할 수 있습니다(형식) `mm/dd/yyyy`) 또는 달력 아이콘( )을 선택합니다![달력 아이콘 이미지](../images/ui/ttl/calendar-icon.png)) 을 클릭하여 대화 상자에서 날짜를 선택합니다.

![TTL에 대해 설정되는 만료 날짜를 보여주는 이미지](../images/ui/ttl/select-date.png)

다음, 아래 **[!UICONTROL 데이터 집합 세부 정보]**&#x200B;데이터베이스 아이콘( )을 선택합니다.![데이터베이스 아이콘 이미지](../images/ui/ttl/database-icon.png))를 클릭하여 데이터 세트 선택 대화 상자를 엽니다. TTL을 적용할 목록에서 데이터 세트를 선택한 다음 을 선택합니다 **[!UICONTROL 완료]**.

![선택한 데이터 세트를 보여주는 이미지](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>현재 샌드박스에 속하는 데이터 세트만 표시됩니다.

### 요청 제출

데이터 세트와 TTL 날짜를 선택한 후에는 을 선택합니다 **[!UICONTROL 제출]**.

![이미지를 보여주는 이미지 [!UICONTROL 제출] 선택한 단추](../images/ui/ttl/submit.png)

데이터 세트가 삭제되는 날짜를 확인하는 메시지가 표시됩니다. 선택 **[!UICONTROL 제출]** 계속하십시오.

요청이 제출되면 작업 순서가 만들어지고 의 기본 탭에 표시됩니다 [!UICONTROL 데이터 위생] 작업 공간. 여기에서 요청을 처리할 때 작업 주문의 상태를 모니터링할 수 있습니다.

## TTL 편집 또는 취소

TTL을 편집하거나 취소하려면, **[!UICONTROL 데이터 집합]** workspace의 기본 페이지에서 를 선택하고 목록에서 TTL을 선택합니다.

TTL의 세부 사항 페이지에서 오른쪽 레일에 예약된 삭제를 편집하거나 취소할 컨트롤이 표시됩니다.

## 다음 단계

이 문서에서는 Experience Platform UI에서 데이터 세트 TTL을 예약하는 방법을 다룹니다. 데이터 위생 API를 사용하여 데이터 세트 TTL을 예약하는 방법에 대해 알아보려면 [dataset TTL 끝점 안내서](../api/ttl.md).
