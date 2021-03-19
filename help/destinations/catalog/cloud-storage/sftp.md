---
keywords: SFTP;sftp
title: SFTP 연결
description: SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 구분된 데이터 파일을 정기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: 4f0047e7ac4c83e3e17ea0a077bbeb09c86d1db6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# SFTP 연결

SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 구분된 데이터 파일을 정기적으로 내보냅니다.

>[!IMPORTANT]
>
> Adobe은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보낼 권장되는 클라우드 저장소 위치는 [!DNL Amazon S3] 및 [!DNL Azure Blob]입니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

![SFTP 프로파일 기반 내보내기 유형](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 연결 대상 {#connect-destination}

SFTP를 비롯한 클라우드 스토리지 대상에 연결하는 방법에 대한 지침은 [클라우드 스토리지 대상 워크플로우 ](./workflow.md)을 참조하십시오.

SFTP 대상의 경우 **인증** 단계의 대상 만들기 워크플로우에 다음 정보를 입력합니다.

* **호스트**:SFTP 저장소 위치의 주소
* **사용자 이름**:SFTP 저장소 위치에 로그인하는 사용자 이름
* **암호**:SFTP 저장소 위치에 로그인하는 암호

## 내보낸 데이터 {#exported-data}

SFTP 대상의 경우 Platform은 사용자가 제공한 저장 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.

## IP 주소 허용 목록

허용 목록에 Adobe IP를 추가해야 하는 경우 클라우드 스토리지 대상 [IP 주소 허용 목록을 참조하십시오.](./ip-address-allow-list.md)