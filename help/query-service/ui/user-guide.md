---
keywords: Experience Platform;홈;인기 항목;쿼리 편집기;쿼리 편집기;쿼리 서비스;쿼리 서비스;
solution: Experience Platform
title: 쿼리 편집기 UI 안내서
topic-legacy: query editor
description: 쿼리 편집기는 Adobe Experience Platform 쿼리 서비스에서 제공하는 대화형 도구로서 Experience Platform 사용자 인터페이스 내에서 고객 경험 데이터에 대한 쿼리를 작성, 유효성 검사 및 실행할 수 있습니다. 쿼리 편집기는 분석 및 데이터 탐색을 위한 쿼리 개발을 지원하며, Experience Platform에서 데이터 세트를 채우기 위해 비대화형 쿼리는 물론 개발 목적으로 대화형 쿼리를 실행할 수 있도록 해줍니다.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: aa61cb696d647c5f039283ce5926d5fa1e901a13
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 1%

---

# [!DNL Query Editor] UI 안내서

[!DNL Query Editor] 은 Adobe Experience Platform에서 제공하는 대화형 도구입니다 [!DNL Query Service]: 내에서 고객 경험 데이터에 대한 쿼리를 작성, 유효성 검사 및 실행할 수 있습니다 [!DNL Experience Platform] 사용자 인터페이스. [!DNL Query Editor] 은 분석 및 데이터 탐색을 위한 쿼리 개발을 지원하며, 개발 목적으로 대화형 쿼리를 실행할 수 있을 뿐만 아니라 의 데이터 세트를 채울 비대화형 쿼리를 사용할 수 있습니다. [!DNL Experience Platform].

의 개념 및 기능에 대한 자세한 내용 [!DNL Query Service]를 참조하고 [쿼리 서비스 개요](../home.md). Query Service 사용자 인터페이스를 탐색하는 방법에 대해 자세히 알아보려면 [!DNL Platform]를 참조하고 [Query Service UI 개요](./overview.md).

## 시작하기 {#getting-started}

[!DNL Query Editor] 에서는 을 연결하여 유연한 쿼리 실행 기능을 제공합니다 [!DNL Query Service], 및 쿼리는 이 연결이 활성화된 동안에만 실행됩니다.

### 연결 대상 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 를 초기화하고 연결하는 데 몇 초 걸립니다. [!DNL Query Service] 열려 있을 때 콘솔은 아래와 같이 언제 연결되는지 알려줍니다. 편집기가 연결되기 전에 쿼리를 실행하려고 하면 연결이 완료될 때까지 실행이 지연됩니다.

![이미지](../images/ui/query-editor/connect.png)

### 쿼리 실행 방법 [!DNL Query Editor] {#run-a-query}

다음에서 실행된 쿼리 [!DNL Query Editor] 대화식으로 실행. 즉, 브라우저를 닫거나 다른 곳으로 이동하는 경우 쿼리가 취소됩니다. 쿼리 출력에서 데이터 세트를 생성하기 위한 쿼리에도 적용됩니다.

## 을 사용하여 쿼리 작성 [!DNL Query Editor] {#query-authoring}

사용 [!DNL Query Editor], 고객 경험 데이터에 대한 쿼리를 작성, 실행 및 저장할 수 있습니다. 실행 또는 저장된 모든 쿼리 [!DNL Query Editor] 조직의 모든 사용자가 [!DNL Query Service].

### [!DNL Query Editor]에 액세스  {#accessing-query-editor}

에서 [!DNL Experience Platform] UI, 선택 **[!UICONTROL 쿼리]** 왼쪽 탐색 메뉴에서 를 클릭하여 [!DNL Query Service] 작업 공간. 다음 을 선택합니다. **[!UICONTROL 쿼리 만들기]** 화면 오른쪽 상단에서 쿼리 작성을 시작합니다. 이 링크는 [!DNL Query Service] 작업 공간.

![이미지](../images/ui/query-editor/create-query.png)

### 쿼리 쓰기 {#writing-queries}

[!UICONTROL 쿼리 편집기] 는 가능한 한 쉽게 쓰기 쿼리를 만들도록 구성됩니다. 아래 스크린샷은 편집기가 UI에 와 **재생** 단추 및 SQL 항목 필드가 강조 표시되어 있습니다.

![이미지](../images/ui/query-editor/editor.png)

개발 시간을 최소화하려면 반환된 행에 제한이 있는 쿼리를 개발하는 것이 좋습니다. 예, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. 쿼리에서 예상 출력을 생성하는지 확인한 후 제한을 제거하고 쿼리를 `CREATE TABLE tablename AS SELECT` 를 입력하여 해당 출력으로 데이터 세트를 생성합니다.

### 쓰기 도구 [!DNL Query Editor] {#writing-tools}

- **자동 구문 강조 표시:** SQL을 보다 쉽게 읽고 구성할 수 있습니다.

![이미지](../images/ui/query-editor/syntax-highlight.png)

- **SQL 키워드 자동 완료:** 쿼리 입력을 시작한 다음 화살표 키를 사용하여 원하는 용어로 이동한 다음 키를 누릅니다 **Enter 키**.

![이미지](../images/ui/query-editor/syntax-auto.png)

- **테이블 및 필드 자동 완료:** 원하는 테이블 이름 입력 시작 `SELECT` 에서 화살표 키를 사용하여 원하는 테이블로 이동한 다음 키를 누릅니다 **Enter 키**. 테이블을 선택하면 자동 완성 기능이 해당 테이블의 필드를 인식합니다.

![이미지](../images/ui/query-editor/tables-auto.png)

### 오류 감지 {#error-detection}

[!DNL Query Editor] 작성할 때 자동으로 쿼리의 유효성을 검사하여 일반 SQL 유효성 검사 및 특정 실행 유효성 검사를 제공합니다. 쿼리 아래에 빨간색 밑줄이 나타나면(아래 이미지에 표시) 쿼리 내의 오류를 나타냅니다.

![이미지](../images/ui/query-editor/syntax-error-highlight.png)

오류가 감지되면 SQL 코드를 마우스로 가리키면 특정 오류 메시지를 볼 수 있습니다.

![이미지](../images/ui/query-editor/linting-error.png)

### 쿼리 세부 사항 {#query-details}

에서 쿼리를 보는 동안 [!DNL Query Editor], **[!UICONTROL 쿼리 세부 정보]** 패널에서는 선택한 쿼리를 관리하는 도구를 제공합니다.

![이미지](../images/ui/query-editor/query-details.png)

이 패널을 사용하면 UI에서 직접 출력 데이터 세트를 생성하고, 표시된 쿼리를 삭제하거나 이름을 지정하고, 쿼리에 예약을 추가할 수 있습니다.

또한 이 패널에는 마지막으로 쿼리를 수정한 시간과 쿼리를 수정한 사람(해당하는 경우)과 같은 유용한 메타데이터도 표시됩니다. 데이터 세트를 생성하려면 다음을 선택합니다 **[!UICONTROL 출력 데이터 세트]**. 다음 **[!UICONTROL 출력 데이터 세트]** 대화 상자가 나타납니다. 이름과 설명을 입력한 다음 **[!UICONTROL 쿼리 실행]**. 새 데이터 세트는 **[!UICONTROL 데이터 세트]** 탭에서 다음을 수행합니다. [!DNL Query Service] 사용자 인터페이스 [!DNL Platform].

### 예약된 쿼리 {#scheduled-queries}

>[!IMPORTANT]
>
>다음은 쿼리 편집기를 사용할 때 예약된 쿼리에 대한 제한 사항 목록입니다. 에는 적용되지 않습니다 [!DNL Query Service] API:<br/>이미 생성, 저장 및 실행된 쿼리에 예약만 추가할 수 있습니다.<br/>사용자 **사용할 수 없음** 매개 변수가 있는 쿼리에 일정을 추가합니다.<br/>예약된 쿼리 **사용할 수 없음** 익명 블록을 포함합니다.

쿼리에 예약을 추가하려면 **[!UICONTROL 예약 추가]**.

![이미지](../images/ui/query-editor/add-schedule.png)

다음 **[!UICONTROL 예약 세부 사항]** 페이지가 나타납니다. 이 페이지에서 예약된 쿼리의 빈도, 예약된 쿼리가 실행될 날짜 및 쿼리를 내보낼 데이터 세트를 선택할 수 있습니다.

![이미지](../images/ui/query-editor/schedule-details.png)

다음 옵션을 선택할 수 있습니다 **[!UICONTROL 빈도]**:

- **[!UICONTROL 시간별]**: 선택한 날짜 기간에 대해 매시간마다 예약된 쿼리가 실행됩니다.
- **[!UICONTROL 일별]**: 예약된 쿼리는 선택한 시간 및 기간에 X일마다 실행됩니다. 선택한 시간이 다음과 같습니다 **UTC**&#x200B;를 설정하는 것이 좋습니다.
- **[!UICONTROL 주별]**: 선택한 쿼리는 선택한 요일, 시간 및 기간에 실행됩니다. 선택한 시간이 다음과 같습니다 **UTC**&#x200B;를 설정하는 것이 좋습니다.
- **[!UICONTROL 월별]**: 선택한 쿼리는 선택한 일, 시간 및 기간에 매달 실행됩니다. 선택한 시간이 다음과 같습니다 **UTC**&#x200B;를 설정하는 것이 좋습니다.
- **[!UICONTROL 연간]**: 선택한 쿼리는 선택한 일, 월, 시간 및 기간에 매년 실행됩니다. 선택한 시간이 다음과 같습니다 **UTC**&#x200B;를 설정하는 것이 좋습니다.

데이터 세트에 대해 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있는 옵션이 있습니다.

>[!IMPORTANT]
>
> 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들려면 다음을 수행합니다 **not** 다음 중 하나를 포함해야 합니다. `INSERT INTO` 또는 `CREATE TABLE AS SELECT` 데이터 세트가 이미 설정되어 있으므로 쿼리의 일부로 사용됩니다. 다음 중 하나를 포함합니다 `INSERT INTO` 또는 `CREATE TABLE AS SELECT` 예약된 쿼리의 일부로 인해 오류가 발생합니다.

이러한 세부 사항을 모두 확인한 후 **[!UICONTROL 저장]** 일정을 만들려면

쿼리 세부 정보 페이지가 다시 나타나고 이제 예약 ID, 예약 자체 및 예약의 출력 데이터 세트를 포함하여 새로 만든 예약의 세부 정보가 표시됩니다. 예약 ID를 사용하여 예약된 쿼리 자체의 실행에 대한 자세한 정보를 조회할 수 있습니다. 자세한 내용은 [예약된 쿼리 실행 끝점 안내서](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> 예약만 수행할 수 있습니다 **하나** UI를 사용하여 쿼리 템플릿. 쿼리 템플릿에 예약을 더 추가하려면 API를 사용해야 합니다. API를 사용하여 이미 일정을 추가한 경우 다음을 수행합니다. **not** ui를 사용하여 추가 일정을 추가할 수 있습니다. 여러 개의 일정이 이미 쿼리 템플릿에 첨부된 경우 가장 오래된 일정만 표시됩니다. API를 사용하여 일정을 추가하는 방법에 대해 알아보려면 [예약된 쿼리 엔드포인트 가이드](../api/scheduled-queries.md).
>
> 또한 보고 있는 예약에 대한 최신 상태가 있는지 확인하려면 페이지를 새로 고쳐야 합니다.

#### 일정 삭제 {#delete-schedule}

일정을 선택하여 삭제할 수 있습니다 **[!UICONTROL 일정 삭제]**.

![이미지](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> 쿼리의 예약을 삭제하려면 먼저 스케줄을 비활성화해야 합니다.

### 쿼리 저장 {#saving-queries}

[!DNL Query Editor] 은 쿼리를 저장하고 나중에 작업할 수 있는 저장 함수를 제공합니다. 쿼리를 저장하려면 **[!UICONTROL 저장]** 의 오른쪽 상단 모서리에서 [!DNL Query Editor]. 쿼리를 저장하려면 먼저 **[!UICONTROL 쿼리 세부 정보]** 패널.

### 이전 쿼리를 찾는 방법 {#previous-queries}

에서 실행된 모든 쿼리 [!DNL Query Editor] 로그 테이블에서 캡처됩니다. 에서 검색 기능을 사용할 수 있습니다 **[!UICONTROL 로그]** 탭을 클릭하여 쿼리 실행을 찾습니다. 저장된 쿼리는 **[!UICONTROL 찾아보기]** 탭.

자세한 내용은 [Query Service UI 개요](./overview.md) 추가 정보.

>[!NOTE]
>
>실행되지 않는 쿼리는 로그에 저장되지 않습니다. 쿼리를 사용할 수 있도록 하려면 [!DNL Query Service]를 실행해야 합니다. [!DNL Query Editor].

## 쿼리 편집기를 사용하여 쿼리 실행 {#executing-queries}

에서 쿼리를 실행하려면 [!DNL Query Editor]편집기에서 SQL을 입력하거나 **[!UICONTROL 로그]** 또는 **[!UICONTROL 찾아보기]** 탭을 선택하고 **재생**. 쿼리 실행 상태는 **[!UICONTROL 콘솔]** 아래 탭에 출력 데이터가 **[!UICONTROL 결과]** 탭.

### 콘솔 {#console}

콘솔은 의 상태 및 작업에 대한 정보를 제공합니다 [!DNL Query Service]. 콘솔에 연결 상태가 표시됩니다 [!DNL Query Service], 실행 중인 쿼리 작업과 이러한 쿼리에서 발생하는 모든 오류 메시지

![이미지](../images/ui/query-editor/console.png)

>[!NOTE]
>
>콘솔에는 쿼리 실행으로 인한 오류만 표시됩니다. 쿼리를 실행하기 전에 쿼리 유효성 검사 오류가 표시되지 않습니다.

### 쿼리 결과 {#query-results}

쿼리가 완료되면 결과는 **[!UICONTROL 결과]** 탭, 옆에 있습니다. **[!UICONTROL 콘솔]** 탭. 이 보기는 쿼리의 테이블 형식 출력을 보여주며 최대 100개의 행을 표시합니다. 이 보기에서는 쿼리가 예상 출력을 생성하는지 확인할 수 있습니다. 쿼리를 사용하여 데이터 세트를 생성하려면 반환된 행의 제한을 제거하고 `CREATE TABLE tablename AS SELECT` 를 입력하여 해당 출력으로 데이터 세트를 생성합니다. 자세한 내용은 [데이터 세트 생성 자습서](./create-datasets.md) 쿼리에서 데이터 세트를 생성하는 방법에 대한 지침은 [!DNL Query Editor].

![이미지](../images/ui/query-editor/query-results.png)

## 쿼리 실행 [!DNL Query Service] 튜토리얼 비디오 {#query-tutorial-video}

다음 비디오에서는 Adobe Experience Platform 인터페이스와 PSQL 클라이언트에서 쿼리를 실행하는 방법을 보여 줍니다. 또한 XDM 개체에서 개별 속성을 사용하고 Adobe 정의 함수를 사용하고 CREATE TABLE AS SELECT(CTAS)를 사용하는 것이 나와 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 다음 단계

이제 사용 가능한 기능을 알 수 있습니다 [!DNL Query Editor] 응용 프로그램을 탐색하는 방법에서 직접 고유한 쿼리 작성을 시작할 수 있습니다 [!DNL Platform]. 의 데이터 세트에 대해 SQL 쿼리 실행에 대한 자세한 내용은 [!DNL Data Lake]에 대해서는 안내서를 참조하십시오. [쿼리 실행](../best-practices/writing-queries.md).
