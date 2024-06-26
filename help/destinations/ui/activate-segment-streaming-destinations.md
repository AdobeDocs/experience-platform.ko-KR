---
title: 스트리밍 대상으로 대상 데이터 활성화
type: Tutorial
description: 스트리밍 대상에 매핑하여 Adobe Experience Platform에 있는 대상을 활성화하는 방법을 알아봅니다.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 30ad6c32d8ae8a2a68dfafd78f306209ce49b6d5
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 6%

---


# 스트리밍 대상에 대상 활성화

>[!IMPORTANT]
> 
> * 대상을 활성화하고 을 활성화하려면 [매핑 단계](#mapping) 워크플로의 경우 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
> * 을(를) 거치지 않고 대상 활성화 [매핑 단계](#mapping) 워크플로의 경우 **[!UICONTROL 대상 보기]**, **[!UICONTROL 매핑 없이 세그먼트 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}
> 
> 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 스트리밍 대상에서 대상을 활성화하는 데 필요한 워크플로에 대해 설명합니다.

## 전제 조건 {#prerequisites}

대상에 대상을 활성화하려면 다음을 성공적으로 완료해야 합니다. [대상에 연결됨](./connect-destination.md). 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)에서 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상 선택 {#select-destination}

1. 다음으로 이동 **[!UICONTROL 연결 > 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 카탈로그]** 탭.

   ![다양한 스트리밍 대상을 표시하는 대상 카탈로그 탭입니다.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 선택 **[!UICONTROL 대상자 활성화]** 아래 이미지에 표시된 대로 대상을 활성화할 대상에 해당하는 카드에.

   ![대상 카탈로그에서 강조 표시된 컨트롤을 활성화합니다.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. 대상을 활성화하는 데 사용할 대상 연결을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

   ![대상 선택 단계에서 강조 표시된 대상 연결입니다.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. 다음 섹션으로 이동 [대상자 선택](#select-audiences).

## 대상자 선택 {#select-audiences}

대상에 대해 활성화할 대상을 선택하려면 대상 이름 왼쪽에 있는 확인란을 사용한 다음 을 선택합니다 **[!UICONTROL 다음]**.

출처에 따라 여러 유형의 대상 중에서 선택할 수 있습니다.

* **[!UICONTROL 세분화 서비스]**: 세분화 서비스에 의해 Experience Platform 내에서 생성된 대상자. 다음을 참조하십시오. [세그멘테이션 설명서](../../segmentation/ui/overview.md) 을 참조하십시오.
* **[!UICONTROL 사용자 정의 업로드]**: Experience Platform 외부에서 생성되어 CSV 파일로 플랫폼에 업로드된 대상자 외부 대상자에 대한 자세한 내용은 [대상자 가져오기](../../segmentation/ui/overview.md#import-audience).
* 다른 Adobe 솔루션에서 가져온 다른 유형의 대상, 예: [!DNL Audience Manager].

![대상자 선택 단계에서 강조 표시된 여러 대상자입니다.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## 속성 및 ID 매핑 {#mapping}

>[!IMPORTANT]
>
>이 단계는 일부 대상 스트리밍 대상에만 적용됩니다. 대상에 이 없는 경우 **[!UICONTROL 매핑]** 단계, 다음으로 건너뛰기 [대상자 예약](#scheduling).
>
>대상자를 스트리밍 대상으로 활성화할 때 매핑해야 합니다 *하나 이상의 target id 네임스페이스*, target 프로필 속성 외에 사용할 수도 있습니다. 그렇지 않으면 대상자가 대상 플랫폼에 활성화되지 않습니다.
> ![필수 ID 네임스페이스 매핑을 보여 주는 매핑 단계 이미지.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


일부 대상 스트리밍 대상에서는 소스 속성이나 ID 네임스페이스를 선택하여 대상의 타겟 ID로 매핑해야 합니다.

1. 다음에서 **[!UICONTROL 매핑]** 페이지, 선택 **[!UICONTROL 새 매핑 추가]**.

   ![강조 표시된 새 매핑 컨트롤을 추가합니다.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. 오른쪽 화살표를 선택합니다. **[!UICONTROL 소스 필드]** 입력.

   ![소스 필드 컨트롤을 강조 표시합니다.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. 다음에서 **[!UICONTROL 소스 필드 선택]** 페이지, 사용 **[!UICONTROL 속성 선택]** 또는 **[!UICONTROL ID 네임스페이스 선택]** 사용 가능한 두 가지 범주의 소스 필드 사이를 전환하는 옵션. 사용 가능한 날짜부터 [!DNL XDM] 프로필 속성 및 id 네임스페이스를 선택하고 대상에 매핑할 속성을 선택한 다음 을(를) 선택합니다 **[!UICONTROL 선택]**.

   사용 **[!UICONTROL 데이터가 있는 필드만 표시]** 값으로 채워진 스키마 필드만 표시하도록 전환합니다. 기본적으로 채워진 스키마 필드만 표시됩니다.

   ![사용 가능한 여러 소스 필드를 표시하는 소스 필드 선택 페이지입니다.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. 오른쪽 버튼을 선택합니다. **[!UICONTROL 대상 필드]** 입력.

   ![강조 표시된 대상 필드 선택.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. 다음에서 **[!UICONTROL 대상 필드 선택]** 소스 필드를 매핑할 대상 id 네임스페이스를 선택한 다음 을(를) 선택합니다 **[!UICONTROL 선택]**.

   ![대상 필드 매핑에 사용 가능한 옵션을 보여 주는 대상 필드 선택 페이지입니다.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 매핑을 더 추가하려면 1~5단계를 반복합니다.

### 변환 적용 {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="변환 적용"
>abstract="해시되지 않은 소스 필드를 사용할 때 이 옵션을 선택하면 Adobe Experience Platform에서 활성화 시 해당 필드를 자동으로 해시할 수 있습니다."

해시되지 않은 소스 속성을 대상이 해시할 것으로 예상하는 타겟 속성에 매핑할 때(예: `email_lc_sha256` 또는 `phone_sha256`), 다음을 확인합니다. **변환 적용** 활성화 시 Adobe Experience Platform이 소스 속성을 자동으로 해시하도록 하는 옵션입니다.

![ID 매핑 단계에서 강조 표시된 변환 제어 적용.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 대상자 내보내기 예약 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="종료 날짜"
>abstract="대상자 예약에 종료 날짜를 추가할 수 없습니다."

기본적으로 **[!UICONTROL 대상자 일정]** 페이지에는 현재 활성화 플로우에서 선택한 새로 선택한 대상만 표시됩니다.

대상에 대해 활성화된 모든 대상을 보려면 필터링 옵션을 사용하고 을(를) 비활성화합니다. **[!UICONTROL 새 대상자만 표시]** 필터.

![모든 대상](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. 다음에서 **[!UICONTROL 대상자 일정]** 페이지를 열고 각 대상을 선택한 다음 **[!UICONTROL 시작일]** 및 **[!UICONTROL 종료일]** 선택기를 사용하여 데이터를 대상으로 전송하는 시간 간격을 구성할 수 있습니다.

   ![대상 일정 필터가 강조 표시되었습니다.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * 일부 대상에서는 다음을 선택해야 합니다. **[!UICONTROL 대상자 원본]** 각 대상에 대해 달력 선택기 아래의 드롭다운 메뉴를 사용합니다. 대상에 이 선택기가 포함되지 않은 경우 이 단계를 건너뜁니다.

     ![매핑 ID 드롭다운이 강조 표시됩니다.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 일부 대상에서는 수동으로 매핑해야 합니다. [!DNL Platform] 대상 대상의 상대 대상에게 전달합니다. 이렇게 하려면 각 대상을 선택한 다음, 의 대상 플랫폼에서 해당 대상 ID를 입력합니다 **[!UICONTROL 매핑 ID]** 필드. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

     ![대상자 출처 드롭다운이 강조 표시됩니다.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 일부 대상에는 다음을 입력해야 합니다. **[!UICONTROL 앱 ID]** 활성화 시 [!DNL IDFA] 또는 [!DNL GAID] 대상. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

     ![앱 ID 드롭다운이 강조 표시됩니다.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. 선택 **[!UICONTROL 다음]** 로 이동 [!UICONTROL 리뷰] 페이지를 가리키도록 업데이트하는 중입니다.

## 검토 {#review}

다음에서 **[!UICONTROL 리뷰]** 페이지에서 선택 사항의 요약을 볼 수 있습니다. 선택 **[!UICONTROL 취소]** 흐름을 끊으려면, **[!UICONTROL 뒤로]** 설정을 수정하려면 **[!UICONTROL 완료]** 을 클릭하여 선택 항목을 확인하고 데이터를 대상으로 보내기 시작합니다.

![검토 단계의 선택 요약입니다.](../assets/ui/activate-segment-streaming-destinations/review.png)

### 동의 정책 평가 {#consent-policy-evaluation}

조직에서 **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;를 구매한 경우 **[!UICONTROL 해당 동의 정책 보기]**&#x200B;를 선택하여 적용된 동의 정책을 조회하고 그 결과로 활성화에 포함된 프로필 수를 확인합니다. 읽어보기 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 추가 정보.

### 데이터 사용 정책 확인 {#data-usage-policy-checks}

다음에서 **[!UICONTROL 리뷰]** 단계, Experience Platform은 데이터 사용 정책 위반도 확인합니다. 다음은 정책이 위반되는 예입니다. 위반을 해결할 때까지 대상 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [데이터 사용 정책 위반](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) (데이터 거버넌스 설명서 섹션)

![활성화 워크플로에 표시된 데이터 정책 위반의 예입니다.](../assets/common/data-policy-violation.png)

### 대상자 필터링 {#filter-audiences}

또한 이 단계에서는 페이지에서 사용 가능한 필터를 사용하여 이 워크플로우의 일부로 일정이나 매핑이 업데이트된 대상자만 표시할 수 있습니다. 보려는 테이블 열을 전환할 수도 있습니다.

![검토 단계에서 사용 가능한 대상 필터를 보여 주는 화면 기록입니다.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

선택에 만족하고 정책 위반이 감지되지 않은 경우 다음을 선택합니다. **[!UICONTROL 완료]** 을 클릭하여 선택 항목을 확인하고 데이터를 대상으로 보내기 시작합니다.

## 대상자 활성화 확인 {#verify}

다음 확인: [대상 모니터링 설명서](../../dataflows/ui/monitor-destinations.md) 대상으로의 데이터 흐름을 모니터링하는 방법에 대한 자세한 정보.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
