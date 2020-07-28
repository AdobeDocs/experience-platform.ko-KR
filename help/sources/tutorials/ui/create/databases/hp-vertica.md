---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에 HP Vertica 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---


# UI에서 HP [!DNL Vertica] 소스 커넥터 만들기

>[!NOTE]
> HP 커넥터 [!DNL Vertica] 가 베타 버전입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

Adobe Experience Platform의 소스 커넥터는 외부에서 가져온 데이터를 예약된 기준으로 인제스트하는 기능을 제공합니다. 이 자습서에서는 [!DNL Vertica] [!DNL Platform] 사용자 인터페이스를 사용하여 HP 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md): 고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 HP [!DNL Vertica] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성 자습서로 진행할 수 있습니다](../../dataflow/databases.md).

### 필요한 자격 증명 수집

다음 섹션에서는 [!DNL Vertica] [!DNL Flow Service] API를 사용하여 HP에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | HP 인스턴스에 연결하는 데 사용되는 연결 [!DNL Vertica] 문자열입니다. HP의 연결 문자열 패턴 [!DNL Vertica] 은 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

시작하는 방법에 대한 자세한 내용은 [이 HP Vertica 문서를 참조하십시오](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## HP [!DNL Vertica] 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 연결할 새 HP [!DNL Vertica] 계정을 만들 수 있습니다 [!DNL Platform].

Adobe Experience Platform에 [로그인한](https://platform.adobe.com) 다음 왼쪽 탐색 **[!UICONTROL 모음에서]** 소스 *[!UICONTROL 를 선택하여]* 소스 작업 영역에액세스합니다. [ *[!UICONTROL 카탈로그]* ] 화면에는 인바운드 계정을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 기존 계정 및 데이터 세트 흐름 수가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

Databases *[!UICONTROL 카테고리]* 아래에서 **[!UICONTROL HP Vertica를]** 선택하고 + 아이콘 **을 클릭하여 새 HP Vertica 커넥터를 만듭니다** .

![카탈로그](../../../../images/tutorials/create/hp-vertica/catalog.png)

HP Vertica *[!UICONTROL 에 연결]* 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정을 선택합니다]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 HP 자격 증명과 함께 연결을 [!DNL Vertica] 제공합니다. 완료되면 **[!UICONTROL Connect를]** 선택한 다음 새 계정이 설정되기까지 약간의 시간이 소요됩니다.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### 기존 계정

기존 계정을 연결하려면 연결하려는 HP [!DNL Vertica] 계정을 선택한 다음 **[!UICONTROL 오른쪽 상단]** 모서리에서 다음을 선택하여 진행하십시오.

![기존](../../../../images/tutorials/create/hp-vertica/existing.png)

## 다음 단계

이 튜토리얼을 따라 HP [!DNL Vertica] 계정에 연결되었습니다. 이제 다음 튜토리얼로 계속 이동하여 데이터를 Platform으로 가져오도록 [데이터 흐름을 구성할 수 있습니다](../../dataflow/databases.md).