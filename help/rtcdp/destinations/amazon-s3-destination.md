---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3 대상
seo-title: Amazon S3 대상
description: Amazon 웹 서비스(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.
seo-description: Amazon 웹 서비스(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# [!DNL Amazon S3] 대상

## 개요

AWS) [!DNL Amazon Web Services] S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예:이메일 주소, 전화 번호, 성)을 [대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 선택합니다](/help/rtcdp/destinations/activate-destinations.md#select-attributes).

![Amazon S3 프로필 기반 내보내기 유형](/help/rtcdp/destinations/assets/aws-export-type.png)

## 연결 대상 {#connect-destination}

클라우드 [스토리지 대상 워크플로우 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)에서 클라우드 스토리지 대상에 연결하는 방법에 대한 지침을 참조하십시오 [!DNL Amazon S3].

대상에 대해 [!DNL Amazon S3] 대상 만들기 워크플로우에서 다음 정보를 입력합니다.

* **[!DNL Amazon S3]액세스 키 및[!DNL Amazon S3]비밀 키**:이 [!DNL Amazon S3]에서 `access key - secret access key` 쌍을 생성하여 계정에 대한 Adobe 실시간 CDP 액세스 권한을 [!DNL Amazon S3] 부여합니다. 자세한 내용은 [Amazon 웹 서비스 문서를 참조하십시오](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>Adobe 실시간 CDP는 내보내기 파일이 전달될 버킷 객체에 대한 `write` 권한이 필요합니다.

## 내보낸 데이터 {#exported-data}

대상 [!DNL Amazon S3] 의 경우 Adobe 실시간 CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 파일 또는 `.csv` 파일을 생성합니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상을](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 참조하십시오.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
