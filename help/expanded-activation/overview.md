---
title: Audience Manager 확장 활성화
description: Audience Manager Expanded Activation을 통해 Audience Manager 대상자를 소셜 및 광고 대상으로 활성화하는 방법을 알아봅니다.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# Audience Manager 확장 활성화

Adobe Experience Platform을 기반으로 구축된 Audience Manager 확장 활성화는 기존 [Audience Manager](https://experienceleague.adobe.com/ko/docs/audience-manager/user-guide/aam-home) 사용자가 대상을 Real-Time CDP의 [소셜](../destinations/catalog/social/overview.md) 및 [광고](../destinations/catalog/advertising/overview.md) 대상 플랫폼(예: [Facebook](../destinations/catalog/social/facebook.md), [Google 광고](../destinations/catalog/advertising/google-ads-destination.md) 등)으로 활성화하도록 지원합니다.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation]은(는) 기존 [!DNL Audience Manager]명의 사용자만 사용할 수 있습니다.

## 용어 {#terminology}

Audience Manager Expanded Activation은 Adobe Experience Platform의 개념 및 구성 요소를 사용합니다. 확장된 활성화 워크플로 및 사용할 구성 요소를 더 잘 이해하려면 다음 개념을 기본적으로 이해해야 합니다.

* [대상](../segmentation/ui/overview.md): 대상은 유사한 동작 및/또는 특성을 공유하는 사람들의 집합입니다. 이 인물 컬렉션은 Adobe Experience Platform에서 세그먼트 정의 또는 대상자 구성(Experience Platform 생성 대상자)을 사용하여 생성하거나, 외부 소스(예: 사용자 정의 업로드(외부 생성 대상자)에서 생성할 수 있습니다. 확장된 활성화에서 Audience Manager 세그먼트(대상자)를 [사용자 지정 업로드](../segmentation/ui/audience-portal.md#import-audience)(으)로 가져옵니다.
* [Source 커넥터](../sources/home.md): Source 커넥터(소스라고도 함)는 Experience Platform 사용자가 여러 소스의 데이터를 쉽게 수집할 수 있도록 지원하므로 Experience Platform 서비스를 사용하여 데이터의 구조, 레이블 지정 및 개선을 허용합니다. 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.
* [대상 커넥터](../destinations/home.md): 대상은 대상이 활성화되고 전달되는 Adobe 애플리케이션, 광고 플랫폼, 클라우드 저장소 서비스 또는 마케팅 서비스와 같은 끝점을 설명합니다. [!DNL Expanded Activation]은(는) [advertising](../destinations/catalog/advertising/overview.md) 및 [social](../destinations/catalog/social/overview.md) 대상 커넥터에 대한 대상 활성화를 지원합니다.

## 전제 조건 {#prerequisites}

확장된 활성화를 통해 대상을 활성화하려면 먼저 아래에 설명된 사전 요구 사항을 충족하는지 확인하십시오.

### 사용자 및 역할 요구 사항 {#permission-requirements}

[!DNL Expanded Activation]을(를) 사용하려면 먼저 Admin Console에서 사용자 계정을 만들어 [!DNL Expanded Activation] 역할에 할당해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 지침은 [관리](administration.md) 페이지를 참조하세요.

### 대상 요구 사항 {#audience-requirements}

[!DNL Expanded Activation]을(를) 통해 대상자를 활성화하려면 Audience Manager 대상자가 **해시된 이메일 주소**&#x200B;를 기반으로 하는지 확인하십시오. Audience Manager 사용을 기반으로 두 가지 방법으로 이를 확인할 수 있습니다.

* [Audience Manager 사용자 기반 대상](https://experienceleague.adobe.com/ko/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 기능을 사용하는 경우 Audience Manager에서 이미 해시된 이메일 주소를 섭취하는 것입니다. 이 경우 수행해야 하는 추가 단계는 없습니다. [확장된 활성화를 통해 대상자 활성화](activate-audiences.md)(으)로 건너뛸 수 있습니다.
* [Audience Manager 사용자 기반 대상](https://experienceleague.adobe.com/ko/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 기능을 사용하는 _not_&#x200B;인 경우 Audience Manager에서 새 데이터 원본을 만들고 이를 사용하여 해시된 전자 메일 주소를 저장해야 합니다. 이 작업을 수행하는 방법에 대해 알아보려면 [해시된 이메일 워크플로우에 대한 데이터 소스 구성](https://experienceleague.adobe.com/ko/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails)에 대한 설명서를 참조하십시오. Audience Manager 데이터 소스에서 해시된 이메일 주소를 수집했으면 [확장된 활성화를 통해 대상 활성화](activate-audiences.md)에 대한 설명서를 읽어 보십시오.

## 다음 단계 {#next-steps}

[!DNL Expanded Activation]을(를) 사용하여 사용 사례와 이점을 더 잘 이해했으므로 [계정 구성](administration.md)을 시작한 다음 [대상자를 활성화](activate-audiences.md)하세요.
