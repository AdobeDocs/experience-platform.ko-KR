---
keywords: 비행선 속성;비행선 목적지
title: Airship 속성 연결
description: Airship 내에서 타깃팅할 대상 속성으로 Adobe 대상 데이터를 Airship에 원활하게 전달합니다.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# [!DNL Airship Attributes] 연결 {#airship-attributes-destination}

## 개요 {#overview}

[!DNL Airship] 는 고객 참여형 플랫폼을 기반으로 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공할 수 있습니다.

이 통합은 Adobe 프로필 데이터를 [!DNL Airship] 로서의 [속성](https://docs.airship.com/guides/audience/attributes/) 타깃팅 또는 트리거용.

에 대해 자세히 알아보려면 [!DNL Airship]를 참조하고 [항공편 문서](https://docs.airship.com).

>[!TIP]
>
>이 설명서 페이지는 [!DNL Airship] 팀 문의 사항이나 업데이트 요청에 대해서는 [support.airship.com](https://support.airship.com/).

## 전제 조건 {#prerequisites}

대상 세그먼트를 보내기 전에 [!DNL Airship]:

* 에서 속성을 활성화합니다 [!DNL Airship] 프로젝트.
* 인증을 위한 베어러 토큰을 생성합니다.

>[!TIP]
>
>만들기 [!DNL Airship] 다음 계정으로 [이 등록 링크](https://go.airship.eu/accounts/register/plan/starter/) 아직 안하셨다면

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 필드 매핑에 따라 이메일 주소, 전화번호, 성) 및/또는 id를 지정합니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 속성 활성화 {#enable-attributes}

Adobe Experience Platform 프로필 속성은 다음과 유사합니다 [!DNL Airship] 이 페이지에서 아래에 자세히 나와 있는 매핑 도구를 사용하여 Platform에서 특성을 쉽게 서로 매핑할 수 있습니다.

[!DNL Airship] 프로젝트에는 몇 가지 사전 정의된 및 기본 속성이 있습니다. 사용자 지정 속성이 있는 경우에서 정의해야 합니다 [!DNL Airship] 먼저 자세한 내용은 [속성 설정 및 관리](https://docs.airship.com/tutorials/audience/attributes/) 자세한 내용

## 베어러 토큰 생성 {#bearer-token}

이동 **[!UICONTROL 설정]** &quot; **[!UICONTROL API 및 통합]** 에서 [항공기 대시보드](https://go.airship.com) 을(를) 선택합니다. **[!UICONTROL 토큰]** 왼쪽 메뉴에 있습니다.

클릭 **[!UICONTROL 토큰 만들기]**.

토큰에 대해 사용자에게 친숙한 이름을 입력하고(예: &quot;Adobe 속성 대상&quot;) 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.

클릭 **[!UICONTROL 토큰 만들기]** 자세한 내용은 기밀로 저장합니다.

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Airship Attributes] 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 #1

Adobe Experience Platform 내에서 수집된 프로필 데이터를 활용하여 메시지 및 풍부한 컨텐츠를 개인화할 수 있습니다 [!DNL Airship]의 채널입니다. 예를 들어, [!DNL Experience Platform] 내에서 위치 속성을 설정하기 위한 프로필 데이터 [!DNL Airship]. 이를 통해 호텔 브랜드에서는 각 사용자의 가장 가까운 호텔 위치에 대한 이미지를 표시할 수 있습니다.

### 사용 사례 #2

Adobe Experience Platform의 특성을 활용하여 추가 기능 강화 [!DNL Airship] 프로필 및 SDK와 결합 또는 [!DNL Airship] 예측 데이터. 예를 들어 소매업체는 충성도 상태 및 위치 데이터(플랫폼의 특성)가 있는 세그먼트를 만들 수 있습니다. [!DNL Airship] 라스베이거스에 사는 골드 충성도 상태에 있는 사용자에게 고도로 타겟팅된 메시지를 전송하기 위해 데이터를 이탈할 것으로 예상되며 대량 추교 가능성이 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 베어러 토큰]**: 에서 생성한 bearer 토큰 [!DNL Airship] 대시보드 .

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 도메인]**: EU 데이터 센터를 선택할 때 [!DNL Airship] 데이터 센터는 이 대상에 적용됩니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 매핑 고려 사항 {#mapping-considerations}

[!DNL Airship] 속성은 모든 사용자의 장치를 고객 ID와 같은 일반 식별자에 매핑하는 장치 인스턴스(예: iPhone 또는 명명된 사용자)를 나타내는 채널에서 설정할 수 있습니다. 스키마에 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우, **[!UICONTROL 소스 속성]** 및에 매핑 [!DNL Airship] 아래의 오른쪽 열에 이름이 지정된 사용자 **[!UICONTROL Target ID]**&#x200B;아래에 표시된 대로,

![명명된 사용자 매핑](../../assets/catalog/mobile-engagement/airship/mapping.png)

채널에 매핑되어야 하는 식별자, 즉 장치의 경우 소스를 기반으로 적절한 채널에 매핑해야 합니다. 다음 이미지는 두 개의 매핑을 만드는 방법을 보여줍니다.

* IDFA iOS 광고 ID를 [!DNL Airship] iOS 채널
* Adobe `fullName` 속성 [!DNL Airship] &quot;Full Name&quot; 속성

>[!NOTE]
>
>에 표시되는 사용자에게 친숙한 이름을 사용합니다. [!DNL Airship] 대시보드 를 클릭합니다.

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

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](../../../data-governance/home.md).
