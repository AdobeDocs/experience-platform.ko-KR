---
title: (베타) Experience Platform UI를 사용하여 온디맨드 파일을 배치 대상으로 내보내기
type: Tutorial
description: Experience Platform UI를 사용하여 온디맨드 파일을 배치 대상으로 내보내는 방법을 알아봅니다.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 874c590e83712a45e75308239fb71db04614bd1e
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# (베타) Experience Platform UI를 사용하여 온디맨드 파일을 배치 대상으로 내보내기

>[!IMPORTANT]
>
>다음 **[!UICONTROL 지금 파일 내보내기]** Adobe Experience Platform Destination SDK의 옵션은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.
>이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오.

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

## **[!UICONTROL 지금 파일 내보내기]** 개요 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="지금 파일 내보내기"
>abstract="이전에 예약된 내보내기 외에 전체 파일 내보내기를 전달하려면 이 컨트롤을 선택합니다. 파일 내보내기는 즉시 트리거되며 Experience Platform 세그먼테이션 실행의 최신 결과를 선택합니다."

이 문서에서는 Experience Platform UI를 사용하여 요청 시 파일을 배치 대상으로 내보내는 방법을 설명합니다(예: ) [클라우드 스토리지](/help/destinations/catalog/cloud-storage/overview.md) 및 [이메일 마케팅](/help/destinations/catalog/email-marketing/overview.md) 대상.

다음 **[!UICONTROL 지금 파일 내보내기]** 제어로 이전에 예약된 세그먼트의 현재 내보내기 일정을 중단하지 않고 전체 파일을 내보낼 수 있습니다. 이 내보내기는 이전에 예약한 내보내기 외에 추가로 발생하며 세그먼트의 내보내기 빈도를 변경하지 않습니다. 파일 내보내기는 즉시 트리거되며 Experience Platform 세그먼테이션 실행의 최신 결과를 선택합니다.

이러한 용도로 Experience Platform API를 사용할 수도 있습니다. 방법 읽기 [ad-hoc 활성화 API를 통해 요청 시 배치 대상에 대상 세그먼트 활성화](/help/destinations/api/ad-hoc-activation-api.md).

## 전제 조건 {#prerequisites}

온디맨드 파일을 배치 대상으로 내보내려면 성공적으로 내보내야 합니다 [대상에 연결](./connect-destination.md). 아직 하지 않았다면 을(를) 참조하십시오. [대상 카탈로그](../catalog/overview.md)를 클릭하고 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 주문형 파일을 내보내는 방법 {#how-to-export-files-on-demand}

1. 이동 **[!UICONTROL 연결 > 대상]**&#x200B;에서 을(를) 선택합니다. **[!UICONTROL 찾아보기]** 탭 및 필터 기호를 사용하여 원하는 배치 대상에 대한 기존 연결을 표시할 수 있습니다.

   ![찾아보기 탭으로 이동하여 기존 데이터 흐름을 필터링하는 방법을 강조 표시하는 이미지](../assets/ui/activate-on-demand/browse-tab.png)

2. 기존 데이터 흐름을 대상으로 검사하려면 원하는 대상 연결을 선택합니다.

   ![필터링된 데이터 흐름을 강조 표시하는 이미지](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 을(를) 선택합니다 **[!UICONTROL 활성화 데이터]** 탭을 클릭하고 필요할 때 파일을 내보낼 세그먼트를 선택한 다음 **[!UICONTROL 지금 파일 내보내기]** 파일을 배치 대상에 전달하는 일회성 내보내기를 트리거하는 컨트롤.

   >[!IMPORTANT]
   >
   >현재 UI에서 주문형 파일을 대량으로 내보낼 세그먼트를 여러 개 선택할 수 없습니다. 를 사용하십시오 [ad-hoc 활성화 API](/help/destinations/api/ad-hoc-activation-api.md) 그러한 목적으로 사용됩니다.

   ![지금 파일 내보내기 단추를 강조 표시하는 이미지](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. 선택 **[!UICONTROL 예]** 파일 내보내기를 확인하고 트리거하려면 다음을 수행하십시오.

   ![지금 파일 내보내기 확인 대화 상자를 표시하는 이미지입니다.](../assets/ui/activate-on-demand/confirm-activation.png)

5. 파일 내보내기가 시작되었음을 알리는 확인 메시지가 나타납니다.

   ![성공적인 임시 활성화 확인을 보여주는 이미지.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 을 사용하여 **[!UICONTROL 데이터 흐름 실행]** 탭 을 클릭하여 파일 내보내기가 시작되었는지 확인합니다.

## 고려 사항 {#considerations}

를 사용할 때는 다음 고려 사항을 염두에 두십시오 **[!UICONTROL 지금 파일 내보내기]** 제어:

* **[!UICONTROL 지금 파일 내보내기]** 배치 활성화 데이터 플로우에서 현재 날짜와 겹치는 일정이 있는 세그먼트에만 작동합니다. 여기에는 종료 날짜(내보내기 빈도)가 없는 일정이 있는 세그먼트가 포함됩니다 **[!UICONTROL 한 번]**) 또는 종료 날짜가 아직 전달되지 않은 경우
* 기존 데이터 플로우에 세그먼트를 추가할 때는 **[!UICONTROL 지금 파일 내보내기]** 제어.
* 세그먼트의 병합 정책을 변경하거나 새 병합 정책을 사용하는 세그먼트를 만드는 경우, **[!UICONTROL 지금 파일 내보내기]** 제어.

## UI 오류 메시지 {#ui-error-messages}

를 사용할 때 **[!UICONTROL 지금 파일 내보내기]** 제어하면 아래에 나열된 오류 메시지가 표시될 수 있습니다. 테이블이 표시될 때 해당 주소를 지정하는 방법을 이해하려면 표를 검토하십시오.

| 오류 메시지 | 해상도 |
|---------|----------|
| 세그먼트에 대해 이미 실행 `segment ID` 주문 `dataflow ID` 실행 id 사용 `flow run ID` | 이 오류 메시지는 임시 활성화 흐름이 현재 세그먼트에 대해 진행 중임을 나타냅니다. 활성화 작업을 다시 트리거하기 전에 작업이 완료될 때까지 기다립니다. |
| 세그먼트 `<segment name>` 이 데이터 흐름의 일부가 아니거나 일정 범위를 벗어났습니다. | 이 오류 메시지는 활성화하도록 선택한 세그먼트가 데이터 플로우에 매핑되지 않거나 세그먼트에 대해 설정된 활성화 일정이 만료되었거나 아직 시작되지 않았음을 나타냅니다. 세그먼트가 실제로 데이터 플로우에 매핑되었는지 확인하고 세그먼트 활성화 일정이 현재 날짜와 겹치는지 확인합니다. |

## 관련 정보 {#related-information}

* [Experience Platform API를 사용하여 요청 시 배치 대상에 대상 세그먼트 활성화](/help/destinations/api/ad-hoc-activation-api.md)
* [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)
