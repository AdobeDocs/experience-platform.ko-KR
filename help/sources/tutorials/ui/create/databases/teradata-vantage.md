---
keywords: Experience Platform;홈;인기 항목;Teradata Vantage
title: UI에서 Teradata Vantage Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Teradata Vantage 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 322b9aa5b817276eb4b56daf6e410944591c1d51
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta) [!DNL Teradata Vantage] UI의 소스 연결

>[!NOTE]
>
> 다음 [!DNL Teradata Vantage] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Teradata Vantage] Adobe Experience Platform 사용자 인터페이스를 사용하는 소스 커넥터입니다.

## 시작하기

이 자습서에서는 다음 플랫폼 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Teradata Vantage] 플랫폼의 계정에서 다음 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 연결 문자열 | 연결 문자열은 데이터 소스 및 데이터 소스에 연결할 수 있는 방법에 대한 정보를 제공하는 문자열입니다. 에 대한 연결 문자열 패턴입니다 [!DNL Teradata Vantage] 은(는) `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Teradata Vantage] 문서](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## 연결 [!DNL Teradata Vantage] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 데이터베이스] 범주, 선택 **[!UICONTROL Teradata 밴티지]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

다음 **[!UICONTROL teradata Vantage에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 [!DNL Teradata Vantage] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![](../../../../images/tutorials/create/teradata/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL Teradata Vantage] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![](../../../../images/tutorials/create/teradata/new.png)

## 다음 단계

이 자습서에 따라 Teradata Vantage 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터를 Platform으로 가져오는 데이터 흐름 구성](../../dataflow/databases.md).
