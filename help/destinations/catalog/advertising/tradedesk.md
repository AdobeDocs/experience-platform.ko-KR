---
keywords: 광고, 무역데스크, 광고 무역데스크
title: 트레이드 데스크 연결
description: Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 2%

---

# [!DNL The Trade Desk] 연결

## 개요 {#overview}

이 대상 커넥터를 사용하여 [!DNL The Trade Desk]&#x200B;(으)로 프로필 데이터를 보냅니다. 이 커넥터는 [!DNL The Trade Desk] 자사 끝점으로 데이터를 보냅니다. Adobe Experience Platform과 [!DNL The Trade Desk] 간의 통합은 [!DNL The Trade Desk] 타사 끝점으로 데이터 내보내기를 지원하지 않습니다.

[!DNL The Trade Desk]은(는) 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다.

[!DNL The Trade Desk]에 프로필 데이터를 보내려면 먼저 이 페이지의 다음 섹션에 설명된 대로 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터로서 [!DNL Trade Desk IDs] 또는 장치 ID로 구축된 대상을 사용하여 리타겟팅 또는 대상 타겟팅된 디지털 캠페인을 만들 수 있기를 원합니다.

## 지원되는 ID {#supported-identities}

[!DNL The Trade Desk]은(는) 아래 표에 표시된 ID를 기반으로 대상자 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

다음은 [!DNL The Trade Desk] 대상에서 지원하는 ID입니다. 이러한 ID를 사용하여 대상자를 [!DNL The Trade Desk]에 활성화할 수 있습니다.

아래 표의 모든 ID는 사전 구성되어 있으며 활성화 중에 자동으로 매핑됩니다. 활성화 워크플로에서 이러한 매핑을 수동으로 구성할 필요는 없습니다.

| 타겟 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | GAID가 프로필에 있으면 활성화됩니다. |
| IDFA | 광고주용 Apple ID | IDFA가 프로필에 있으면 활성화됩니다. |
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 자세한 내용은 [ECID](/help/identity-service/features/ecid.md)에서 다음 문서를 참조하십시오. |
| [!DNL Tradedesk] | [!DNL TDID] 플랫폼의 [!DNL The Trade Desk] | 프로필에 ECID가 있고 ECID-to-Trade Desk ID 매핑이 Experience Platform에 있는 경우 활성화됩니다. |

{style="table-layout:auto"}

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
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | 대상의 모든 구성원을 대상으로 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

사전 요구 사항은 대상자 활성화에 사용할 ID 유형에 따라 다릅니다.

**모바일 ID 활성화에만**&#x200B;하려면 필수 구성 요소가 없습니다. 고객에 대한 ID(GAID 및/또는 IDFA)를 수집 및 관리하는 한 대상을 [!DNL The Trade Desk]에 활성화할 수 있습니다.

**[!DNL The Trade Desk]**&#x200B;에서 쿠키 기반 타깃팅을 사용하려면 ECID와 [!DNL Trade Desk ID] 간의 매핑이 설정되어 있는지 확인하십시오. 이렇게 하려면 아래 단계를 완료하십시오.

1. **ID 동기화 기능 사용**: [!DNL The Trade Desk ID] 활성화를 처음 설정하는 경우로서 이전에 Experience Cloud ID 서비스(Adobe Audience Manager 또는 다른 응용 프로그램 포함)에서 [ID 동기화 기능](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync)을 활성화하지 않은 경우 Adobe Consulting 또는 고객 지원 센터에 문의하여 ID 동기화를 활성화하십시오.
   * 이전에 Audience Manager에서 [!DNL The Trade Desk] 통합을 설정한 경우 기존 ID 동기화가 자동으로 Experience Platform으로 이전됩니다.

2. **웹 페이지 계측**: [!DNL The Trade Desk ID]과(와) Adobe ECID 간의 매핑을 만들려면 웹 페이지에 코드를 구현하십시오. 이렇게 하면 Experience Platform에서 트레이드 데스크 ID를 고객 프로필과 연결할 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Account ID]**: 내 [!DNL The Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: 사용할 지역 서버를 [!DNL The Trade Desk] 담당자에게 문의하십시오. 다음은 선택할 수 있는 사용 가능한 지역 서버입니다.

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

[대상 일정](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계에서는 대상을 대상 플랫폼의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

대상을 매핑할 때에는 Adobe에서 사용하기 쉽도록 Experience Platform 대상 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 그러나 대상의 대상 ID 또는 이름은 Experience Platform 계정의 대상 ID 또는 이름과 일치할 필요가 없습니다. 매핑 필드에 삽입하는 모든 값은 대상에 의해 반영됩니다.

### 사전 구성된 매핑 {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="사전 구성된 매핑 세트"
>abstract="4개의 매핑 세트가 사전 구성되어 있습니다. 데이터를 The Trade Desk에 활성화하면 이 대상이 여기에 표시된 대상 ID와 작동하므로 활성화된 대상에 적합한 프로필에는 4개의 ID가 모두 있을 필요는 없습니다. <br> Trade Desk ID를 기반으로 하는 쿠키 기반 타깃팅의 경우 프로필에 ECID가 있어야 하며 Trade Desk ID와 ECID 간의 ID 동기화 매핑이 필요합니다."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="미리 구성된 매핑에 대해 자세히 알아보십시오"

다음 ID 매핑은 대상 활성화 워크플로에서 **사전 구성되어 자동으로 채워집니다**.

* GAID (Google Advertising ID)
* IDFA (광고주용 Apple ID)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![필수 매핑을 보여 주는 스크린샷](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

이러한 매핑은 회색으로 표시되며 읽기 전용입니다. 이 단계에서는 아무것도 구성하지 않아도 됩니다. 계속하려면 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

Experience Platform은 지원되는 모든 id 유형에 대해 활성화 워크플로에서 매핑된 대상자에 속하는 각 프로필을 자동으로 확인한 다음, 존재하는 id를 사용하여 프로필을 활성화합니다.

### 활성화 유형별 ID 요구 사항

**Mobile ID 활성화(GAID/IDFA):** GAID 또는 IDFA만 있는 프로필로 활성화할 수 있습니다. 추가 ID 또는 필수 구성 요소는 필요하지 않습니다.

**쿠키 기반 타깃팅([!DNL Trade Desk ID]):**&#x200B;에는 다음 두 가지가 모두 필요합니다.

* 프로필에 있는 ECID
* [!DNL Trade Desk ID]과(와) ECID 간의 ID 동기화 매핑([필수 구성 요소](#prerequisites) 섹션에 설명된 대로 구성됨)

**여러 ID 동작:** 프로필에 지원되는 여러 ID가 포함된 경우 각 ID가 [!DNL The Trade Desk]에 대해 개별적으로 활성화됩니다. 이를 통해 대상자 활성화에 대한 최대 도달 범위와 유연성을 확보할 수 있습니다.

### 활성화 예

* **모바일 ID 프로필:** GAID 및/또는 IDFA가 있는 프로필이 해당 광고 ID를 사용하여 활성화됩니다. 프로필에 GAID와 IDFA가 모두 포함된 경우 각 ID가 별도로 활성화됩니다.
* **쿠키 기반 프로필:** ECID와 해당 [!DNL Trade Desk ID] 매핑이 있는 프로필은 쿠키 기반 타깃팅에 Trade Desk ID를 사용하여 활성화됩니다.
* **ECID 전용 프로필:** ECID만 있고 [!DNL Trade Desk ID] 매핑이 없는 프로필은 **내보낼 수 없습니다**. ECID만으로는 활성화할 수 없습니다.

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL The Trade Desk] 대상으로 내보냈는지 확인하려면 [!DNL The Trade Desk] 계정을 확인하세요. 활성화가 성공하면 계정에 대상자가 채워집니다.
