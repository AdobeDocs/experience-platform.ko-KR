---
title: Audience Manager 확장 활성화
description: 확장된 Audience Manager 활성화를 통해 소셜 및 광고 대상에 Audience Manager 대상을 활성화하는 방법을 알아봅니다.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Audience Manager 확장 활성화

Adobe Experience Platform을 기반으로 구축된 Audience Manager 확장 활성화는 기존 [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) 사용자는 대상자를에 활성화합니다. [소셜](../destinations/catalog/social/overview.md) 및 [advertising](../destinations/catalog/advertising/overview.md) 다음과 같은 Real-Time CDP의 대상 플랫폼 [Facebook](../destinations/catalog/social/facebook.md), [Google 광고](../destinations/catalog/advertising/google-ads-destination.md)등.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] 은(는) 기존 에만 사용할 수 있습니다. [!DNL Audience Manager] 사용자.

## 용어 {#terminology}

Audience Manager 확장 활성화는 Adobe Experience Platform의 개념 및 구성 요소를 사용합니다. 확장된 활성화 워크플로 및 사용할 구성 요소를 더 잘 이해하려면 다음 개념을 기본적으로 이해해야 합니다.

* [대상](../segmentation/ui/overview.md): 대상자는 유사한 행동 및/또는 특성을 공유하는 사람들의 집합입니다. 이 인물 컬렉션은 세그먼트 정의 또는 대상자 구성(플랫폼 생성 대상자)을 사용하여 Adobe Experience Platform에서 생성하거나, 사용자 지정 업로드(외부 생성 대상자)와 같은 외부 소스에서 생성할 수 있습니다. 확장된 활성화에서 Audience Manager 세그먼트(대상)를 (으)로 가져옵니다. [사용자 정의 업로드](../segmentation/ui/audience-portal.md#import-audience).
* [Source 커넥터](../sources/home.md): Source 커넥터(소스라고도 함)는 Experience Platform 사용자가 여러 소스의 데이터를 쉽게 수집할 수 있도록 지원하므로 Experience Platform 서비스를 사용하여 데이터의 구조, 레이블 지정 및 개선을 허용합니다. 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.
* [대상 커넥터](../destinations/home.md): 대상은 대상이 활성화되고 전달되는 Adobe 애플리케이션, 광고 플랫폼, 클라우드 스토리지 서비스 또는 마케팅 서비스와 같은 끝점을 설명합니다. [!DNL Expanded Activation] 는에 대한 대상 활성화를 지원합니다. [advertising](../destinations/catalog/advertising/overview.md) 및 [소셜](../destinations/catalog/social/overview.md) 대상 커넥터.

## 전제 조건 {#prerequisites}

확장된 활성화를 통해 대상을 활성화하려면 먼저 아래에 설명된 사전 요구 사항을 충족하는지 확인하십시오.

### 사용자 및 역할 요구 사항 {#permission-requirements}

을(를) 사용하기 전에 [!DNL Expanded Activation]을(를) 사용하려면 Admin Console에서 사용자 계정을 만들고 [!DNL Expanded Activation] 역할. 다음을 참조하십시오. [관리](administration.md) 페이지 를 클릭하여 이 작업을 수행하는 방법에 대한 자세한 지침을 확인하십시오.

### 대상 요구 사항 {#audience-requirements}

다음을 통해 대상자를 활성화하려면 [!DNL Expanded Activation], Audience Manager 대상이 다음을 기반으로 하는지 확인합니다. **해시된 이메일 주소**. Audience Manager 사용을 기반으로 두 가지 방법으로 이를 확인할 수 있습니다.

* 를 사용하는 경우 [사용자 기반 대상 Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 그러면 이미 Audience Manager에서 해시된 이메일 주소를 수집하고 있는 것입니다. 이 경우 수행해야 하는 추가 단계는 없습니다. 다음으로 건너뛸 수 있습니다. [확장된 활성화를 통해 대상자 활성화](activate-audiences.md).
* 다음과 같은 경우 _아님_ 사용 [사용자 기반 대상 Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 기능을 사용하려면 Audience Manager에서 새 데이터 소스를 만들고 이 데이터 소스를 사용하여 해시된 이메일 주소를 저장해야 합니다. 다음에서 설명서를 참조하십시오. [해시된 이메일 워크플로우에 대한 데이터 소스 구성](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) 을(를) 만드는 방법을 알아봅니다. Audience Manager 데이터 소스에서 해시된 이메일 주소를 수집하면에 대한 설명서를 읽습니다. [확장된 활성화를 통해 대상자 활성화](activate-audiences.md).

## 다음 단계 {#next-steps}

이제 사용 사례와 사용의 이점을 더 잘 이해했습니다 [!DNL Expanded Activation], 시작 [계정 구성](administration.md) 그런 다음 [대상자 활성화](activate-audiences.md).
