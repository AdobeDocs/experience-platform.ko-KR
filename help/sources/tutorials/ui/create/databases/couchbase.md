---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 쿠치베이스 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: adb9c46e7337897e2336971e58ebc90b0e497ea0
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# UI에서 쿠치베이스 소스 커넥터 만들기

> [!NOTE]
> Couchbase 커넥터가 베타에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

의 소스 커넥터는 [!DNL Adobe Experience Platform] 외부에서 가져온 데이터를 예약된 기준으로 인제스트하는 기능을 제공합니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 Couchbase 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음의 구성 요소에 대해 작업해야 [!DNL Platform]합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md): 고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 Couchbase 연결이 있는 경우 이 문서의 나머지 부분은 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/databases.md).

### 필요한 자격 증명 수집

Couchbase 소스 커넥터를 인증하려면 다음 연결 속성 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | Couchbase 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. Couchbase의 연결 문자열 패턴은 입니다 `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. 연결 문자열 가져오기에 대한 자세한 내용은 Couchbase 연결에 대한 설명서를 [참조하십시오](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## 계정 연결

필요한 자격 증명을 모았으면 아래 절차에 따라 연결할 새 Cloud 계정을 만들 수 있습니다 [!DNL Platform].

Adobe [Experience Platform에](https://platform.adobe.com) 로그인한 다음 왼쪽 탐색 **[!UICONTROL 모음에서]** Sources를 *[!UICONTROL 선택하여]* Sources 작업 영역에액세스합니다. [ *[!UICONTROL 카탈로그]* ] 화면에는 인바운드 계정을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 기존 계정 및 데이터 세트 흐름 수가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

데이터베이스 *[!UICONTROL 카테고리]* 아래에서 **[!UICONTROL + 아이콘]** (+) **을** 클릭하여 새 Couchbase 커넥터를 만듭니다.

![카탈로그](../../../../images/tutorials/create/couchbase/catalog.png)

[ *[!UICONTROL Connect to Cookbase]* ] 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정을 선택합니다]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 Couchbase 자격 증명과 함께 연결을 제공합니다. 완료되면 소스에 **[!UICONTROL 연결을]** 선택한 다음 새 계정이 설정되기까지 약간의 시간이 소요됩니다.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### 기존 계정

기존 계정을 연결하려면 연결하려는 Cumchbase 계정을 선택한 다음 **[!UICONTROL 오른쪽]** 상단 모서리에서 다음을 선택하여 진행하십시오.

![기존](../../../../images/tutorials/create/couchbase/existing.png)

## 다음 단계

이 튜토리얼을 따라 Couchbase 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼로 계속 진행하여 데이터 흐름을 [구성하여 Platform으로 데이터를 가져올 수 있습니다](../../dataflow/databases.md).