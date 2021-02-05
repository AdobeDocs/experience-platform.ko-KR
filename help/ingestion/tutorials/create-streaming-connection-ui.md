---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결 만들기;ui 안내서;자습서;스트리밍 연결 만들기;스트리밍 통합;통합;;home;popular topics;streaming connection;tutorial;streaming connection;streaming ingestion;
solution: Experience Platform
title: UI를 사용하여 스트리밍 연결 만들기
topic: tutorial
type: Tutorial
description: 이 UI 가이드는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# UI를 사용하여 스트리밍 연결 만들기

이 UI 가이드는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.

## 시작하기

데이터 스트리밍을 [!DNL Experience Platform]에 시작하려면 먼저 스트리밍 HTTP 연결을 만들어야 합니다. 스트리밍 연결을 만들 때 스트리밍 데이터의 소스 및 신뢰할 수 있는(인증된) 소스 또는 신뢰할 수 없는(인증되지 않은) 소스에서 데이터를 전송할지 여부와 같은 주요 세부 정보를 제공해야 합니다.

스트리밍 연결을 등록하고 나면 데이터를 [!DNL Platform]에 스트리밍하는 데 사용할 수 있는 고유한 URL이 있습니다.

이 안내서를 완료하려면 Adobe Experience Platform에 대한 액세스 권한이 있어야 합니다. [!DNL Platform]에 대한 액세스 권한이 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

## 스트리밍 연결 만들기

[!DNL Experience Platform] UI에 로그인한 후 **[!UICONTROL 소스]**&#x200B;를 클릭하여 **[!UICONTROL 카탈로그]** 탭을 엽니다. 이 페이지에는 사용 가능한 소스 유형이 개별 카드로 표시됩니다. 이 카드에는 스트리밍 연결에서 데이터 세트로 생성된 데이터 흐름 수가 표시되는 버블이 들어 있습니다.

![](../images/streaming-ingestion/ui/click-sources.png)

**[!UICONTROL 소스]** 페이지에서 **[!UICONTROL HTTP API]**&#x200B;을 클릭한 다음 **[!UICONTROL Connect 소스]**&#x200B;를 클릭합니다.

![](../images/streaming-ingestion/ui/click-connect-source.png)

**[!UICONTROL HTTP에 연결]** 화면이 나타납니다. **[!UICONTROL 서비스 세부 정보]**&#x200B;에서 새 스트리밍 연결에 대한 이름과 설명을 모두 입력합니다.

**[!UICONTROL 계정 인증]**&#x200B;에서 스트리밍 연결에 대해 다음 구성 속성을 선택합니다.

- **[!UICONTROL 인증]:** 스트리밍 연결에 인증이 필요한지 여부입니다. 인증을 통해 신뢰할 수 있는 소스에서 데이터를 수집할 수 있습니다. PII(개인 식별 정보)를 취급하는 경우 이 기능을 사용하는 것이 좋습니다.
- **[!UICONTROL XDM 스키마 호환성]:** 이 스트리밍 연결이 XDM 스키마와 호환되는 이벤트를 전송할지 여부를 결정합니다. 기본적으로 이 속성은 **on**&#x200B;으로 설정됩니다.

구성 속성 선택이 끝나면 **[!UICONTROL Connect]**&#x200B;를 클릭합니다. 이제 스트리밍 HTTP 연결이 생성되며 이제 **[!UICONTROL 소스]** 작업 영역의 **[!UICONTROL 찾아보기]** 탭 아래에서 볼 수 있습니다.

![](../images/streaming-ingestion/ui/http-sources-details.png)

**[!UICONTROL 찾아보기]** 탭에서 새로 만든 스트리밍 HTTP 연결을 클릭하고 해당 연결의 세부 정보를 볼 수 있습니다.

![](../images/streaming-ingestion/ui/browse-sources.png)

연결 이름의 하이퍼링크를 클릭하면 **[!UICONTROL 데이터 선택]**&#x200B;을 클릭하여 연결된 데이터 세트를 구성하여 표시할 데이터를 선택할 수 있습니다.

![](../images/streaming-ingestion/ui/select-data.png)

[새 데이터 세트](#create-a-new-dataset) 또는 [기존 데이터 세트](#use-an-existing-dataset)를 사용할 수 있습니다.

### 새 데이터 세트 만들기

새 데이터 세트를 만들려면 데이터 세트에 대한 대상 스키마는 물론 이름, 설명을 입력합니다.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

모든 세부 사항을 삽입하고 **[!UICONTROL 다음]**&#x200B;을 클릭하면 **[!UICONTROL 완료]**&#x200B;를 클릭하기 전에 제공된 세부 정보를 검토하여 데이터 세트를 스트리밍 HTTP 연결에 연결할 수 있습니다.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### 기존 데이터 세트 사용

기존 데이터 집합을 사용하려면 **[!UICONTROL 출력 데이터 집합 이름]**&#x200B;을 선택합니다.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

**[!UICONTROL 다음]**&#x200B;을 클릭한 후 **[!UICONTROL 완료]**&#x200B;를 클릭하여 선택한 데이터 집합을 스트리밍 HTTP 연결에 연결할 수 있습니다.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## 다음 단계

이 자습서를 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 다양한 [!DNL Data Ingestion] API에 액세스할 수 있습니다. API에서 스트리밍 연결을 만들기 위한 지침은 [스트리밍 연결 자습서](../tutorials/create-streaming-connection.md)를 참조하십시오.
