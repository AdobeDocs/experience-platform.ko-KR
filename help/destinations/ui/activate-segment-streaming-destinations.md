---
keywords: 세그먼트 스트리밍 대상 활성화;세그먼트 스트리밍 대상 활성화;데이터 활성화
title: 스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화
type: Tutorial
description: 세그먼트를 세그먼트 스트리밍 대상에 매핑하여 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 9bde403338187409892d76de68805535de03d59f
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 세그먼트 스트리밍 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로우에 대해 설명합니다.

## 사전 요구 사항 {#prerequisites}

대상에 데이터를 활성화하려면 [대상에 연결](./connect-destination.md). 아직 하지 않았다면 을(를) 참조하십시오. [대상 카탈로그](../catalog/overview.md)를 클릭하고 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상을 선택합니다 {#select-destination}

1. 이동 **[!UICONTROL 연결 > 대상]**, 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 카탈로그]** 탭.

   ![대상 카탈로그 탭](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 선택 **[!UICONTROL 세그먼트 활성화]** 세그먼트를 활성화할 대상에 해당하는 카드에서 아래 그림과 같이 세그먼트를 활성화하십시오.

   ![단추 활성화](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. 세그먼트를 활성화하는 데 사용할 대상 연결을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

   ![대상 선택](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. 다음 섹션으로 이동 [세그먼트 선택](#select-segments).

## 세그먼트 선택 {#select-segments}

세그먼트 이름 왼쪽에 있는 확인란을 사용하여 대상으로 활성화할 세그먼트를 선택한 다음 선택합니다 **[!UICONTROL 다음]**.

![세그먼트 선택](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## 특성 및 ID 매핑 {#mapping}

>[!IMPORTANT]
>
>이 단계는 일부 세그먼트 스트리밍 대상에만 적용됩니다. 대상에 **[!UICONTROL 매핑]** step, skip [세그먼트 내보내기 예약](#scheduling).

일부 세그먼트 스트리밍 대상을 사용하려면 소스 특성 또는 ID 네임스페이스를 선택하여 대상의 타겟 ID로 매핑해야 합니다.

1. 에서 **[!UICONTROL 매핑]** 페이지를 선택하고 **[!UICONTROL 새 매핑 추가]**.

   ![새 매핑 추가](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. 오른쪽 화살표를 선택합니다 **[!UICONTROL 소스 필드]** 을 입력합니다.

   ![소스 필드 선택](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. 에서 **[!UICONTROL 소스 필드 선택]** 페이지, **[!UICONTROL 속성 선택]** 또는 **[!UICONTROL ID 네임스페이스 선택]** 사용 가능한 소스 필드의 두 범주 간에 전환하는 옵션. 사용 가능한 [!DNL XDM] 프로필 속성 및 ID 네임스페이스에서 대상에 매핑할 속성을 선택한 다음 **[!UICONTROL 선택]**.

   ![소스 필드 선택 페이지](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. 오른쪽의 버튼을 선택합니다 **[!UICONTROL Target 필드]** 을 입력합니다.

   ![대상 필드 선택](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. 에서 **[!UICONTROL 대상 필드 선택]** 페이지에서 소스 필드를 매핑할 대상 ID 네임스페이스를 선택하고 **[!UICONTROL 선택]**.

   ![대상 필드 선택 페이지](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 매핑을 더 추가하려면 1~5단계를 반복합니다.

### 변형 적용 {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="변형 적용"
>abstract="해시되지 않은 소스 필드를 사용할 때 이 옵션을 선택하여 Adobe Experience Platform에서 활성화 시 자동으로 해시하도록 합니다."

해시되지 않은 소스 속성을 대상이 해시될 대상 속성에 매핑하는 경우(예: `email_lc_sha256` 또는 `phone_sha256`), 을(를) 선택합니다. **변형 적용** Adobe Experience Platform이 활성화 시 소스 속성을 자동으로 해시하도록 하는 옵션입니다.

![ID 매핑](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 세그먼트 내보내기 예약 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="종료 날짜"
>abstract="세그먼트 예약에 대한 종료 날짜를 추가할 수 없습니다."

기본적으로 [!UICONTROL 세그먼트 예약] 페이지에는 현재 활성화 플로우에서 선택한 새로 선택한 세그먼트만 표시됩니다.

![새 세그먼트](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

대상에 대해 활성화되는 모든 세그먼트를 보려면 필터링 옵션을 사용하고 을 비활성화하십시오 **[!UICONTROL 새 세그먼트만 표시]** 필터.

![모든 세그먼트](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. 설정 **[!UICONTROL 세그먼트 예약]** 페이지에서 각 세그먼트를 선택한 다음 **[!UICONTROL 시작 날짜]** 및 **[!UICONTROL 종료 날짜]** 선택기를 사용하여 데이터를 대상에 전송할 시간 간격을 구성합니다.

   ![세그먼트 예약](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * 일부 대상에서는 다음을 선택해야 합니다 **[!UICONTROL 대상의 기원]** 각 세그먼트에 대해 달력 선택기 아래에 있는 드롭다운 메뉴를 사용합니다. 대상에 이 선택기가 포함되지 않은 경우 이 단계를 건너뜁니다.

      ![매핑 ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 일부 대상을 사용하려면 수동으로 매핑해야 합니다 [!DNL Platform] 세그먼트를 타겟 대상의 상대 세그먼트에 추가합니다. 이렇게 하려면 각 세그먼트를 선택한 다음 의 대상 플랫폼에서 해당 세그먼트 ID를 입력합니다 **[!UICONTROL 매핑 ID]** 필드. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

      ![매핑 ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 일부 대상의 경우 다음을 입력해야 합니다 **[!UICONTROL 앱 ID]** 활성화할 때 [!DNL IDFA] 또는 [!DNL GAID] 세그먼트 를 참조하십시오. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

      ![앱 ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. 선택 **[!UICONTROL 다음]** 로 이동 [!UICONTROL 검토] 페이지.

## 검토 {#review}

설정 **[!UICONTROL 검토]** 페이지에서 선택 사항에 대한 요약을 볼 수 있습니다. 선택 **[!UICONTROL 취소]** 흐름을 분해하려면 **[!UICONTROL 뒤로]** 설정을 수정하려면 **[!UICONTROL 완료]** 을(를) 클릭하여 선택 내용을 확인하고 데이터를 대상으로 보내기 시작합니다.

![검토 단계의 선택 요약](/help/destinations/assets/ui/activate-segment-streaming-destinations/review.png)

### 동의 정책 평가 {#consent-policy-evaluation}

조직에서 구입한 경우 **Adobe 의료 보호** 또는 **Adobe 개인 정보 보호 및 보안 차단**, 선택 **[!UICONTROL 적용 가능한 동의 정책 보기]** 적용된 동의 정책 및 그 결과로 활성화에 포함되는 프로필 수를 확인하려면 다음을 수행하십시오. 자세한 내용 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 추가 정보.

### 데이터 사용 정책 검사 {#data-usage-policy-checks}

에서 **[!UICONTROL 검토]** 또한 Experience Platform은 데이터 사용 정책 위반도 확인합니다. 아래는 정책이 위반되는 예입니다. 위반을 해결해야 세그먼트 활성화 워크플로우를 완료할 수 있습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 [데이터 사용 정책 위반](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) ( 데이터 거버넌스 설명서 섹션) 을 참조하십시오.

![데이터 정책 위반](../assets/common/data-policy-violation.png)

### 세그먼트 필터링 {#filter-segments}

또한 이 단계에서는 페이지의 사용 가능한 필터를 사용하여 이 워크플로우의 일부로 일정이나 매핑이 업데이트된 세그먼트만 표시할 수 있습니다. 표시할 테이블 열을 전환할 수도 있습니다.

![검토 단계에서 사용 가능한 세그먼트 필터를 보여주는 화면 기록](/help/destinations/assets/ui/activate-segment-streaming-destinations/filter-segments-review-step.gif)

선택한 내용에 만족하고 정책 위반이 감지되지 않은 경우 을(를) 선택합니다 **[!UICONTROL 완료]** 을(를) 클릭하여 선택 내용을 확인하고 데이터를 대상으로 보내기 시작합니다.

## 세그먼트 활성화 확인 {#verify}

을(를) 확인합니다. [대상 모니터링 설명서](../../dataflows/ui/monitor-destinations.md) 를 참조하십시오.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
