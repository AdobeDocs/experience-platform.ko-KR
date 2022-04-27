---
keywords: 항공 태그;항공 운항 대상
title: Airship 태그 연결
description: Airship 내에서 타깃팅할 대상 태그로 Adobe 대상 데이터를 Airship에 원활하게 전달합니다.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 1%

---

# [!DNL Airship Tags] 연결 {#airship-tags-destination}

## 개요

[!DNL Airship] 는 고객 참여형 플랫폼을 기반으로 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공할 수 있습니다.

이 통합은 Adobe Experience Platform 세그먼트 데이터를 [!DNL Airship] 로서의 [태그](https://docs.airship.com/guides/audience/tags/) 타깃팅 또는 트리거용.

에 대해 자세히 알아보려면 [!DNL Airship]를 참조하고 [항공편 문서](https://docs.airship.com).


>[!TIP]
>
>이 설명서 페이지는 [!DNL Airship] 팀 문의 사항이나 업데이트 요청에 대해서는 [support.airship.com](https://support.airship.com/).

## 전제 조건

Adobe Experience Platform 세그먼트를 [!DNL Airship]:

* 에서 태그 그룹을 만듭니다 [!DNL Airship] 프로젝트.
* 인증을 위한 베어러 토큰을 생성합니다.

>[!TIP]
> 
>만들기 [!DNL Airship] 다음 계정으로 [이 등록 링크](https://go.airship.eu/accounts/register/plan/starter/) 아직 안하셨다면

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | Airship 태그 대상에 사용된 식별자를 사용하여 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 태그 그룹

Adobe Experience Platform의 세그먼트 개념은 다음과 유사합니다 [태그](https://docs.airship.com/guides/audience/tags/) 비행선에서 약간의 차이가 있습니다. 이 통합은 사용자의 상태를 매핑합니다 [Experience Platform 세그먼트의 멤버십](../../../xdm/field-groups/profile/segmentation.md) 무참히 [!DNL Airship] 태그에 가깝게 포함했습니다. 예를 들어, `xdm:status` 변경 사항 `realized`로 지정하는 경우, 태그가 [!DNL Airship] 이 프로필이 매핑된 채널 또는 명명된 사용자입니다. 만약 `xdm:status` 변경 사항 `exited`로 설정되면 태그가 제거됩니다.

이 통합을 사용하려면 *태그 그룹* in [!DNL Airship] 명명된 이름 `adobe-segments`.

>[!IMPORTANT]
>
>새 태그 그룹을 만들 때 **확인 안 함** &quot;라는 라디오 버튼[!DNL Allow these tags to be set only from your server]&quot;. 이렇게 하면 Adobe 태그 통합이 실패합니다.

자세한 내용은 [태그 그룹 관리](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 를 참조하십시오.

## 베어러 토큰 생성

이동 **[!UICONTROL 설정]** &quot; **[!UICONTROL API 및 통합]** 에서 [항공기 대시보드](https://go.airship.com) 을(를) 선택합니다. **[!UICONTROL 토큰]** 왼쪽 메뉴에 있습니다.

클릭 **[!UICONTROL 토큰 만들기]**.

토큰에 대해 사용자에게 친숙한 이름을 입력하고(예: &quot;Adobe 태그 대상&quot;) 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.

클릭 **[!UICONTROL 토큰 만들기]** 자세한 내용은 기밀로 저장합니다.

## 사용 사례

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Airship Tags] 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 #1

소매업체 또는 엔터테인먼트 플랫폼은 충성도 고객에 대한 사용자 프로필을 만들고 이러한 세그먼트를 로 전달할 수 있습니다 [!DNL Airship] 모바일 캠페인에 대한 메시지 타깃팅용.

### 사용 사례 #2

사용자가 Adobe Experience Platform 내의 특정 세그먼트에 속하거나 해당 세그먼트에 포함할 때 실시간으로 일대일 메시지를 트리거합니다.

예를 들어 소매업체는 플랫폼에서 청바지 브랜드별 세그먼트를 설정합니다. 이제 해당 소매업체는 고객이 청바지의 선호도를 특정 브랜드로 설정하자마자 모바일 메시지를 트리거할 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 베어러 토큰]**: 에서 생성한 bearer 토큰 [!DNL Airship] 대시보드 .
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 도메인]**: EU 데이터 센터를 선택할 때 [!DNL Airship] 데이터 센터는 이 대상에 적용됩니다.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 매핑 고려 사항 {#mapping-considerations}

[!DNL Airship] 태그는 장치 인스턴스(예: iPhone 또는 명명된 사용자)를 나타내는 채널에서 설정할 수 있으며, 이 사용자는 모든 사용자의 장치를 고객 ID와 같은 일반 식별자에 매핑합니다. 스키마에 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우, **[!UICONTROL 소스 속성]** 및에 매핑 [!DNL Airship] 아래의 오른쪽 열에 이름이 지정된 사용자 **[!UICONTROL Target ID]**&#x200B;아래에 표시된 대로,

![명명된 사용자 매핑](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

채널에 매핑되어야 하는 식별자, 즉 장치의 경우 소스를 기반으로 적절한 채널에 매핑해야 합니다. 다음 이미지는 Google 광고 ID를 [!DNL Airship] Android 채널.

![비행기 태그에 연결](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![비행기 태그에 연결](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![채널 매핑](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용 을 참조하십시오. [데이터 거버넌스 개요](../../../data-governance/home.md).
