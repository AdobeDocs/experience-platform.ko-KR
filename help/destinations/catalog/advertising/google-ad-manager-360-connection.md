---
title: (베타) [!DNL Google Ad Manager 360] 연결
description: Google Ad Manager 360은 게시자가 비디오 및 모바일 앱을 통해 웹 사이트에서 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 서비스 플랫폼입니다.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 5174c65970aa8df9bc3f2c8d612c26c72c20e81f
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 4%

---

# (베타) [!DNL Google Ad Manager 360] 연결

## 개요 {#overview}

다음 [!DNL Google Ad Manager 360] 연결을 통해 일괄 업로드를 수행할 수 있습니다. [!DNL publisher provided identifiers] (PPID)을 [!DNL Google Ad Manager 360], 를 통해 [!DNL Google Cloud Storage].

게시자가 Google Ad Manager 360에서 식별자를 제공하는 방법에 대한 자세한 내용은 [공식 Google 설명서](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>이 대상은 현재 베타에 있으며 제한된 수의 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 [!DNL Google Ad Manager 360] 연결되면 Adobe 담당자에게 연락하여 [!DNL organization ID].

다음 [!DNL Google Ad Manager 360] 대상 내보내기 [!DNL CSV] 파일에 [!DNL Google Cloud Storage] 버킷. 를 내보낸 후 [!DNL CSV] 파일을 가져올 때 [!DNL Google Ad Manager 360] 계정이 필요합니다.

## 대상 세부 사항 {#specifics}

에 해당하는 다음 세부 사항을 참고하십시오 [!DNL Google Ad Manager 360] 대상.

* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 만들어지고 CSV 파일로 채워집니다.

## 지원되는 ID {#supported-identities}

[!DNL This integration] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 대상을 보낼 대상 ID를 선택합니다 [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 세그먼트의 프로필 속성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드(예: PPID)와 함께 세그먼트의 모든 구성원을 내보냅니다 [대상 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 사전 요구 사항 {#prerequisites}

### 허용 목록 {#allow-listing}

첫 번째 목록을 설정하기 전에 허용 목록이 필수입니다 [!DNL Google Ad Manager 360] 대상 을 참조하십시오. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스를 완료해야 합니다.

>[!NOTE]
>
>이 규칙의 예외는 기존 규칙입니다 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객. Audience Manager에서 이 Google 대상에 이미 연결을 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 계속 진행할 수 있습니다.

1. 에 설명된 단계를 수행합니다. [Google Ad Manager 설명서](https://support.google.com/admanager/answer/3289669?hl=en) 를 연결된 DMP(데이터 관리 플랫폼)로 추가하려면,
2. 에서 [!DNL Google Ad Manager] 인터페이스, **[!UICONTROL 관리]** > **[!UICONTROL 전역 설정]** > **[!UICONTROL 네트워크 설정]**, 활성화 **[!UICONTROL API 액세스]** 슬라이더.


## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 입력합니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 액세스 키 ID]**: 인증을 위해 사용되는 61자의 영숫자 문자열입니다 [!DNL Google Cloud Storage] Platform에 계정을 설정합니다.
* **[!UICONTROL 비밀 액세스 키]**: 인증을 위해 사용되는 40자의 base64로 인코딩된 문자열입니다 [!DNL Google Cloud Storage] Platform에 계정을 설정합니다.

이러한 값에 대한 자세한 내용은 [Google 클라우드 스토리지 HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서. 고유한 액세스 키 ID 및 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 소스 개요](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 대상 세부 사항 채우기 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="세그먼트 이름에 세그먼트 ID 추가"
>abstract="Google Ad Manager 360에서 세그먼트 이름에 다음과 같이 Experience Platform의 세그먼트 ID가 포함되도록 하려면 이 옵션을 선택하십시오. `Segment Name (Segment ID)`"

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스트할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 버킷 이름]**: 이름 입력 [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷입니다.
* **[!UICONTROL 계정 ID]**: 을(를) 입력합니다. [!DNL Audience Link ID] 다음 [!DNL Google] 계정이 필요합니다. 와 관련된 특정 식별자입니다 [!DNL Google Ad Manager] 네트워크(아님) [!DNL Network code]). 아래에서 찾을 수 있습니다 **[!UICONTROL 관리자 > 전역 설정]** 에서 [!DNL Google Ad Manager] 인터페이스.
* **[!UICONTROL 계정 유형]**: 옵션에 따라 옵션을 선택합니다 [!DNL Google] 계정:
   * 사용 `AdX buyer` 대상 [!DNL Google AdX]
   * 사용 `DFP by Google` 대상 [!DNL DoubleClick] 게시자
* **[!UICONTROL 세그먼트 이름에 세그먼트 ID 추가]**: 다음과 같이 Google Ad Manager 360의 세그먼트 이름에 Experience Platform의 세그먼트 ID가 포함되도록 하려면 이 옵션을 선택합니다. `Segment Name (Segment ID)`.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

ID 매핑 단계에서 다음과 같은 미리 채워진 매핑을 볼 수 있습니다.

| 미리 채워진 매핑 | 설명 |
|---------|----------|
| `ECID` -> `ppid` | 사용자가 편집할 수 있는 유일한 미리 채워진 매핑입니다. Platform에서 특성 또는 ID 네임스페이스를 선택하여 다음 위치에 매핑할 수 있습니다 `ppid`. |
| `metadata.segment.alias` -> `list_id` | Experience Platform 세그먼트 이름을 Google 플랫폼의 세그먼트 ID에 매핑합니다. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 세그먼트에서 자격이 없는 사용자를 제거할 시기를 Google 플랫폼에 알려줍니다. |

이러한 매핑은 [!DNL Google Ad Manager 360] 모든 사용자에 대해 Adobe Experience Platform이 자동으로 만듭니다 [!DNL Google Ad Manager 360] 연결.

![Google Ad Manager 360의 매핑 단계를 보여주는 UI 이미지입니다.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 내보낸 데이터 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Google Cloud Storage] 버킷하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.

## 문제 해결 {#troubleshooting}

이 대상을 사용하는 동안 오류가 발생하여 Adobe 또는 Google에 연결해야 하는 경우 다음 ID를 즉시 보관하십시오.

Adobe의 Google 계정 ID입니다.

* **[!UICONTROL 계정 ID]**: 87933855
* **[!UICONTROL 고객 ID]**: 89690775