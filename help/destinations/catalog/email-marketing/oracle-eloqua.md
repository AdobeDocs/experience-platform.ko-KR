---
keywords: 전자 메일;전자 메일;전자 메일 대상;oracle oqua;oracle
title: Oracle Eloqua 연결
description: Oracle Eloqua는 B2B 마케터와 조직이 마케팅 캠페인 및 판매 리드 생성을 관리하는 데 도움이 되도록 Oracle이 제공하는 마케팅 자동화를 위한 SaaS(Software as a Service) 플랫폼입니다.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] 연결

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 는 B2B 마케터와 조직이 마케팅 캠페인 및 영업 리드 생성을 관리하는 데  [!DNL Oracle] 도움이 되는 마케팅 자동화를 위한 SaaS(Software as a Service) 플랫폼입니다.

세그먼트 데이터를 [!DNL Oracle Eloqua]에 보내려면 먼저 [Adobe Experience Platform에서 대상](#connect-destination)을 연결한 다음, [저장소 위치에서 [!DNL Oracle Eloqua]로 데이터 가져오기](#import-data-into-eloqua)를 설정해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 이메일 주소,  [전화 번호, 성)](../../ui/activate-destinations.md#select-attributes).

## IP 주소 허용 목록 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe에서 특정 IP 범위를 허용 목록에 추가하는 것을 권장합니다.

허용 목록에 Adobe IP를 추가해야 하는 경우 클라우드 저장소 대상에 대한 [IP 주소 허용 목록](../cloud-storage/ip-address-allow-list.md)을 참조하십시오.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

이 대상은 다음 연결 유형을 지원합니다.

* **[!UICONTROL SFTP와 암호]**
* **[!UICONTROL SSH 키가 있는 SFTP]**

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* 암호&#x200B;]**연결이 있는**[!UICONTROL  SFTP의 경우 다음을 제공해야 합니다.
   * [!UICONTROL 도메인]
   * [!UICONTROL 포트]
   * [!UICONTROL 사용자 이름]
   * [!UICONTROL 암호]
* SSH 키&#x200B;]**연결이 있는**[!UICONTROL  SFTP의 경우 다음을 제공해야 합니다.
   * [!UICONTROL 도메인]
   * [!UICONTROL 포트]
   * [!UICONTROL 사용자 이름]
   * [!UICONTROL SSH 키]

* 원할 경우 RSA 형식의 공개 키를 첨부하여 **[!UICONTROL 키]** 섹션 아래의 내보낸 파일에 PGP/GPG를 사용한 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩 문자열로 기록해야 합니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: Platform이 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 예치할 스토리지 위치의 경로를 제공합니다.
* **[!UICONTROL 파일 형식]**:  **** CSV 또는  **TAB_DISTINGUISHED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상 세그먼트 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 대상 속성 {#destination-attributes}

[Adobe이 이 대상에 세그먼트](../../ui/activate-destinations.md)를 활성화하면 [결합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다. 자세한 내용은 내보낸 파일에서 대상 특성으로 사용할 스키마 필드 선택](./overview.md#destination-attributes)을 참조하십시오.[

## 내보낸 데이터 {#exported-data}

[!DNL Oracle Eloqua] 대상의 경우 Platform은 사용자가 제공한 저장소 위치에 탭으로 구분된 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.

## 데이터 가져오기를 [!DNL Oracle Eloqua]에 설정 {#import-data-into-eloqua}

[!DNL Platform]을 [!DNL SFTP] 저장소에 연결한 후 저장소 위치에서 [!DNL Oracle Eloqua]로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 [!DNL Oracle Eloqua Help Center]에서 [연락처 또는 계정 가져오기](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)를 참조하십시오.
