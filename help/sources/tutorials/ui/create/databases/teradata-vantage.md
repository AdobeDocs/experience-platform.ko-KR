---
keywords: Experience Platform;홈;인기 항목;Teradata Vantage
title: UI에서 Teradata Vantage Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Teradata Vantage 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 2%

---

# UI에서 [!DNL Teradata Vantage] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL Teradata Vantage] 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

Experience Platform에서 [!DNL Teradata Vantage] 계정에 액세스하려면 다음 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 연결 문자열 | 연결 문자열은 데이터 소스 및 데이터 소스에 연결할 수 있는 방법에 대한 정보를 제공하는 문자열입니다. [!DNL Teradata Vantage]에 대한 연결 문자열 패턴은 `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`입니다. |

시작에 대한 자세한 내용은 이 [[!DNL Teradata Vantage] 문서](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options)를 참조하세요.

## [!DNL Teradata Vantage] 계정 연결

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 데이터베이스] 범주에서 **[!UICONTROL Teradata Vantage]**&#x200B;를 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정이 있으면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.

![Teradata Vantage 소스가 있는 소스 카탈로그를 선택했습니다.](../../../../images/tutorials/create/teradata/catalog.png)

**[!UICONTROL Teradata Vantage에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정에 연결하려면 연결할 [!DNL Teradata Vantage] 계정을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![원본 작업 영역의 기존 계정 페이지입니다.](../../../../images/tutorials/create/teradata/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하십시오. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL Teradata Vantage] 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 시간을 허용합니다.

![원본 작업 영역의 새 계정 만들기 인터페이스입니다.](../../../../images/tutorials/create/teradata/new.png)

## 다음 단계

이 자습서를 따라 Teradata Vantage 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/databases.md)할 수 있습니다.
