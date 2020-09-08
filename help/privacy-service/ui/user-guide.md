---
keywords: Experience Platform;home;popular topics;export;Export
solution: Experience Platform
title: Privacy Service 사용 안내서
topic: UI guide
translation-type: tm+mt
source-git-commit: a09d80f4bacd5d4be77443d75aad278ad89259ef
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---


# [!DNL Privacy Service] 사용 안내서

이 문서에서는 [!DNL Privacy Service] 사용자 인터페이스를 사용하여 개인 정보 요청을 만들고 관리하는 단계를 제공합니다.

## UI [!DNL Privacy Service] 대시보드 찾아보기

UI에 대한 대시보드에서는 개인 정보 작업의 상태를 볼 수 있는 두 개의 [!DNL Privacy Service] 위젯을 제공합니다. **[!UICONTROL 상태 보고서]** 및 **[!UICONTROL 작업 요청]**. 대시보드에는 표시된 작업에 대해 현재 선택된 규칙이 표시됩니다.

![UI 대시보드](../images/user-guide/dashboard.png)

### 규정 유형

[!DNL Privacy Service] 네 가지 규칙 유형에 대한 작업 요청 지원:

* 유럽 연합( [!DNL General Data Protection Regulation] GDPR)
* The [!DNL California Consumer Privacy Act] ([!UICONTROL CPA])
* 브라질 [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* 태국 [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])

각 규제 유형에 대한 작업은 별도로 추적됩니다. 규칙 유형 간에 전환하려면 **[!UICONTROL 규정 유형]** 드롭다운 메뉴를 클릭하고 목록에서 원하는 규칙을 선택합니다.

![규정 유형 드롭다운](../images/user-guide/regulation.png)

규정 유형을 변경하면 선택한 규정에 적용되는 모든 작업, 필터, 위젯 및 작업 생성 대화 상자가 표시되도록 대시보드가 업데이트됩니다.

![업데이트된 대시보드](../images/user-guide/dashboard-update.png)

### 상태 보고서

상태 보고서 위젯의 왼쪽에 있는 그래프는 오류가 있는 다시 보고될 수 있는 작업에 대해 제출한 작업을 추적합니다. 오른쪽의 그래프는 30일 준수 창의 끝에 있는 작업을 추적합니다.

그래프 위에 있는 두 개의 전환 단추 중 하나를 클릭하여 각각의 지표를 표시하거나 숨깁니다.

![](../images/user-guide/hide-errors.png)

마우스를 해당 데이터 포인트 위로 가져가면 그래프의 데이터 포인트와 연관된 정확한 작업 수를 볼 수 있습니다.

![마우스 오버 데이터 포인트](../images/user-guide/mouse-over.png)

지정된 데이터 포인트에 대한 세부 정보를 보려면 해당 데이터 포인트를 클릭하여 작업 요청 위젯에 연관된 작업을 표시합니다. 작업 목록 바로 위에 적용된 필터를 참고하십시오.

![위젯에서 적용된 필터](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>작업 요청 위젯에 필터가 적용되면 필터 알림에서 **X를** 클릭하여 필터를 제거할 수 있습니다. 작업 요청은 기본 추적 목록으로 돌아갑니다.

### 작업 요청

작업 요청 위젯은 요청 유형, 현재 상태, 기한, 요청자 이메일 등 조직에서 사용 가능한 모든 작업 요청을 나열합니다.

>[!NOTE]
>
>이전에 만든 작업의 데이터는 완료 날짜로부터 30일 동안만 액세스할 수 있습니다.

작업 요청 제목 아래의 검색 표시줄에 키워드를 입력하여 목록을 필터링할 수 있습니다. 입력과 동시에 목록이 자동으로 필터링되어 검색어와 일치하는 값이 포함된 요청을 표시합니다. 요청 위치 **[!UICONTROL 드롭다운 메뉴를]** 사용하여 나열된 작업에 대한 시간 범위를 선택할 수도 있습니다.

![작업 요청 검색 옵션](../images/user-guide/job-search.png)

특정 작업 요청의 세부 정보를 보려면 목록에서 요청의 작업 ID를 클릭하여 **[!UICONTROL 작업 세부 정보]** 페이지를 엽니다.

![GDPR UI 작업 세부 정보](../images/user-guide/job-details.png)

이 대화 상자에는 전체 작업과 관련된 각 [!DNL Experience Cloud] 솔루션과 현재 상태에 대한 상태 정보가 포함되어 있습니다. 모든 개인 정보 보호 작업이 비동기 중이기 때문에, 페이지는 각 솔루션의 최신 통신 날짜 및 시간(GMT)을 표시합니다. 어떤 경우에는 요청을 처리하는 데 다른 솔루션보다 시간이 더 필요합니다.

솔루션이 추가 데이터를 제공한 경우 이 대화 상자에서 볼 수 있습니다. 개별 제품 행을 클릭하여 이 데이터를 볼 수 있습니다.

전체 작업 데이터를 CSV 파일로 다운로드하려면 대화 상자 오른쪽 **[!UICONTROL 상단에 있는 CSV로]** 내보내기를 클릭합니다.

## 새 개인 정보 작업 요청 만들기

>[!NOTE]
>
>개인 정보 작업 요청을 만들려면 데이터를 액세스하거나 삭제할 특정 고객에 대한 ID 정보를 제공해야 합니다. 이 섹션을 계속하기 전에 [ID 데이터에 대한 개인 정보 요청](../identity-data.md) 문서를 검토하십시오.

UI는 새 작업 요청을 만드는 두 가지 방법을 제공합니다. [!DNL Privacy Service]

* [요청 빌더 사용](#request-builder)
* [JSON 파일 업로드](#json)

이러한 방법 각각에 대한 사용 단계는 다음 섹션에 제공됩니다.

### 요청 빌더 사용 {#request-builder}

요청 빌더를 사용하면 사용자 인터페이스에서 새 개인 정보 보호 작업 요청을 수동으로 만들 수 있습니다. 요청 빌더는 요청 빌더가 사용자당 ID 유형만 갖도록 요청을 제한하므로 더 간단하고 작은 요청 세트에 가장 적합합니다. 보다 복잡한 요청의 경우 JSON 파일 [을](#json) 대신 업로드하는 것이 좋습니다.

요청 빌더 사용을 시작하려면 화면 오른쪽의 상태 보고서 **[!UICONTROL 위젯]** 아래에 있는 요청 만들기를 클릭합니다.

![요청 만들기를 클릭합니다](../images/user-guide/create-request.png)

현재 **[!UICONTROL 선택된 규칙 유형에 대한 개인 정보 작업 요청을 제출하는 데 사용할 수 있는 옵션이 표시된 요청]** 만들기 대화 상자가 열립니다.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

요청의 **[!UICONTROL 작업 유형]** (&quot;삭제&quot; 또는 &quot;액세스&quot;)과 목록에서 하나 이상의 사용 가능한 **[!UICONTROL 제품을]** 선택합니다.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

네임스페이스 유형 **[!UICONTROL 에서]**&#x200B;보낼 고객 ID에 적합한 네임스페이스 유형을 [!DNL Privacy Service]선택합니다.

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

표준 _네임스페이스 유형을 사용하는 경우 드롭다운 메뉴(이메일, ECID 또는 AID)에서 네임스페이스를 선택한 다음 오른쪽에 있는 텍스트 상자에 ID 값을 입력한 다음 각 ID에 대해_ \&lt;enter> **** 키를 눌러 목록에 추가합니다.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

사용자 _지정_ 네임스페이스 유형을 사용할 때는 아래 ID 값을 제공하기 전에 네임스페이스에 수동으로 입력해야 합니다.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

When finished, click **[!UICONTROL Create]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 작업 요청 위젯에 나열됩니다.

### JSON 파일 업로드 {#json}

처리 중인 각 데이터 주체에 대해 여러 ID 유형을 사용하는 요청 등 보다 복잡한 요청을 만들 때 JSON 파일을 업로드하여 요청을 만들 수 있습니다.

요청 **[!UICONTROL 만들기]**&#x200B;옆에 있는 화살표를 클릭합니다. 화면의 오른쪽에 있는 상태 보고서 위젯 아래에 있습니다. 표시되는 옵션 목록에서 JSON **[!UICONTROL 업로드를 선택합니다]**.

![요청 생성 옵션](../images/user-guide/create-options.png)

JSON **[!UICONTROL 파일]** 드래그 앤 드롭을 위한 창을 제공하는 JSON 업로드 대화 상자가 나타납니다.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

업로드할 JSON 파일이 없는 경우 **[!UICONTROL Adobe-GDPR-Request.json]** 다운로드를 클릭하여 데이터 주체로부터 수집한 값에 따라 템플릿을 다운로드할 수 있습니다.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


컴퓨터에서 JSON 파일을 찾아 대화 상자 창으로 드래그합니다. 업로드에 성공하면 파일 이름이 대화 상자에 나타납니다. JSON 파일을 대화 상자로 드래그하여 놓아 필요에 따라 계속 추가할 수 있습니다.

When finished, click **[!UICONTROL Create]**. 대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 _작업 요청_ 위젯에 나열됩니다.

### 다음 단계

이 문서를 읽음으로써 UI를 사용하여 개인 정보 작업을 만들고, 작업 세부 사항을 보고 처리 상태를 모니터링하고, 완료된 결과를 다운로드하는 방법을 학습했습니다. [!DNL Privacy Service]

API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [!DNL Privacy Service] 개발자 안내서를 참조하십시오 [](../api/getting-started.md).