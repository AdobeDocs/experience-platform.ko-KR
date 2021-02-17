---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결 만들기;ui 안내서;자습서;스트리밍 연결 만들기;스트리밍 통합;통합;;home;popular topics;streaming connection;tutorial;streaming connection;streaming ingestion;
solution: Experience Platform
title: UI를 사용하여 스트리밍 연결 만들기
topic: tutorial
type: Tutorial
description: 이 UI 가이드는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# UI를 사용하여 스트리밍 연결 만들기

이 UI 가이드는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 스트리밍 연결 만들기

[!DNL Experience Platform] UI에 로그인한 후 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 **[!UICONTROL 소스]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL 스트리밍]** 범주에서 **[!UICONTROL HTTP API]**&#x200B;를 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**&#x200B;을 선택합니다. 그렇지 않은 경우 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 새 HTTP 스트리밍 커넥터를 만듭니다.

![](../../../../images/tutorials/create/http/catalog.png)

**[!UICONTROL Connect HTTP API 계정]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 계정 이름과 선택적 설명을 입력합니다. 다음 구성 속성을 제공하는 옵션도 제공됩니다.

- **[!UICONTROL 인증]:** 이 속성은 스트리밍 연결에 인증이 필요한지 여부를 결정합니다. 인증을 통해 신뢰할 수 있는 소스에서 데이터를 수집할 수 있습니다. PII(개인 식별 정보)를 취급하는 경우 이 속성을 설정해야 합니다. 기본적으로 이 속성은 꺼져 있습니다.
- **[!UICONTROL XDM 스키마 호환성]:** 이 속성은 이 스트리밍 연결이 XDM 스키마와 호환되는 이벤트를 전송할지 여부를 나타냅니다. 기본적으로 이 속성은 켜져 있습니다.

완료되면 **[!UICONTROL 소스 연결]**&#x200B;을 선택하고 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/create/http/new-account.png)

### 기존 계정

기존 자격 증명을 사용하여 연결하려면 사용할 HTTP API 연결을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속 진행합니다.

![](../../../../images/tutorials/create/http/existing-account.png)

## 데이터 선택

HTTP API 연결을 만든 후 연결할 데이터 세트를 선택할 수 있는 인터페이스를 제공하는 **[!UICONTROL 데이터 선택]** 단계가 나타납니다. 새 데이터 세트를 만들거나 기존 데이터 세트에 연결할 수 있습니다.

### 새 데이터 세트 만들기

새 데이터 집합을 만들려면 **[!UICONTROL 새 데이터 집합]**&#x200B;을 선택합니다. 표시되는 양식에서 데이터 세트에 대한 대상 스키마는 물론 이름, 선택적 설명을 제공합니다. 프로필 사용 스키마를 선택하는 경우 데이터 집합도 프로필 사용 가능 여부를 선택할 수 있습니다.

![](../../../../images/tutorials/create/http/new-dataset.png)

### 기존 데이터 세트 사용

기존 데이터 집합을 사용하려면 **[!UICONTROL 기존 데이터 집합]**&#x200B;을 선택합니다. 나타나는 양식에서 사용할 데이터 세트를 선택합니다. 데이터 세트를 선택하고 나면 데이터 세트에 대해 프로필 사용 여부를 선택할 수 있습니다.

![](../../../../images/tutorials/create/http/existing-dataset.png)

## 데이터 흐름 세부 정보

**[!UICONTROL 데이터 흐름 세부 정보]** 단계가 나타납니다. 이 페이지에서 이름 및 선택적 설명을 지정하여 만든 데이터 플로우에 대한 세부 정보를 제공할 수 있습니다.

데이터 흐름에 대한 세부 정보를 제공한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## 리뷰

데이터 흐름을 만들기 전에 데이터 흐름 세부 정보를 검토할 수 있도록 **[!UICONTROL 검토]** 단계가 표시됩니다. 세부 사항은 다음 카테고리 내에 있는 그룹입니다.

- **[!UICONTROL 연결]**:계정 이름, 소스 플랫폼 및 소스 이름을 표시합니다.
- **[!UICONTROL 데이터 세트 및 맵 필드 할당]**:데이터 세트가 준수하는 대상 데이터 세트와 스키마를 표시합니다.

세부 사항이 올바른지 확인한 후 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

![](../../../../images/tutorials/create/http/review.png)

## 스트리밍 끝점 URL 가져오기

연결이 생성되면 소스 세부 정보 페이지가 나타납니다. 이 페이지에는 이전에 실행한 데이터 흐름, ID 및 스트리밍 끝점 URL을 비롯하여 새로 만든 연결에 대한 세부 정보가 표시됩니다.

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## 다음 단계

이 자습서를 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 다양한 [!DNL Data Ingestion] API에 액세스할 수 있습니다. API에서 스트리밍 연결을 만들기 위한 지침은 [스트리밍 연결 자습서](../../../api/create/streaming/http.md)를 참조하십시오.

데이터를 플랫폼으로 스트리밍하는 방법을 알아보려면 [스트리밍 시간 시리즈 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md)에 대한 자습서 또는 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md)에 대한 자습서를 읽으십시오.
