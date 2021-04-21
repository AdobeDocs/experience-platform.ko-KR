---
keywords: Experience Platform;홈;인기 항목;내보내기;Export;home;popular topics;export
solution: Experience Platform
title: Privacy Service UI에서 개인 정보 작업 관리
topic-legacy: UI guide
description: Privacy Service 사용자 인터페이스를 사용하여 다양한 Experience Cloud 응용 프로그램에서 개인 정보 요청을 조정하고 모니터링하는 방법을 알아봅니다.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# Privacy Service UI에서 개인 정보 작업 관리

이 문서에서는 [!DNL Privacy Service] 사용자 인터페이스를 사용하여 개인 정보 요청을 만들고 관리하는 단계를 제공합니다.

## [!DNL Privacy Service] UI 대시보드 찾아보기

[!DNL Privacy Service] UI에 대한 대시보드에서는 개인 정보 작업 상태를 볼 수 있는 2개의 위젯을 제공합니다.&quot;[!UICONTROL Status Report]&quot; 및 &quot;[!UICONTROL Job Requests]&quot;. 대시보드에는 표시된 작업에 대해 현재 선택된 규칙이 표시됩니다.

![UI 대시보드](../images/user-guide/dashboard.png)

### 규정 유형

[!DNL Privacy Service] 여러 개인 정보 보호 규정에 대한 작업 요청 지원:

* 다음 [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* 유럽 연합의 [!DNL General Data Protection Regulation]([!UICONTROL GDPR])
* 태국의 [!DNL Personal Data Protection Act]([!UICONTROL PDPA_THA])
* 브라질의 [!DNL Lei Geral de Proteção de Dados]([!UICONTROL LGPD_BRA])
* 뉴질랜드 [!DNL Privacy Act]([!UICONTROL NZPA_NZL])

각 규제 유형에 대한 작업은 별도로 추적됩니다. 규칙 유형 간에 전환하려면 **[!UICONTROL Regulation Type]** 드롭다운 메뉴를 선택하고 목록에서 원하는 규칙을 선택합니다.

![규정 유형 드롭다운](../images/user-guide/regulation.png)

규정 유형을 변경하면 선택한 규정에 적용되는 모든 작업, 필터, 위젯 및 작업 생성 대화 상자가 표시되도록 대시보드가 업데이트됩니다.

![업데이트된 대시보드](../images/user-guide/dashboard-update.png)

### 상태 보고서

상태 보고서 위젯의 왼쪽에 있는 그래프는 오류가 있는 다시 보고될 수 있는 작업에 대해 제출한 작업을 추적합니다. 오른쪽의 그래프는 30일 준수 창의 끝에 가까운 작업을 추적합니다.

그래프 위에 있는 두 전환 단추 중 하나를 선택하여 각각의 지표를 표시하거나 숨깁니다.

![](../images/user-guide/hide-errors.png)

마우스를 해당 데이터 포인트 위로 가져가면 그래프에서 데이터 포인트와 연관된 정확한 작업 수를 볼 수 있습니다.

![마우스 오버 데이터 포인트](../images/user-guide/mouse-over.png)

지정된 데이터 포인트에 대한 세부 정보를 보려면 해당 데이터 포인트를 선택하여 [작업 요청] 위젯에 연결된 작업을 표시합니다. 작업 목록 바로 위에 적용되는 필터를 주목하십시오.

![위젯에서 적용된 필터](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>필터가 작업 요청 위젯에 적용되면 필터 알림에서 **X**&#x200B;을 선택하여 필터를 제거할 수 있습니다. 작업 요청은 기본 추적 목록으로 돌아갑니다.

### 작업 요청

작업 요청 위젯은 요청 유형, 현재 상태, 기한 및 요청자 이메일 등 조직에서 사용할 수 있는 모든 작업 요청을 나열합니다.

>[!NOTE]
>
>이전에 만든 작업에 대한 데이터는 완료 날짜 이후 30일 동안에만 액세스할 수 있습니다.

[작업 요청] 제목 아래의 검색 표시줄에 키워드를 입력하여 목록을 필터링할 수 있습니다. 목록이 입력하면 자동으로 필터링되어 검색어와 일치하는 값이 포함된 요청을 표시합니다. **[!UICONTROL Requested on]** 드롭다운 메뉴를 사용하여 나열된 작업의 시간 범위를 선택할 수도 있습니다.

![작업 요청 검색 옵션](../images/user-guide/job-search.png)

특정 작업 요청의 세부 정보를 보려면 목록에서 요청의 작업 ID를 선택하여 **[!UICONTROL Job Details]** 페이지를 엽니다.

![GDPR UI 작업 세부 사항](../images/user-guide/job-details.png)

이 대화 상자에는 전체 작업과 관련된 각 [!DNL Experience Cloud] 솔루션과 현재 상태에 대한 상태 정보가 포함되어 있습니다. 모든 개인 정보 작업이 비동기식으로 진행되므로, 페이지 보기 시 각 솔루션의 최신 통신 날짜 및 시간(GMT)이 표시됩니다. 이러한 경우 요청을 처리하는 데 다른 솔루션보다 시간이 더 오래 걸립니다.

솔루션이 추가 데이터를 제공한 경우 이 대화 상자에서 볼 수 있습니다. 개별 제품 행을 선택하여 이 데이터를 볼 수 있습니다.

전체 작업 데이터를 CSV 파일로 다운로드하려면 대화 상자의 오른쪽 상단에 있는 **[!UICONTROL Export to CSV]**&#x200B;을 선택합니다.

## 새 개인 정보 작업 요청 만들기

>[!NOTE]
>
>개인 정보 보호 작업 요청을 만들려면 액세스 또는 삭제하려는 특정 고객에 대한 ID 정보를 제공해야 합니다. 이 섹션을 계속하기 전에 [ID 데이터에 대한 개인 정보 요청](../identity-data.md)의 문서를 검토하십시오.

[!DNL Privacy Service] UI는 새 작업 요청을 만드는 두 가지 방법을 제공합니다.

* [요청 빌더 사용](#request-builder)
* [JSON 파일 업로드](#json)

이러한 각 메서드 사용 단계는 다음 섹션에 제공됩니다.

### 요청 빌더 {#request-builder} 사용

요청 빌더를 사용하여 사용자 인터페이스에서 새 개인 정보 보호 작업 요청을 수동으로 만들 수 있습니다. 요청 빌더는 요청 빌더가 요청마다 ID 유형만 갖도록 제한하므로 더 간단하고 작은 요청 세트에 가장 적합합니다. 보다 복잡한 요청의 경우 대신 [JSON 파일](#json)을 업로드하는 것이 좋습니다.

요청 빌더 사용을 시작하려면 화면 오른쪽의 상태 보고서 위젯 아래에서 **[!UICONTROL Create Request]** 을 선택합니다.

![요청 만들기 선택](../images/user-guide/create-request.png)

현재 선택된 규칙 유형에 대한 개인 정보 작업 요청을 제출하는 데 사용할 수 있는 옵션이 표시된 **[!UICONTROL Create Request]** 대화 상자가 열립니다.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

요청(&quot;삭제&quot; 또는 &quot;액세스&quot;)의 **[!UICONTROL Job Type]** 및 목록에서 하나 이상의 사용 가능한 제품을 선택합니다.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

**[!UICONTROL Namespace type]**&#x200B;에서 [!DNL Privacy Service]로 보내지는 고객 ID에 적합한 네임스페이스 유형을 선택합니다.

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

표준 네임스페이스 유형을 사용하는 경우 드롭다운 메뉴(이메일, ECID 또는 AID)에서 네임스페이스를 선택한 다음 오른쪽에 있는 텍스트 상자에 ID 값을 입력하고 각 ID에 대해 **\&lt;enter>**&#x200B;을 눌러 목록에 추가합니다.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

사용자 지정 네임스페이스 유형을 사용할 때는 아래 ID 값을 제공하기 전에 네임스페이스를 직접 입력해야 합니다.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

완료되면 **[!UICONTROL Create]**&#x200B;을 선택합니다.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 [작업 요청] 위젯에 나열됩니다.

### JSON 파일 {#json} 업로드

처리 중인 각 데이터 주체에 대해 여러 ID 유형을 사용하는 요청과 같이 더 복잡한 요청을 만들 때 JSON 파일을 업로드하여 요청을 만들 수 있습니다.

화면 오른쪽의 상태 보고서 위젯 아래에 있는 **[!UICONTROL Create Request]** 옆의 화살표를 선택합니다. 나타나는 옵션 목록에서 **[!UICONTROL Upload JSON]**&#x200B;을 선택합니다.

![요청 만들기 옵션](../images/user-guide/create-options.png)

JSON 파일을 드래그하여 놓을 수 있는 창을 제공하는 **[!UICONTROL Upload JSON]** 대화 상자가 나타납니다.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

업로드할 JSON 파일이 없는 경우 **[!UICONTROL Download Adobe-GDPR-Request.json]**&#x200B;을 선택하여 데이터 주체로부터 수집한 값에 따라 채울 수 있는 템플릿을 다운로드합니다.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


컴퓨터에서 JSON 파일을 찾아 대화 상자 창으로 드래그합니다. 업로드에 성공하면 파일 이름이 대화 상자에 나타납니다. JSON 파일을 대화 상자로 드래그하여 놓아 필요에 따라 계속 추가할 수 있습니다.

완료되면 **[!UICONTROL Create]**&#x200B;을 선택합니다. 대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 [작업 요청] 위젯에 나열됩니다.

### 다음 단계

이 문서를 읽음으로써 [!DNL Privacy Service] UI를 사용하여 개인 정보 작업을 만들고, 작업 세부 사항을 보고 처리 상태를 모니터링하고, 완료되면 결과를 다운로드하는 방법을 학습했습니다.

[!DNL Privacy Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [개발자 안내서](../api/getting-started.md)를 참조하십시오.
