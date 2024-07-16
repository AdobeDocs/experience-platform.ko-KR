---
title: 데이터 라이프사이클 작업 주문 찾아보기
description: Adobe Experience Platform 사용자 인터페이스에서 기존 데이터 라이프사이클 작업 주문을 보고 관리하는 방법을 알아봅니다.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 27%

---

# 데이터 라이프사이클 작업 주문 검색 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="작업 주문 ID"
>abstract="데이터 라이프사이클 요청이 시스템으로 전송되면 작업 주문이 생성되어 요청된 작업을 실행합니다. 즉, 작업 주문은 현재 상태와 기타 관련 세부 정보가 포함된 특정 데이터 라이프사이클 프로세스를 나타냅니다. 생성 시 각 작업 주문에 고유 ID가 자동으로 할당됩니다."
>text="See the data lifecycle UI guide to learn more."

데이터 라이프사이클 요청이 시스템으로 전송되면 작업 주문이 생성되어 요청된 작업을 실행합니다. 작업 주문은 현재 상태 및 기타 관련 세부 정보를 포함하는 특정 데이터 라이프사이클 프로세스(예: 예약된 데이터 세트 만료)를 나타냅니다.

이 안내서에서는 Adobe Experience Platform UI에서 기존 작업 주문을 보고 관리하는 방법을 다룹니다.

## 기존 작업 주문 나열 및 필터링

UI에서 **[!UICONTROL 데이터 수명 주기]** 작업 영역에 처음 액세스하면 기본 세부 정보와 함께 기존 작업 주문 목록이 표시됩니다.

![Platform UI에서 [!UICONTROL 데이터 라이프사이클] 작업 영역을 표시하는 이미지](../images/ui/browse/work-order-list.png)

목록에는 한 번에 한 범주에 대한 작업 주문만 표시됩니다. 레코드 삭제 작업 목록을 보려면 **[!UICONTROL 소비자]**&#x200B;를 선택하고, 예약된 데이터 세트 만료 목록을 보려면 **[!UICONTROL 데이터 세트]**&#x200B;를 선택하십시오.

![[!UICONTROL 데이터 집합] 탭을 표시하는 이미지](../images/ui/browse/dataset-tab.png)

단계 아이콘(![단계 아이콘 이미지](../images/ui/browse/funnel-icon.png))을 선택하여 표시된 작업 주문에 대한 필터 목록을 확인합니다.

![표시된 작업 순서 필터의 이미지](../images/ui/browse/filters.png)

보고 있는 작업 주문 유형에 따라 다양한 필터 옵션을 사용할 수 있습니다.

### 레코드 삭제 필터

다음 필터는 삭제 요청을 기록하는 데 적용됩니다.

| 필터 | 설명 |
| --- | --- |
| [!UICONTROL 상태] | 작업 주문의 현재 상태를 기반으로 필터링:<ul><li>**[!UICONTROL 완료]**: 작업이 완료되었습니다.</li><li>**[!UICONTROL 실패]**: 작업에 오류가 발생하여 완료할 수 없습니다.</li><li>**[!UICONTROL 처리 중]**: 요청이 시작되었으며 현재 처리 중입니다.</li></ul> |
| [!UICONTROL 만든 날짜] | 작업 순서가 지정된 시간을 기준으로 필터링합니다. |
| [!UICONTROL 업데이트 날짜] | 작업 주문이 마지막으로 업데이트된 날짜를 기준으로 필터링합니다. 생성은 업데이트로 계산됩니다. |

### 데이터 세트 만료 필터

데이터 세트 만료 요청에는 다음 필터가 적용됩니다.

| 필터 | 설명 |
| --- | --- |
| [!UICONTROL 상태] | 작업 주문의 현재 상태를 기반으로 필터링:<ul><li>**[!UICONTROL 완료]**: 작업이 완료되었습니다.</li><li>**[!UICONTROL 보류 중]**: 작업이 만들어졌지만 아직 실행되지 않았습니다. [데이터 집합 만료 요청](./dataset-expiration.md)은(는) 예약된 삭제 날짜 이전에 이 상태를 가정합니다. 삭제 날짜가 되면 작업이 미리 취소되지 않는 한 상태가 [!UICONTROL 실행 중](으)로 업데이트됩니다.</li><li>**[!UICONTROL 실행 중]**: 데이터 세트 만료 요청이 시작되었으며 현재 처리 중입니다.</li><li>**[!UICONTROL 취소됨]**: 수동 사용자 요청의 일부로 작업이 취소되었습니다.</li></ul> |
| [!UICONTROL 만든 날짜] | 작업 순서가 지정된 시간을 기준으로 필터링합니다. |
| [!UICONTROL 만료 날짜] | 해당 데이터 세트에 대해 예약된 삭제 날짜를 기준으로 데이터 세트 만료 요청을 필터링합니다. |
| [!UICONTROL 업데이트 날짜] | 작업 주문이 마지막으로 업데이트된 날짜를 기준으로 필터링합니다. 생성 및 만료는 업데이트로 계산됩니다. |

{style="table-layout:auto"}

## 작업 주문의 세부 정보 보기 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="서비스별 상태"
>abstract="데이터 라이프사이클 요청은 여러 Experience Platform 서비스에서 독립적으로 처리됩니다. 이 섹션에서는 각 해당 서비스에 대한 요청의 현재 처리 상태에 대해 간략히 소개합니다. 자세한 내용은 데이터 라이프사이클 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="ID 수"
>abstract="이 작업 주문의 일부로 요청된 레코드를 업데이트하거나 삭제할 수 있는 ID 수입니다. 카운터에 포함된 ID는 해당 데이터 세트에 실제로 존재할 필요는 없습니다. 자세한 내용은 데이터 라이프사이클 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="레코드 삭제 응답"
>abstract="레코드 삭제 프로세스가 시스템에서 응답을 수신하면 해당 메시지가 **[!UICONTROL 결과]** 섹션 아래에 표시됩니다. 작업 주문이 처리되는 동안 문제가 발생하는 경우 이 섹션에 관련 오류 메시지가 표시되면 문제를 해결하는 데 도움이 됩니다. 자세한 내용은 데이터 라이프사이클 UI 안내서를 참조하십시오."

나열된 작업 주문의 ID를 선택하여 세부 정보를 확인합니다.

![작업 주문 ID를 선택하고 있는 이미지](../images/ui/browse/select-work-order.png)

선택한 작업 주문 유형에 따라 다른 정보와 제어 기능이 제공됩니다. 이러한 내용은 아래 섹션에 설명되어 있습니다.

### 삭제 세부 정보 기록 {#record-delete}

레코드 삭제 요청의 세부 정보에는 현재 상태와 요청이 수행된 이후 경과된 시간이 포함됩니다. 각 요청에는 삭제와 관련된 각 다운스트림 서비스의 개별 상태 세부 정보를 제공하는 **[!UICONTROL 서비스별 상태]** 섹션도 포함됩니다. 오른쪽 레일에서 컨트롤을 사용하여 작업 주문의 이름과 설명을 업데이트할 수 있습니다.

![레코드 삭제 작업 순서에 대한 세부 정보 페이지를 표시하는 이미지](../images/ui/browse/record-delete-details.png)

### 데이터 세트 만료 세부 정보 {#dataset-expiration}

데이터 세트 만료에 대한 세부 정보 페이지에서는 삭제하기 전까지 남은 일수의 예약된 만료 날짜를 포함하여 해당 기본 속성에 대한 정보를 제공합니다. 오른쪽 레일에서 컨트롤을 사용하여 만료를 편집하거나 취소할 수 있습니다.

![데이터 집합 만료 작업 순서에 대한 세부 정보 페이지를 표시하는 이미지](../images/ui/browse/ttl-details.png)

## 다음 단계

이 안내서에서는 Platform UI에서 기존 데이터 라이프사이클 작업 주문을 보고 관리하는 방법을 다룹니다. 고유한 작업 주문 생성에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [데이터 세트 만료 관리](./dataset-expiration.md)
* [레코드 삭제 관리](./record-delete.md)
