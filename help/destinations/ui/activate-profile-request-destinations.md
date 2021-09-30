---
keywords: 프로필 요청 대상 활성화;데이터 활성화;프로필 요청 대상 활성화
title: 프로필 요청 대상에 대상 데이터 활성화(베타)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: 세그먼트를 프로필 요청 대상에 매핑하여 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 프로필 요청 대상에 대상 데이터 활성화(베타)

## 개요 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform의 프로필 요청 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

이 문서에서는 Adobe Experience Platform 프로필 요청 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로우에 대해 설명합니다. 프로필 요청 대상의 예로는 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화](../../destinations/catalog/personalization/custom-personalization.md) 연결이 있습니다.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 [이(가) 대상](./connect-destination.md)에 연결되어 있어야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

### 세그먼트 병합 정책 {#merge-policy}

현재 프로필 요청 대상은 [기본 병합 정책](../../segmentation/ui/segment-builder.md#merge-policies)을 사용하는 세그먼트의 활성화만 지원합니다.

## 대상을 선택합니다 {#select-destination}

1. **[!UICONTROL 연결 > 대상]**&#x200B;으로 이동하고 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   ![대상 카탈로그 탭](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 아래 그림과 같이 세그먼트를 활성화할 대상에 해당하는 카드에서 **[!UICONTROL 세그먼트 활성화]** 를 선택합니다.

   ![단추 활성화](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 세그먼트를 활성화하는 데 사용할 대상 연결을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

   ![대상 선택](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 다음 섹션으로 이동하여 [세그먼트 선택](#select-segments).

## 세그먼트 선택 {#select-segments}

세그먼트 이름의 왼쪽에 있는 확인란을 사용하여 대상으로 활성화할 세그먼트를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![세그먼트 선택](../assets/ui/activate-profile-request-destinations/select-segments.png)

## 세그먼트 내보내기 예약 {#scheduling}

기본적으로 [!UICONTROL 세그먼트 예약] 페이지에는 현재 활성화 플로우에서 선택한 새로 선택한 세그먼트만 표시됩니다.

![새 세그먼트](../assets/ui/activate-profile-request-destinations/new-segments.png)

대상에 활성화된 모든 세그먼트를 보려면 필터링 옵션을 사용하고 **[!UICONTROL 새 세그먼트만 표시]** 필터를 비활성화하십시오.

![모든 세그먼트](../assets/ui/activate-profile-request-destinations/all-segments.png)

**[!UICONTROL 세그먼트 일정]** 페이지에서 각 세그먼트를 선택한 다음 **[!UICONTROL 시작 날짜]** 및 **[!UICONTROL 종료 날짜]** 선택기를 사용하여 데이터를 대상에 전송할 시간 간격을 구성합니다.

![세그먼트 예약](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

**[!UICONTROL 다음]**&#x200B;을 선택하여 [!UICONTROL 검토] 페이지로 이동합니다.

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택 요약이 표시됩니다. **[!UICONTROL 취소]**&#x200B;를 선택하여 플로우를 분류하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택 내용을 확인하고 데이터를 대상에 보내려면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

>[!IMPORTANT]
>
>이 단계에서 Adobe Experience Platform은 데이터 사용 정책 위반을 확인합니다. 아래는 정책이 위반되는 예입니다. 위반을 해결해야 세그먼트 활성화 워크플로우를 완료할 수 있습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 설명서 섹션의 [정책 적용](../../rtcdp/privacy/data-governance-overview.md#enforcement)을 참조하십시오.

![데이터 정책 위반](../assets/common/data-policy-violation.png)

정책 위반이 감지되지 않은 경우 **[!UICONTROL 완료]**&#x200B;를 선택하여 선택 내용을 확인하고 데이터를 대상에 보냅니다.

![검토](../assets/ui/activate-profile-request-destinations/review.png)

## 세그먼트 활성화 확인 {#verify}

대상으로 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 [대상 모니터링 설명서](../../dataflows/ui/monitor-destinations.md)를 참조하십시오.