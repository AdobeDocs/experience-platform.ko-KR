---
title: Adobe Advertising Cloud DSP 연결
description: Adobe Advertising Cloud DSP은 Adobe Real-time Customer Data Platform의 통합 대상이므로, 캠페인 활성화를 위해 승인된 광고주 및 사용자와 인증된 자사 세그먼트를 공유할 수 있습니다.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---

# Adobe Advertising Cloud DSP 연결

## 개요 {#overview}

더 Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) 대상을 사용하면 DSP과의 캠페인 활성화를 위해 인증된 자사 세그먼트를 승인된 광고주 및 사용자와 공유할 수 있습니다. DSP과의 Real-Time CDP 통합에 대한 자세한 내용은 다음을 참조하십시오. [대상 소스에서 인증된 세그먼트 활성화 정보](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>이 페이지는 DSP 팀에서 만들었습니다. 문의 사항이나 업데이트 요청은 다음에서 Advertising Cloud 지원 센터에 직접 문의하십시오. `adcloud_support@adobe.com`.

## 사용 사례 {#use-cases}

Advertising Cloud DSP 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 브랜드 광고 사용 사례

온라인 소매업체는 타깃팅에 쿠키를 사용하지 않고 디스플레이 캠페인을 통해 가치가 높은 고객을 다시 타깃팅하려고 합니다. 소매업체는 고가치 고객의 해시된 이메일 ID로 구성된 세그먼트를 Adobe Real-time Customer Data Platform(Real-Time CDP) 계정에서 DSP 계정으로 공유합니다. 그런 다음 DSP은 해시된 이메일 ID를 인증됨으로 변환합니다 [!DNL RampIDs] DSP과 LiveRamp 간의 파트너십을 통해. 결과 [!DNL RampIDs] 디스플레이 캠페인에서 대상자를 타깃팅하는 데 사용할 수 있습니다.

### 에이전시 사용 사례

DSP 계정이 있는 미디어 에이전시는 호스피탈리티 업계의 상위 브랜드인 고객을 대신하여 리타겟팅 캠페인을 실행하고 있습니다. 그 브랜드는 새로운 판촉 오퍼와 함께 작년에 있었던 모든 손님들을 다시 타겟팅하고 싶어한다. 브랜드는에서 모든 게스트 정보를 호스팅합니다. [!DNL Real-Time CDP]. 브랜드는 해당 브랜드에서 게스트의 해시된 이메일 ID로 구성된 세그먼트를 공유할 수 있습니다 [!DNL Real-Time CDP] 미디어 캠페인을 통해 게스트를 재타겟팅하기 위해 미디어 에이전시의 DSP 계정에 연결합니다.

## 사전 요구 사항 {#prerequisites}

* 와 세그먼트 공유를 활성화하는 DSP 계정 수준 및 캠페인 수준 설정 [!DNL LiveRamp RampID]고객 데이터를 로 변환합니다. [!DNL RampIDs] 타겟팅 가능한 세그먼트를 만듭니다. DSP 계정 팀이 이 구성을 수행합니다. [!DNL RampID] 는 DSP과 간의 파트너십을 통해 사용할 수 있습니다. [!DNL LiveRamp], 그리고 자신의 것은 필요 없습니다 [!DNL LiveRamp] 멤버십을 사용하여 쿠키를 사용할 수 있습니다.
* Experience Platform 계정용 Experience Cloud 조직 ID입니다. ID는 [!DNL Real-Time CDP] 사용자 프로필 페이지입니다.
* A [[!DNL Real-Time CDP] DSP의 소스](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) : 캠페인 활성화를 위한 세그먼트를 수신합니다. DSP 계정 팀은 Experience Cloud 조직 ID를 사용하여 소스를 만듭니다.
* DSP 계정 또는 광고주에 대한 소스 키로서, [[!DNL Real-Time CDP] 소스가 DSP에서 생성됨](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). DSP 계정 팀이 이 키를 공유합니다. Experience Platform 내에서 를 사용하여 다음과 같이 Advertising Cloud DSP 대상에 대한 대상 연결을 만듭니다. [아래에 설명](#authenticate).
* 이메일 또는 해시된 이메일로 구성된 고객 데이터.

## 지원되는 ID {#supported-identities}

Adobe Advertising Cloud DSP 대상은 아래 표에 설명된 ID 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 활성화 시 Experience Platform이 데이터를 자동으로 해시하도록 하는 옵션입니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 다음 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | Advertising Cloud DSP 대상에 사용된 식별자(이메일 또는 해시된 이메일)로 세그먼트(대상자)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되면 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions) Experience Platform. 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

대상에 연결하려면 다음 지침을 따르십시오. [대상 연결 만들기](/help/destinations/ui/connect-destination.md) Experience Platform 사용자 인터페이스 사용. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상에 연결하려면 다음에서 매개 변수를 제공합니다. [!UICONTROL 연결 유형] 섹션을 선택한 다음 **[!UICONTROL 대상에 연결]**.:

* **[!UICONTROL 계정 또는 광고주 키]**: 이 [!UICONTROL 소스 키] 다음 경우에 생성됩니다. [[!DNL Real-Time CDP] 소스는 DSP 사용자 인터페이스에서 만들어집니다.](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). DSP 계정 팀은 소스를 만든 후 이 키를 사용자와 공유합니다.

![연결 유형 필드](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

![대상 세부 사항 필드](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

## 데이터 내보내기 유효성 검사 {#exported-data}

데이터 세그먼트가 Advertising Cloud과 공유되었는지 확인하려면 다음을 확인하십시오.

* 의 데이터 흐름 [!DNL Real-Time CDP] 대상이 성공했습니다.

* DSP에서 세그먼트는 대상자를 만들거나 편집할 때 사용할 수 있습니다 [!UICONTROL 대상] > [!UICONTROL 모든 대상] 또는 [!UICONTROL 대상 타기팅] 배치 설정의 일부입니다. 세그먼트는 다음에 표시되어야 합니다. [!UICONTROL Adobe 세그먼트] 탭 아래에 있는 [!UICONTROL Real-Time CDP] 폴더를 삭제합니다.

![DSP 대상자 설정의 Real-Time CDP 세그먼트](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
