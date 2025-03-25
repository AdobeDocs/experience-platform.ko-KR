---
keywords: 비행선 속성;비행선 목적지
title: 비행선 속성 연결
description: Airship 내에서 타깃팅할 대상 속성으로 Adobe 대상 데이터를 Airship에 원활하게 전달합니다.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 453884612e787439ea58f312d8080622ee0441f7
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# [!DNL Airship Attributes] 연결 {#airship-attributes-destination}

>[!IMPORTANT]
>
>* 2025년 3월 25일부터 대상 카탈로그에서 두 개의 [!DNL Airship Attributes] 카드를 나란히 볼 수 있습니다. 이는 대상 서비스에 대한 내부 업그레이드 때문입니다. 기존 [!DNL Airship Attributes] 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음) 비행선 특성]**(으)로 변경되었으며 이제 이름이 **[!UICONTROL 비행선 특성]**&#x200B;인 새 카드를 사용할 수 있습니다.
>* 새 활성화 데이터 흐름을 보려면 카탈로그의 **[!UICONTROL 비행선 특성]** 연결을 사용하십시오. **[!UICONTROL (더 이상 사용되지 않는) 비행선 특성]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 조치가 필요하지 않습니다.
>* [흐름 서비스 API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 만드는 경우 [!DNL flow spec ID] 및 [!DNL connection spec ID]을(를) 다음 값으로 업데이트해야 합니다.
>   * 흐름 사양 ID: `a862e0be-966e-4e5a-80d3-1bb566461986`
>   * 연결 사양 ID: `594bc002-4a47-49b7-8a98-ac0d21045502`

## 개요 {#overview}

[!DNL Airship]은(는) 선도적인 고객 참여 플랫폼으로, 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공할 수 있습니다.

이 통합은 타깃팅 또는 트리거를 위해 Adobe 프로필 데이터를 [특성](https://docs.airship.com/guides/audience/attributes/)&#x200B;(으)로 [!DNL Airship]에 전달합니다.

[!DNL Airship]에 대한 자세한 내용은 [비행선 문서](https://docs.airship.com)를 참조하세요.

>[!TIP]
>
>이 대상 커넥터 및 설명서 페이지는 [!DNL Airship] 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 [support.airship.com](https://support.airship.com/)으로 직접 연락하십시오.

## 전제 조건 {#prerequisites}

대상자를 [!DNL Airship]&#x200B;(으)로 보내려면 먼저 다음을 수행해야 합니다.

* [!DNL Airship] 프로젝트에서 특성을 사용하도록 설정합니다.
* 인증을 위한 전달자 토큰을 생성합니다.

>[!TIP]
>
>아직 만들지 않은 경우 [이 등록 링크](https://go.airship.eu/accounts/register/plan/starter/)를 통해 [!DNL Airship] 계정을 만드십시오.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 필드 매핑에 따라 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성) 및/또는 ID와 함께 세그먼트의 모든 멤버를 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 속성 활성화 {#enable-attributes}

Adobe Experience Platform 프로필 속성은 [!DNL Airship] 속성과 유사하며 이 페이지의 아래에 표시된 매핑 도구를 사용하여 플랫폼에서 서로 쉽게 매핑할 수 있습니다.

[!DNL Airship] 프로젝트에는 몇 가지 사전 정의된 특성과 기본 특성이 있습니다. 사용자 지정 특성이 있는 경우 먼저 [!DNL Airship]에서 정의해야 합니다. 자세한 내용은 [특성 설정 및 관리](https://docs.airship.com/tutorials/audience/attributes/)를 참조하십시오.

## 전달자 토큰 생성 {#bearer-token}

[비행선 대시보드](https://go.airship.com)의 **[!UICONTROL 설정]**&quot; **[!UICONTROL API 및 통합]**(으)로 이동한 다음 왼쪽 메뉴에서 **[!UICONTROL 토큰]**&#x200B;을(를) 선택하십시오.

**[!UICONTROL 토큰 만들기]**&#x200B;를 클릭합니다.

토큰에 대해 사용자에게 친숙한 이름(예: &quot;Adobe 속성 대상&quot;)을 제공하고 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.

**[!UICONTROL 토큰 만들기]**&#x200B;를 클릭하고 세부 정보를 기밀로 저장합니다.

## 사용 사례 {#use-cases}

[!DNL Airship Attributes] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 사용 사례 #1

[!DNL Airship]의 채널 내에서 메시지 및 풍부한 콘텐츠를 개인화하기 위해 Adobe Experience Platform 내에서 수집된 프로필 데이터를 활용합니다. 예를 들어 [!DNL Experience Platform] 프로필 데이터를 활용하여 [!DNL Airship] 내에서 위치 특성을 설정합니다. 이렇게 하면 호텔 브랜드에서 각 사용자에 대해 가장 가까운 호텔 위치에 대한 이미지를 표시할 수 있습니다.

### 사용 사례 #2

Adobe Experience Platform의 특성을 활용하여 [!DNL Airship] 프로필을 더욱 보강하고 SDK 또는 [!DNL Airship] 예측 데이터와 결합합니다. 예를 들어, 소매업체는 충성도 상태 및 위치 데이터(플랫폼의 속성)와 이탈할 것으로 예상되는 [!DNL Airship] 데이터로 대상자를 만들어 NV의 Las Vegas에 거주하고 이탈 가능성이 높은 Gold 충성도 상태의 사용자에게 타깃팅된 메시지를 보낼 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL 전달자 토큰]**: [!DNL Airship] 대시보드에서 생성한 전달자 토큰입니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력하십시오.
* **[!UICONTROL 도메인]**: 이 대상에 적용되는 [!DNL Airship] 데이터 센터에 따라 미국 또는 유럽 연합 데이터 센터를 선택하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 매핑 고려 사항 {#mapping-considerations}

[!DNL Airship] 특성은 장치 인스턴스(예: iPhone)를 나타내는 채널 또는 사용자의 모든 장치를 고객 ID와 같은 공통 식별자에 매핑하는 명명된 사용자에 대해 설정할 수 있습니다. 스키마에 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우 **[!UICONTROL Source 특성]**&#x200B;에서 이메일 필드를 선택하고 아래와 같이 **[!UICONTROL Target ID]** 아래의 오른쪽 열에 있는 [!DNL Airship] 명명된 사용자에게 매핑합니다.

![명명된 사용자 매핑](../../assets/catalog/mobile-engagement/airship/mapping.png)

채널, 즉 디바이스에 매핑해야 하는 식별자의 경우 소스를 기반으로 적절한 채널에 매핑합니다. 다음 이미지는 두 개의 매핑이 생성되는 방식을 보여 줍니다.

* [!DNL Airship] iOS 채널에 대한 IDFA iOS Advertising ID
* [!DNL Airship] &quot;Full Name&quot; 특성에 대한 Adobe `fullName` 특성

>[!NOTE]
>
>특성 매핑에 대한 대상 필드를 선택할 때 [!DNL Airship] 대시보드에 나타나는 알기 쉬운 이름을 사용하십시오.

**ID 매핑**

소스 필드 선택:

![비행선 특성에 연결](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

대상 필드 선택:

![비행선 특성에 연결](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**특성 매핑**

소스 속성 선택:

![소스 필드 선택](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

대상 속성 선택:

![대상 필드 선택](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

매핑 확인:

![채널 매핑](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../../data-governance/home.md)를 참조하십시오.
