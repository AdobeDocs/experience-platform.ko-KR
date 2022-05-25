---
title: 데이터 위생 작업 주문 찾아보기
description: Adobe Experience Platform 사용자 인터페이스에서 기존 데이터 위생 작업 순서를 보고 관리하는 방법을 알아봅니다.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 18ef55a084ced8c26e583598f9016dd9f4741153
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 데이터 위생 작업 주문 찾아보기

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="작업 순서 ID"
>abstract="시스템에 데이터 위생 요청이 전송되면 요청된 작업을 실행하기 위한 작업 순서가 생성됩니다. 즉, 작업 순서는 현재 상태 및 기타 관련 세부 사항을 포함하는 특정 데이터 위생 프로세스를 나타냅니다. 각 작업 순서는 작성 시 자동으로 고유한 ID가 할당됩니다. 자세한 내용은 데이터 위생 UI 안내서를 참조하십시오."

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 Healthcare용 Adobe Shield를 구입한 조직에서만 사용할 수 있습니다.

시스템에 데이터 위생 요청이 전송되면 요청된 작업을 실행하기 위한 작업 순서가 생성됩니다. 작업 순서는 현재 상태 및 기타 관련 세부 정보를 포함하는 특정 데이터 위생 프로세스(예: 소비자 데이터 삭제)를 나타냅니다.

이 안내서에서는 Adobe Experience Platform UI에서 기존 작업 지시를 보고 관리하는 방법을 다룹니다.

## 기존 작업 지시 목록 및 필터링

처음 액세스할 때 **[!UICONTROL 데이터 위생]** 작업 공간 의 경우, 기존 작업 주문 목록이 기본 세부 정보와 함께 표시됩니다.

![이미지를 보여주는 이미지 [!UICONTROL 데이터 위생] 플랫폼 UI의 작업 영역](../images/ui/browse/work-order-list.png)

목록에는 한 번에 하나의 카테고리에 대한 작업 주문만 표시됩니다. 선택 **[!UICONTROL 소비자]** 소비자 삭제 작업 목록을 보려면 **[!UICONTROL 데이터 집합]** 데이터 세트에 대한 TTL(time-to-live) 일정 목록을 보려면 을 클릭합니다.

![이미지를 보여주는 이미지 [!UICONTROL 데이터 집합] 탭](../images/ui/browse/dataset-tab.png)

단계 아이콘( )을 선택합니다![단계 아이콘 이미지](../images/ui/browse/funnel-icon.png))을 클릭하여 표시된 작업 주문에 대한 필터 목록을 확인합니다.

![표시된 작업 순서 필터의 이미지](../images/ui/browse/filters.png)

보고 있는 탭에 따라 다양한 필터를 사용할 수 있습니다.

| 필터 | 카테고리 | 설명 |
| --- | --- | --- |
| [!UICONTROL 상태] | [!UICONTROL 소비자] &amp; [!UICONTROL 데이터 집합] | 작업 순서의 현재 상태에 따라 필터링합니다. |
| [!UICONTROL 만든 날짜] | [!UICONTROL 소비자] | 소비자 삭제 요청이 수행된 시기를 기준으로 필터링합니다. |
| [!UICONTROL 만든 날짜] | [!UICONTROL 데이터 세트] | 소비자 삭제 요청이 수행된 시기를 기준으로 필터링합니다. |
| [!UICONTROL 삭제 날짜] | [!UICONTROL 데이터 세트] | TTL이 예약한 삭제 날짜를 기준으로 필터링합니다. |
| [!UICONTROL 업데이트 날짜] | [!UICONTROL 데이터 세트] | 데이터 집합 TTL이 마지막으로 업데이트된 시기를 기준으로 필터링합니다. TTL 만들기 및 기간은 업데이트로 계산됩니다. |

{style=&quot;table-layout:auto&quot;}

## 작업 주문의 세부 정보 보기

나열된 작업 주문의 ID를 선택하여 해당 상세내역을 확인합니다.

![선택한 작업 순서 ID를 보여주는 이미지](../images/ui/browse/select-work-order.png)

선택한 작업 순서의 유형에 따라 다양한 정보와 컨트롤이 제공됩니다. 이러한 내용은 아래 섹션에서 다룹니다.

### 소비자 삭제 세부 사항

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

소비자 삭제 요청의 세부 사항은 읽기 전용이며, 현재 상태 및 요청이 수행된 이후 경과된 시간과 같은 기본 속성을 표시합니다.

![소비자 삭제 작업 순서에 대한 세부 정보 페이지를 표시하는 이미지](../images/ui/browse/consumer-delete-details.png)

### 데이터 집합 TTL 세부 정보

데이터 집합 TTL의 세부 정보 페이지에서는 삭제가 발생하기 전 남은 날짜의 예약된 만료 날짜를 포함하여 기본 속성에 대한 정보를 제공합니다. 오른쪽 레일에서 컨트롤을 사용하여 TTL을 편집하거나 취소할 수 있습니다.

![데이터 집합 TTL 작업 순서에 대한 세부 정보 페이지를 보여주는 이미지](../images/ui/browse/ttl-details.png)

## 다음 단계

이 안내서에서는 Platform UI에서 기존 데이터 위생 작업 순서를 보고 관리하는 방법을 다룹니다. 고유한 작업 주문 생성에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [소비자 삭제](./delete-consumer.md)
* [데이터 세트 TTL 예약](./ttl.md)
