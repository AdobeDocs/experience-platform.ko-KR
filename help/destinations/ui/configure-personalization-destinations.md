---
keywords: 개인화; target; 대상; 개인화 대상 개인화 대상 구성 동일한 페이지. 다음 페이지;
title: 동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization
description: 동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상을 구성하는 방법을 알아봅니다
seo-description: Configure personalization destinations for same-page and next-page personalization
source-git-commit: 628e7a993a3566322e0249a5a9864cf6b3fe4493
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---


# 동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성

## 개요 {#overview}

Adobe Experience Platform 사용 [에지 세분화](../../segmentation/ui/edge-segmentation.md) 고객이 높은 규모로 대상 세그먼트를 실시간으로 만들고 타겟팅할 수 있도록 하는 것.

이 기능은 동일한 페이지 및 다음 페이지 개인화 사용 사례를 구성하는 데 도움이 됩니다.

이 문서에서는 이러한 사용 사례에 대한 Experience Platform 및 개인화 대상을 구성하는 방법에 대한 단계별 지침을 제공합니다.

## 1단계: Experience Platform Web SDK 데이터 스트림 구성 {#configure-datastream}

개인화 사용 사례를 구성하는 첫 번째 단계는 [!DNL Web SDK datastream].

다음 설명서에 설명된 지침을 따르십시오. [데이터 스트림 구성](../../edge/fundamentals/datastreams.md) 설명서.

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