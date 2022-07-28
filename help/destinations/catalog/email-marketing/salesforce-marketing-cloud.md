---
keywords: 이메일;이메일;이메일;이메일 대상;salesforce;salesforce 대상
title: Salesforce Marketing Cloud 연결
description: Salesforce Marketing Cloud은 방문자와 고객이 경험을 개인화할 수 있도록 여정을 만들고 사용자 지정할 수 있도록 해주는 이전에 ExactTarget이라고 하는 디지털 마케팅 세트입니다.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 30e75b8fbaa4a8269a32f82ade435b67767630c5
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] 연결

## 개요 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 는 방문자와 고객이 자신의 경험을 개인화할 수 있도록 여정을 작성하고 사용자 지정할 수 있도록 해주는 이전에 ExactTarget이라고 하는 디지털 마케팅 세트입니다.

세그먼트 데이터를에 보내려면 [!DNL Salesforce Marketing Cloud], 먼저 [대상 연결](#connect-destination) 플랫폼, [데이터 가져오기 설정](#import-data-into-salesforce) 스토리지 위치에서 로 [!DNL Salesforce Marketing Cloud].

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP 주소 허용 목록 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe에서 특정 IP 범위를 허용 목록에 추가하는 것을 권장합니다.

을(를) 참조하십시오. [클라우드 스토리지 대상에 대한 IP 주소 허용 목록](../cloud-storage/ip-address-allow-list.md) Adobe IP를 허용 목록에 추가해야 하는 경우

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

이 대상은 다음 연결 유형을 지원합니다.

* **[!UICONTROL SFTP와 암호]**
* **[!UICONTROL SSH 키가 있는 SFTP]**

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* 대상 **[!UICONTROL SFTP와 암호]** 연결을 제공해야 합니다.
   * [!UICONTROL 도메인]
   * [!UICONTROL 포트]
   * [!UICONTROL 사용자 이름]
   * [!UICONTROL 암호]
* 대상 **[!UICONTROL SSH 키가 있는 SFTP]** 연결을 제공해야 합니다.
   * [!UICONTROL 도메인]
   * [!UICONTROL 포트]
   * [!UICONTROL 사용자 이름]
   * [!UICONTROL SSH 키]

* 원할 경우 RSA 형식의 공개 키를 연결하여 PGP/GPG를 사용하여 암호화를 내보낸 파일에 추가할 수 있습니다. **[!UICONTROL 키]** 섹션을 참조하십시오. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: Platform이 내보내기 데이터를 CSV 파일로 예치할 스토리지 위치의 경로를 제공합니다.
* **[!UICONTROL 파일 형식]**: 선택 **CSV** csv 파일을 저장소 위치로 내보내려면 를 클릭합니다.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 대상 속성 {#destination-attributes}

세그먼트를 이 대상에 활성화할 때, Adobe에서 고유 식별자를 선택할 것을 권장합니다 [조합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다. 자세한 내용은 [이메일을 마케팅 대상으로 대상을 활성화할 때 모범 사례에 대한 우수 사례입니다](overview.md#best-practices).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Salesforce Marketing Cloud] 대상, 플랫폼에서 `.csv` 파일을 입력한 저장 위치에 저장합니다. 파일에 대한 자세한 내용은 [세그먼트 활성화 확인](../../ui/activate-batch-profile-destinations.md#verify) 세그먼트 활성화 자습서에서 를 참조하십시오.

## 데이터 가져오기를에 설정 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

연결 후 [!DNL Platform] 아래와 같이 [!DNL SFTP] 저장소 위치에서 로 데이터 가져오기를 설정해야 합니다 [!DNL Salesforce Marketing Cloud]. 이를 수행하는 방법에 대해 알아보려면 [파일에서 Marketing Cloud으로 구독자 가져오기](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 에서 [!DNL Salesforce Help Center].
