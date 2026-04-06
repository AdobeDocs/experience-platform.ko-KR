---
title: Adobe Advertising DSP 연결
description: 여러 ID 유형을 사용하여 인증되고 인증되지 않은 자사 대상을 Adobe Advertising Demand-Side Platform(DSP)와 공유하는 방법을 알아봅니다.
feature: Destinations
exl-id: 0ff80d38-993f-4609-bf2a-01a3e6cfe10b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 6%

---

# Adobe Advertising DSP 연결

## 개요 {#overview}

Adobe Advertising Demand-Side Platform(DSP) 대상을 사용하면 인증된 퍼스트 파티 대상과 인증되지 않은 퍼스트 파티 대상을 DSP 계정 또는 계정 내의 특정 광고주와 공유할 수 있습니다.

이 대상을 통해 고객은 다음 ID 중 일부 또는 모두와 자사 대상을 공유할 수 있습니다.

* DSP에서 타깃팅하기 위해 [!DNL LiveRamp RampID] 또는 [!DNL Unified ID 2.0]&#x200B;(UID2.0)로 변환되는 해시된 이메일 ID

* Experience Cloud ID(ECID) 및 Adobe Advertising 서드파티 쿠키

* 모바일 광고 ID(MAID):

   * [!DNL Google] 장치의 [!DNL Android] Advertising ID(GAID)

   * [!DNL Apple iOS]개 장치의 IDFA(광고주)에 대한 식별자

이 연결은 해시된 이메일 주소만 지원하는 [기존 Adobe Advertising Cloud DSP 연결](adobe-advertising-cloud-dsp-connection-legacy.md)을 대체합니다.

>[!IMPORTANT]
>
>이 페이지는 Adobe Advertising [!DNL DSP] 팀에서 만들었습니다. 문의 사항이나 업데이트 요청이 있으면 `adcloud_support@adobe.com`에서 직접 Advertising 지원 팀에 문의하십시오.

## 사용 사례 {#use-cases}

이 대상을 사용하면 광고주가 쿠키 없이 쿠키를 사용하여 브라우저 전반의 대상자에게 도달할 수 있습니다.

광고주는 인증된 자사 식별자(예: [!DNL RampID] 및 [!DNL UID2.0])나 인증되지 않은 ID(예: 쿠키 및 MAID)로 세그먼트를 공유할 수 있습니다.

## 전제 조건 {#prerequisites}

* [!DNL RampID activation]의 경우 [!DNL DSP] 계정 수준 및 캠페인 수준 설정을 통해 대상자를 [!DNL LiveRamp RampID]과(와) 공유할 수 있게 함으로써 고객 데이터를 [!DNL RampIDs]&#x200B;(으)로 변환하여 타깃팅 가능한 세그먼트를 만듭니다. Adobe 계정 팀이 이 구성을 수행합니다. [!DNL RampID]은(는) [!DNL DSP]과(와) [!DNL LiveRamp] 간의 파트너 관계를 통해 사용할 수 있으며, [!DNL LiveRamp] 멤버십이 없어도 사용할 수 있습니다.

* 대상 ID:

   * [!DNL RampID] 및 [!DNL UID2.0]의 경우 프로필에 해시된 이메일 ID가 있어야 합니다.

   * 쿠키의 경우 [!DNL Web SDK] 데이터스트림 또는 [!DNL Experience Cloud ID Service] 중 하나로 쿠키 동기화 프로세스를 설정하십시오. 아래 [쿠키를 공유하도록 ID 동기화 설정](#cookie-sync)을 참조하세요.

   * MAID가 있는 프로필:

      * 각 GAID에 대해 IdentityMap 열에 값 `GAID`을(를) 포함합니다.

      * 각 IDFA에 대해 IdentityMap 열에 값 `IDFA`을(를) 포함합니다.

* Experience Platform 계정용 Experience Cloud 조직 ID입니다. ID는 Adobe [!DNL Real-Time Customer Data Platform]&#x200B;([!DNL Real-Time CDP]) 사용자 프로필 페이지에서 찾을 수 있습니다.

* 캠페인 활성화를 위한 대상을 받을 [[!DNL Real-Time CDP] DSP의 소스](https://experienceleague.adobe.com/en/docs/advertising/dsp/audiences/sources/source-manage)입니다. Adobe 계정 팀은 Experience Cloud 조직 ID를 사용하여 소스를 만듭니다.

* [!DNL DSP] 계정 또는 광고주에 대한 소스 키입니다. [[!DNL Real-Time CDP] 소스가  [!DNL DSP]](https://experienceleague.adobe.com/en/docs/advertising/dsp/audiences/sources/source-manage)에 생성될 때 생성됩니다. [!DNL DSP] 계정 팀이 이 키를 공유합니다. 아래 설명된 대로 Experience Platform 내에서 이를 사용하여 Advertising DSP 대상에 대한 대상 연결을 만듭니다.

### 쿠키를 공유하도록 ID 동기화 설정 {#cookie-sync}

ID 동기화는 서드파티 쿠키를 공유하기 위한 필수 조건입니다. [!DNL Web SDK] 데이터스트림 또는 [!DNL Experience Cloud ID Service] 중 하나로 쿠키 동기화 프로세스를 설정합니다. 타사 쿠키에 대한 ID 처리에 대한 자세한 내용은 [타사 쿠키 통합에 의존하는 Advertising 대상](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations)을 참조하십시오.

**타사 ID 동기화를[!DNL Web SDK]**&#x200B;과(와) 사용

[!DNL Experience Platform Web SDK]을(를) 사용하는 경우 고급 설정에서 [!UICONTROL Third Party ID Sync] 옵션을 구성하여 데이터 스트림에서 타사 ID 동기화를 사용하도록 설정하십시오. 지침은 데이터스트림 설명서에서 [고급 옵션 구성](/help/datastreams/configure.md#advanced-options)을 참조하십시오.

**타사 ID 동기화를[!DNL Experience Cloud ID Service]**&#x200B;과(와) 사용합니다.

[!DNL Experience Platform]에 [!DNL Experience Cloud ID Service] 태그를 사용하는 경우 [Experience Cloud ID 서비스 확장](/help/tags/extensions/client/id-service/overview.md)을 사용하여 타사 ID 동기화를 구성하십시오. 이렇게 하면 [!DNL Real-Time CDP]에서 대상자를 활성화할 때 특정 ECID에 대해 일치하는 Adobe Advertising 쿠키를 사용할 수 있습니다.

## 지원되는 ID {#supported-identities}

Adobe Advertising DSP 대상은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | SHA256 알고리즘으로 해시된 이메일 주소 | Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 Experience Platform이 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| `ECID` | Experience Cloud용 자사 쿠키 | 쿠키 기반 세그먼트를 만드는 데 필요합니다. |
| `adcloud` | Adobe Advertising용 서드파티 쿠키 | 쿠키 기반 세그먼트를 만드는 데 필요합니다. |
| `GAID` | [!DNL Android] 장치 ID | [!DNL Android]개 장치를 타깃팅하는 데 필요합니다. |
| `IDFA` | [!DNL iOS] 장치 ID | [!DNL iOS]개 장치를 타깃팅하는 데 필요합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 예 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> [!DNL Adobe Journey Optimizer]과(와) 같은 다른 Experience Platform 앱에서 생성된 대상, </li><li> 등. </li></ul> |

{style="table-layout:auto"}

대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
| -------------------- | --------- | ----------- | --------- |
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 다음 표를 참조하십시오.

| 항목 | 유형 | 참고 |
| ---- | ---- | ----- |
| 내보내기 유형 | **[!UICONTROL Audience export]** | 선택한 식별자를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 Experience Platform에 대해 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

대상에 연결하려면 Experience Platform 사용자 인터페이스를 사용하여 [대상 연결을 만듭니다](/help/destinations/ui/connect-destination.md) 지침을 따르십시오. 대상 구성 워크플로에서 아래 하위 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 연결하려면 [!UICONTROL Connection type] 섹션에 다음 매개 변수를 입력한 다음 **[!UICONTROL Connect to destination]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL Account or Advertiser Key]**: 이 [!UICONTROL Source Key]은(는) DSP 사용자 인터페이스에 [[!DNL Real-Time CDP] 소스가 만들어지면](https://experienceleague.adobe.com/en/docs/advertising/dsp/audiences/sources/source-manage)에 생성됩니다. Adobe 계정 팀은 소스를 만든 후 이 키를 사용자와 공유합니다.

![계정 또는 광고주 키 필드를 표시하는 연결 유형 섹션의 스크린샷입니다.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

![이름 및 설명 입력을 표시하는 대상 세부 정보 필드의 스크린샷입니다.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_adcloud_dsp"
>title="사전 구성된 매핑 세트"
>abstract="ECID와 [!DNL adcloud] 쿠키 등 두 가지 매핑 세트가 사전 구성되어 있습니다. Adobe Advertising DSP에 데이터를 활성화할 때 활성화된 대상자에 적합한 프로필에는 해당 프로필과 연결된 ECID ID가 적어도 있어야 대상자에 성공적으로 내보낼 수 있습니다."
>additional-url="https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/advertising/adobe-advertising-dsp-connection#preconfigured-mappings" text="사전 구성된 매핑에 대해 자세히 알아보십시오"

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* ID를 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

이 대상에 대한 ID 매핑은 부분적으로 사전 구성되어 있습니다. 아래에 사전 구성된 매핑을 검토하고 포함하려는 선택적 ID를 추가하십시오.

### 사전 구성된 매핑 {#preconfigured-mappings}

다음 ID 매핑은 대상 활성화 워크플로 중에 **사전 구성되어 자동으로 채워집니다**.

* **`ECID`**(Experience Cloud ID)
* **`adcloud`**(Adobe Advertising 타사 쿠키)

쿠키 식별자, 해시된 이메일, IDFA 및 GAID 옵션을 보여 주는 ID 매핑 섹션의 ![스크린샷.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

이러한 매핑은 회색으로 표시되며 읽기 전용입니다. 이 단계에서는 아무것도 구성하지 않아도 됩니다. 선택적으로 다음 매핑을 추가할 수 있습니다.

* **`email_lc_sha256`**(해시된 이메일)
* **IDFA**([!DNL Apple iOS] 장치 ID)
* **GAID**([!DNL Android] 장치 ID)

계속하려면 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

>[!IMPORTANT]
>
>쿠키 기반 내보내기를 수행하려면 **ECID가 필요합니다.ECID가 없는** 프로필은 쿠키 기반 세그먼트에 포함되지 않습니다. [!DNL RampID] 또는 [!DNL UID2.0]을(를) 사용하는 인증된 대상 세그먼트의 경우 프로필에 해시된 이메일 ID가 있어야 합니다.

지침은 [특성 및 ID 매핑](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)을 참조하십시오.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상 데이터가 Adobe Advertising과 공유되었는지 확인하려면 다음을 확인하십시오.

* [!DNL Real-Time CDP] 대상의 데이터 흐름이 정상적으로 완료되었습니다.

* DSP에서 대상자는 **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]**&#x200B;에서 또는 배치 설정의 **[!UICONTROL Audience Targeting]** 섹션 내에서 대상자를 만들거나 편집할 때 사용할 수 있습니다. 대상자는 [!UICONTROL Adobe Segments] 폴더 아래의 [!UICONTROL Real-Time CDP] 탭에 표시되어야 합니다.

DSP 세그먼트 탭에 나열된 가져온 대상 세그먼트가 있는 ![ 폴더를 표시하는 Adobe 대상 인터페이스의 [!DNL Real-Time CDP]스크린샷입니다.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
