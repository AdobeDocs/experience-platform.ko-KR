---
keywords: 광고; bing;
title: Microsoft Bing 연결
description: Microsoft Bing 연결 대상을 사용하면 디스플레이 광고, 검색 및 네이티브를 포함하여 전체 Microsoft Advertising 네트워크에서 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있습니다.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: e75a5562820490bc56adaa1d21e4066fc649cc44
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 5%

---

# [!DNL Microsoft Bing] 연결 {#bing-destination}

## 개요 {#overview}


>[!IMPORTANT]
>
>2025년 8월부터 대상 서비스로 내부 업그레이드한 후 데이터 흐름에서 **활성화된 프로필 수가**&#x200B;개 감소[!DNL Microsoft Bing]될 수 있습니다.
>
> 이 삭제는 이 대상 플랫폼에 대한 모든 활성화에 대한 **ECID 매핑 요구 사항**&#x200B;의 도입으로 인해 발생합니다. 자세한 내용은 이 페이지의 [필수 매핑](#mandatory-mappings) 섹션을 참조하십시오.
>
>**변경 사항:**
>
>* 이제 모든 프로필 활성화에서 ECID(Experience Cloud ID) 매핑이 **필수**&#x200B;입니다.
>* ECID 매핑이 없는 프로필은 기존 활성화 데이터 흐름에서 **삭제**&#x200B;됩니다.
>
>**수행할 작업:**
>
>* 대상자 데이터를 검토하여 프로필에 유효한 ECID 값이 있는지 확인하십시오.
>* 활성화 지표를 모니터링하여 예상 프로필 수를 확인합니다.

[!DNL Microsoft Bing] 대상을 사용하여 [!DNL Microsoft Advertising Network], [!DNL Display Advertising] 및 [!DNL Search]을(를) 포함하여 전체 [!DNL Native]에 프로필 데이터를 보냅니다.

[!DNL Microsoft Bing] 대상은 Microsoft에서 *[!DNL Custom Audiences]*&#x200B;을(를) 만듭니다. [!DNL Microsoft Search Network]Microsoft Advertising 설명서[!DNL Audience Network]에 나열된 대로 [!DNL Native] 및 [!DNL Display]&#x200B;([!DNL Programmatic] /[&#x200B; /](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500))에서 모두 사용할 수 있습니다.

[!DNL Microsoft Bing]에 프로필 데이터를 보내려면 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터로서 [!DNL Microsoft Advertising IDs]로 만들어진 대상을 사용하여 [!DNL Microsoft Advertising]개 채널에서 디스플레이 또는 검색 광고를 통해 사용자를 타깃팅하고 싶습니다.

## 지원되는 ID {#supported-identities}

[!DNL Microsoft Bing]은(는) 아래 표에 표시된 ID를 기반으로 대상자 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| ID | 설명 |
|---|---|
| 하녀 | MICROSOFT ADVERTISING ID |
| ECID | Experience Cloud ID. 이 ID는 통합이 올바르게 작동하기 위해 필수이지만 대상 활성화에 사용되지 않습니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

**[!DNL Audience Export]** - 대상의 모든 구성원을 [!DNL Microsoft Bing] 대상으로 내보내고 있습니다.

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | 대상의 모든 구성원을 [!DNL Microsoft Bing] 대상으로 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>[!DNL Microsoft Bing]을(를) 사용하여 첫 번째 대상을 만들려고 하는데 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=ko)을(를) 활성화하지 않은 경우(Adobe Audience Manager 또는 기타 응용 프로그램 사용) Adobe Consulting 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL Microsoft Bing] 통합을 설정한 경우 설정한 ID 동기화가 Experience Platform으로 이월됩니다.

대상을 구성할 때는 다음 정보를 제공해야 합니다.

* [!UICONTROL Account ID]: 정수 형식의 [!DNL Bing Ads CID]입니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 대상 세부 정보 입력 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Account ID]**: 내 [!DNL Bing Ads Customer ID]&#x200B;(CID). CID는 정수입니다. [!DNL Microsoft Advertising]에 로그인할 때 URL에 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID 매핑"
>abstract="선택한 대상자를 매핑할 숫자 Bing 세그먼트 ID를 입력합니다. 입력한 [!UICONTROL Mapping ID]이(가) Bing 대상의 대상 ID와 일치하지 않으면 Bing 계정에 예상 대상 데이터가 표시되지 않습니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="사전 구성된 매핑 세트"
>abstract="이 두 매핑 세트가 사전 구성되어 있습니다. Microsoft Bing에 데이터를 활성화할 때 대상으로 성공적으로 내보내려면 활성화된 대상에 적합한 프로필에 해당 프로필과 연결된 ECID ID가 적어도 있어야 합니다."
>additional-url="https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings" text="미리 구성된 매핑에 대해 자세히 알아보십시오"

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

[대상 일정](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계에서는 [!UICONTROL Mapping ID] 필드에 대상 이름을 수동으로 매핑해야 합니다. 이렇게 하면 대상 메타데이터가 [!DNL Bing]에 올바르게 전달됩니다.

대상 이름을 Bing 매핑 ID에 매핑하는 방법에 대한 예와 함께 대상 일정 화면을 표시하는 ![UI 이미지.](../../assets/catalog/advertising/bing/mapping-id.png)

### 필수 매핑 {#mandatory-mappings}

[지원되는 ID](#supported-identities) 섹션에 설명된 모든 대상 ID는 필수이며 대상 활성화 프로세스 중에 매핑해야 합니다. 여기에는 다음 항목이 포함되어 있습니다.

* **MAID**(Microsoft Advertising ID)
* **ECID**(Experience Cloud ID)

필요한 모든 ID를 매핑하지 못하면 활성화 워크플로우를 완료할 수 없습니다. 각 ID는 통합에서 특정 용도로 사용되며 대상이 올바르게 작동하려면 모두 필요합니다.

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Microsoft Bing] 대상으로 내보냈는지 확인하려면 [!DNL Microsoft Bing Ads] 계정을 확인하세요. 활성화가 성공하면 계정에 대상자가 채워집니다.
