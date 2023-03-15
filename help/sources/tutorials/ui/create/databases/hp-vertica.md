---
keywords: Experience Platform;홈;인기 항목;HP Vertica
solution: Experience Platform
title: UI에서 HP Vertica 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 HP Vertica 소스 연결을 만드는 방법을 알아봅니다.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---

# HP 만들기 [!DNL Vertica] UI의 소스 연결

>[!NOTE]
>
> HP [!DNL Vertica] 커넥터가 Beta 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 HP를 만드는 단계를 제공합니다 [!DNL Vertica] 를 사용하는 소스 커넥터 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 HP가 있는 경우 [!DNL Vertica] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

다음 섹션에서는 HP에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다 [!DNL Vertica] 사용 [!DNL Flow Service] API.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | HP에 연결하는 데 사용되는 연결 문자열 [!DNL Vertica] 인스턴스. HP에 대한 연결 문자열 패턴입니다. [!DNL Vertica] 은(는) `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

시작하기에 대한 자세한 내용은 을(를) 참조하십시오. [이 HP [!DNL Vertica] 문서](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## HP 연결 [!DNL Vertica] account

필요한 자격 증명을 수집했으면 아래 단계에 따라 HP를 연결할 수 있습니다 [!DNL Vertica] 계정 위치: [!DNL Platform].

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: **[!UICONTROL 소스]** 작업 영역. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL 데이터베이스]** 범주, 선택 **[!UICONTROL HP Vertica]**. 이 커넥터를 처음 사용하는 경우 다음을 선택합니다. **[!UICONTROL 구성]**. 그렇지 않으면 를 선택합니다. **[!UICONTROL 데이터 추가]** 새 HP 를 만들려면 [!DNL Vertica] 커넥터.

![카탈로그](../../../../images/tutorials/create/hp-vertica/catalog.png)

다음 **[!UICONTROL HP Vertica에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에 이름, 설명(선택 사항) 및 HP를 입력합니다. [!DNL Vertica] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![연결](../../../../images/tutorials/create/hp-vertica/new.png)

### 기존 계정

기존 계정을 연결하려면 HP를 선택합니다. [!DNL Vertica] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 을 참조하십시오.

![기존](../../../../images/tutorials/create/hp-vertica/existing.png)

## 다음 단계

이 자습서를 따라 HP에 대한 연결을 설정했습니다 [!DNL Vertica] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 데이터 가져오기 [!DNL Platform]](../../dataflow/databases.md).
