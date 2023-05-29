---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;oracle;
title: (베타) Platform UI를 사용하여 Oracle Responsys 소스 연결 만들기
description: Platform UI를 사용하여 Adobe Experience Platform을 Oracle Responsys에 연결하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta) [!DNL Oracle Responsys] 플랫폼 UI를 사용한 소스 연결

>[!NOTE]
>
>다음 [!DNL Oracle Responsys] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

이 자습서에서는 다음을 만드는 단계를 제공합니다 [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) Adobe Experience Platform 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 안내서를 사용하려면 다음 Platform 구성 요소에 대한 작업 이해가 필요합니다.

* [소스](../../../../home.md): Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이미 인증된 사용자가 있는 경우 [!DNL Oracle Responsys] 플랫폼에서 작업하는 경우 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [마케팅 자동화 데이터를 Platform으로 가져오기 위한 데이터 흐름 만들기](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

연결하려면 [!DNL Oracle Responsys] 플랫폼에 다음 인증 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 엔드포인트 | 의 REST 인증 끝점 URL [!DNL Oracle Responsys] 인스턴스. |
| 클라이언트 ID | 에 대한 클라이언트 ID [!DNL Oracle Responsys] 인스턴스. |
| 클라이언트 암호 | 의 클라이언트 암호 [!DNL Oracle Responsys] 인스턴스. |

의 인증 자격 증명에 대한 자세한 정보 [!DNL Oracle Responsys], 다음을 참조하십시오. [[!DNL Oracle Responsys] 인증 안내서](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL Oracle Responsys] 계정을 플랫폼에 추가합니다.

## 연결 [!DNL Oracle Responsys] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 마케팅 자동화] 범주, 선택 **[!UICONTROL Oracle Responsys]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![oracle Responsys 소스가 강조 표시된 Adobe Experience Platform 소스 카탈로그입니다.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

다음 **[!UICONTROL oracle Responsys 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Oracle Responsys] 새 데이터 흐름을 만들 계정 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![oracle Responsys에 대한 기존 계정 인증 화면입니다.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 새 계정

새 계정을 만들려면 다음을 선택합니다. **[!UICONTROL 새 계정]**&#x200B;을 누르고 이름, 설명(선택 사항) 및 의 적절한 값을 제공합니다. [!DNL Oracle Responsys] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![oracle Responsys에 대한 새 계정 인증 화면입니다.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 다음 단계

이 자습서에 따라 간의 소스 연결을 인증하고 만들었습니다. [!DNL Oracle Responsys] 계정과 플랫폼. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 만들어 Platform으로 마케팅 자동화 데이터 가져오기](../../dataflow/marketing-automation.md).
