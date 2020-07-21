---
title: Amazon S3 대상
seo-title: Amazon S3 대상
description: AWS(Amazon Web Services) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.
seo-description: AWS(Amazon Web Services) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] 대상

## 개요

AWS) [!DNL Amazon Web Services] S3 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.

## 연결 대상 {#connect-destination}

클라우드 [스토리지 대상 워크플로우 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)에서 클라우드 스토리지 대상에 연결하는 방법에 대한 지침을 참조하십시오 [!DNL Amazon S3].

대상에 대해 [!DNL Amazon S3] 대상 만들기 워크플로우에서 다음 정보를 입력합니다.

* **[!DNL Amazon S3]액세스 키 및[!DNL Amazon S3]비밀 키&#x200B;**: 액세스 키[!DNL Amazon S3]를 생성하여 Adobe에서 실시간 CDP에 계정에 대한 액세스 권한을[!DNL Amazon S3]부여합니다.



>[!IMPORTANT]
>
>Adobe Real-time CDP는 내보내기 파일이 전달될 버킷 객체에 대한 `write` 권한이 필요합니다.
