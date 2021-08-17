---
keywords: SFTP;sftp
title: SFTP 연결
description: SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 구분된 데이터 파일을 주기적으로 내보냅니다.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# SFTP 연결

## 개요 {#overview}

SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 구분된 데이터 파일을 주기적으로 내보냅니다.

>[!IMPORTANT]
>
> Adobe은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보내는 권장 클라우드 저장소 위치는 [!DNL Amazon S3] 및 [!DNL Azure Blob]입니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 이메일 주소,  [전화 번호, 성)](../../ui/activate-destinations.md#select-attributes).

![SFTP 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **호스트**: SFTP 저장소 위치의 주소입니다
* **사용자 이름**: SFTP 저장소 위치에 로그인할 사용자 이름입니다
* **암호**: SFTP 저장소 위치에 로그인하는 암호입니다
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.

선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩 문자열로 기록해야 합니다.

## 내보낸 데이터 {#exported-data}

[!DNL SFTP] 대상의 경우 Platform은 사용자가 제공한 저장소 위치에 탭으로 구분된 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.

## IP 주소 허용 목록

허용 목록에 Adobe IP를 추가해야 하는 경우 클라우드 저장소 대상에 대한 [IP 주소 허용 목록 를 참조하십시오](ip-address-allow-list.md).
