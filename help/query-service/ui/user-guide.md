---
keywords: Experience Platform;홈;인기 항목;쿼리 편집기;쿼리 서비스;쿼리 서비스;쿼리 서비스;;home;popular topics;query editor;Query service;query service;
solution: Experience Platform
title: 쿼리 편집기 UI 안내서
topic-legacy: query editor
description: 쿼리 편집기는 Experience Platform 사용자 인터페이스 내에서 고객 경험 데이터에 대한 쿼리를 작성하고 유효성을 확인하고 실행할 수 있는 Adobe Experience Platform 쿼리 서비스에서 제공하는 대화형 도구입니다. 쿼리 편집기는 분석 및 데이터 탐색을 위한 쿼리 개발을 지원하며, Experience Platform에 데이터 세트를 채우는 비대화형 쿼리뿐만 아니라 개발 목적으로 대화형 쿼리를 실행할 수 있습니다.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# [!DNL Query Editor] UI 가이드

[!DNL Query Editor] 는 Adobe Experience Platform에서 제공하는 대화형 도구로서,  [!DNL Query Service]  [!DNL Experience Platform] 사용자 인터페이스 내에서 고객 경험 데이터에 대한 쿼리를 작성, 확인 및 실행할 수 있도록 해줍니다. [!DNL Query Editor] 은 분석 및 데이터 탐색을 위한 쿼리 개발을 지원하며, 개발용으로 대화형 쿼리를 실행하고 상호 작용 기능이 없는 쿼리를 실행하여 데이터 세트를 채울 수 있도록  [!DNL Experience Platform]해줍니다.

[!DNL Query Service]의 개념과 기능에 대한 자세한 내용은 [쿼리 서비스 개요][query-service-overview]를 참조하십시오. [!DNL Platform]에서 쿼리 서비스 사용자 인터페이스를 탐색하는 방법에 대한 자세한 내용은 [쿼리 서비스 UI 개요][query-service-ui]를 참조하십시오.

## 시작하기

[!DNL Query Editor] 에 연결하여 쿼리를 유연하게 실행할 수  [!DNL Query Service]있으며 이 연결이 활성화된 상태에서만 쿼리가 실행됩니다.

### [!DNL Query Service]에 연결 중

[!DNL Query Editor] 초기화하여 열었을  [!DNL Query Service] 때 연결하는 데 몇 초 정도 소요됩니다. 콘솔은 아래와 같이 언제 연결되는지 알려줍니다. 편집기가 연결되기 전에 쿼리를 실행하면 연결이 완료될 때까지 실행이 지연됩니다.

![이미지](../images/queries/query-editor-overview/initializing-connection.png)

### 쿼리가 [!DNL Query Editor]에서 실행되는 방식

[!DNL Query Editor]에서 실행된 쿼리는 대화식으로 실행됩니다. 즉, 브라우저를 닫거나 다른 곳으로 이동하면 쿼리가 취소됩니다. 쿼리 출력에서 데이터 세트를 생성하기 위해 수행된 쿼리에도 적용됩니다.

## [!DNL Query Editor]을(를) 사용하여 쿼리 작성

[!DNL Query Editor]을 사용하여 고객 경험 데이터에 대한 쿼리를 작성하고 실행 및 저장할 수 있습니다. [!DNL Query Editor]에서 실행되거나 저장된 모든 쿼리는 [!DNL Query Service]에 액세스할 수 있는 조직의 모든 사용자가 사용할 수 있습니다.

### [!DNL Query Editor]에 액세스 

[!DNL Experience Platform] UI에서 왼쪽 탐색 메뉴에서 **[!UICONTROL Queries]**&#x200B;을 클릭하여 [!DNL Query Service] 작업 영역을 엽니다. 그런 다음 화면 오른쪽 상단에 있는 **[!UICONTROL Create Query]**&#x200B;을 클릭하여 쿼리 작성을 시작합니다. 이 링크는 [!DNL Query Service] 작업 영역의 모든 페이지에서 사용할 수 있습니다.

![이미지](../images/queries/query-editor-overview/create-query.png)

### 쿼리 쓰기

[!UICONTROL Query Editor] 은 가능한 쉽게 쿼리를 작성하기 위해 구성됩니다. 아래 스크린샷은 **재생** 버튼 및 SQL 입력 필드가 강조 표시된 상태에서 편집기가 UI에 어떻게 표시되는지를 보여줍니다.

![이미지](../images/queries/query-editor-overview/editor.png)

개발 시간을 최소화하려면 반환된 행에 제한이 있는 쿼리를 개발하는 것이 좋습니다. 예, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. 쿼리가 예상 출력을 생성하는지 확인한 후 제한을 제거하고 `CREATE TABLE tablename AS SELECT`으로 쿼리를 실행하여 출력이 있는 데이터 세트를 생성합니다.

### [!DNL Query Editor]에 도구 쓰기

- **자동 구문 강조 표시:** SQL을 보다 손쉽게 읽고 구성할 수 있습니다.

![이미지](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL 키 단어 자동 완성: 쿼리** 를 입력하기 시작한 다음 화살표 키를 사용하여 원하는 용어로 이동한 다음 Enter 키를  **누릅니다**.

![이미지](../images/queries/query-editor-overview/syntax-auto.png)

- **테이블 및 필드 자동 완성:** 원하는 테이블 이름 `SELECT` 을 입력하기 시작한 다음 화살표 키를 사용하여 원하는 테이블로 이동한 다음 Enter 키를  **누릅니다**. 테이블을 선택하면 자동 완성 기능에서 해당 테이블의 필드를 인식합니다.

![이미지](../images/queries/query-editor-overview/tables-auto.png)

### 오류 감지

[!DNL Query Editor] 쿼리를 작성할 때 자동으로 유효성을 검사하여 일반 SQL 유효성 검사와 특정 실행 유효성 검사를 제공합니다. 쿼리 아래에 빨간색 밑줄이 나타나면(아래 이미지에 표시됨) 쿼리 내의 오류를 나타냅니다.

![이미지](../images/queries/query-editor-overview/syntax-error-highlight.png)

오류가 감지되면 SQL 코드 위로 마우스를 가져가면 특정 오류 메시지를 볼 수 있습니다.

![이미지](../images/queries/query-editor-overview/linting-error.png)

### 쿼리 세부 사항

[!DNL Query Editor]에서 쿼리를 보는 동안 **[!UICONTROL Query Details]** 패널은 선택한 쿼리를 관리하는 도구를 제공합니다.

![이미지](../images/queries/query-editor-overview/query-details.png)

이 패널에서는 UI에서 직접 출력 데이터 세트를 생성하고, 표시된 쿼리를 삭제하거나 이름을 지정하고, **[!UICONTROL SQL Query]** 탭의 복사 쉬운 형식으로 SQL 코드를 볼 수 있습니다. 또한 이 패널에는 마지막으로 쿼리를 수정한 시간과 쿼리를 수정한 사람(해당하는 경우)과 같은 유용한 메타데이터도 표시됩니다. 데이터 세트를 생성하려면 **[!UICONTROL Output Dataset]**&#x200B;을 클릭합니다. **[!UICONTROL Output Dataset]** 대화 상자가 나타납니다. 이름과 설명을 입력한 다음 **[!UICONTROL Run Query]**&#x200B;을 클릭합니다. 새 데이터 집합은 [!DNL Platform]의 [!DNL Query Service] 사용자 인터페이스의 **[!UICONTROL Datasets]** 탭에 표시됩니다.

### 쿼리 저장

[!DNL Query Editor] 쿼리를 저장하고 나중에 작업할 수 있도록 해주는 저장 함수를 제공합니다. 쿼리를 저장하려면 [!DNL Query Editor] 오른쪽 위 모서리에서 **[!UICONTROL Save]**&#x200B;을 클릭합니다. 쿼리를 저장하려면 먼저 **[!UICONTROL Query Details]** 패널을 사용하여 쿼리에 사용할 이름을 제공해야 합니다.

### 이전 쿼리를 찾는 방법

[!DNL Query Editor]에서 실행된 모든 쿼리는 로그 테이블에서 캡처됩니다. **[!UICONTROL Log]** 탭에서 검색 기능을 사용하여 쿼리 실행을 찾을 수 있습니다. 저장된 쿼리는 **[!UICONTROL Browse]** 탭에 나열됩니다.

자세한 내용은 [쿼리 서비스 UI 개요][query-service-ui]를 참조하십시오.

>[!NOTE]
>
>실행되지 않은 쿼리는 로그에 저장되지 않습니다. 쿼리를 [!DNL Query Service]에서 사용할 수 있으려면 [!DNL Query Editor]에서 실행하거나 저장해야 합니다.

## 쿼리 편집기를 사용하여 쿼리 실행

[!DNL Query Editor]에서 쿼리를 실행하려면 편집기에서 SQL을 입력하거나 **[!UICONTROL Log]** 또는 **[!UICONTROL Browse]** 탭에서 이전 쿼리를 로드한 다음 **재생**&#x200B;을 클릭합니다. 쿼리 실행 상태는 아래의 **[!UICONTROL Console]** 탭에 표시되며 출력 데이터는 **[!UICONTROL Results]** 탭에 표시됩니다.

### 콘솔

콘솔은 [!DNL Query Service]의 상태 및 작업에 대한 정보를 제공합니다. 콘솔에는 [!DNL Query Service]에 대한 연결 상태, 실행 중인 쿼리 작업 및 이러한 쿼리에서 발생한 오류 메시지가 표시됩니다.

![이미지](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>콘솔에는 쿼리 실행으로 인한 오류만 표시됩니다. 쿼리가 실행되기 전에는 쿼리 유효성 검사 오류가 표시되지 않습니다.

### 쿼리 결과

쿼리가 완료되면 결과는 **[!UICONTROL Console]** 탭 옆의 **[!UICONTROL Results]** 탭에 표시됩니다. 이 보기는 최대 100개의 행을 표시하는 쿼리의 테이블 형식 출력을 보여줍니다. 이 보기에서는 쿼리가 예상 출력을 생성하는지 확인할 수 있습니다. 쿼리를 사용하여 데이터 세트를 생성하려면 반환된 행의 제한을 제거하고 `CREATE TABLE tablename AS SELECT`으로 쿼리를 실행하여 출력이 있는 데이터 세트를 생성합니다. [!DNL Query Editor]의 쿼리 결과에서 데이터 세트를 생성하는 방법에 대한 지침은 [데이터 집합 생성 자습서][query-service-create-datasets]를 참조하십시오.

![이미지](../images/queries/query-editor-overview/query-results.png)

## [!DNL Query Service] 자습서 비디오로 쿼리 실행

다음 비디오에서는 Adobe Experience Platform 인터페이스와 PSQL 클라이언트에서 쿼리를 실행하는 방법을 보여 줍니다. 또한 XDM 객체에서 개별 속성을 사용하고, Adobe 정의 함수를 사용하고, CREATE TABLE AS SELECT(CTAS SELECT) 를 사용하는 방법도 표시됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 다음 단계

이제 [!DNL Query Editor]에서 사용할 수 있는 기능과 애플리케이션을 탐색하는 방법을 알고 있으므로 [!DNL Platform]에서 직접 고유한 쿼리를 작성할 수 있습니다. [!DNL Data Lake]에서 데이터 집합에 대한 SQL 쿼리를 실행하는 방법에 대한 자세한 내용은 [쿼리 실행][query-service-running-queries]에 대한 안내서를 참조하십시오.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
