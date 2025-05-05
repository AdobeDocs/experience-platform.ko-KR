---
title: Adobe Advertising Cloud DSP 연결
description: Adobe Advertising Cloud DSP은 Adobe Real-time Customer Data Platform의 통합 대상으로서, 캠페인 활성화를 위해 인증된 자사 대상을 승인된 광고주 및 사용자와 공유할 수 있습니다.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 2%

---

# Adobe Advertising Cloud DSP 연결

## 개요 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) 대상을 사용하면 DSP과의 캠페인 활성화를 위해 인증된 자사 대상을 승인된 광고주 및 사용자와 공유할 수 있습니다. DSP과의 Real-Time CDP 통합에 대한 자세한 내용은 [Audience Sources에서 인증된 대상 활성화 정보](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html?lang=ko)를 참조하세요.

>[!IMPORTANT]
>
>이 페이지는 DSP 팀에서 만들었습니다. 문의 사항이나 업데이트 요청이 있으면 `adcloud_support@adobe.com`에서 직접 Advertising Cloud 지원 팀에 문의하십시오.

## 사용 사례 {#use-cases}

Advertising Cloud DSP 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 브랜드 광고 사용 사례

온라인 소매업체는 타깃팅에 쿠키를 사용하지 않고 디스플레이 캠페인을 통해 가치가 높은 고객을 다시 타깃팅하려고 합니다. 소매업체는 자사 Adobe Real-time Customer Data Platform(Real-Time CDP) 계정에서 DSP 계정으로 고가치 고객의 해시된 이메일 ID로 구성된 대상을 공유합니다. 그런 다음 DSP은 DSP과 LiveRamp 간의 파트너십을 통해 해시된 전자 메일 ID를 인증된 [!DNL RampIDs] (으)로 변환합니다. 결과 [!DNL RampIDs]은(는) 디스플레이 캠페인에서 대상자를 타겟팅하는 데 사용할 수 있습니다.

### 에이전시 사용 사례

DSP 계정이 있는 미디어 에이전시는 호스피탈리티 업계의 상위 브랜드인 고객을 대신하여 리타겟팅 캠페인을 실행하고 있습니다. 그 브랜드는 새로운 판촉 오퍼와 함께 작년에 있었던 모든 손님들을 다시 타겟팅하고 싶어한다. 브랜드가 [!DNL Real-Time CDP]에서 모든 게스트 정보를 호스팅합니다. 브랜드는 게스트의 해시된 이메일 ID로 구성된 대상을 해당 [!DNL Real-Time CDP] 계정에서 미디어 에이전시의 DSP 계정으로 공유하여 미디어 캠페인을 통해 게스트를 재타겟팅할 수 있습니다.

## 전제 조건 {#prerequisites}

* [!DNL LiveRamp RampID]과(와) 대상을 공유할 수 있도록 DSP 계정 수준 및 캠페인 수준 설정을 사용하면 고객 데이터가 [!DNL RampIDs] (으)로 변환되어 타깃팅 가능한 세그먼트를 만들 수 있습니다. DSP 계정 팀이 이 구성을 수행합니다. [!DNL RampID]은(는) DSP과 [!DNL LiveRamp] 간의 파트너십을 통해 사용할 수 있으며, [!DNL LiveRamp] 멤버십이 없어도 사용할 수 있습니다.
* Experience Platform 계정용 Experience Cloud 조직 ID입니다. ID는 [!DNL Real-Time CDP] 사용자 프로필 페이지에서 찾을 수 있습니다.
* 캠페인 활성화를 위한 대상을 받을 [[!DNL Real-Time CDP] DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=ko)의 소스. DSP 계정 팀은 Experience Cloud 조직 ID를 사용하여 소스를 만듭니다.
* [[!DNL Real-Time CDP] 소스가 DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=ko)에서 만들어질 때 생성되는 DSP 계정 또는 광고주의 소스 키. DSP 계정 팀이 이 키를 공유합니다. 아래 [설명](#authenticate)처럼 Experience Platform 내에서 Advertising Cloud DSP 대상에 대한 대상 연결을 만드는 데 사용합니다.
* 이메일 또는 해시된 이메일로 구성된 고객 데이터.

## 지원되는 ID {#supported-identities}

Adobe Advertising Cloud DSP 대상은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 Experience Platform이 활성화 시 데이터를 자동으로 해시하도록 합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 다음 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | Advertising Cloud DSP 대상에 사용된 식별자(이메일 또는 해시된 이메일)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 Experience Platform을 위해 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

대상에 연결하려면 Experience Platform 사용자 인터페이스를 사용하여 [대상 연결을 만듭니다](/help/destinations/ui/connect-destination.md) 지침을 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 연결하려면 [!UICONTROL 연결 형식] 섹션에서 다음 매개 변수를 제공한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하십시오.

* **[!UICONTROL 계정 또는 광고주 키]**: 이 [!UICONTROL Source 키]은(는) DSP 사용자 인터페이스에 [[!DNL Real-Time CDP] 소스가 만들어지면](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=ko)생성됩니다. DSP 계정 팀은 소스를 만든 후 이 키를 사용자와 공유합니다.

![연결 유형 필드](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

![대상 세부 정보 필드](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 데이터 내보내기 유효성 검사 {#exported-data}

데이터 대상이 Advertising Cloud과 공유되었는지 확인하려면 다음을 확인하십시오.

* [!DNL Real-Time CDP] 대상의 데이터 흐름이 정상적으로 완료되었습니다.

* DSP에서 대상은 [!UICONTROL 대상] > [!UICONTROL 모든 대상]에서 또는 배치 설정의 [!UICONTROL 대상 타깃팅] 섹션 내에서 대상을 만들거나 편집할 때 사용할 수 있습니다. 대상은 [!UICONTROL Real-Time CDP] 폴더 아래의 [!UICONTROL Adobe 세그먼트] 탭에 표시되어야 합니다.

DSP 대상자 설정의 ![Real-Time CDP 대상자](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
