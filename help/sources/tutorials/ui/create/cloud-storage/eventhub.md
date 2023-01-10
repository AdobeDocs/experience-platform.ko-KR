---
keywords: Experience Platform;홈;인기 항목;Azure 이벤트 허브;이벤트 허브;azure 이벤트 허브
solution: Experience Platform
title: UI에서 Azure 이벤트 허브 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Azure 이벤트 허브 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 만들기 [!DNL Azure Event Hubs] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 튜토리얼에서는 [!DNL Azure Event Hubs] (이하 &quot;라 한다)[!DNL Event Hubs]&quot;) 소스 커넥터 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   - [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Event Hubs] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/streaming/cloud-storage-streaming.md).

### 필요한 자격 증명 수집

인증을 위해 [!DNL Event Hubs] 소스 커넥터에서는 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `sasKey` | 의 기본 키 [!DNL Event Hubs] 네임스페이스. 다음 `sasPolicy` 저것은 `sasKey` 에 해당해야 함 `manage` 순서대로 구성된 권한 [!DNL Event Hubs] 채울 목록입니다. |
| `namespace` | 의 네임스페이스 [!DNL Event Hubs] 액세스 중입니다. |

이러한 값에 대한 자세한 내용은 [이 [!DNL Event Hubs] 문서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## 연결 [!DNL Event Hubs] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Event Hubs] 계정 대상 [!DNL Platform].

에 로그인합니다. [Adobe Experience Platform](https://platform.adobe.com) 그런 다음 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 **[!UICONTROL 소스]** 작업 공간. 다음 **[!UICONTROL 카탈로그]** 탭에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 **[!UICONTROL 클라우드 스토리지]** 카테고리, 선택 **[!UICONTROL Azure 이벤트 허브]**. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**. 그렇지 않으면 을 선택합니다. **[!UICONTROL 데이터 추가]** 새 이벤트 허브 커넥터를 만들려면

![](../../../../images/tutorials/create/eventhub/catalog.png)

다음 **[!UICONTROL Azure 이벤트 허브에 연결]** 대화 상자가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL Event Hubs] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL Connect]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![](../../../../images/tutorials/create/eventhub/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL Event Hubs] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../../../images/tutorials/create/eventhub/existing.png)

## 다음 단계

이 자습서에 따르면 [!DNL Event Hubs] 계정 대상 [!DNL Platform]. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 구성하여 클라우드 스토리지에서 로 데이터를 가져옵니다. [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
