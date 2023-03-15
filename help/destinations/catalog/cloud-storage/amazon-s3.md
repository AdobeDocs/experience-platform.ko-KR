---
keywords: Amazon S3;S3 대상;s3;amazon s3
title: Amazon S3 연결
description: Amazon Web Services(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform의 CSV 데이터 파일을 정기적으로 자체 S3 버킷으로 내보냅니다.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Amazon S3] 연결 {#s3-connection}

## 대상 변경 로그 {#changelog}

>[!IMPORTANT]
>
>데이터 세트 내보내기 기능의 베타 릴리스와 향상된 파일 내보내기 기능으로 이제 두 가지가 표시될 수 있습니다 [!DNL Amazon S3] 대상 카탈로그의 카드.
>* 이미 파일을 로 내보내고 있는 경우 **[!UICONTROL Amazon]** 대상. 새 데이터 흐름을 만드십시오. **[!UICONTROL Amazon S3 베타]** 대상.
>* 에 대한 데이터 흐름을 아직 만들지 않은 경우 **[!UICONTROL Amazon]** 대상, 새 대상을 사용하십시오. **[!UICONTROL Amazon S3 베타]** 파일을 내보낼 카드 **[!UICONTROL Amazon]**.


![두 Amazon S3 대상 카드의 나란히 표시된 이미지](../../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

새로운 기능 개선 [!DNL Amazon S3] 대상 카드에는 다음이 포함됩니다.

* [데이터 세트 내보내기 지원](/help/destinations/ui/export-datasets.md).
* 추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능 [매핑 단계 개선](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 개요 {#overview}

에 대한 실시간 아웃바운드 연결 만들기 [!DNL Amazon S3] Adobe Experience Platform의 데이터 파일을 고유한 S3 버킷으로 정기적으로 내보내는 저장소입니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Amazon S3 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 공개 키"
>abstract="원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 설명서 링크에서 올바른 형식의 키의 예를 봅니다."

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: 위치 [!DNL Amazon S3], 생성 `access key - secret access key` 쌍으로 플랫폼에 액세스 권한 부여 [!DNL Amazon S3] 계정입니다. 다음에서 자세히 알아보기 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

   ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="버킷 이름"
>abstract="길이는 3~63자 사이여야 합니다. 문자 또는 숫자로 시작하고 끝나야 합니다. 소문자, 숫자 또는 하이픈( - )만 포함해야 합니다. IP 주소(예: 192.100.1.1)로 포맷해서는 안 됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="폴더 경로"
>abstract="문자 A-Z, a-z, 0-9만 포함해야 하며 다음 특수 문자를 포함할 수 있습니다. `/!-_.'()"^[]+$%.*"`. 세그먼트 파일별로 폴더를 만들려면 매크로를 삽입합니다 `/%SEGMENT_NAME%` 또는 `/%SEGMENT_ID%` 또는 `/%SEGMENT_NAME%/%SEGMENT_ID%` 텍스트 필드에 입력합니다. 폴더 경로 끝에만 매크로를 삽입할 수 있습니다. 설명서에서 매크로 예제를 봅니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="매크로를 사용하여 저장소 위치에 폴더를 만듭니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: 의 이름을 입력합니다. [!DNL Amazon S3] 이 대상에서 사용할 버킷.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 이 옵션은 에만 사용할 수 있습니다. **[!UICONTROL Amazon S3 베타]** 대상. 을(를) 선택할 때 [!UICONTROL CSV] 옵션을 사용하여 다음을 수행할 수도 있습니다. [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 대해 Experience Platform이 사용해야 하는 압축 유형을 선택합니다. 이 옵션은 에만 사용할 수 있습니다. **[!UICONTROL Amazon S3 베타]** 대상.


>[!TIP]
>
>연결 대상 워크플로우에서는 내보낸 세그먼트 파일별로 Amazon S3 스토리지에 사용자 지정 폴더를 만들 수 있습니다. 읽기 [매크로를 사용하여 저장소 위치에 폴더를 만듭니다.](overview.md#use-macros) 설명서를 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

### 필수 [!DNL Amazon S3] 권한 {#required-s3-permission}

에 데이터를 성공적으로 연결하고 내보내려면 [!DNL Amazon S3] 스토리지 위치에서 IAM(Identity and Access Management) 사용자를 [!DNL Platform] 위치: [!DNL Amazon S3] 및 다음 작업에 대한 권한을 할당할 수 있습니다.

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

## (베타) 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기를 설정하는 방법에 대한 자세한 내용은 [데이터 세트 내보내기 자습서](/help/destinations/ui/export-datasets.md).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Amazon S3] 대상, [!DNL Platform] 은 사용자가 제공한 저장 위치에 데이터 파일을 생성합니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 세그먼트 활성화 자습서에서 참조하십시오.
