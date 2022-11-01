---
title: 데이터 위생 작업 주문 찾아보기
description: Adobe Experience Platform 사용자 인터페이스에서 기존 데이터 위생 작업 순서를 보고 관리하는 방법을 알아봅니다.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# 데이터 위생 작업 주문 찾아보기 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="작업 순서 ID"
>abstract="시스템에 데이터 위생 요청이 전송되면 요청된 작업을 실행하기 위한 작업 순서가 생성됩니다. 즉, 작업 순서는 현재 상태 및 기타 관련 세부 사항을 포함하는 특정 데이터 위생 프로세스를 나타냅니다. 각 작업 순서는 작성 시 자동으로 고유한 ID가 할당됩니다."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 구입한 조직에만 사용할 수 있습니다 **Adobe 의료 보호** 또는 **Adobe 개인 정보 보호 및 보안 차단**.

시스템에 데이터 위생 요청이 전송되면 요청된 작업을 실행하기 위한 작업 순서가 생성됩니다. 작업 순서는 예약된 데이터 세트 만료와 같은 특정 데이터 위생 프로세스를 나타냅니다. 여기에는 현재 상태 및 기타 관련 세부 정보가 포함됩니다.

이 안내서에서는 Adobe Experience Platform UI에서 기존 작업 지시를 보고 관리하는 방법을 다룹니다.

## 기존 작업 지시 목록 및 필터링

처음 액세스할 때 **[!UICONTROL 데이터 위생]** 작업 공간 의 경우, 기존 작업 주문 목록이 기본 세부 정보와 함께 표시됩니다.

![이미지를 보여주는 이미지 [!UICONTROL 데이터 위생] 플랫폼 UI의 작업 영역](../images/ui/browse/work-order-list.png)

목록에는 한 번에 하나의 카테고리에 대한 작업 주문만 표시됩니다. 선택 **[!UICONTROL 소비자]** 소비자 삭제 작업 목록을 보려면 **[!UICONTROL 데이터 집합]** 예약된 데이터 세트 만료 목록을 보려면

![이미지를 보여주는 이미지 [!UICONTROL 데이터 집합] 탭](../images/ui/browse/dataset-tab.png)

단계 아이콘( )을 선택합니다![단계 아이콘 이미지](../images/ui/browse/funnel-icon.png))을 클릭하여 표시된 작업 주문에 대한 필터 목록을 확인합니다.

![표시된 작업 순서 필터의 이미지](../images/ui/browse/filters.png)

보고 있는 작업 순서 유형에 따라 다양한 필터 옵션을 사용할 수 있습니다.

### 소비자 삭제 필터

다음 필터는 소비자 삭제 요청에 적용됩니다.

| 필터 | 설명 |
| --- | --- |
| [!UICONTROL 상태] | 작업 순서의 현재 상태에 따라 필터링합니다.<ul><li>**[!UICONTROL 완료됨]**: 작업이 완료되었습니다.</li><li>**[!UICONTROL 실패]**: 작업에서 오류가 발생하여 완료할 수 없습니다.</li><li>**[!UICONTROL 처리 중]**: 요청이 시작되어 현재 처리 중입니다.</li></ul> |
| [!UICONTROL 만든 날짜] | 작업 순서가 수행된 시기를 기준으로 필터링합니다. |
| [!UICONTROL 업데이트 날짜] | 작업 순서가 마지막으로 업데이트된 시점을 기준으로 필터링합니다. 생성은 업데이트로 계산됩니다. |

### 데이터 집합 만료 필터

다음 필터는 데이터 세트 만료 요청에 적용됩니다.

| 필터 | 설명 |
| --- | --- |
| [!UICONTROL 상태] | 작업 순서의 현재 상태에 따라 필터링합니다.<ul><li>**[!UICONTROL 완료됨]**: 작업이 완료되었습니다.</li><li>**[!UICONTROL 보류 중]**: 작업이 생성되었지만 아직 실행되지 않았습니다. A [데이터 세트 만료 요청](./dataset-expiration.md) 은 예약된 삭제 날짜 이전에 이 상태를 가정합니다. 삭제 날짜가 되면 상태가 로 업데이트됩니다 [!UICONTROL 실행 중] 작업을 미리 취소하지 않는 한.</li><li>**[!UICONTROL 실행 중]**: 데이터 집합 만료 요청이 시작되었으며 현재 처리 중입니다.</li><li>**[!UICONTROL 취소됨]**: 수동 사용자 요청의 일부로 작업이 취소되었습니다.</li></ul> |
| [!UICONTROL 만든 날짜] | 작업 순서가 수행된 시기를 기준으로 필터링합니다. |
| [!UICONTROL 만료 날짜] | 해당 데이터 세트에 대한 예약된 삭제 날짜를 기반으로 데이터 세트 만료 요청을 필터링합니다. |
| [!UICONTROL 업데이트 날짜] | 작업 순서가 마지막으로 업데이트된 시점을 기준으로 필터링합니다. 생성과 만료는 업데이트로 계산됩니다. |

{style=&quot;table-layout:auto&quot;}

## 작업 주문의 세부 정보 보기 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="서비스별 상태"
>abstract="데이터 위생 요청은 여러 Experience Platform 서비스에서 독립적으로 처리됩니다. 이 섹션에서는 각 서비스에 대한 요청의 현재 처리 상태에 대해 설명합니다. 자세한 내용은 데이터 위생 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="ID 수"
>abstract="이 작업 순서의 일부로 삭제되도록 요청한 ID 수입니다. 개수에 포함된 ID가 영향을 받는 데이터 세트에 반드시 존재하지 않을 수 있습니다. 자세한 내용은 데이터 위생 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="소비자 삭제 응답"
>abstract="소비자 삭제 프로세스가 시스템에서 응답을 받으면 이러한 메시지가 **[!UICONTROL 결과]** 섹션을 참조하십시오. 작업 순서가 처리되는 동안 문제가 발생하면 이 섹션에 관련 오류 메시지가 표시되어 문제를 해결하는 데 도움이 됩니다. 자세한 내용은 데이터 위생 UI 안내서를 참조하십시오."

나열된 작업 주문의 ID를 선택하여 해당 상세내역을 확인합니다.

![선택한 작업 순서 ID를 보여주는 이미지](../images/ui/browse/select-work-order.png)

선택한 작업 순서의 유형에 따라 다양한 정보와 컨트롤이 제공됩니다. 이러한 내용은 아래 섹션에서 다룹니다.

### 소비자 삭제 세부 사항 {#consumer-delete}

소비자 삭제 요청의 세부 사항에는 현재 상태와 요청이 수행된 이후 경과된 시간이 포함됩니다. 각 요청에는 또한 **[!UICONTROL 서비스별 상태]** 삭제와 관련된 각 다운스트림 서비스에 대한 개별 상태 세부 정보를 제공하는 섹션입니다. 오른쪽 레일에서 컨트롤을 사용하여 작업 순서의 이름과 설명을 업데이트할 수 있습니다.

![소비자 삭제 작업 순서에 대한 세부 정보 페이지를 표시하는 이미지](../images/ui/browse/consumer-delete-details.png)

### 데이터 집합 만료 세부 정보 {#dataset-expiration}

데이터 세트 만료에 대한 세부 정보 페이지에서는 삭제가 발생하기 전 남은 날짜에 예약된 만료 날짜를 포함하여 기본 속성에 대한 정보를 제공합니다. 오른쪽 레일에서 컨트롤을 사용하여 만료를 편집하거나 취소할 수 있습니다.

![데이터 집합 만료 작업 순서에 대한 세부 정보 페이지를 표시하는 이미지](../images/ui/browse/ttl-details.png)

## 다음 단계

이 안내서에서는 Platform UI에서 기존 데이터 위생 작업 순서를 보고 관리하는 방법을 다룹니다. 고유한 작업 주문 생성에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [데이터 집합 만료 관리](./dataset-expiration.md)
* [소비자 삭제 관리](./delete-consumer.md)
