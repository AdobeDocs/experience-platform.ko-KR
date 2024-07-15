---
title: UI에서 Azure Event Hubs Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Azure Event Hubs 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1256f0c76b29edad4808fc4be1d61399bfbae8fa
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# UI에서 [!DNL Azure Event Hubs] 소스 연결 만들기

>[!IMPORTANT]
>
>[!DNL Azure Event Hubs] 원본은 Real-time Customer Data Platform Ultimate를 구입한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL Azure Event Hubs] 계정을 만드는 방법에 대해 알아보려면 이 자습서를 참조하십시오.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL Event Hubs] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/streaming/cloud-storage-streaming.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Event Hubs] 원본 커넥터를 인증하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 표준 인증]

| 자격 증명 | 설명 |
| --- | --- |
| SAS 키 이름 | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| SAS 키 | [!DNL Event Hubs] 네임스페이스의 기본 키입니다. [!DNL Event Hubs] 목록을 채우려면 `sasKey`에 해당하는 `sasPolicy`에 `manage` 권한이 구성되어 있어야 합니다. |
| 네임스페이스 | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |

>[!TAB SAS 인증]

| 자격 증명 | 설명 |
| --- | --- |
| SAS 키 이름 | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| SAS 키 | [!DNL Event Hub] 네임스페이스의 기본 키입니다. [!DNL Event Hubs] 목록을 채우려면 `sasKey`에 해당하는 `sasPolicy`에 `manage` 권한이 구성되어 있어야 합니다. |
| 네임스페이스 | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |
| 이벤트 허브 이름 | [!DNL Azure Event Hub] 이름을 입력하십시오. [!DNL Event Hub] 이름에 대한 자세한 내용은 [Microsoft 설명서](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)를 참조하십시오. |

>[!TAB 이벤트 허브 Azure Active Directory 인증]

| 자격 증명 | 설명 |
| --- | --- |
| 임차인 ID | 권한을 요청하려는 테넌트 ID입니다. 테넌트 ID는 GUID 또는 친숙한 이름으로 포맷할 수 있습니다. **참고**: 테넌트 ID는 [!DNL Microsoft Azure] 인터페이스에서 &quot;디렉터리 ID&quot;라고 합니다. |
| 클라이언트 ID | 앱에 할당된 애플리케이션 ID입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 이 ID를 검색할 수 있습니다. |
| 클라이언트 암호 값 | 앱을 인증하기 위해 클라이언트 ID와 함께 사용되는 클라이언트 암호입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 클라이언트 암호를 검색할 수 있습니다. |
| 네임스페이스 | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |

[!DNL Azure Active Directory]에 대한 자세한 내용은 [Microsoft Entra ID 사용에 대한 Azure 안내서](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)를 참조하세요.

>[!TAB 이벤트 허브에서 Azure Active Directory 인증 범위를 지정함]

| 자격 증명 | 설명 |
| --- | --- |
| 임차인 ID | 권한을 요청하려는 테넌트 ID입니다. 테넌트 ID는 GUID 또는 친숙한 이름으로 포맷할 수 있습니다. **참고**: 테넌트 ID는 [!DNL Microsoft Azure] 인터페이스에서 &quot;디렉터리 ID&quot;라고 합니다. |
| 클라이언트 ID | 앱에 할당된 애플리케이션 ID입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 이 ID를 검색할 수 있습니다. |
| 클라이언트 암호 값 | 앱을 인증하기 위해 클라이언트 ID와 함께 사용되는 클라이언트 암호입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 클라이언트 암호를 검색할 수 있습니다. |
| 네임스페이스 | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |
| 이벤트 허브 이름 | [!DNL Azure Event Hub] 이름을 입력하십시오. [!DNL Event Hub] 이름에 대한 자세한 내용은 [Microsoft 설명서](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)를 참조하십시오. |

[!DNL Azure Active Directory]에 대한 자세한 내용은 [Microsoft Entra ID 사용에 대한 Azure 안내서](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)를 참조하세요.

>[!ENDTABS]

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Event Hubs] 계정을 Experience Platform에 연결할 수 있습니다.

## [!DNL Event Hubs] 계정 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 범주에서 **[!UICONTROL Azure Event Hubs]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![Azure 이벤트 허브가 있는 원본 카탈로그를 선택했습니다.](../../../../images/tutorials/create/eventhub/catalog.png)

**[!UICONTROL Azure 이벤트 허브에 연결]** 대화 상자가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 사용할 [!DNL Event Hubs] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![기존 Azure Event Hubs 원본 계정의 목록입니다.](../../../../images/tutorials/create/eventhub/existing.png)

### 새 계정

>[!TIP]
>
>만든 후에는 [!DNL Event Hubs] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 새 [!DNL Event Hubs] 계정에 대한 이름과 선택적 설명을 입력하십시오.

![Azure 이벤트 허브에 대한 새 계정 만들기 인터페이스입니다.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB 표준 인증]

표준 인증을 사용하여 [!DNL Event Hubs] 계정을 만들려면 [!UICONTROL 계정 인증] 드롭다운 메뉴를 사용한 다음 **[!UICONTROL 표준 인증]**&#x200B;을 선택하십시오. 그런 다음 [!UICONTROL SAS 키 이름], [!UICONTROL SAS 키] 및 [!UICONTROL 네임스페이스]에 대한 값을 제공합니다.

인증 자격 증명을 입력했으면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택합니다.

![Azure 이벤트 허브용 표준 인증 인터페이스](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS 인증]

SAS 인증을 사용하여 [!DNL Event Hubs] 계정을 만들려면 [!UICONTROL 계정 인증] 드롭다운 메뉴를 사용한 다음 **[!UICONTROL SAS 인증]**&#x200B;을 선택하십시오. 그런 다음 [!UICONTROL SAS 키 이름], [!UICONTROL SAS 키], [!UICONTROL 네임스페이스] 및 [!UICONTROL 이벤트 허브 이름]에 대한 값을 제공하십시오.

인증 자격 증명을 입력했으면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택합니다.

![Azure 이벤트 허브용 SAS 인증 인터페이스](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB 이벤트 허브 Azure Active Directory 인증]

Event Hub Azure Active Directory 인증을 사용하여 [!DNL Event Hubs] 계정을 만들려면 [!UICONTROL 계정 인증] 드롭다운 메뉴를 사용한 다음 **[!UICONTROL Event Hub Azure Active Directory]**&#x200B;를 선택합니다. 그런 다음 [!UICONTROL 테넌트 ID], [!UICONTROL 클라이언트 ID], [!UICONTROL 클라이언트 암호 값] 및 [!UICONTROL 네임스페이스]에 대한 값을 제공합니다.

![Azure 이벤트 허브 Azure Active Directory 인증](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB 이벤트 허브에서 Azure Active Directory 인증 범위를 지정함]

이벤트 허브 범위 Azure Active Directory 인증을 사용하여 [!DNL Event Hubs] 계정을 만들려면 [!UICONTROL 계정 인증] 드롭다운 메뉴를 사용한 다음 **[!UICONTROL 이벤트 허브 범위 Azure Active Directory]**&#x200B;를 선택하십시오. 그런 다음 [!UICONTROL 테넌트 ID], [!UICONTROL 클라이언트 ID], [!UICONTROL 클라이언트 암호 값], [!UICONTROL 네임스페이스] 및 [!UICONTROL 이벤트 허브 이름]에 대한 값을 제공하십시오.

![Azure 이벤트 허브에서 Azure Activity Directory 인증 범위를 지정함](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## 다음 단계

이 자습서에 따라 [!DNL Event Hubs] 계정을 Experience Platform에 연결했습니다. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서 Experience Platform으로 데이터를 가져오도록 데이터 흐름을 구성](../../dataflow/streaming/cloud-storage-streaming.md)할 수 있습니다.
