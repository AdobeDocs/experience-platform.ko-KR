---
title: UI에서 Chatlio 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Chatlio 소스 연결을 만드는 방법을 알아봅니다.
badge: "Beta"
source-git-commit: 4a2ed14a55736a9dde1adbb8c7996a5659216ec8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 1%

---

# 만들기 [!DNL Chatlio] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL Chatlio] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Chatlio] Adobe Experience Platform 사용자 인터페이스를 사용한 소스 연결.

## 시작하기 {#getting-started}

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 전제 조건 {#prerequisites}

다음 섹션에서는 만들기 전에 완료해야 하는 사전 요구 사항에 대해 설명합니다 [!DNL Chatlio] 소스 연결.

### 소스 스키마를 정의하기 위한 샘플 JSON [!DNL Chatlio] {#prerequisites-json-schema}

만들기 전 [!DNL Chatlio] 소스 연결을 사용하려면 소스 스키마를 제공해야 합니다. 아래에서 JSON을 사용할 수 있습니다.

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

### 용 플랫폼 스키마 만들기 [!DNL Chatlio] {#create-platform-schema}

또한 소스에 사용할 플랫폼 스키마를 만들어야 합니다. 에서 자습서 읽기 [플랫폼 스키마 만들기](../../../../../xdm/schema/composition.md) 를 참조하십시오.

![Chatlio에 대한 예제 스키마를 보여주는 Platform UI](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## 연결 [!DNL Chatlio] account {#connect-account}

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간 및 Experience Platform에서 사용할 수 있는 소스 카탈로그를 참조하십시오.

를 사용하십시오 *[!UICONTROL 카테고리]* 메뉴를 사용하여 범주별로 소스를 필터링합니다. 또는 검색 막대에 소스 이름을 입력하여 카탈로그에서 특정 소스를 찾습니다.

로 이동합니다. [!UICONTROL 마케팅 자동화] 카테고리를 클릭하여 [!DNL Chatlio] 소스 카드. 시작하려면 다음을 선택합니다 **[!UICONTROL 데이터 추가]**.

![Chatlio 카드가 있는 Platform UI 카탈로그](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## 데이터 선택 {#select-data}

다음 **[!UICONTROL 데이터 선택]** Platform으로 가져올 데이터를 선택할 수 있는 인터페이스를 제공하는 단계가 나타납니다.

* 인터페이스 왼쪽 부분은 계정 내에서 사용 가능한 데이터 스트림을 볼 수 있는 브라우저입니다.
* 인터페이스의 오른쪽 부분에서 JSON 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

선택 **[!UICONTROL 파일 업로드]** 를 눌러 로컬 시스템에서 JSON 파일을 업로드합니다. 또는 업로드할 JSON 파일을 [!UICONTROL 파일 드래그 앤 드롭] 패널.

![소스 워크플로우의 데이터 추가 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

파일이 업로드되면 미리 보기 인터페이스가 업데이트되어 업로드한 스키마 미리 보기가 표시됩니다. 미리 보기 인터페이스를 사용하면 파일의 내용 및 구조를 검사할 수 있습니다. 를 사용할 수도 있습니다 [!UICONTROL 검색 필드] 스키마 내에서 특정 항목에 액세스할 수 있는 유틸리티입니다.

완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![소스 워크플로우의 미리 보기 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## 데이터 흐름 세부 정보 {#dataflow-detail}

다음 **데이터 흐름 세부 정보** 기존 데이터 집합을 사용하거나 데이터 집합에 대한 새 데이터 집합을 설정할 수 있는 옵션과 데이터 집합에 대한 이름 및 설명을 제공할 수 있는 단계가 나타납니다. 이 단계 동안 프로필 수집, 오류 진단, 부분 수집 및 경고에 대한 설정을 구성할 수도 있습니다.

완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![소스 워크플로우의 데이터 흐름 세부 사항 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## 매핑 {#mapping}

다음 [!UICONTROL 매핑] 소스 스키마의 소스 필드를 대상 스키마의 적절한 대상 XDM 필드에 매핑하는 인터페이스를 제공하는 단계가 나타납니다.

플랫폼은 선택한 대상 스키마나 데이터 세트를 기반으로 자동 매핑 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산 또는 계산된 값을 도출할 수 있습니다. 매퍼 인터페이스 및 계산된 필드를 사용하는 방법에 대한 포괄적인 단계는 다음을 참조하십시오 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md).

아래 나열된 매핑은 필수 항목이며, [!UICONTROL 검토] 단계.

| Target 필드 | 설명 |
| --- | --- |
| `UUID` | 다음 [!DNL Chatlio] 이벤트의 식별자입니다. |

소스 데이터가 매핑되면 을 선택합니다 **[!UICONTROL 다음]**.

![소스 워크플로우의 매핑 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## 검토 {#review}

다음 **[!UICONTROL 검토]** 새 데이터 흐름을 만들기 전에 검토할 수 있는 단계가 나타납니다. 세부 사항은 다음 범주 내에 그룹화됩니다.

* **[!UICONTROL 연결]**: 소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 양을 표시합니다.
* **[!UICONTROL 데이터 세트 및 맵 필드 할당]**: 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 세트를 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]** 데이터 흐름을 만들 시간을 허용합니다.

![소스 워크플로우의 검토 단계입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## 스트리밍 끝점 URL 가져오기 {#get-streaming-endpoint-url}

이제 스트리밍 데이터 흐름을 만든 다음 스트리밍 끝점 URL을 검색할 수 있습니다. 이 종단점은 웹 후크에 가입하는 데 사용되며 스트리밍 소스가 Experience Platform과 통신할 수 있도록 합니다.

웹 후크를 구성하는 데 사용되는 URL을 구성하려면 [!DNL Chatlio] 다음을 검색해야 합니다.

* **[!UICONTROL 데이터 흐름 ID]**
* **[!UICONTROL 스트리밍 끝점]**

를 검색하려면 **[!UICONTROL 데이터 흐름 ID]** 및 **[!UICONTROL 스트리밍 끝점]**&#x200B;로 이동합니다. [!UICONTROL 데이터 흐름 활동] 방금 만든 데이터 흐름 페이지의 맨 아래에서 세부 사항을 복사하고 복사합니다 [!UICONTROL 속성] 패널.

![데이터 흐름 활동의 스트리밍 끝점입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

스트리밍 종단점 및 데이터 흐름 ID를 검색한 후에는 다음 패턴을 기반으로 URL을 빌드합니다. ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. 예를 들어 만들어진 웹 후크 URL은 다음과 같을 수 있습니다. ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## 에서 웹 후크 설정 [!DNL Chatlio] {#set-up-webhook}

이제 웹 후크 URL을 만들어 [!DNL Chatlio] 사용자 인터페이스.

에 로그인합니다. [[!DNL Chatlio]](https://chatlio.com/) 계정 및 팔로우 [설치 및 설치에 대한 안내서](https://chatlio.com/docs/setup/) 위젯을 만들려면

위젯이 만들어지면 위젯의 설정 페이지로 이동하여 해당 위젯에 웹 후크 URL을 추가합니다.

![Chatlio의 웹 후크 설정 페이지입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

다음으로, **[!DNL Behavior]** 탭하여 웹 후크 URL을 *[!DNL Webhook when a new conversation starts]* 구독하려는 필드 및 기타 webhook 이벤트 필드.

![웹 후크 끝점 필드를 표시하는 Chatlio UI입니다.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>을 위해 다양한 이벤트에 가입할 수 있습니다 [!DNL Chatlio] 웹 후크 다른 이벤트에 대한 자세한 내용은 [[!DNL Chatlio] 이벤트 설명서](https://chatlio.com/docs/webhooks/).

## 다음 단계 {#next-steps}

이 자습서를 따라 스트리밍 데이터 흐름을 구성하여 [!DNL Chatlio] Experience Platform 데이터. 수집되는 데이터를 모니터링하려면 다음 안내서를 참조하십시오 [플랫폼 UI를 사용하여 스트리밍 데이터 흐름 모니터링](../../monitor-streaming.md).

## 추가 리소스 {#additional-resources}

아래 섹션에서는 를 사용할 때 참조할 수 있는 추가 리소스를 제공합니다. [!DNL Chatlio] 소스.

### 유효성 검사 {#validation}

소스 및 [!DNL Chatlio] 메시지를 수집하는 중입니다. 아래 단계를 수행하십시오.

* 확인할 수 있습니다 [!DNL Chatlio] **[!UICONTROL 보고서]** > **[!UICONTROL 채팅 내역]** 페이지에 캡처되는 이벤트를 식별합니다. [!DNL Chatlio].

![채팅 내역을 보여주는 Chatlio UI 스크린샷](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* 플랫폼 UI에서 **[!UICONTROL 데이터 흐름 보기]** 옆에 [!DNL Chatlio] 소스 카탈로그의 카드 메뉴. 다음 을 선택합니다. **[!UICONTROL 데이터 세트 미리 보기]** 에서 구성한 웹 후크에 대해 수집된 데이터를 확인하려면 [!DNL Chatlio].

![수집된 이벤트를 보여주는 Platform UI 스크린샷](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

에 대한 추가 정보 [!DNL Chatlio]를 방문하면 [[!DNL Chatlio] 설명서](https://chatlio.com/docs/) 및 [FAQ](https://chatlio.com/pricing/#FAQ).