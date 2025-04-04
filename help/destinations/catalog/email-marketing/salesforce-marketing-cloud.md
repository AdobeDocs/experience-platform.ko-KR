---
title: Salesforce Marketing Cloud 연결
description: Salesforce Marketing Cloud은 이전에 ExactTarget으로 알려졌던 디지털 마케팅 제품군으로, 방문자와 고객이 경험을 개인화할 수 있도록 여정을 작성하고 사용자 정의할 수 있습니다.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] 연결

## 개요 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/)은(는) 이전에 ExactTarget으로 알려졌던 디지털 마케팅 제품군으로, 방문자와 고객이 자신의 경험을 개인화할 수 있도록 여정을 만들고 사용자 지정할 수 있습니다.

대상 데이터를 [!DNL Salesforce Marketing Cloud]에 보내려면 먼저 Experience Platform에서 [대상에 연결](#connect-destination)한 다음 저장소 위치에서 [!DNL Salesforce Marketing Cloud]&#x200B;(으)로 [데이터 가져오기를 설정](#import-data-into-salesforce)해야 합니다.

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
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 허용 목록에 추가하다 IP 주소 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe에서는 특정 허용 목록에 추가하다에 IP 범위를 추가할 것을 권장합니다.

허용 목록에 추가하다에 Adobe IP를 추가해야 하는 경우 [SFTP 대상에 대한 IP 주소 허용 목록](../cloud-storage/ip-address-allow-list.md)을 참조하세요.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

이 대상은 다음 연결 유형을 지원합니다.

* **[!UICONTROL 암호가 있는 SFTP]**
* **[!UICONTROL SSH 키가 있는 SFTP]**

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL 암호를 사용하는 SFTP]** 연결의 경우 다음을 제공해야 합니다.
   * **[!UICONTROL 도메인]**: SFTP 계정의 IP 주소 또는 도메인 이름;
   * **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용하는 포트입니다.
   * **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름;
   * **[!UICONTROL 암호]**: SFTP 저장소 위치에 로그인할 암호입니다.
* SSH 키가 있는 **[!UICONTROL SFTP]** 연결의 경우 다음을 제공해야 합니다.
   * **[!UICONTROL 도메인]**: SFTP 계정의 IP 주소 또는 도메인 이름;
   * **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용하는 포트입니다.
   * **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름;
   * **[!UICONTROL SSH 키]**: SFTP 저장소 위치에 로그인하는 데 사용되는 개인 SSH 키입니다. 개인 키의 형식은 Base64로 인코딩된 문자열이어야 하며 암호로 보호되어서는 안 됩니다.

* 필요한 경우 RSA 형식의 공개 키를 연결하여 **[!UICONTROL 키]** 섹션 아래에서 내보낸 파일에 PGP/GPG를 사용한 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩된 문자열로 작성되어야 합니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택하십시오.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력하십시오.
* **[!UICONTROL 폴더 경로]**: Experience Platform에서 내보내기 데이터를 CSV 파일로 저장할 저장소 위치의 경로를 제공합니다.
* **[!UICONTROL 파일 형식]**: CSV 파일을 저장소 위치로 내보내려면 **CSV**&#x200B;을(를) 선택하십시오.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 대상 속성 {#destination-attributes}

Adobe 이 대상에 대한 대상을 활성화할 때 [공용 구조체 스키마](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 [대상자를 이메일 마케팅 대상으로 활성화할 때의 모범 사례](overview.md#best-practices)를 참조하세요.

## 내보낸 데이터 {#exported-data}

[!DNL Salesforce Marketing Cloud] 대상의 경우 Experience Platform은 제공한 저장소 위치에 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 대상 활성화 자습서에서 [대상 활성화 확인](../../ui/activate-batch-profile-destinations.md#verify)을 참조하십시오.

## [!DNL Salesforce Marketing Cloud]&#x200B;(으)로 데이터 가져오기 설정 {#import-data-into-salesforce}

[!DNL Experience Platform]을(를) [!DNL SFTP] 저장소에 연결한 후 저장소 위치에서 [!DNL Salesforce Marketing Cloud]&#x200B;(으)로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대해 알아보려면 [!DNL Salesforce Help Center]의 [파일에서 Marketing Cloud으로 구독자 가져오기](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5)를 참조하십시오.
