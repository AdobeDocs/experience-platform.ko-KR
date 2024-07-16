---
title: UI에서 Chatlio Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Chatlio 소스 연결을 만드는 방법을 알아봅니다.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 1%

---

# UI에서 [!DNL Chatlio] 소스 연결 만들기

>[!NOTE]
>
>[!DNL Chatlio] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL Chatlio] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기 {#getting-started}

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 전제 조건 {#prerequisites}

다음 섹션에서는 [!DNL Chatlio] 원본 연결을 만들기 전에 완료해야 하는 필수 구성 요소에 대해 설명합니다.

### [!DNL Chatlio]에 대한 소스 스키마를 정의하는 샘플 JSON {#prerequisites-json-schema}

[!DNL Chatlio] 원본 연결을 만들기 전에 원본 스키마를 제공해야 합니다. 아래 JSON을 사용할 수 있습니다.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### [!DNL Chatlio]에 대한 플랫폼 스키마 만들기 {#create-platform-schema}

또한 소스에 사용할 Platform 스키마를 생성해야 합니다. 스키마를 만드는 방법에 대한 포괄적인 단계를 보려면 [플랫폼 스키마 만들기](../../../../../xdm/schema/composition.md)에 대한 자습서를 참조하십시오.

![Chatlio에 대한 예제 스키마를 표시하는 플랫폼 UI](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## [!DNL Chatlio] 계정 연결 {#connect-account}

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스하고 Experience Platform에서 사용할 수 있는 소스 카탈로그를 확인합니다.

*[!UICONTROL 범주]* 메뉴를 사용하여 범주별로 원본을 필터링하세요. 또는 검색 막대에 소스 이름을 입력하여 카탈로그에서 특정 소스를 찾습니다.

[!UICONTROL 마케팅 자동화] 범주로 이동하여 [!DNL Chatlio] 원본 카드를 확인합니다. 시작하려면 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하세요.

![Chatlio 카드가 있는 Platform UI 카탈로그](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## 데이터 선택 {#select-data}

플랫폼으로 가져올 데이터를 선택할 수 있는 인터페이스를 제공하는 **[!UICONTROL 데이터 선택]** 단계가 나타납니다.

* 인터페이스의 왼쪽 부분은 계정 내에서 사용 가능한 데이터 스트림을 볼 수 있는 브라우저입니다.
* 인터페이스의 오른쪽 부분에서 JSON 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

로컬 시스템에서 JSON 파일을 업로드하려면 **[!UICONTROL 파일 업로드]**&#x200B;를 선택하십시오. 또는 업로드할 JSON 파일을 [!UICONTROL 파일 끌어다 놓기] 패널로 끌어다 놓을 수 있습니다.

![원본 워크플로의 데이터 추가 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

파일이 업로드되면 미리보기 인터페이스가 업데이트되어 업로드한 스키마의 미리보기가 표시됩니다. 미리보기 인터페이스를 사용하여 파일의 내용과 구조를 검사할 수 있습니다. [!UICONTROL 검색 필드] 유틸리티를 사용하여 스키마 내의 특정 항목에 액세스할 수도 있습니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![원본 워크플로의 미리 보기 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## 데이터 흐름 세부 정보 {#dataflow-detail}

**데이터 흐름 세부 정보** 단계가 표시되어 기존 데이터 집합을 사용하거나 데이터 흐름의 새 데이터 집합을 설정하는 옵션을 제공하고 데이터 흐름의 이름과 설명을 제공할 수 있습니다. 이 단계에서는 프로필 수집, 오류 진단, 부분 수집 및 경고에 대한 설정을 구성할 수도 있습니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![원본 워크플로의 데이터 흐름 세부 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## 매핑 {#mapping}

소스 스키마의 소스 필드를 대상 스키마의 해당 대상 XDM 필드에 매핑할 수 있는 인터페이스를 제공하는 [!UICONTROL 매핑] 단계가 나타납니다.

Platform은 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md)를 참조하십시오.

아래 나열된 매핑은 필수이며 [!UICONTROL 검토] 단계로 진행하기 전에 설정해야 합니다.

| 대상 필드 | 설명 |
| --- | --- |
| `UUID` | 이벤트의 [!DNL Chatlio] 식별자입니다. |

원본 데이터가 성공적으로 매핑되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![원본 워크플로의 매핑 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## 검토 {#review}

새 데이터 흐름을 만들기 전에 검토할 수 있는 **[!UICONTROL 검토]** 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 원본 형식, 선택한 원본 파일의 관련 경로 및 해당 원본 파일에 있는 열의 양을 표시합니다.
* **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 데이터 집합이 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 집합을 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 선택하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![원본 워크플로의 검토 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## 스트리밍 끝점 URL 가져오기 {#get-streaming-endpoint-url}

스트리밍 데이터 흐름이 만들어지면 이제 스트리밍 끝점 URL을 검색할 수 있습니다. 이 끝점은 Webhook에 가입하는 데 사용되며 스트리밍 소스에서 Experience Platform과 통신할 수 있습니다.

[!DNL Chatlio]에서 Webhook를 구성하는 데 사용되는 URL을 만들려면 다음을 검색해야 합니다.

* **[!UICONTROL 데이터 흐름 ID]**
* **[!UICONTROL 스트리밍 끝점]**

**[!UICONTROL 데이터 흐름 ID]** 및 **[!UICONTROL 스트리밍 끝점]**&#x200B;을 검색하려면 방금 만든 데이터 흐름의 [!UICONTROL 데이터 흐름 활동] 페이지로 이동하여 [!UICONTROL 속성] 패널 아래쪽에서 세부 정보를 복사합니다.

![데이터 흐름 활동의 스트리밍 끝점입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

스트리밍 끝점 및 데이터 흐름 ID를 검색한 후에는 ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}``` 패턴을 기반으로 URL을 빌드합니다. 예를 들어 구성된 웹후크 URL의 형태는 다음과 같습니다. ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## [!DNL Chatlio]에서 웹후크 설정 {#set-up-webhook}

웹후크 URL이 생성되면 이제 [!DNL Chatlio] 사용자 인터페이스를 사용하여 웹후크를 설정할 수 있습니다.

[[!DNL Chatlio]](https://chatlio.com/) 계정에 로그인하고 [설정 및 설치에 대한 안내서](https://chatlio.com/docs/setup/)를 따라 위젯을 만듭니다.

위젯이 생성되면 위젯의 설정 페이지로 이동하여 해당 위젯에 Webhook URL을 추가합니다.

![Chatlio의 웹후크 설정 페이지입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

그런 다음 **[!DNL Behavior]** 탭을 선택하고 *[!DNL Webhook when a new conversation starts]* 필드 및 구독하려는 다른 웹후크 이벤트 필드에 웹후크 URL을 추가합니다.

![Webhook 끝점 필드를 표시하는 Chatlio UI입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>[!DNL Chatlio] 웹후크에 대해 다양한 이벤트를 구독할 수 있습니다. 다른 이벤트에 대한 자세한 내용은 [[!DNL Chatlio] 이벤트 설명서](https://chatlio.com/docs/webhooks/)를 참조하세요.

## 다음 단계 {#next-steps}

이 자습서를 따라 [!DNL Chatlio] 데이터를 Experience Platform 상태로 전환하기 위한 스트리밍 데이터 흐름을 구성했습니다. 수집 중인 데이터를 모니터링하려면 [플랫폼 UI를 사용하여 스트리밍 데이터 흐름 모니터링](../../monitor-streaming.md)에 대한 안내서를 참조하세요.

## 추가 리소스 {#additional-resources}

아래 섹션에서는 [!DNL Chatlio] 소스를 사용할 때 참조할 수 있는 추가 리소스를 제공합니다.

### 유효성 검사 {#validation}

원본을 올바르게 설정했는지 확인하고 [!DNL Chatlio]개의 메시지가 수집되고 있는지 확인하려면 아래 단계를 수행하십시오.

* [!DNL Chatlio] **[!UICONTROL 보고서]** > **[!UICONTROL 채팅 기록]** 페이지에서 [!DNL Chatlio]이(가) 캡처하는 이벤트를 확인할 수 있습니다.

![채팅 내역을 표시하는 Chatlio UI 스크린샷](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Platform UI에서 소스 카탈로그의 [!DNL Chatlio] 카드 메뉴 옆에 있는 **[!UICONTROL 데이터 흐름 보기]**&#x200B;를 선택합니다. 그런 다음 **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 선택하여 [!DNL Chatlio] 내에 구성한 웹후크에 대해 수집된 데이터를 확인합니다.

![수집된 이벤트를 보여주는 플랫폼 UI 스크린샷](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

[!DNL Chatlio]에 대한 자세한 내용은 [[!DNL Chatlio] 설명서](https://chatlio.com/docs/) 및 [FAQ](https://chatlio.com/pricing/#FAQ)를 참조하세요.
