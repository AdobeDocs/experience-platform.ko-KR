---
keywords: 개인화; target; 대상; 개인화 대상 개인화 대상 구성 동일한 페이지. 다음 페이지;
title: 동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성
type: Tutorial
description: 동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상을 구성하는 방법을 알아봅니다.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성

## 개요 {#overview}

>[!NOTE]
>
>When [Adobe Target 연결 구성](../catalog/personalization/adobe-target-connection.md) 데이터 스트림 ID를 사용하지 않으면 이 문서에 설명된 사용 사례가 지원되지 않습니다.

Adobe Experience Platform 사용 [에지 세분화](../../segmentation/ui/edge-segmentation.md) 고객이 높은 규모로 대상 세그먼트를 실시간으로 만들고 타겟팅할 수 있도록 하는 것.

이 기능은 동일한 페이지 및 다음 페이지 개인화 사용 사례를 구성하는 데 도움이 됩니다.

이 문서에서는 이러한 사용 사례에 대한 Experience Platform 및 개인화 대상을 구성하는 방법에 대한 단계별 지침을 제공합니다.

또한 종단 간 구성 프로세스에 대한 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며 이 비디오를 기록한 후 변경되었을 수 있습니다. 최신 정보는 아래 섹션에 설명된 구성 단계를 참조하십시오.

## 1단계: Data Collection UI에서 데이터 스트림 구성 {#configure-datastream}

개인화 대상을 설정하는 첫 번째 단계는 Experience Platform Web SDK에 대한 데이터 스트림을 구성하는 것입니다. 이 작업은 데이터 수집 UI에서 수행됩니다.

데이터 스트림을 구성할 때 아래의 **[!UICONTROL Adobe Experience Platform]** 둘 다 **[!UICONTROL 에지 세그멘테이션]** 및 **[!UICONTROL 개인화 대상]** 을 선택합니다.

![데이터 스트림 구성](../assets/ui/configure-personalization-destinations/datastream-config.png)

데이터 스트림을 설정하는 방법에 대한 자세한 내용은 [Platform 웹 SDK 설명서](../../edge/datastreams/overview.md).

## 2단계: 개인화 대상 구성 {#configure-destination}

데이터 스트림을 구성한 후 개인화 대상 구성을 시작할 수 있습니다.

다음을 수행합니다 [대상 연결 만들기 자습서](../ui/connect-destination.md) 를 참조하십시오.

구성하는 대상에 따라 대상 특정 사전 요구 사항 및 관련 정보가 필요하면 다음 문서를 참조하십시오.

* [Adobe Target 연결](../catalog/personalization/adobe-target-connection.md)
* [사용자 지정 개인화 연결](../catalog/personalization/custom-personalization.md)

## 3단계: 만들기 [!DNL Active-On-Edge] 병합 정책 {#create-merge-policy}

대상 연결을 만든 후 [!DNL Active-On-Edge] 병합 정책.

다음 지침을 따르십시오 [병합 정책 만들기](../../profile/merge-policies/ui-guide.md#create-a-merge-policy), 및에서 **[!UICONTROL Active-On-Edge 병합 정책]** 토글.

## 4단계: Platform에서 새 세그먼트 만들기 {#create-segment}

을(를) 만든 후 [!DNL Active-On-Edge] 병합 정책에서는 Platform에서 새 세그먼트를 만들어야 합니다.

다음을 수행합니다 [세그먼트 빌더](../../segmentation/ui/segment-builder.md) 새 세그먼트를 만드는 방법을 안내하고 다음을 확인합니다. [할당](../../segmentation/ui/segment-builder.md#merge-policies) a [!DNL Active-On-Edge] 3단계에서 만든 병합 정책.

## 5단계: 대상에 세그먼트 활성화

구성 프로세스의 마지막 단계는 4단계에서 만든 세그먼트를 2단계에서 만든 대상으로 활성화하는 것입니다.

이렇게 하려면 다음을 수행합니다 [활성화 자습서](../ui/activate-profile-request-destinations.md).

## 구성 유효성 확인 {#validate-configuration}

위의 단계를 성공적으로 수행하면 개인화 대상에 새 세그먼트가 표시됩니다.
