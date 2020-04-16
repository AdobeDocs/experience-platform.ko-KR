---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Microsoft Dynamics 또는 Salesforce 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# UI에서 Microsoft Dynamics 또는 Salesforce 소스 커넥터 만들기

Adobe Experience Platform의 소스 커넥터는 외부에서 소스의 CRM 데이터를 일정 단위로 인제스트하는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Microsoft Dynamics(이하 &quot;Dynamics&quot;)나 Salesforce 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의](../../../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

이미 Microsoft Dynamics 또는 Salesforce 기본 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/crm.md).

### 필요한 자격 증명 수집

플랫폼에서 Dynamics 계정에 액세스하려면 서비스 URI, **사용자******&#x200B;이름 **및**&#x200B;암호를제공해야 합니다.

마찬가지로, 플랫폼에서 Salesforce 계정에 액세스하려면 **환경 URL**, **사용자 이름**, **암호,**&#x200B;보안 **토큰을 제공해야 합니다**.

## Dynamics 또는 Salesforce 계정 연결

CRM 시스템의 자격 증명이 준비되면 아래 절차에 따라 Dynamics 또는 Salesforce 계정을 플랫폼에 연결할 새 인바운드 기본 연결을 만들 수 있습니다.

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 막대에서 소스를 선택하여 소스 작업 영역에 액세스합니다. [ *카탈로그* ] 화면에는 인바운드 기본 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연결된 기존 기본 연결의 수가 표시됩니다.

CRM *카테고리* 아래에서 **Microsoft Dynamics** 또는 **Salesforce를** 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄은 선택한 소스에 대한 간단한 설명과 해당 설명서를 보거나 소스와 연결할 수 있는 옵션을 제공합니다. 새 인바운드 기본 연결을 만들려면 Connect **소스를**&#x200B;클릭합니다.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

입력 양식에서 이름, 선택적 설명 및 Dynamics 또는 Salesforce 자격 증명과 함께 기본 연결을 제공합니다. 마지막으로 Connect **를** 클릭한 다음 새 기본 연결을 설정하는 데 약간의 시간이 소요됩니다.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

CRM 시스템과의 기본 연결이 설정되면 다음 섹션으로 계속 이동하여 데이터 흐름을 구성하여 CRM 데이터를 플랫폼으로 가져올 수 있습니다.

## 다음 단계

이 튜토리얼을 따라 Dynamics 또는 Salesforce 계정에 기본 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하고 데이터를 Platform으로 가져오도록 데이터 흐름을 [구성할 수 있습니다](../../dataflow/crm.md).