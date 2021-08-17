---
keywords: 세그먼트 스트리밍 대상 활성화;세그먼트 스트리밍 대상 활성화;데이터 활성화
title: 스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화
type: Tutorial
seo-title: 스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화
description: 세그먼트를 세그먼트 스트리밍 대상에 매핑하여 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
seo-description: 세그먼트를 세그먼트 스트리밍 대상에 매핑하여 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
source-git-commit: 65e74041aeb285cb80c67e47ccdaca18de9889fa
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---


# 스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 세그먼트 스트리밍 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로우에 대해 설명합니다.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 [이(가) 대상](./connect-destination.md)에 연결되어 있어야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상을 선택합니다 {#select-destination}

1. **[!UICONTROL 연결 > 대상]**&#x200B;으로 이동하고 **[!UICONTROL 찾아보기]** 탭을 선택합니다.

   ![대상 찾아보기 탭](../assets/ui/activate-segment-streaming-destinations/browse-tab.png)

1. 아래 그림과 같이 세그먼트를 활성화할 대상에 해당하는 **[!UICONTROL 세그먼트 추가]** 단추를 선택하십시오.

   ![단추 활성화](../assets/ui/activate-segment-streaming-destinations/activate-buttons-browse.png)

1. 다음 섹션으로 이동하여 [세그먼트 선택](#select-segments).

## 세그먼트 선택 {#select-segments}

세그먼트 이름의 왼쪽에 있는 확인란을 사용하여 대상으로 활성화할 세그먼트를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![세그먼트 선택](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## 특성 및 ID 매핑 {#mapping}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="변형 적용"
>abstract="해시되지 않은 소스 필드를 사용할 때 이 옵션을 선택하여 Adobe Experience Platform에서 활성화 시 자동으로 해시하도록 합니다."

>[!IMPORTANT]
>
>이 단계는 일부 세그먼트 스트리밍 대상에만 적용됩니다. 대상에 **[!UICONTROL 매핑]** 단계가 없는 경우 [세그먼트 내보내기 예약](#scheduling)으로 건너뜁니다.

일부 세그먼트 스트리밍 대상을 사용하려면 소스 특성 또는 ID 네임스페이스를 선택하여 대상의 타겟 ID로 매핑해야 합니다.

1. **[!UICONTROL 매핑]** 페이지에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택합니다.

   ![새 매핑 추가](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. **[!UICONTROL 소스 필드]** 항목 오른쪽에 있는 화살표를 선택합니다.

   ![소스 필드 선택](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. **[!UICONTROL 소스 필드 선택]** 페이지에서 **[!UICONTROL 속성 선택]** 또는 **[!UICONTROL ID 네임스페이스 선택]** 옵션을 사용하여 사용 가능한 소스 필드의 두 범주 간에 전환합니다. 사용 가능한 [!DNL XDM] 프로필 속성 및 ID 네임스페이스에서 대상에 매핑할 속성을 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

   ![소스 필드 선택 페이지](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. **[!UICONTROL Target 필드]** 항목 오른쪽에 있는 단추를 선택합니다.

   ![대상 필드 선택](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. **[!UICONTROL 대상 필드 선택]** 페이지에서 소스 필드를 매핑할 대상 ID 네임스페이스를 선택하고 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

   ![대상 필드 선택 페이지](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 매핑을 더 추가하려면 1~5단계를 반복합니다.

### 매핑 예: [!DNL Facebook Custom Audience]에서 대상 데이터 활성화 {#example-facebook}

다음은 [!DNL Facebook Custom Audience]에서 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* 사용 중인 전자 메일 주소가 해시되지 않은 경우 `Email` 네임스페이스를 소스 ID로 선택합니다.
* [!DNL Facebook] [이메일 해싱 요구 사항](../catalog/social/facebook.md#email-hashing-requirements)에 따라 [!DNL Platform]로 데이터 처리에 대한 고객 이메일 주소를 해시한 경우 `Email_LC_SHA256` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 해시되지 않은 전화 번호로 구성된 경우 `PHONE_E.164` 네임스페이스를 소스 ID로 선택합니다. [!DNL Platform] 은 요구 사항을 준수하도록 전화 번호를 해시합니다 [!DNL Facebook] .
* [!DNL Facebook] [전화 번호 해싱 요구 사항](../catalog/social/facebook.md#phone-number-hashing-requirements)에 따라 데이터 처리에 대한 전화 번호를 해시하면 `Phone_SHA256` 네임스페이스를 소스 ID로 선택합니다.[!DNL Platform]
* 데이터가 [!DNL Apple] 장치 ID로 구성된 경우 `IDFA` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 [!DNL Android] 장치 ID로 구성된 경우 `GAID` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 다른 유형의 식별자로 구성된 경우 `Custom` 네임스페이스를 소스 ID로 선택합니다.

대상 필드 선택:

* 소스 네임스페이스가 `Email` 또는 `Email_LC_SHA256`인 경우 `Email_LC_SHA256` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 `PHONE_E.164` 또는 `Phone_SHA256`인 경우 `Phone_SHA256` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 `IDFA` 또는 `GAID`인 경우 `IDFA` 또는 `GAID` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 사용자 지정 네임스페이스일 때 `Extern_ID` 네임스페이스를 대상 ID로 선택합니다.

>[!IMPORTANT]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Platform]에 의해 자동으로 해시됩니다.
> 
>속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오.

![ID 매핑](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

### 매핑 예: [!DNL Google Customer Match]에서 대상 데이터 활성화 {#example-gcm}

이는 [!DNL Google Customer Match]에서 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* 사용 중인 전자 메일 주소가 해시되지 않은 경우 `Email` 네임스페이스를 소스 ID로 선택합니다.
* [!DNL Google Customer Match] [이메일 해싱 요구 사항](../catalog/social/../advertising/google-customer-match.md)에 따라 [!DNL Platform]로 데이터 처리에 대한 고객 이메일 주소를 해시한 경우 `Email_LC_SHA256` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 해시되지 않은 전화 번호로 구성된 경우 `PHONE_E.164` 네임스페이스를 소스 ID로 선택합니다. [!DNL Platform] 은 요구 사항을 준수하도록 전화 번호를 해시합니다 [!DNL Google Customer Match] .
* [!DNL Facebook] [전화 번호 해싱 요구 사항](../catalog/social/../advertising/google-customer-match.md)에 따라 데이터 처리에 대한 전화 번호를 해시하면 `Phone_SHA256_E.164` 네임스페이스를 소스 ID로 선택합니다.[!DNL Platform]
* 데이터가 [!DNL Apple] 장치 ID로 구성된 경우 `IDFA` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 [!DNL Android] 장치 ID로 구성된 경우 `GAID` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 다른 유형의 식별자로 구성된 경우 `Custom` 네임스페이스를 소스 ID로 선택합니다.

대상 필드 선택:

* 소스 네임스페이스가 `Email` 또는 `Email_LC_SHA256`인 경우 `Email_LC_SHA256` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 `PHONE_E.164` 또는 `Phone_SHA256_E.164`인 경우 `Phone_SHA256_E.164` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 `IDFA` 또는 `GAID`인 경우 `IDFA` 또는 `GAID` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 사용자 지정 네임스페이스일 때 `User_ID` 네임스페이스를 대상 ID로 선택합니다.

![ID 매핑](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Platform]에 의해 자동으로 해시됩니다.

속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오.

![ID 매핑 변환](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 세그먼트 내보내기 예약 {#scheduling}

1. **[!UICONTROL 세그먼트 일정]** 페이지에서 각 세그먼트를 선택한 다음 **[!UICONTROL 시작 날짜]** 및 **[!UICONTROL 종료 날짜]** 선택기를 사용하여 데이터를 대상에 전송할 시간 간격을 구성합니다.

   ![세그먼트 예약](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * 일부 대상에서는 달력 선택기 아래에 있는 드롭다운 메뉴를 사용하여 각 세그먼트에 대한 **[!UICONTROL 대상]**&#x200B;의 출처를 선택해야 합니다. 대상에 이 선택기가 포함되지 않은 경우 이 단계를 건너뜁니다.

      ![매핑 ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 일부 대상을 사용하려면 [!DNL Platform] 세그먼트를 수동으로 타겟 대상의 상대편에 매핑해야 합니다. 이렇게 하려면 각 세그먼트를 선택한 다음 **[!UICONTROL 매핑 ID]** 필드에 대상 플랫폼의 해당 세그먼트 ID를 입력합니다. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

      ![매핑 ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 일부 대상에서는 [!DNL IDFA] 또는 [!DNL GAID] 세그먼트를 활성화할 때 **[!UICONTROL 앱 ID]**&#x200B;를 입력해야 합니다. 대상에 이 필드가 포함되지 않은 경우 이 단계를 건너뜁니다.

      ![앱 ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. **[!UICONTROL 다음]**&#x200B;을 선택하여 [!UICONTROL 검토] 페이지로 이동합니다.

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택 요약이 표시됩니다. **[!UICONTROL 취소]**&#x200B;를 선택하여 플로우를 분류하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택 내용을 확인하고 데이터를 대상에 보내려면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

>[!IMPORTANT]
>
>이 단계에서 Adobe Experience Platform은 데이터 사용 정책 위반을 확인합니다. 아래는 정책이 위반되는 예입니다. 위반을 해결해야 세그먼트 활성화 워크플로우를 완료할 수 있습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 설명서 섹션의 [정책 적용](../../rtcdp/privacy/data-governance-overview.md#enforcement)을 참조하십시오.

![데이터 정책 위반](../assets/common/data-policy-violation.png)

정책 위반이 감지되지 않은 경우 **[!UICONTROL 완료]**&#x200B;를 선택하여 선택 내용을 확인하고 데이터를 대상에 보냅니다.

![검토](../assets/ui/activate-segment-streaming-destinations/review.png)

## 세그먼트 활성화 확인 {#verify}

대상 계정을 확인합니다. 활성화가 성공하면 대상이 대상 플랫폼에서 채워집니다.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
