---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI 파섹
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# UI 파섹

Adobe Experience Platform의 소스 커넥터는 외부 소스 데이터를 일정 단위로 인제스트할 수 있는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Azure Blob(이하 &quot;Blob&quot;) 또는 Amazon S3(이하 &quot;S3&quot;) 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의](../../../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

이미 Blob 또는 S3 기본 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/cloud-storage.md).

### 지원되는 파일 형식

Experience Platform은 외부 스토리지에서 인제스트할 다음 파일 형식을 지원합니다.

* 구분 기호 구분 값(DSV):DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 문자와 밑줄로만 구성되어야 합니다. 일반 DSV 파일에 대한 지원이 나중에 제공될 예정입니다.
* JavaScript 개체 표기법(JSON):JSON 형식 데이터 파일은 XDM과 호환되어야 합니다.
* Apache Partiquet:쪽모이 세공 마루 형식 데이터 파일은 XDM과 호환되어야 합니다.

### 필요한 자격 증명 수집

플랫폼의 Blob 저장소에 액세스하려면 올바른 Azure 저장소 **연결 문자열을**&#x200B;제공해야 합니다. 이 Microsoft Azure 문서를 <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string" target="_blank"></a>통해 연결 문자열을 얻는 방법을 포함하여 연결 문자열에 대해 자세히 알아볼 수 있습니다.

마찬가지로, 플랫폼에서 S3 버킷에 액세스하려면 S3 **액세스 키와** S3 **비밀 키를 제공해야 합니다**. 자세한 내용은 <a href="https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/" target="_blank">이 AWS 문서를</a>참조하십시오.

## Blob 또는 S3 계정 연결

클라우드 스토리지의 자격 증명이 준비되면 아래 단계에 따라 Blob 또는 S3 계정을 플랫폼에 연결하는 새로운 인바운드 기본 연결을 만들 수 있습니다.

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 막대에서 소스를 선택하여 소스 작업 영역에 액세스합니다. [ *카탈로그* ] 화면에는 인바운드 기본 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연결된 기존 기본 연결의 수가 표시됩니다.

클라우드 *저장소* 카테고리 아래에서 **Azure Blob** 저장소 또는 **Amazon S3를** 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄은 선택한 소스에 대한 간단한 설명과 해당 설명서를 보거나 소스와 연결할 수 있는 옵션을 제공합니다. 새 인바운드 기본 연결을 만들려면 Connect **소스를**&#x200B;클릭합니다.

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

입력 양식에서 이름, 선택적 설명, Blob 또는 S3 자격 증명을 사용하여 기본 연결을 제공합니다. 마지막으로 Connect **를** 클릭한 다음 새 기본 연결을 설정하는 데 약간의 시간이 소요됩니다.

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## 다음 단계

이 자습서를 따라 Azure Blob 또는 Amazon S3 계정에 기본 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하고 데이터를 Platform으로 가져오도록 데이터 흐름을 [구성할 수 있습니다](../../dataflow/cloud-storage.md).