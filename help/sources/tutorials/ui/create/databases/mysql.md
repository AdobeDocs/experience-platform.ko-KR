---
keywords: Experience Platform;홈;인기 항목;mysql;MySQL
solution: Experience Platform
title: UI에서 MySQL 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 MySQL 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# 만들기 [!DNL MySQL] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL MySQL] Adobe Experience Platform UI를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 다음 항목이 있는 경우: [!DNL MySQL] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL MySQL] 다음에 대한 계정 [!DNL Platform], 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | 다음 [!DNL MySQL] 계정과 연결된 연결 문자열입니다. 다음 [!DNL MySQL] 연결 문자열 패턴: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. 연결 문자열과 연결 문자열을 가져오는 방법에 대해 자세히 알아보려면 [[!DNL MySQL] 문서](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## 연결 [!DNL MySQL] account

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL MySQL] 계정 위치: [!DNL Platform].

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: **[!UICONTROL 소스]** 작업 영역. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

아래 **[!UICONTROL 데이터베이스]** 범주, 선택 **[!UICONTROL MySQL]**. 이 커넥터를 처음 사용하는 경우 다음을 선택합니다. **[!UICONTROL 구성]**. 그렇지 않으면 를 선택합니다. **[!UICONTROL 데이터 추가]** 새로 만들려면 [!DNL MySQL] 커넥터.

![](../../../../images/tutorials/create/my-sql/catalog.png)

다음 **[!UICONTROL MySQL에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL MySQL] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![](../../../../images/tutorials/create/my-sql/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL MySQL] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![](../../../../images/tutorials/create/my-sql/existing.png)

## 다음 단계

이 자습서를 따라 MySQL 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 데이터 가져오기 [!DNL Platform]](../../dataflow/databases.md).
