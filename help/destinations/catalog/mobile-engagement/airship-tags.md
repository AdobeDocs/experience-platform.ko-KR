---
keywords: 항공 태그;항공 운항 대상
title: Airship 태그 연결
description: Airship 내에서 타깃팅할 대상 태그로 Adobe 대상 데이터를 Airship에 원활하게 전달합니다.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: e413933920028e3239f6044111d9cf215c865eba
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# (베타) [!DNL Airship Tags] 연결 {#airship-tags-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform의 [!DNL Airship Tags] 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요

[!DNL Airship] 는 고객 참여형 플랫폼을 기반으로 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공할 수 있습니다.

이 통합은 타깃팅 또는 트리거링을 위해 Adobe Experience Platform 세그먼트 데이터를 [태그](https://docs.airship.com/guides/audience/tags/)로 [!DNL Airship]에 전달합니다.

[!DNL Airship]에 대해 자세히 알아보려면 [Airship Docs](https://docs.airship.com)를 참조하십시오.


>[!TIP]
>
>이 설명서 페이지는 [!DNL Airship] 팀이 만들었습니다. 문의 사항이나 업데이트 요청은 [support.airship.com](https://support.airship.com/)에서 직접 문의하십시오.

## 전제 조건

Adobe Experience Platform 세그먼트를 [!DNL Airship]에 보내려면 먼저 다음을 수행해야 합니다.

* [!DNL Airship] 프로젝트에서 태그 그룹을 만듭니다.
* 인증을 위한 베어러 토큰을 생성합니다.

>[!TIP]
> 
>아직 수행하지 않았다면 [이 등록 링크](https://go.airship.eu/accounts/register/plan/starter/)를 통해 [!DNL Airship] 계정을 만듭니다.

## 태그 그룹

Adobe Experience Platform의 세그먼트 개념은 Airship의 [태그](https://docs.airship.com/guides/audience/tags/)와 비슷하며 구현에 약간 차이가 있습니다. 이 통합은 Experience Platform 세그먼트](../../../xdm/field-groups/profile/segmentation.md)에서 사용자의 [멤버십의 상태를 [!DNL Airship] 태그의 존재 여부에 매핑합니다. 예를 들어 `xdm:status`이 `realized`로 변경되는 Platform 세그먼트에서 태그가 [!DNL Airship] 채널에 추가되거나 이 프로필이 매핑된 이름이 지정된 사용자에게 추가됩니다. `xdm:status`이 `exited`로 변경되면 태그가 제거됩니다.

이 통합을 사용하려면 `adobe-segments`라는 [!DNL Airship]에 *태그 그룹*&#x200B;을 만드십시오.

>[!IMPORTANT]
>
>새 태그 그룹 **을 만들 때 &quot;[!DNL Allow these tags to be set only from your server]&quot;라는 라디오 단추를 선택하지 마십시오.** 이렇게 하면 Adobe 태그 통합이 실패합니다.

태그 그룹 만들기에 대한 지침은 [태그 그룹 관리](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)를 참조하십시오.

## 베어러 토큰 생성

[Airship Dashboard](https://go.airship.com)에서 **[!UICONTROL 설정]**&quot; **[!UICONTROL API 및 통합]**&#x200B;으로 이동한 다음 왼쪽 메뉴에서 **[!UICONTROL 토큰]**&#x200B;을 선택합니다.

**[!UICONTROL 토큰 만들기]**&#x200B;를 클릭합니다.

토큰에 대해 사용자에게 친숙한 이름을 입력하고(예: &quot;Adobe 태그 대상&quot;) 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.

**[!UICONTROL 토큰 만들기]**&#x200B;를 클릭하고 세부 정보를 기밀로 저장합니다.

## 사용 사례

[!DNL Airship Tags] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례가 여기에 있습니다.

### 사용 사례 #1

소매업체 또는 엔터테인먼트 플랫폼은 충성도 고객에 대한 사용자 프로필을 만들고 모바일 캠페인에 대한 메시지 타깃팅을 위해 해당 세그먼트를 [!DNL Airship]에 전달할 수 있습니다.

### 사용 사례 #2

사용자가 Adobe Experience Platform 내의 특정 세그먼트에 속하거나 해당 세그먼트에 포함할 때 실시간으로 일대일 메시지를 트리거합니다.

예를 들어 소매업체는 플랫폼에서 청바지 브랜드별 세그먼트를 설정합니다. 이제 해당 소매업체는 고객이 청바지의 선호도를 특정 브랜드로 설정하자마자 모바일 메시지를 트리거할 수 있습니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 베어러 토큰]**: 대시보드에서 생성한 베어러  [!DNL Airship] 토큰입니다.
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 도메인]**: 이 대상에 적용되는  [!DNL Airship] 데이터 센터에 따라 미국 또는 EU 데이터 센터를 선택합니다.


## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 매핑 고려 사항 {#mapping-considerations}

[!DNL Airship] 태그는 장치 인스턴스(예: iPhone 또는 지정된 사용자)를 나타내는 채널에서 설정할 수 있으며, 이 채널에서는 사용자의 모든 장치를 고객 ID와 같은 일반 식별자에 매핑합니다. 스키마에 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우, **[!UICONTROL 소스 속성]**&#x200B;에서 이메일 필드를 선택하고 아래 표시된 대로 **[!UICONTROL Target ID]** 아래의 오른쪽 열에 있는 [!DNL Airship] 명명된 사용자에게 매핑합니다.

![명명된 사용자 매핑](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

채널에 매핑되어야 하는 식별자, 즉 장치의 경우 소스를 기반으로 적절한 채널에 매핑해야 합니다. 다음 이미지는 Google 광고 ID를 [!DNL Airship] Android 채널에 매핑하는 방법을 보여줍니다.

![Airship 태그에 ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![연결Airship 태그](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![에 연결채널 매핑](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../../data-governance/home.md)를 참조하십시오.
