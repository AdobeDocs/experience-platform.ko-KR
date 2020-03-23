---
title: Amazon S3 대상
seo-title: Amazon S3 대상
description: Amazon Web Services(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.
seo-description: Amazon Web Services(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342

---


# Amazon S3 대상

## 개요

Amazon Web Services(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.

## 연결 대상 {#connect-destination}

Amazon [S3를 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)비롯한 클라우드 스토리지 대상에 연결하는 방법에 대한 지침은 클라우드 스토리지 대상 워크플로우 워크플로우를 참조하십시오.

Amazon S3 대상의 경우, 대상 만들기 워크플로우에 다음 정보를 입력합니다.

* **Amazon S3 액세스 키 및 Amazon S3 비밀 키**:Amazon S3에서 액세스 키(비밀 액세스 키 쌍)를 생성하여 Adobe에서 Amazon S3 계정에 대한 실시간 CDP 액세스를 부여합니다.



>[!IMPORTANT]
>
>Adobe Real-time CDP는 내보내기 파일이 전달되는 버킷 개체에 대한 `write` 권한이 필요합니다.
