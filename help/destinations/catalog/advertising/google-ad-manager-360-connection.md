---
title: (베타) [!DNL Google Ad Manager 360] 연결
description: Google Ad Manager 360은 게시자가 비디오 및 모바일 앱을 통해 웹 사이트에서 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 서비스 플랫폼입니다.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---

# (베타) [!DNL Google Ad Manager 360] 연결

## 개요 {#overview}

다음 [!DNL Google Ad Manager 360] 연결을 통해 일괄 업로드를 수행할 수 있습니다. [!DNL publisher provided identifiers] (PPID)을 [!DNL Google Ad Manager 360], 를 통해 [!DNL Google Cloud Storage].

게시자가 Google Ad Manager 360에서 식별자를 제공하는 방법에 대한 자세한 내용은 [공식 Google 설명서](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>이 대상은 현재 베타에 있으며 제한된 수의 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 [!DNL Google Ad Manager 360] 연결되면 Adobe 담당자에게 연락하여 [!DNL IMS Organization ID].

다음 [!DNL Google Ad Manager 360] 대상 내보내기 [!DNL CSV] 파일에 [!DNL Google Cloud Storage] 버킷. 를 내보낸 후 [!DNL CSV] 파일을 가져올 때 [!DNL Google Ad Manager 360] 계정이 필요합니다.

## 대상 세부 사항 {#specifics}

에 해당하는 다음 세부 사항을 참고하십시오 [!DNL Google Ad Manager 360] 대상.

* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 만들어지고 CSV 파일로 채워집니다.

## 지원되는 ID {#supported-identities}

[!DNL This integration] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 대상을 보낼 대상 ID를 선택합니다 [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 전제 조건 {#prerequisites}

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>허용 목록은 첫 번째 설정을 수행하기 전에 필수입니다 [!DNL Google Ad Manager] 대상 을 참조하십시오. 아래 설명된 허용 목록 프로세스가 [!DNL Google] 대상을 만들기 전에

만들기 전 [!DNL Google Ad Manager 360] 플랫폼의 대상은 [!DNL Google] Adobe이 허용된 데이터 공급자 목록에 추가되고 허용 목록에 계정이 추가되도록 하는 경우입니다. 연락처 [!DNL Google] 및 는 다음 정보를 제공합니다.

* **계정 ID**: Adobe의 계정 ID와 Google. 계정 ID: 87933855.
* **고객 ID**: Google을 사용하는 Adobe의 고객 계정 ID입니다. 고객 ID: 89690775.
* **네트워크 ID**: 이 계정은 [!DNL Google Ad Manager]
* **대상 링크 ID**: 이 계정은 [!DNL Google Ad Manager]
* 계정 유형입니다. Google 또는 AdX 구매자의 DFP.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 버킷 이름]**: 이름 입력 [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷입니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.

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
