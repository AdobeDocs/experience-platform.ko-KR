---
keywords: Experience Platform;홈;인기 항목;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: UI에서 IBM DB2 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 IBM DB2 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# UI에서 IBM DB2 소스 연결 만들기

>[!NOTE]
>
> IBM DB2 커넥터는 Beta 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 를 사용하여 IBM DB2(이하 &quot;DB2&quot;) 소스 커넥터를 만드는 단계를 제공합니다. [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 DB2 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

다음 섹션에서는 를 사용하여 DB2에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `server` | DB2 서버의 이름입니다. 콜론으로 구분된 서버 이름 다음에 포트 번호를 지정할 수 있습니다. 예: server:port. |
| `database` | DB2 데이터베이스의 이름입니다. |
| `username` | DB2 데이터베이스에 접속하는 데 사용되는 사용자 이름. |
| `password` | 사용자 이름에 지정한 사용자 계정의 암호입니다. |

시작하기에 대한 자세한 내용은 을(를) 참조하십시오. [이 DB2 문서](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## IBM DB2 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 DB2 계정을 연결할 수 있습니다. [!DNL Platform].

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: **[!UICONTROL 소스]** 작업 영역. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL 데이터베이스]** 범주, 선택 **[!UICONTROL IBM DB2]**. 이 커넥터를 처음 사용하는 경우 다음을 선택합니다. **[!UICONTROL 구성]**. 그렇지 않으면 를 선택합니다. **[!UICONTROL 데이터 추가]** 새 DB2 커넥터를 만드는 방법.

![카탈로그](../../../../images/tutorials/create/ibm-db2/catalog.png)

다음 **[!UICONTROL IBM DB2에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 DB2 자격 증명을 제공합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![연결](../../../../images/tutorials/create/ibm-db2/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 DB2 계정을 선택한 다음 를 선택합니다 **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/ibm-db2/existing.png)

## 다음 단계

이 자습서에 따라 DB2 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 데이터 가져오기 [!DNL Platform]](../../dataflow/databases.md).
