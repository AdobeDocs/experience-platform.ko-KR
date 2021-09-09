---
keywords: 비행선 속성;비행선 목적지
title: Airship 속성 연결
description: Airship 내에서 타깃팅할 대상 속성으로 Adobe 대상 데이터를 Airship에 원활하게 전달합니다.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# [!DNL Airship Attributes] 연결 {#airship-attributes-destination}

## 개요 {#overview}

[!DNL Airship] 는 고객 참여형 플랫폼을 기반으로 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공할 수 있습니다.

이 통합은 타깃팅 또는 트리거링을 위해 Adobe 프로필 데이터를 [속성](https://docs.airship.com/guides/audience/attributes/)으로 [!DNL Airship]에 전달합니다.

[!DNL Airship]에 대해 자세히 알아보려면 [Airship Docs](https://docs.airship.com)를 참조하십시오.

>[!TIP]
>
>이 설명서 페이지는 [!DNL Airship] 팀이 만들었습니다. 문의 사항이나 업데이트 요청은 [support.airship.com](https://support.airship.com/)에서 직접 문의하십시오.

## 전제 조건 {#prerequisites}

대상 세그먼트를 [!DNL Airship]에 보내려면 먼저 다음을 수행해야 합니다.

* [!DNL Airship] 프로젝트에서 특성을 활성화합니다.
* 인증을 위한 베어러 토큰을 생성합니다.

>[!TIP]
>
>아직 수행하지 않았다면 [이 등록 링크](https://go.airship.eu/accounts/register/plan/starter/)를 통해 [!DNL Airship] 계정을 만듭니다.

## 속성 활성화 {#enable-attributes}

Adobe Experience Platform 프로필 속성은 [!DNL Airship] 속성과 유사하며 이 페이지에서 아래에 자세히 나와 있는 매핑 도구를 사용하여 Platform에서 서로 쉽게 매핑할 수 있습니다.

[!DNL Airship] 프로젝트에는 몇 가지 사전 정의된 및 기본 속성이 있습니다. 사용자 지정 특성이 있는 경우 먼저 [!DNL Airship]에서 정의해야 합니다. 자세한 내용은 [속성 설정 및 관리](https://docs.airship.com/tutorials/audience/attributes/)를 참조하십시오.

## 베어러 토큰 생성 {#bearer-token}

[Airship Dashboard](https://go.airship.com)에서 **[!UICONTROL 설정]**&quot; **[!UICONTROL API 및 통합]**&#x200B;으로 이동한 다음 왼쪽 메뉴에서 **[!UICONTROL 토큰]**&#x200B;을 선택합니다.

**[!UICONTROL 토큰 만들기]**&#x200B;를 클릭합니다.

토큰에 대해 사용자에게 친숙한 이름을 입력하고(예: &quot;Adobe 속성 대상&quot;) 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.

**[!UICONTROL 토큰 만들기]**&#x200B;를 클릭하고 세부 정보를 기밀로 저장합니다.

## 사용 사례 {#use-cases}

[!DNL Airship Attributes] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례가 여기에 있습니다.

### 사용 사례 #1

Adobe Experience Platform 내에서 수집된 프로필 데이터를 활용하여 메시지의 개인화와 [!DNL Airship] 의 채널 내에 있는 풍부한 콘텐츠를 활용하십시오. 예를 들어 [!DNL Experience Platform] 프로필 데이터를 활용하여 [!DNL Airship] 내에서 위치 속성을 설정합니다. 이를 통해 호텔 브랜드에서는 각 사용자의 가장 가까운 호텔 위치에 대한 이미지를 표시할 수 있습니다.

### 사용 사례 #2

Adobe Experience Platform의 속성을 활용하여 [!DNL Airship] 프로필을 추가로 보강하고 SDK 또는 [!DNL Airship] 예측 데이터와 결합합니다. 예를 들어 소매업체는 충성도 상태 및 위치 데이터(플랫폼의 특성)가 있는 세그먼트를 만들고, Las Vegas, NV에 거주하는 골드 충성도 상태의 사용자에게 고도로 타겟팅된 메시지를 전송하기 위해 데이터를 이탈할 것으로 예측하여 대량 추론 가능성이 높은 세그먼트를 만들 수 있습니다.[!DNL Airship]

## 대상에 연결 {#connect}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 베어러 토큰]**: 대시보드에서 생성한 베어러  [!DNL Airship] 토큰입니다.
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 도메인]**: 이 대상에 적용되는  [!DNL Airship] 데이터 센터에 따라 미국 또는 EU 데이터 센터를 선택합니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 매핑 고려 사항 {#mapping-considerations}

[!DNL Airship] 속성은 모든 사용자의 장치를 고객 ID와 같은 일반 식별자에 매핑하는 장치 인스턴스(예: iPhone 또는 명명된 사용자)를 나타내는 채널에서 설정할 수 있습니다. 스키마에 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우, **[!UICONTROL 소스 속성]**&#x200B;에서 이메일 필드를 선택하고 아래 표시된 대로 **[!UICONTROL Target ID]** 아래의 오른쪽 열에 있는 [!DNL Airship] 명명된 사용자에게 매핑합니다.

![명명된 사용자 매핑](../../assets/catalog/mobile-engagement/airship/mapping.png)

채널에 매핑되어야 하는 식별자, 즉 장치의 경우 소스를 기반으로 적절한 채널에 매핑해야 합니다. 다음 이미지는 두 개의 매핑을 만드는 방법을 보여줍니다.

* IDFA iOS 광고 ID를 [!DNL Airship] iOS 채널에
* [!DNL Airship] &quot;Full Name&quot; 속성에 대한 `fullName` 속성

>[!NOTE]
>
>속성 매핑에 대한 대상 필드를 선택할 때 [!DNL Airship] 대시보드에 나타나는 사용자에게 친숙한 이름을 사용합니다.

**ID 매핑**

소스 필드 선택:

![Airship 속성에 연결](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

대상 필드 선택:

![Airship 속성에 연결](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**맵 속성**

소스 속성 선택:

![소스 필드 선택](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

대상 속성 선택:

![대상 필드 선택](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

매핑 확인:

![채널 매핑](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../../data-governance/home.md)를 참조하십시오.
