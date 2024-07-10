---
title: Salesforce Marketing Cloud 연결
description: Salesforce Marketing Cloud은 방문자와 고객이 여정을 만들고 사용자 정의하여 경험을 개인화할 수 있도록 하는 이전 ExactTarget의 디지털 마케팅 제품군입니다.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] 연결

## 개요 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 는 방문자와 고객이 자신의 경험을 개인화할 수 있도록 여정을 구축하고 맞춤화할 수 있는 이전 ExactTarget으로 알려진 디지털 마케팅 세트입니다.

대상 데이터를에 보내려면 [!DNL Salesforce Marketing Cloud], 먼저 다음을 수행해야 합니다. [대상에 연결](#connect-destination) Platform에서 [데이터 가져오기 설정](#import-data-into-salesforce) 스토리지 위치에서 로 [!DNL Salesforce Marketing Cloud].

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ 덧신 | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 허용 목록에 추가하다 IP 주소 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe은 특정 IP 범위를 허용 목록에 추가하다에 추가할 것을 권장합니다.

을(를) 참조하십시오 [허용 목록에 추가하다 SFTP 대상의 IP 주소](../cloud-storage/ip-address-allow-list.md) Adobe IP를 허용 목록에 추가하다에 추가해야 하는 경우

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

이 대상은 다음 연결 유형을 지원합니다.

* **[!UICONTROL 암호가 포함된 SFTP]**
* **[!UICONTROL SSH 키가 포함된 SFTP]**

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* 대상 **[!UICONTROL 암호가 포함된 SFTP]** 연결, 다음을 제공해야 합니다.
   * **[!UICONTROL 도메인]**: SFTP 계정의 IP 주소 또는 도메인 이름;
   * **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용하는 포트
   * **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름
   * **[!UICONTROL 암호]**: SFTP 저장소 위치에 로그인하기 위한 암호입니다.
* 대상 **[!UICONTROL SSH 키가 포함된 SFTP]** 연결, 다음을 제공해야 합니다.
   * **[!UICONTROL 도메인]**: SFTP 계정의 IP 주소 또는 도메인 이름;
   * **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용하는 포트
   * **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름
   * **[!UICONTROL SSH 키]**: SFTP 저장소 위치에 로그인하는 데 사용되는 개인 SSH 키입니다. 개인 키의 형식은 Base64로 인코딩된 문자열이어야 하며 암호로 보호되어서는 안 됩니다.

* 원할 경우 RSA 형식의 공개 키를 첨부하여 PGP/GPG를 사용한 암호화를 내보낸 파일에 추가할 수 있습니다. **[!UICONTROL 키]** 섹션. 공개 키는 다음으로 작성되어야 합니다. [!DNL Base64] 인코딩된 문자열입니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: Platform이 내보내기 데이터를 CSV 파일로 저장할 스토리지 위치의 경로를 제공합니다.
* **[!UICONTROL 파일 형식]**: 선택 **CSV** csv 파일을 저장소 위치로 내보냅니다.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 대상 속성 {#destination-attributes}

이 대상에 대한 대상을 활성화할 때 Adobe은에서 고유 식별자를 선택할 것을 권장합니다. [유니온 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 다음을 참조하십시오. [이메일 마케팅 대상으로 대상자를 활성화할 때의 모범 사례](overview.md#best-practices).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Salesforce Marketing Cloud] 대상, 플랫폼에서 다음을 생성합니다. `.csv` 파일을 제공한 저장소 위치에 있습니다. 파일에 대한 자세한 내용은 [대상자 활성화 확인](../../ui/activate-batch-profile-destinations.md#verify) audience activation 튜토리얼에서 을 참조하십시오.

## 데이터 가져오기 설정 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

연결 후 [!DNL Platform] (으)로 [!DNL SFTP] storage, 스토리지 위치에서 로 데이터 가져오기를 설정해야 합니다. [!DNL Salesforce Marketing Cloud]. 이 작업을 수행하는 방법에 대해 알아보려면 다음을 참조하십시오. [파일에서 Marketing Cloud으로 구독자 가져오기](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 다음에서 [!DNL Salesforce Help Center].
