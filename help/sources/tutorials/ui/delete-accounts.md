---
keywords: Experience Platform;홈;인기 항목; 계정 삭제
description: Adobe Experience Platform의 Source 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 계정을 삭제하는 단계를 제공합니다.
solution: Experience Platform
title: UI에서 Source 연결 계정 삭제
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 소스 연결 계정 삭제

Adobe Experience Platform의 Source 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 **[!UICONTROL 소스]** 작업 영역에서 계정을 삭제하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## UI를 사용하여 계정 삭제

>[!TIP]
>
>소스 계정을 삭제하기 전에 먼저 소스 계정과 연결된 기존 데이터 흐름을 삭제해야 합니다. 기존 데이터 흐름을 삭제하려면 [UI에서 소스 데이터 흐름 삭제](./delete.md)에 대한 자습서를 참조하십시오.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 **[!UICONTROL 소스]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에 계정과 데이터 흐름을 만들 수 있는 다양한 소스가 표시됩니다. 각 소스에는 기존 계정 및 연결된 데이터 흐름의 수가 표시됩니다.

**[!UICONTROL 계정]** 페이지에 액세스하려면 **[!UICONTROL 계정]**&#x200B;을(를) 선택하십시오.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

기존 계정 목록이 나타납니다. 이 페이지에는 소스, 사용자 이름, 연관된 데이터 흐름 및 생성된 날짜와 같은 기존 계정에 대한 정렬 가능한 정보 목록이 있습니다. 왼쪽 상단의 **단계 아이콘**&#x200B;을(를) 선택하여 정렬하십시오.

![데이터 흐름 목록](../../images/tutorials/delete-accounts/accounts.png)

사용 가능한 소스 목록이 포함된 정렬 패널이 화면 왼쪽에 나타납니다. 정렬 기능을 사용하여 두 개 이상의 소스를 선택할 수 있습니다.

액세스하려는 소스를 선택하고 주 인터페이스의 계정 목록에서 삭제하려는 계정을 찾습니다. 이 예제에서 선택한 원본은 **[!DNL Azure Blob Storage]**&#x200B;이고 계정 이름은 **[!UICONTROL blobTestConnector]**&#x200B;입니다. 정렬 패널에서 여러 소스를 선택하면 목록이 만든 날짜별로 정렬되므로 가장 최근에 만든 계정이 먼저 표시됩니다.

삭제할 계정을 선택합니다.

![데이터 흐름 정렬](../../images/tutorials/delete-accounts/sort.png)

선택한 계정에 대한 정보가 포함된 **[!UICONTROL 속성]** 패널이 화면 오른쪽에 나타납니다.

삭제하려는 계정 이름 옆의 생략 부호(`...`)를 선택합니다. **[!UICONTROL 데이터 추가]**, **[!UICONTROL 세부 정보 편집]** 및 **[!UICONTROL 삭제]**&#x200B;에 옵션을 제공하는 팝업 패널이 나타납니다. 계정을 삭제하려면 **[!UICONTROL 삭제]**&#x200B;를 선택하십시오.

![데이터 흐름 정렬](../../images/tutorials/delete-accounts/delete.png)

마지막 확인 대화 상자가 나타나면 **[!UICONTROL 삭제]**&#x200B;를 선택하여 프로세스를 완료합니다.

![삭제](../../images/tutorials/delete-accounts/confirm.png)

## 다음 단계

이 자습서에 따라 **[!UICONTROL 소스]** 작업 영역을 사용하여 기존 계정을 삭제했습니다.

[!DNL Flow Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [흐름 서비스 API를 사용하여 연결 삭제](../../tutorials/api/delete.md)에 대한 자습서를 참조하십시오.
