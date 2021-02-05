---
keywords: Experience Platform;홈;인기 항목;Microsoft SQL Server;SQL Server;sql server;home;popular topics;Microsoft SQL Server;sql server;server
solution: Experience Platform
title: UI에서 Microsoft SQL Server 소스 연결 만들기
topic: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Microsoft SQL Server 소스 연결을 만드는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# UI에 [!DNL Microsoft SQL Server] 소스 연결 만들기

>[!NOTE]
>
> [!DNL Microsoft SQL Server] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform의 소스 커넥터는 예약된 기준에 따라 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 [!DNL Microsoft SQL Server](이하 &quot;[!DNL SQL Server]&quot;) 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL SQL Server] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름](../../dataflow/databases.md)을 구성하는 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Platform]의 [!DNL SQL Server]에 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | [!DNL SQL Server] 계정과 연결된 연결 문자열입니다. [!DNL SQL Server] 연결 문자열 패턴은 다음과 같습니다.`Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

시작하는 방법에 대한 자세한 내용은 [이 [!DNL SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)를 참조하십시오.

## [!DNL SQL Server] 계정 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 [!DNL SQL Server] 계정을 [!DNL Platform]에 연결할 수 있습니다.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 **[!UICONTROL 소스]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL 데이터베이스]** 범주에서 **[!UICONTROL Microsoft SQL Server]**&#x200B;를 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**&#x200B;을 선택합니다. 그렇지 않은 경우 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 새 [!DNL SQL Server] 커넥터를 만듭니다.

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

**[!UICONTROL Microsoft SQL Server에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL SQL Server] 자격 증명을 입력합니다. 완료되면 **[!UICONTROL Connect]**&#x200B;를 선택한 다음 새 연결이 설정될 때까지 잠시 기다려 주십시오.

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 [!DNL SQL Server] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속 진행합니다.

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL SQL Server] 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 데이터를 [!DNL Platform]](../../dataflow/databases.md)로 가져올 수 있습니다.