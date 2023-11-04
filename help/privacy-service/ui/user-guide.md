---
keywords: Experience Platform;홈;인기 항목;내보내기;내보내기
solution: Experience Platform
title: Privacy Service UI의 개인 정보 작업 관리
description: Privacy Service 사용자 인터페이스를 사용하여 다양한 Experience Cloud 애플리케이션에서 개인 정보 요청을 조정하고 모니터링하는 방법에 대해 알아봅니다.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 9d05752f3db78d9d10fd91fd0d3fed924217199c
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 15%

---

# Privacy Service UI에서 개인 정보 작업 관리 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="데이터 주체 개인 정보 보호 요청 이행"
>abstract="<h2>설명</h2><p>Adobe Experience Platform Privacy Service를 사용하면 법적 개인 정보 보호 규정에 따라 개인 데이터에 액세스하거나 삭제하려는 고객을 대신하여 개인 정보 보호 요청을 생성하고 관리할 수 있습니다.</p>"

이 문서에서는 다음을 사용하여 개인 정보 보호 요청을 만들고 관리하는 단계를 제공합니다. [!DNL Privacy Service] 사용자 인터페이스.

>[!IMPORTANT]
>
>Privacy Service은 데이터 주체 및 소비자 권한 요청용으로만 사용됩니다. 데이터 정리 또는 유지 관리를 위한 다른 Privacy Service 사용은 지원되지 않거나 허용되지 않습니다. Adobe은 적시에 이를 이행할 법적 의무가 있다. 따라서 프로덕션 전용 환경이며 유효한 개인 정보 보호 요청에 대한 불필요한 백로그를 만들기 때문에 Privacy Service에 대한 로드 테스트는 허용되지 않습니다.
>
>이제 서비스 남용을 방지하기 위해 엄격한 일일 업로드 제한이 적용됩니다. 시스템을 남용하는 것으로 확인된 사용자는 서비스에 액세스할 수 없게 됩니다. 그런 다음 후속 회의가 그들과 함께 개최되어 그들의 행동에 대해 이야기하고 Privacy Service에 허용되는 사용에 대해 논의합니다.

## 찾아보기 [!DNL Privacy Service] UI 대시보드

다음에 대한 대시보드 [!DNL Privacy Service] UI는 개인 정보 작업의 상태를 볼 수 있는 두 가지 위젯을 제공합니다.&quot;[!UICONTROL 상태 보고서]&quot; 및 &quot;[!UICONTROL 작업 요청]&quot;. 대시보드에는 표시된 작업에 대해 현재 선택한 규정도 표시됩니다.

![UI 대시보드](../images/user-guide/dashboard.png)

### 규정 유형

[!DNL Privacy Service] 은 여러 개인 정보 보호 규정에 대한 작업 요청을 지원합니다. 다음 표에는 UI에 표시되는 지원되는 규정 및 해당 레이블이 나열되어 있습니다.

| UI 레이블 | 규정 |
| --- | --- |
| [!UICONTROL APA_AUS] | [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL GDPR] | 유럽 연합의 [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | 브라질 [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | 뉴질랜드 [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | 태국 [!DNL Personal Data Protection Act] |
| [!UICONTROL UPA] | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>의 개요 보기 [지원되는 개인 정보 보호 규정](../regulations/overview.md) 각 규정의 법적 맥락에 대한 자세한 내용.

각 규정 유형에 대한 직무는 별도로 추적된다. 규정 유형 간에 전환하려면 **[!UICONTROL 규정 유형]** 드롭다운 메뉴를 클릭하고 목록에서 원하는 규제를 선택합니다.

![규정 유형 드롭다운이 있는 Privacy Service 콘솔.](../images/user-guide/regulation.png)

규정 유형을 변경하면 대시보드가 업데이트되어 선택한 규정에 적용되는 모든 작업, 필터, 위젯 및 작업 생성 대화 상자가 표시됩니다.

![업데이트된 대시보드](../images/user-guide/dashboard-update.png)

### 상태 보고서

상태 보고서 위젯 왼쪽의 그래프는 오류와 함께 다시 보고되었을 수 있는 모든 작업에 대해 제출된 작업을 추적합니다. 오른쪽의 그래프는 30일 준수 기간이 거의 끝나가는 작업을 추적합니다.

그래프 위에 있는 두 개의 전환 버튼 중 하나를 선택하여 해당 지표를 표시하거나 숨깁니다.

![](../images/user-guide/hide-errors.png)

마우스를 해당 데이터 포인트 위로 가져가면 그래프에서 데이터 포인트와 연관된 정확한 작업 수를 볼 수 있습니다.

![마우스 오버 데이터 포인트](../images/user-guide/mouse-over.png)

지정된 데이터 포인트에 대한 세부 정보를 보려면 해당 데이터 포인트를 선택하여 작업 요청 위젯에 연관된 작업을 표시합니다. 작업 목록 바로 위에 적용된 필터를 확인합니다.

![위젯에서 필터 적용됨](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>필터가 작업 요청 위젯에 적용되면 다음을 선택하여 필터를 제거할 수 있습니다. **X** 필터 알약. 그런 다음 작업 요청은 기본 추적 목록으로 돌아갑니다.

### 작업 요청

작업 요청 위젯은 요청 유형, 현재 상태, 기한 및 요청자 이메일과 같은 세부 정보를 포함하여 조직에서 사용 가능한 모든 작업 요청을 나열합니다.

>[!NOTE]
>
>이전에 생성된 작업의 데이터는 완료 날짜 후 30일 동안만 액세스할 수 있습니다.

Job 요청 제목 아래의 검색 막대에 키워드를 입력하여 목록을 필터링할 수 있습니다. 이 목록은 입력할 때 자동으로 필터링되며, 검색어와 일치하는 값이 포함된 요청을 표시합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 요청일]** 드롭다운 메뉴를 사용하여 나열된 작업에 대한 시간 범위를 선택합니다.

![작업 요청 검색 옵션](../images/user-guide/job-search.png)

특정 작업 요청의 세부 정보를 보려면 목록에서 요청의 작업 ID를 선택하여 **[!UICONTROL 작업 세부 정보]** 페이지를 가리키도록 업데이트하는 중입니다.

![GDPR UI 작업 세부 정보](../images/user-guide/job-details.png)

이 대화 상자에는 각 의 상태 정보가 포함되어 있습니다. [!DNL Experience Cloud] 솔루션 및 전체 작업과 관련된 현재 상태입니다. 모든 개인 정보 보호 작업은 비동기적으로 수행되므로, 일부는 요청을 처리하는 데 다른 작업보다 더 많은 시간이 필요하므로 페이지에는 각 솔루션의 최신 통신 날짜 및 시간(GMT)이 표시됩니다.

솔루션에서 추가 데이터가 제공된 경우 이 대화 상자에서 볼 수 있습니다. 개별 제품 행을 선택하여 이 데이터를 볼 수 있습니다.

전체 작업 데이터를 CSV 파일로 다운로드하려면 다음을 선택합니다. **[!UICONTROL CSV로 내보내기]** 대화 상자의 오른쪽 상단

## 새 개인정보 보호 작업 요청 만들기 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="지침"
>abstract="<ul><li>왼쪽 탐색 메뉴에서 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">요청</a> 을 선택하여 Privacy Ul를 연 다음 <b>요청 만들기</b>를 선택합니다.</li><li>여기에서 요청 빌더를 사용하거나 데이터 주체의 JSON 파일을 업로드할 수 있습니다.</li><li>요청 빌더를 사용하는 경우 작업 유형(액세스 및/또는 삭제)을 선택한 다음 제공하는 자격 증명 유형(이메일, ECID 또는 AAID)을 선택하거나 사용자 정의 자격 증명 네임스페이스를 입력합니다. 고객에 대한 적절한 ID 값을 입력하고 완료되면 <b>만들기</b>를 선택합니다.</li><li>JSON 파일을 업로드하는 경우 요청 만들기 옆에 있는 화살표를 선택합니다. 옵션 목록에서 <b>JSON 업로드</b>를 선택하고 파일을 업로드합니다. 업로드할 JSON 파일이 없는 경우 <b>Adobe-GDPR-Request.json 다운로드</b>를 선택하여 작성할 수 있는 템플릿을 다운로드합니다. JSON을 업로드하고 완료되면 <b>만들기</b>를 선택합니다.</li><li>이 기능에 대한 자세한 내용은 Experience League의 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=ko">Privacy Service 사용 안내서</a>를 참조하십시오.</li></ul>"

>[!NOTE]
>
>개인 정보 작업 요청을 만들려면 데이터에 액세스하거나 삭제할 특정 고객에 대한 ID 정보를 제공해야 합니다. 다음에 대한 문서를 검토하십시오. [개인 정보 보호 요청에 대한 id 데이터](../identity-data.md) 이 섹션을 계속하기 전에

다음 [!DNL Privacy Service] UI는 새 작업 요청을 만드는 두 가지 방법을 제공합니다.

* [요청 빌더 사용](#request-builder)
* [JSON 파일 업로드](#json)

이러한 각 방법을 사용하는 단계는 다음 섹션에 나와 있습니다.

### 요청 빌더 사용 {#request-builder}

요청 빌더를 사용하여 사용자 인터페이스에서 새 개인 정보 보호 작업 요청을 수동으로 만들 수 있습니다. Request Builder는 요청을 사용자당 ID 유형만 갖도록 제한하므로 더 간단하고 작은 요청 세트에 가장 적절하게 사용됩니다. 보다 복잡한 요청의 경우 다음과 같은 작업을 수행하는 것이 좋습니다. [json 파일 업로드](#json) 대신,

요청 빌더를 사용하려면 을 선택합니다. **[!UICONTROL 요청 만들기]** 화면 오른쪽의 상태 보고서 위젯 아래에 있습니다.

![요청 생성 선택](../images/user-guide/create-request.png)

다음 **[!UICONTROL 요청 만들기]** 대화 상자가 열리고 현재 선택한 규정 유형에 대한 개인 정보 작업 요청을 제출하는 데 사용할 수 있는 옵션이 표시됩니다.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

다음 항목 선택 **[!UICONTROL 작업 유형]** 목록에서 사용 가능한 하나 이상의 제품 및 요청(&quot;삭제&quot; 또는 &quot;액세스&quot;)의

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

아래 **[!UICONTROL 네임스페이스 유형]**&#x200B;로 보낼 고객 ID에 대한 적절한 네임스페이스 유형을 선택합니다. [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

표준 네임스페이스 유형을 사용할 때 드롭다운 메뉴에서 네임스페이스(이메일, ECID 또는 AAID)를 선택한 다음 오른쪽에 있는 텍스트 상자에 ID 값을 입력하고 **\&lt;enter>** 각 ID에 대해 목록에 추가합니다.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

사용자 지정 네임스페이스 유형을 사용하는 경우, 아래 ID 값을 제공하기 전에 네임스페이스를 수동으로 입력해야 합니다.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

완료되면 다음을 선택합니다. **[!UICONTROL 만들기]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 작업 요청 위젯에 나열됩니다.

### JSON 파일 업로드 {#json}

처리되는 각 데이터 주체에 대해 여러 ID 유형을 사용하는 요청과 같이 보다 복잡한 요청을 만들 때 JSON 파일을 업로드하여 요청을 만들 수 있습니다.

옆에 있는 화살표를 선택합니다 **[!UICONTROL 요청 만들기]**&#x200B;을 클릭하고, 화면 오른쪽의 상태 보고서 위젯 아래에서 을 클릭합니다. 표시되는 옵션 목록에서 을 선택합니다 **[!UICONTROL JSON 업로드]**.

![요청 생성 옵션](../images/user-guide/create-options.png)

다음 **[!UICONTROL JSON 업로드]** 대화 상자가 나타나고 JSON 파일을에 끌어다 놓을 수 있는 창이 제공됩니다.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

업로드할 JSON 파일이 없는 경우 다음을 선택합니다. **[!UICONTROL 다운로드 Adobe-GDPR-Request.json]** 데이터 주제에서 수집한 값에 따라 채울 수 있는 템플릿을 다운로드하려면 다음을 수행하십시오.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


컴퓨터에서 JSON 파일을 찾아 대화 상자 창으로 드래그합니다. 업로드가 성공적으로 수행되면 대화 상자에 파일 이름이 표시됩니다. 필요에 따라 JSON 파일을 대화 상자로 끌어다 놓아 계속 추가할 수 있습니다.

완료되면 다음을 선택합니다. **[!UICONTROL 만들기]**. 대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 작업 요청 위젯에 나열됩니다.

### 다음 단계

이 문서를 읽고 다음을 사용하는 방법을 배웠습니다. [!DNL Privacy Service] 개인 정보 작업을 생성하고, 작업의 세부 정보를 보고, 처리 상태를 모니터링하고, 작업이 완료되면 결과를 다운로드하기 위한 UI.

프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 자세한 내용은 [!DNL Privacy Service] API, 다음을 참조하십시오. [API 안내서](../api/overview.md).
