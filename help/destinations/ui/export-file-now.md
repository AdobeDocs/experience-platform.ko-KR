---
title: Experience Platform UI를 사용하여 주문형 파일을 배치 대상으로 내보내기
type: Tutorial
description: Experience Platform UI를 사용하여 주문형 파일을 배치 대상으로 내보내는 방법을 알아봅니다.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: d3bd76f5b36b6a6afcb67fe923eb8e4f3d7a9415
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 9%

---


# Experience Platform UI를 사용하여 주문형 파일을 배치 대상으로 내보내기

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

## **[!UICONTROL 지금 파일 내보내기]** 개요 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="지금 파일 내보내기"
>abstract="이 컨트롤을 선택하여 이전에 예약된 내보내기와 전체 파일 내보내기를 게재합니다. 파일 내보내기가 즉시 트리거되어 Experience Platform 세분화 실행에서 최신 결과를 선택합니다."

이 문서에서는 Experience Platform UI를 사용하여 주문형 파일을 [클라우드 저장소](/help/destinations/catalog/cloud-storage/overview.md) 및 [이메일 마케팅](/help/destinations/catalog/email-marketing/overview.md) 대상과 같은 배치 대상으로 내보내는 방법에 대해 설명합니다.

**[!UICONTROL 지금 파일 내보내기]** 컨트롤을 사용하면 이전에 예약된 대상자의 현재 내보내기 일정을 중단하지 않고 전체 파일을 내보낼 수 있습니다. 이 내보내기는 이전에 예약한 내보내기 외에 추가로 수행되며 대상자의 내보내기 빈도는 변경되지 않습니다. 파일 내보내기가 즉시 트리거되어 Experience Platform 세분화 실행에서 최신 결과를 선택합니다.

이러한 목적으로 Experience Platform API를 사용할 수도 있습니다. 임시 활성화 API를 통해 [주문형 대상을 일괄 대상으로 활성화](/help/destinations/api/ad-hoc-activation-api.md)하는 방법을 읽어 보십시오.

## 전제 조건 {#prerequisites}

주문형 파일을 일괄 처리 대상으로 내보내려면 대상에 성공적으로 [연결](./connect-destination.md)해야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)(으)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 온디맨드로 파일을 내보내는 방법 {#how-to-export-files-on-demand}

1. **[!UICONTROL 연결 > 대상]**(으)로 이동하고 **[!UICONTROL 찾아보기]** 탭과 필터 기호를 선택하여 원하는 배치 대상에 대한 기존 연결을 표시합니다.

   ![검색 탭으로 이동하여 기존 데이터 흐름을 필터링하는 방법을 강조 표시하는 이미지](../assets/ui/activate-on-demand/browse-tab.png)

2. 원하는 대상 연결을 선택하여 대상에 대한 기존 데이터 흐름을 검사합니다.

   ![필터링된 데이터 흐름을 강조 표시하는 이미지](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. **[!UICONTROL 활성화 데이터]** 탭을 선택하고 필요 시 파일을 내보낼 대상을 선택한 다음 **[!UICONTROL 지금 파일 내보내기]** 컨트롤을 선택하여 선택한 각 대상에 대한 파일을 배치 대상으로 전달하는 일회성 내보내기를 트리거합니다.

   ![지금 파일 내보내기 단추를 강조 표시하는 이미지](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. 파일 내보내기를 확인하고 트리거하려면 **[!UICONTROL 예]**&#x200B;를 선택하십시오.

   ![지금 파일 내보내기 확인 대화 상자를 표시하는 이미지입니다.](../assets/ui/activate-on-demand/confirm-activation.png)

5. 파일 내보내기가 시작되었음을 알리는 확인 메시지가 나타납니다.

   ![임시 활성화 성공 확인을 보여 주는 이미지](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. **[!UICONTROL 데이터 흐름 실행]** 탭으로 전환하여 파일 내보내기가 시작되었는지 확인할 수도 있습니다.

## 고려 사항 {#considerations}

**[!UICONTROL 지금 파일 내보내기]** 컨트롤을 사용할 때는 다음 사항을 고려해야 합니다.

* **[!UICONTROL 지금 파일 내보내기]**&#x200B;는 배치 활성화 데이터 흐름의 일정이 현재 날짜와 겹치는 대상자에 대해서만 작동합니다. 여기에는 종료 날짜(**[!UICONTROL Once]**&#x200B;의 내보내기 빈도)가 없거나 종료 날짜가 아직 지나지 않은 일정이 있는 대상자가 포함됩니다.
* 기존 데이터 흐름에 대상을 추가할 때 **[!UICONTROL 지금 파일 내보내기]** 컨트롤을 사용하기 전에 **1시간**&#x200B;이상 기다리십시오.
* 대상자의 병합 정책을 변경하거나 새 병합 정책을 사용하는 대상자를 만드는 경우 **[!UICONTROL 지금 파일 내보내기]** 컨트롤을 사용할 때까지 24시간 대기하십시오.

## UI 오류 메시지 {#ui-error-messages}

**[!UICONTROL 지금 파일 내보내기]** 컨트롤을 사용하는 경우 아래 나열된 오류 메시지가 표시될 수 있습니다. 표가 표시될 때 이를 처리하는 방법을 이해하려면 표를 검토하십시오.

| 오류 메시지 | 해결 방법 |
|---------|----------|
| 실행 ID가 `flow run ID`인 주문 `dataflow ID`의 대상 `segment ID`에 대해 이미 실행 중입니다. | 이 오류 메시지는 대상에 대해 현재 임시 활성화 흐름이 진행 중임을 나타냅니다. 활성화 작업을 다시 트리거하기 전에 작업이 완료될 때까지 기다립니다. |
| 대상 `<segment name>`이(가) 이 데이터 흐름의 일부가 아니거나 일정 범위를 벗어났습니다. | 이 오류 메시지는 활성화하기 위해 선택한 대상이 데이터 흐름에 매핑되지 않았거나 대상에 대해 설정된 활성화 일정이 만료되었거나 아직 시작되지 않았음을 나타냅니다. 대상이 데이터 흐름에 실제로 매핑되었는지 확인하고 대상 활성화 일정이 현재 날짜와 겹치는지 확인합니다. |

## 관련 정보 {#related-information}

* [Experience Platform API를 사용하여 대상을 온디맨드로 일괄 처리할 수 있도록 활성화](/help/destinations/api/ad-hoc-activation-api.md)
* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](/help/destinations/ui/activate-batch-profile-destinations.md)
