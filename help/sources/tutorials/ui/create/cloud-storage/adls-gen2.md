---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Azure Data Lake Storage Gen2 원본 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# UI에서 Azure Data Lake Storage Gen2 원본 커넥터 만들기

Adobe Experience Platform의 소스 커넥터는 외부 소스 데이터를 일정 기준에 따라 인제스트할 수 있는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Azure Data Lake Storage Gen2(이하 &quot;ADLS Gen2&quot;) 소스 커넥터를 인증하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의](../../../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
- [실시간 고객 프로필](../../../../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

이미 ADLS Gen2 기본 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/cloud-storage.md).

### 필요한 자격 증명 수집

ADLS Gen2 소스 커넥터를 인증하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | ADLS Gen2의 끝점입니다. |
| `servicePrincipalId` | 응용 프로그램의 클라이언트 ID입니다. |
| `servicePrincipalKey` | 응용 프로그램 키 |
| `tenant` | 응용 프로그램이 포함된 테넌트 정보. |

이러한 값에 대한 자세한 내용은 [이 ADLS Gen2 문서를](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)참조하십시오.

## ADLS Gen2 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 ADLS Gen2 계정을 플랫폼에 연결하는 새로운 인바운드 기본 연결을 만들 수 있습니다.

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 표시줄에서 Sources를 선택하여 *Sources* 작업 영역에 액세스할 수있습니다. [ *카탈로그* ] 탭에는 인바운드 기본 연결을 생성하는 데 사용할 수 있는 다양한 소스가 표시됩니다. 각 소스에는 연결된 기존 기본 연결의 수가 표시됩니다.

클라우드 *저장소* 카테고리 아래에서 **Azure Data Lake Gen2를** 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄에서는 선택한 소스에 대한 간단한 설명과 해당 설명서를 소스 뷰와 연결하는 옵션을 제공합니다. 새 인바운드 기본 연결을 만들려면 Connect **소스를**&#x200B;클릭합니다.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Azure *Data Lake Gen2에* 연결 대화 상자가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 새 계정을 **선택합니다**. 표시되는 입력 양식에서 이름, 선택적 설명 및 ADLS Gen2 자격 증명으로 기본 연결을 제공합니다. 완료되면 Connect **를** 선택한 다음 새 기본 연결이 설정될 시간을 허용합니다.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 기존 계정

기존 계정을 연결하려면 연결할 ADLS Gen2 계정을 선택한 다음 **다음을** 선택하여 진행합니다.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 다음 단계

이 자습서를 따라 ADLS Gen2 계정에 대한 기본 연결을 설정했습니다. 이제 다음 튜토리얼을 통해 데이터 흐름을 [구성하여 클라우드 스토리지의 데이터를 Platform으로 가져올 수 있습니다](../../dataflow/cloud-storage.md).