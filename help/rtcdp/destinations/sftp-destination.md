---
title: SFTP 대상
seo-title: SFTP 대상
description: SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Experience Platform에서 구분된 데이터 파일을 정기적으로 내보냅니다.
seo-description: SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Experience Platform에서 구분된 데이터 파일을 정기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# SFTP 대상

## 개요

SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Experience Platform에서 구분된 데이터 파일을 정기적으로 내보냅니다.

데이터를 내보내려면 다음 단계를 완료하십시오.

## 연결 대상 {#connect-destination}

SFTP를 비롯한 클라우드 스토리지 대상에 연결하는 방법 [](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)에 대한 지침은 클라우드 스토리지 대상 워크플로우를 참조하십시오.

SFTP 대상의 경우 **인증** 단계에서 대상 만들기 워크플로우에 다음 정보를 입력합니다.

* **호스트**: SFTP 저장소 위치의 주소
* **사용자 이름**: SFTP 저장소 위치에 로그인하는 사용자 이름
* **암호**: SFTP 저장소 위치에 로그인하는 암호

## 내보낸 데이터 {#exported-data}

대상 [!SFTP] 의 경우 Adobe 실시간 CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 파일 또는 `.csv` 파일을 생성합니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상을](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 참조하십시오.