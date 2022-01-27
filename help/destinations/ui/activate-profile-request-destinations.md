---
keywords: 프로필 요청 대상 활성화;데이터 활성화;프로필 요청 대상 활성화
title: 프로필 요청 대상에 대상 데이터 활성화(베타)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: 세그먼트를 프로필 요청 대상에 매핑하여 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: dd9493077706b102467493e90b363ac202550eee
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 프로필 요청 대상에 대상 데이터 활성화

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 프로필 요청 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로우에 대해 설명합니다. 프로필 요청 대상의 예는 다음과 같습니다 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 그리고 [사용자 지정 개인화](../../destinations/catalog/personalization/custom-personalization.md) 연결.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 [대상에 연결](./connect-destination.md). 아직 하지 않았다면 을(를) 참조하십시오. [대상 카탈로그](../catalog/overview.md)를 클릭하고 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

### 세그먼트 병합 정책 {#merge-policy}

현재 프로필 요청 대상은 [기본 병합 정책](../../segmentation/ui/segment-builder.md#merge-policies).

## 대상을 선택합니다 {#select-destination}

1. 이동 **[!UICONTROL 연결 > 대상]**, 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 카탈로그]** 탭.

   ![대상 카탈로그 탭](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 선택 **[!UICONTROL 세그먼트 활성화]** 세그먼트를 활성화할 대상에 해당하는 카드에서 아래 그림과 같이 세그먼트를 활성화하십시오.

   ![단추 활성화](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 세그먼트를 활성화하는 데 사용할 대상 연결을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

   ![대상 선택](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 다음 섹션으로 이동 [세그먼트 선택](#select-segments).

## 세그먼트 선택 {#select-segments}

세그먼트 이름 왼쪽에 있는 확인란을 사용하여 대상으로 활성화할 세그먼트를 선택한 다음 선택합니다 **[!UICONTROL 다음]**.

![세그먼트 선택](../assets/ui/activate-profile-request-destinations/select-segments.png)

## 세그먼트 내보내기 예약 {#scheduling}

기본적으로 [!UICONTROL 세그먼트 예약] 페이지에는 현재 활성화 플로우에서 선택한 새로 선택한 세그먼트만 표시됩니다.

![새 세그먼트](../assets/ui/activate-profile-request-destinations/new-segments.png)

대상에 대해 활성화되는 모든 세그먼트를 보려면 필터링 옵션을 사용하고 을 비활성화하십시오 **[!UICONTROL 새 세그먼트만 표시]** 필터.

![모든 세그먼트](../assets/ui/activate-profile-request-destinations/all-segments.png)

설정 **[!UICONTROL 세그먼트 예약]** 페이지에서 각 세그먼트를 선택한 다음 **[!UICONTROL 시작 날짜]** 및 **[!UICONTROL 종료 날짜]** 선택기를 사용하여 데이터를 대상에 전송할 시간 간격을 구성합니다.

![세그먼트 예약](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

선택 **[!UICONTROL 다음]** 로 이동 [!UICONTROL 검토] 페이지.

## 검토 {#review}

설정 **[!UICONTROL 검토]** 페이지에서 선택 사항에 대한 요약을 볼 수 있습니다. 선택 **[!UICONTROL 취소]** 흐름을 분해하려면 **[!UICONTROL 뒤로]** 설정을 수정하려면 **[!UICONTROL 완료]** 을(를) 클릭하여 선택 내용을 확인하고 데이터를 대상으로 보내기 시작합니다.

>[!IMPORTANT]
>
>이 단계에서 Adobe Experience Platform은 데이터 사용 정책 위반을 확인합니다. 아래는 정책이 위반되는 예입니다. 위반을 해결해야 세그먼트 활성화 워크플로우를 완료할 수 있습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 [정책 적용](../../rtcdp/privacy/data-governance-overview.md#enforcement) ( 데이터 거버넌스 설명서 섹션) 을 참조하십시오.

![데이터 정책 위반](../assets/common/data-policy-violation.png)

정책 위반이 검색되지 않은 경우 **[!UICONTROL 완료]** 을(를) 클릭하여 선택 내용을 확인하고 데이터를 대상으로 보내기 시작합니다.

![검토](../assets/ui/activate-profile-request-destinations/review.png)

## 세그먼트 활성화 확인 {#verify}

을(를) 확인합니다. [대상 모니터링 설명서](../../dataflows/ui/monitor-destinations.md) 를 참조하십시오.
