---
keywords: Amazon S3;S3 대상;s3;amazon s3
title: Amazon S3 연결
description: Amazon Web Services(AWS) S3 저장소에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform의 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# [!DNL Amazon S3] 연결 {#s3-connection}

## 개요 {#overview}

에 대한 라이브 아웃바운드 연결을 만듭니다. [!DNL Amazon Web Services] (AWS) S3 저장소를 사용하여 Adobe Experience Platform의 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Amazon S3 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="버킷 이름"
>abstract="길이는 3자에서 63자 사이여야 합니다. 문자나 숫자로 시작하고 끝나야 합니다. 소문자, 숫자 또는 하이픈( - )만 포함해야 합니다. IP 주소 형식(예: 192.100.1.1)을 지정해서는 안 됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="폴더 경로"
>abstract="A-Z, a-z, 0-9 문자만 포함해야 하며 다음 특수 문자를 포함할 수 있습니다. `/!-_.'()"^[]+$%.*"`. 세그먼트 파일당 폴더를 만들려면 매크로 /%SEGMENT_NAME% 또는 /%SEGMENT_ID% 또는 /%SEGMENT_NAME%/%SEGMENT_ID%를 텍스트 필드에 삽입합니다. 매크로는 폴더 경로 끝에만 삽입할 수 있습니다. 설명서에서 매크로 예제를 봅니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="매크로를 사용하여 저장소 위치에 폴더를 만듭니다"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 공개 키"
>abstract="선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 Base64 인코딩 문자열로 작성해야 합니다."

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: in [!DNL Amazon S3], 생성 `access key - secret access key` 플랫폼에 대한 액세스 권한을 부여하기 위한 쌍 [!DNL Amazon S3] 계정이 필요합니다. 자세한 내용은 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: 이름 입력 [!DNL Amazon S3] 이 대상에서 사용할 버킷입니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.

선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.

>[!TIP]
>
>연결 대상 워크플로우에서 내보낸 세그먼트 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 읽기 [매크로를 사용하여 저장소 위치에 폴더를 만듭니다](overview.md#use-macros) 참조하십시오.

### 필수 여부 [!DNL Amazon S3] 권한 {#required-s3-permission}

데이터를 성공적으로 연결하고 로 내보내려면 [!DNL Amazon S3] 저장소 위치, [!DNL Platform] in [!DNL Amazon S3] 및 는 다음 작업에 대한 권한을 할당합니다.

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

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

대상 [!DNL Amazon S3] 대상, [!DNL Platform] 만들기 `.csv` 파일을 입력한 저장 위치에 저장합니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 세그먼트 활성화 자습서에서 를 참조하십시오.
