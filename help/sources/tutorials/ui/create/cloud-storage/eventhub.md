---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;Event Hubs;azure event hubs
solution: Experience Platform
title: UI에서 Azure 이벤트 허브 원본 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Azure 이벤트 허브(이하 "이벤트 허브") 소스 커넥터를 인증하는 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---


# UI에서 [!DNL Azure Event Hubs] 소스 커넥터 만들기

>[!NOTE]
>
> 커넥터의 [!DNL Azure Event Hubs] 베타입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 [!DNL Azure Event Hubs] 사용자 인터페이스를 사용하여 소스 커넥터(이하 &quot;[!DNL Event Hubs][!DNL Platform] &quot;라 한다)를 인증하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model] (XDM) 시스템](../../../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL 실시간 고객 프로필]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Event Hubs] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성 자습서로 진행할 수 있습니다](../../dataflow/streaming/cloud-storage-streaming.md).

### 필요한 자격 증명 수집

소스 커넥터를 인증하려면 [!DNL Event Hubs] 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `sasKey` | 생성된 공유 액세스 서명. |
| `namespace` | 액세스하려는 [!DNL Event Hubs] 네임스페이스입니다. |

이러한 값에 대한 자세한 내용은 이 문서 [ [!DNL Event Hubs] 를 참조하십시오](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## 계정 [!DNL Event Hubs] 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 [!DNL Event Hubs] 계정을 연결할 수 있습니다 [!DNL Platform].

[Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택하여 **[!UICONTROL 소스 작업 영역에]** 액세스합니다. [ **[!UICONTROL 카탈로그]** ] 탭에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[ **[!UICONTROL 클라우드 스토리지]** ] 범주 아래에서 **[!UICONTROL Azure 이벤트 허브를 선택합니다]**. 이 커넥터를 처음 사용하는 경우 구성을 **[!UICONTROL 선택합니다]**. 그렇지 않은 경우 **[!UICONTROL 데이터]** 추가를 선택하여 새 이벤트 허브 커넥터를 만듭니다.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Azure **[!UICONTROL 이벤트 허브에 연결 대화 상자가]** 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 새 계정 **[!UICONTROL 을 선택합니다]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 자격 증명을 [!DNL Event Hubs] 제공합니다. 완료되면 **[!UICONTROL Connect를]** 선택한 다음 새 연결이 설정될 때까지 잠시 기다립니다.

![](../../../../images/tutorials/create/eventhub/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 [!DNL Event Hubs] 계정을 선택한 다음 **[!UICONTROL 다음을]** 선택하여 진행합니다.

![](../../../../images/tutorials/create/eventhub/existing.png)

## 다음 단계

이 튜토리얼을 따라 계정을 연결했습니다 [!DNL Event Hubs] [!DNL Platform]. 이제 다음 튜토리얼로 계속 진행하여 데이터 흐름 [을 구성하여 클라우드 스토리지의 데이터를 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md)가져올 수 있습니다.