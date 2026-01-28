---
title: 스트리밍 대상으로 대상 데이터 활성화
type: Tutorial
description: 스트리밍 대상에 매핑하여 Adobe Experience Platform에 있는 대상을 활성화하는 방법을 알아봅니다.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 99bac2ea71003b678a25b3afc10a68d36472bfbc
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 3%

---


# 스트리밍 대상에 대상 활성화

>[!IMPORTANT]
> 
> * 대상을 활성화하고 워크플로의 [매핑 단계](#mapping)을(를) 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
> * 워크플로우의 [매핑 단계](#mapping)를 거치지 않고 대상을 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
> * *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}
> 
> [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 스트리밍 대상에서 대상을 활성화하는 데 필요한 워크플로에 대해 설명합니다.

## 전제 조건 {#prerequisites}

대상을 대상으로 활성화하려면 대상에 [연결됨](./connect-destination.md)이(가) 있어야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)(으)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상 선택 {#select-destination}

1. **[!UICONTROL Connections > Destinations]**(으)로 이동하여 **[!UICONTROL Catalog]** 탭을 선택합니다.

   ![다양한 스트리밍 대상을 표시하는 대상 카탈로그 탭](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 아래 이미지에 표시된 대로 대상을 활성화할 대상에 해당하는 카드에서 **[!UICONTROL Activate audiences]**&#x200B;을(를) 선택합니다.

   ![대상 카탈로그에 강조 표시된 컨트롤을 활성화합니다.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. 대상을 활성화하는 데 사용할 대상 연결을 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

   ![대상 선택 단계에서 강조 표시된 대상 연결입니다.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. 다음 섹션으로 이동하여 [대상자를 선택](#select-audiences)하십시오.

## 대상자 선택 {#select-audiences}

대상으로 활성화할 대상을 선택하려면 대상 이름 왼쪽의 확인란을 사용한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

출처에 따라 여러 유형의 대상 중에서 선택할 수 있습니다.

* **[!UICONTROL Segmentation Service]**: 세분화 서비스에 의해 Experience Platform 내에서 생성된 대상자입니다. 자세한 내용은 [세그먼테이션 설명서](../../segmentation/ui/overview.md)를 참조하세요.
* **[!UICONTROL Custom upload]**: Experience Platform 외부에서 생성되어 Experience Platform에 CSV 파일로 업로드된 대상자입니다. 외부 대상자에 대한 자세한 내용은 [대상자 가져오기](../../segmentation/ui/audience-portal.md#import-audience)에 대한 설명서를 참조하십시오.
* 다른 Adobe 솔루션에서 가져온 다른 유형의 대상(예: [!DNL Audience Manager]).

![대상 선택 단계에서 강조 표시된 여러 대상.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## 속성 및 ID 매핑 {#mapping}

>[!IMPORTANT]
>
>이 단계는 일부 대상 스트리밍 대상에만 적용됩니다. 대상에 **[!UICONTROL Mapping]** 단계가 없는 경우 [대상 예약](#scheduling)(으)로 건너뜁니다.
>
>대상을 스트리밍 대상으로 활성화할 때 대상 프로필 특성 외에 *하나 이상의 대상 ID 네임스페이스*도 매핑해야 합니다. 그렇지 않으면 대상자가 대상 플랫폼에 활성화되지 않습니다.
> ![필수 ID 네임스페이스 매핑을 보여 주는 매핑 단계의 이미지입니다.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


일부 대상 스트리밍 대상에서는 소스 속성이나 ID 네임스페이스를 선택하여 대상의 타겟 ID로 매핑해야 합니다.

1. **[!UICONTROL Mapping]** 페이지에서 **[!UICONTROL Add new mapping]**&#x200B;을(를) 선택합니다.

   ![강조 표시된 새 매핑 컨트롤을 추가합니다.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. **[!UICONTROL Source field]** 항목 오른쪽에 있는 화살표를 선택합니다.

   ![소스 필드 컨트롤을 강조 표시했습니다.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. **[!UICONTROL Select source field]** 페이지에서 **[!UICONTROL Select attributes]** 또는 **[!UICONTROL Select identity namespace]** 옵션을 사용하여 사용 가능한 두 범주의 원본 필드 사이를 전환합니다. 사용 가능한 [!DNL XDM] 프로필 특성 및 ID 네임스페이스에서 대상에 매핑할 특성을 선택한 다음 **[!UICONTROL Select]**&#x200B;을(를) 선택합니다.

   **[!UICONTROL Show only fields with data]** 전환을 사용하여 값으로 채워진 스키마 필드만 표시합니다. 기본적으로 채워진 스키마 필드만 표시됩니다.

   ![사용 가능한 여러 소스 필드를 표시하는 소스 필드 선택 페이지입니다.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

   **[!UICONTROL Show display names for fields]** 전환을 사용하여 스키마 필드 이름 대신 필드에 대한 친숙한 이름을 표시합니다.

   ![표시 이름에 대한 토글을 표시하는 원본 필드 선택 페이지입니다.](../assets/ui/activate-segment-streaming-destinations/show-display-names.gif)

1. **[!UICONTROL Target field]** 항목 오른쪽에 있는 버튼을 선택합니다.

   ![강조 표시된 대상 필드 선택.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. **[!UICONTROL Select target field]** 페이지에서 소스 필드를 매핑할 대상 ID 네임스페이스를 선택하고 **[!UICONTROL Select]**&#x200B;을(를) 선택합니다.

   ![대상 필드 매핑에 사용할 수 있는 옵션을 보여 주는 대상 필드 선택 페이지입니다.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 매핑을 더 추가하려면 1~5단계를 반복합니다.

### 변환 적용 {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="변환 적용"
>abstract="해시되지 않은 소스 필드를 사용할 때 이 옵션을 선택하면 Adobe Experience Platform에서 활성화 시 해당 필드를 자동으로 해시할 수 있습니다."

해시되지 않은 소스 특성을 대상이 해시될 것으로 예상하는 대상 특성(예: `email_lc_sha256` 또는 `phone_sha256`)에 매핑할 때 **변환 적용** 옵션을 선택하여 Adobe Experience Platform이 활성화 시 소스 특성을 자동으로 해시하도록 합니다.

![ID 매핑 단계에서 강조 표시된 변환 컨트롤을 적용하십시오.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 대상자 내보내기 예약 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="종료 날짜"
>abstract="대상자 예약에 종료 날짜를 추가할 수 없습니다."

기본적으로 **[!UICONTROL Audience schedule]** 페이지에는 현재 활성화 흐름에서 선택한 새로 선택한 대상만 표시됩니다.

대상에 대해 활성화된 모든 대상을 보려면 필터링 옵션을 사용하고 **[!UICONTROL Show new audiences only]** 필터를 비활성화하십시오.

![모든 대상](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. **[!UICONTROL Audience schedule]** 페이지에서 각 대상을 선택한 다음 **[!UICONTROL Start date]** 및 **[!UICONTROL End date]** 선택기를 사용하여 데이터를 대상으로 보내는 시간 간격을 구성하십시오.

   ![대상 일정 필터가 강조 표시되었습니다.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * 일부 대상에서는 달력 선택기 아래의 드롭다운 메뉴를 사용하여 각 대상자에 대해 **[!UICONTROL Origin of audience]**&#x200B;을(를) 선택해야 합니다. 대상에 이 선택기가 포함되지 않은 경우 이 단계를 건너뜁니다.

     ![매핑 ID 드롭다운이 강조 표시되었습니다.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 일부 대상을 사용하려면 [!DNL Experience Platform] 대상을 대상 대상의 해당 대상에 수동으로 매핑해야 합니다. 이렇게 하려면 각 대상을 선택한 다음 **[!UICONTROL Mapping ID]** 필드의 대상 플랫폼에서 해당 대상 ID를 입력합니다. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

     ![대상 원본 드롭다운이 강조 표시되었습니다.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * **[!UICONTROL App ID]** 또는 [!DNL IDFA] 대상을 활성화할 때 일부 대상을 사용하려면 [!DNL GAID]을(를) 입력해야 합니다. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

     ![앱 ID 드롭다운이 강조 표시되었습니다.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. **[!UICONTROL Next]** 페이지로 이동하려면 [!UICONTROL Review]을(를) 선택하십시오.

## 검토 {#review}

**[!UICONTROL Review]** 페이지에서 선택 항목의 요약을 볼 수 있습니다. **[!UICONTROL Cancel]**&#x200B;을(를) 선택하여 흐름을 분류하거나, **[!UICONTROL Back]**&#x200B;을(를) 선택하여 설정을 수정하거나, **[!UICONTROL Finish]**&#x200B;을(를) 선택하여 선택을 확인하고 데이터를 대상으로 보내기 시작합니다.

![검토 단계의 선택 요약입니다.](../assets/ui/activate-segment-streaming-destinations/review.png)

### 동의 정책 평가 {#consent-policy-evaluation}

조직에서 **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;을(를) 구입한 경우 **[!UICONTROL View applicable consent policies]**&#x200B;을(를) 선택하여 적용되는 동의 정책 및 그 결과로 활성화에 포함되는 프로필 수를 확인합니다. 자세한 내용은 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)를 참조하세요.

### 데이터 사용 정책 확인 {#data-usage-policy-checks}

**[!UICONTROL Review]** 단계에서 Experience Platform은 데이터 사용 정책 위반도 확인합니다. 다음은 정책이 위반되는 예입니다. 위반을 해결할 때까지 대상 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 설명서 섹션에서 [데이터 사용 정책 위반](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)을 읽어 보십시오.

![활성화 워크플로에 표시된 데이터 정책 위반의 예입니다.](../assets/common/data-policy-violation.png)

### 대상자 필터링 {#filter-audiences}

또한 이 단계에서는 페이지에서 사용 가능한 필터를 사용하여 이 워크플로우의 일부로 일정이나 매핑이 업데이트된 대상자만 표시할 수 있습니다. 보려는 테이블 열을 전환할 수도 있습니다.

![검토 단계에서 사용 가능한 대상 필터를 보여 주는 화면 기록입니다.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

선택에 만족하고 정책 위반이 발견되지 않은 경우 **[!UICONTROL Finish]**&#x200B;을(를) 선택하여 선택을 확인하고 데이터를 대상으로 보내기 시작합니다.

## 대상자 활성화 확인 {#verify}

대상에 대한 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 [대상 모니터링 설명서](../../dataflows/ui/monitor-destinations.md)를 참조하세요.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
