---
title: (Beta) [!DNL Google Ad Manager 360] 연결
description: Google Ad Manager 360은 게시자에게 웹 사이트, 비디오 및 모바일 앱에서의 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 제공 플랫폼입니다.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 6%

---

# (Beta) [!DNL Google Ad Manager 360] 연결

>[!IMPORTANT]
>
> Google은 유럽 연합([EU 사용자 동의 정책](https://www.google.com/about/company/user-consent-policy/))의 [디지털 시장법](https://digital-markets-act.ec.europa.eu/index_en)&#x200B;(DMA)에 정의된 준수 및 동의 관련 요구 사항을 지원하기 위해 [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [고객 일치](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) 및 [디스플레이 및 비디오 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)에 대한 변경 사항을 출시합니다. 동의 요구 사항에 대한 이러한 변경 사항의 시행은 2024년 3월 6일부터 시작됩니다.
><br/>
>EU 사용자 동의 정책을 준수하고 유럽 경제 영역(EEA)의 사용자에 대한 대상 목록을 계속 만들려면 광고주와 파트너는 대상 데이터를 업로드할 때 최종 사용자 동의를 전달하는지 확인해야 합니다. Google 파트너로서 Adobe는 유럽연합의 DMA에 따른 이러한 동의 요구 사항을 준수하는 데 필요한 도구를 제공합니다.
><br/>
>Adobe Privacy &amp; Security Shield를 구매하고 동의하지 않은 프로필을 필터링하도록 [동의 정책](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)을(를) 구성한 고객은 별도의 조치를 취할 필요가 없습니다.
><br/>
>Adobe Privacy &amp; Security Shield를 구매하지 않은 고객은 [세그먼트 빌더](../../../segmentation/ui/segment-builder.md) 내의 [세그먼트 정의](../../../segmentation/home.md#segment-definitions) 기능을 사용하여 동의하지 않은 프로필을 필터링해야 기존 Real-Time CDP Google 대상을 중단 없이 계속 사용할 수 있습니다.

[!DNL Google Ad Manager 360] 연결을 통해 [!DNL publisher provided identifiers]&#x200B;(PPID)의 일괄 업로드를 [!DNL Google Cloud Storage]을(를) 통해 [!DNL Google Ad Manager 360]에 사용할 수 있습니다.

게시자가 Google Ad Manager 360에서 식별자를 제공한 방법에 대한 자세한 내용은 [공식 Google 설명서](https://support.google.com/admanager/answer/2880055?hl=en)를 참조하십시오.

>[!IMPORTANT]
>
>이 대상은 현재 Beta에 있으며 제한된 수의 고객만 사용할 수 있습니다. [!DNL Google Ad Manager 360] 연결에 대한 액세스를 요청하려면 Adobe 담당자에게 연락하여 [!DNL organization ID]을(를) 제공하십시오.

[!DNL Google Ad Manager 360] 대상은 [!DNL CSV]개의 파일을 [!DNL Google Cloud Storage] 버킷으로 내보냅니다. [!DNL CSV] 파일을 내보내면 [!DNL Google Ad Manager 360] 계정으로 가져와야 합니다.

## 대상 세부 사항 {#specifics}

[!DNL Google Ad Manager 360] 대상에 해당하는 다음 세부 정보를 참고하십시오.

* 이 대상은 현재 [요청 시 파일 내보내기](../../ui/export-file-now.md) 기능을 지원하지 않습니다.
* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성되며 CSV 파일로 채워집니다.

## 지원되는 ID {#supported-identities}

[!DNL This integration]은(는) 아래 표에 설명된 ID 활성화를 지원합니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 대상자를 [!DNL Google Ad Manager 360]&#x200B;(으)로 보내려면 이 대상 ID를 선택하십시오. |

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
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드(예: PPID)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

### 허용 목록 {#allow-listing}

Experience Platform에서 첫 번째 [!DNL Google Ad Manager 360] 대상을 설정하기 전에 허용 목록이 필수입니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스를 완료해야 합니다.

>[!NOTE]
>
>이 규칙은 기존 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객에 대해 예외입니다. Audience Manager에서 이 Google 대상에 대한 연결을 이미 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 진행할 수 있습니다.

1. [Google Ad Manager 설명서](https://support.google.com/admanager/answer/3289669?hl=en)에 설명된 단계에 따라 Adobe을 연결된 데이터 관리 플랫폼(DMP)으로 추가합니다.
2. [!DNL Google Ad Manager] 인터페이스에서 **[!UICONTROL 관리자]** > **[!UICONTROL 전역 설정]** > **[!UICONTROL 네트워크 설정]**(으)로 이동하여 **[!UICONTROL API 액세스]** 슬라이더를 사용하도록 설정합니다.


## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL 액세스 키 ID]**: Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 61자 영숫자 문자열입니다.
* **[!UICONTROL 비밀 액세스 키]**: Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 40자의 base64로 인코딩된 문자열입니다.

이러한 값에 대한 자세한 내용은 [Google Cloud Storage HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서를 참조하십시오. 자신의 액세스 키 ID와 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 소스 개요](/help/sources/connectors/cloud-storage/google-cloud-storage.md)를 참조하세요.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="대상자 이름에 대상자 ID 추가"
>abstract="이 대상에서 대상자 이름에 다음과 같이 Experience Platform의 대상자 ID가 포함되도록 하려면 이 옵션을 선택하십시오. `Audience Name (Audience ID)`"

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력하십시오.
* **[!UICONTROL 버킷 이름]**: 이 대상에서 사용할 [!DNL Google Cloud Storage] 버킷의 이름을 입력하십시오.
* **[!UICONTROL 계정 ID]**: [!DNL Google] 계정에서 [!DNL Audience Link ID]을(를) 입력하십시오. [!DNL Network code]이(가) 아닌 [!DNL Google Ad Manager] 네트워크와 연결된 특정 식별자입니다. [!DNL Google Ad Manager] 인터페이스의 **[!UICONTROL 관리자 > 전역 설정]**&#x200B;에서 찾을 수 있습니다.
* **[!UICONTROL 계정 유형]**: [!DNL Google] 계정에 따라 옵션을 선택하십시오.
   * [!DNL Google AdX]에 `AdX buyer` 사용
   * 게시자에 대해 [!DNL DoubleClick]에 `DFP by Google` 사용
* **[!UICONTROL 대상 이름에 대상 ID 추가]**: Google Ad Manager 360의 대상 이름에 다음과 같이 Experience Platform의 대상 ID가 포함되도록 하려면 이 옵션을 선택하십시오. `Audience Name (Audience ID)`.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

ID 매핑 단계에서는 다음과 같은 미리 채워진 매핑을 볼 수 있습니다.

| 미리 채워진 매핑 | 설명 |
|---------|----------|
| `ECID` -> `ppid` | 이는 사용자가 미리 채울 수 있는 유일한 매핑입니다. Experience Platform에서 특성 또는 ID 네임스페이스를 선택하여 `ppid`에 매핑할 수 있습니다. |
| `metadata.segment.alias` -> `list_id` | Experience Platform 대상 이름을 Google 플랫폼의 대상 ID에 매핑합니다. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 세그먼트에서 자격이 없는 사용자를 제거할 시기를 Google 플랫폼에 알려줍니다. |

이러한 매핑은 [!DNL Google Ad Manager 360]에 필요하며 모든 [!DNL Google Ad Manager 360] 연결에 대해 Adobe Experience Platform에서 자동으로 만듭니다.

![Google Ad Manager 360에 대한 매핑 단계를 보여 주는 UI 이미지](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 내보낸 데이터 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Google Cloud Storage] 버킷을 확인하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인하십시오.

## 문제 해결 {#troubleshooting}

이 대상을 사용하는 동안 오류가 발생하여 Adobe 또는 Google에 연결해야 하는 경우 다음 ID를 즉시 사용하십시오.

Adobe의 Google 계정 ID입니다.

* **[!UICONTROL 계정 ID]**: 87933855
* **[!UICONTROL 고객 ID]**: 89690775