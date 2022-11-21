---
keywords: Experience Platform;홈;인기 주제;소스;커넥터;oracle;
title: (베타) Platform UI를 사용하여 Responsys 소스 연결 Oracle 만들기
description: 플랫폼 UI를 사용하여 Adobe Experience Platform을 Responsys에 연결하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (베타) 만들기 [!DNL Oracle Responsys] 플랫폼 UI를 사용한 소스 연결

>[!NOTE]
>
>다음 [!DNL Oracle Responsys] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

이 자습서에서는 다음을 만드는 단계를 제공합니다 [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) Adobe Experience Platform 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 안내서에서는 Platform의 다음 구성 요소를 제대로 이해하고 있어야 합니다.

* [소스](../../../../home.md): 플랫폼을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): 플랫폼은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이미 인증된 경우 [!DNL Oracle Responsys] platform에서 계정을 설정한 경우 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [마케팅 자동화 데이터를 플랫폼으로 가져오기 위한 데이터 흐름 만들기](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

연결하려면 [!DNL Oracle Responsys] 플랫폼에 다음 인증 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 끝점 | 사용자의 REST 인증 끝점 URL입니다 [!DNL Oracle Responsys] 인스턴스. |
| 클라이언트 ID | 사용자의 클라이언트 ID [!DNL Oracle Responsys] 인스턴스. |
| 클라이언트 암호 | 고객의 클라이언트 암호 [!DNL Oracle Responsys] 인스턴스. |

의 인증 자격 증명에 대한 자세한 정보 [!DNL Oracle Responsys]를 참조하고 [[!DNL Oracle Responsys] 인증 안내서](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Oracle Responsys] Platform에 계정을 설정합니다.

## 연결 [!DNL Oracle Responsys] account

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 마케팅 자동화] 카테고리, 선택 **[!UICONTROL Responsys oracle]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![oracle Responsys 소스가 강조 표시된 Adobe Experience Platform 소스 카탈로그.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

다음 **[!UICONTROL oracle Responsys 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Oracle Responsys] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![Responsys Oracle에 대한 기존 계정 인증 화면입니다.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 새 계정

새 계정을 만들려면 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 적절한 값을 제공합니다. [!DNL Oracle Responsys] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![Responsys Oracle에 대한 새 계정 인증 화면입니다.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 다음 단계

이 자습서를 따라 사용자 간에 소스 연결을 인증하고 만들었습니다 [!DNL Oracle Responsys] 계정 및 플랫폼. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 만들어 마케팅 자동화 데이터를 플랫폼으로 가져오기](../../dataflow/marketing-automation.md).
