---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 FTP 또는 SFTP 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---


# UI에서 FTP 또는 SFTP 소스 커넥터 만들기

>[!NOTE]
>FTP 및 SFTP 커넥터가 베타에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

Adobe Experience Platform의 소스 커넥터는 외부에서 소스 데이터를 예약된 기준으로 인제스트하는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 FTP 또는 SFTP 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md): 고객 경험 데이터를 구성하는 표준 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 FTP 또는 SFTP 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/batch/cloud-storage.md).

### 지원되는 파일 형식

Experience Platform은 외부 소스에서 인제스트할 다음 파일 형식을 지원합니다.

* 구분 기호 구분 값(DSV): DSV 형식 데이터 파일에 대한 지원은 현재 CSV(쉼표로 구분된 값)로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 및 밑줄로만 구성되어야 합니다. 일반 DSV에 대한 지원은 나중에 제공될 예정입니다.
* JSON(JavaScript Object Notation): JSON 형식 데이터 파일은 XDM과 호환되어야 합니다.
* Apache Pariter: 쪽모이 세공된 형식의 데이터 파일은 XDM과 호환되어야 합니다.

### 필요한 자격 증명 수집

플랫폼에서 FTP 또는 SFTP 서버에 액세스하려면 서버의 **호스트 이름**, **사용자 이름**&#x200B;및 **암호를 제공해야 합니다**.

## 서버에 연결

서버의 자격 증명이 준비되면 아래 단계에 따라 FTP 또는 SFTP 서버를 플랫폼에 연결하는 새 인바운드 기본 연결을 만들 수 있습니다.

Adobe <a href="https://platform.adobe.com" target="_blank">Experience Platform</a> 에 로그인한 다음 왼쪽 탐색 **모음에서** Sources를선택하여 소스 작업 영역에 액세스합니다. [ *카탈로그* ] 화면에는 인바운드 기본 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연관된 기존 기본 연결의 수가 표시됩니다.

[ *클라우드 스토리지* ] 카테고리 아래에서 **FTP** 또는 **SFTP** 중 하나를 선택하여화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄에는 선택한 소스에 대한 간단한 설명과 해당 설명서를 보거나 소스와 연결할 수 있는 옵션이 제공됩니다. 새 인바운드 기본 연결을 만들려면 **Connect 소스를 클릭합니다**.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

입력 양식에서 이름, 선택적 설명, FTP 또는 SFTP 자격 증명으로 기본 연결을 제공합니다. 마지막으로 **Connect를** 클릭한 다음 새 기본 연결이 설정되기까지 약간의 시간이 소요됩니다.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

FTP 또는 SFTP 서버와의 기본 연결이 설정되면 다음 섹션으로 계속 이동하여 데이터를 Platform으로 가져오도록 데이터 흐름을 구성할 수 있습니다.

## 다음 단계

이 튜토리얼을 따라 FTP 또는 SFTP 서버에 대한 연결을 설정했습니다. 이제 다음 튜토리얼로 계속 진행하여 데이터 흐름을 [구성하여 Platform으로 데이터를 가져올 수 있습니다](../../dataflow/batch/cloud-storage.md).
