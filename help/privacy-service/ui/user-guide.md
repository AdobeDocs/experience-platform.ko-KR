---
keywords: Experience Platform;홈;인기 항목;내보내기;내보내기
solution: Experience Platform
title: Privacy Service UI의 개인 정보 작업 관리
description: Privacy Service 사용자 인터페이스를 사용하여 다양한 Experience Cloud 애플리케이션에서 개인 정보 요청을 조정하고 모니터링하는 방법에 대해 알아봅니다.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 11%

---

# Privacy Service UI에서 개인정보 작업 관리 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="데이터 주체 개인정보 보호 요청 이행"
>abstract="<h2>설명</h2><p>Adobe Experience Platform Privacy Service를 사용하면 법적 개인정보 보호 규정에 따라 개인 데이터에 액세스하거나 삭제하려는 고객을 대신하여 개인정보 보호 요청을 생성하고 관리할 수 있습니다.</p>"

이 문서에서는 [!DNL Privacy Service] 사용자 인터페이스를 사용하여 개인 정보 요청을 만들고 관리하는 단계를 제공합니다.

>[!IMPORTANT]
>
>Privacy Service은 데이터 주체 및 소비자 권한 요청만을 위한 것입니다. 데이터 정리 또는 유지 관리를 위한 다른 Privacy Service 사용은 지원되지 않거나 허용되지 않습니다. Adobe은 적시에 이를 이행할 법적 의무가 있습니다. 따라서 Privacy Service은 프로덕션 전용 환경이며 유효한 개인 정보 보호 요청에 대한 불필요한 백로그를 만들기 때문에 에 대한 로드 테스트가 허용되지 않습니다.
>
>이제 서비스 남용을 방지하기 위해 엄격한 일일 업로드 제한이 적용됩니다. 시스템을 남용하는 것으로 확인된 사용자는 서비스에 액세스할 수 없게 됩니다. 그런 다음 후속 회의가 그들과 함께 개최되어 그들의 행동에 대해 이야기하고 Privacy Service의 허용 가능한 사용에 대해 논의합니다.

## [!DNL Privacy Service] UI 대시보드 찾아보기

[!DNL Privacy Service] UI용 대시보드는 개인 정보 작업의 상태를 볼 수 있는 두 가지 위젯을 제공합니다. &quot;[!UICONTROL 상태 보고서]&quot; 및 &quot;[!UICONTROL 작업 요청]&quot;. 대시보드에는 표시된 작업에 대해 현재 선택한 규정도 표시됩니다.

![UI 대시보드](../images/user-guide/dashboard.png)

### 규정 유형

[!DNL Privacy Service]은(는) 여러 개인 정보 보호 규정에 대한 작업 요청을 지원합니다. 다음 표에는 UI에 표시되는 지원되는 규정 및 해당 레이블이 나열되어 있습니다.

| UI 레이블 | 규정 |
|-------------------------------------|------------------------|
| [!UICONTROL APA_AUS(오스트레일리아)] | [!DNL Australia Privacy Act] |
| [!UICONTROL CCPA(캘리포니아)] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPA_USA(콜로라도)] | [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_USA(캘리포니아)] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA_USA(Connecticut)] | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DPDPA_USA(Delaware)] | [!DNL Delaware Personal Data Privacy Act] |
| [!UICONTROL FDBR_USA(플로리다)] | [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR(유럽 연합)] | 유럽 연합의 [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPPA_USA(미국)] | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPA_USA]&#x200B;(Iowa) | [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA(브라질)] | 브라질의 &quot;[!DNL General Data Protection Law]&quot; [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA_USA(워싱턴)] | [!DNL Washington My Health My Data Act] |
| [!UICONTROL MCDPA_USA(몬타나)] | [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL NDPA_USA(네브래스카)] | [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NZPA_NZL(뉴질랜드)] | 뉴질랜드 [!DNL Privacy Act] |
| [!UICONTROL NHPA_USA(뉴햄프셔)] | [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_USA(뉴저지)] | [!DNL New Jersey Data Protection Act] |
| [!UICONTROL OCPA USA(오레곤)] | [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA(태국)] | 태국 [!DNL Personal Data Protection Act] |
| [!UICONTROL QL25_CAN(퀘벡)] | [!DNL Quebec Law 25] |
| [!UICONTROL TDPSA USA(텍사스)] | [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL UCPA_USA(유타)] | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA(버지니아)] | [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!-- 
Waiting:
| **[!UICONTROL PIPA_KOR]**  ?        | South Korea [!DNL Personal Information Privacy Act] |
 -->

>[!NOTE]
>
>각 규제의 법적 컨텍스트에 대한 자세한 내용은 [지원되는 개인 정보 보호 규정](../regulations/overview.md)에 대한 개요를 참조하십시오.

각 규정 유형에 대한 직무는 별도로 추적된다. 규정 유형 간에 전환하려면 **[!UICONTROL 규정 유형]** 드롭다운 메뉴를 선택하고 목록에서 원하는 규정을 선택하십시오.

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

![위젯에서 적용된 필터](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>필터가 작업 요청 위젯에 적용되면 필터 알약에서 **X**&#x200B;을(를) 선택하여 필터를 제거할 수 있습니다. 그런 다음 작업 요청은 기본 추적 목록으로 돌아갑니다.

### 작업 요청 {#job-requests}

[!UICONTROL 작업 요청] 작업 영역에 조직의 최근 작업 요청에 대한 세부 정보가 나열됩니다. 세부 정보에는 요청 유형, 현재 상태, 기한, 요청자 이메일 등이 포함됩니다. 한 번에 100개의 레코드 집합이 로드됩니다. 기본적으로 가장 최근에 생성된 작업이 맨 위에 표시되며, 탐색하기 위해 아래로 스크롤할 때 더 많은 레코드 세트가 로드됩니다.

>[!NOTE]
>
>이전에 생성된 작업의 데이터는 완료 날짜 후 30일 동안만 액세스할 수 있습니다.

[!UICONTROL 작업 요청] 제목 아래의 검색 표시줄에 키워드를 입력하여 목록을 필터링할 수 있습니다. 이 목록은 입력할 때 자동으로 필터링되며, 검색어와 일치하는 값이 포함된 요청을 표시합니다. 검색 필드는 개인 정보 작업 ID를 UI에서 현재 렌더링/로드된 작업에 일치하는 &quot;빠른&quot; 검색을 수행합니다. 제출된 모든 작업에 대한 포괄적인 검색은 아닙니다. 대신 로드된 결과에 적용되는 필터입니다. Privacy Service API를 사용하여 [특정 규정, 날짜 범위 또는 단일 작업에 따라 작업을 반환](../api/privacy-jobs.md#list)할 수 있습니다.

>[!TIP]
>
>지난 30일 동안 UI에 레코드를 로드하려면 테이블을 아래로 스크롤하여 더 많은 레코드 배치를 로드해야 합니다.

![검색 필드가 강조 표시된 Privacy Console 작업 요청 섹션.](../images/user-guide/job-search.png)

또는 검색 버튼을 사용하여 특정 날짜 범위에 걸친 개인 정보 작업 쿼리를 수행할 수 있습니다. 이 작업은 제공된 기간 동안 조직에서 제출한 모든 개인 정보 작업을 반환합니다. 쿼리의 시작 및 완료 날짜를 선택하려면 **[!UICONTROL 요청한 날짜]** 드롭다운 메뉴를 선택하십시오. 사용 가능한 옵션에는 [!UICONTROL 오늘], [!UICONTROL 최근 7일], [!UICONTROL 최근 2주], [!UICONTROL 최근 30일] 또는 [!UICONTROL 사용자 지정]이 있습니다. [!UICONTROL 요청한 날짜] 옵션과 함께 사용하면 검색 기능에는 선택한 날짜 범위 사이에 제출된 작업 요청만 표시됩니다.

![검색 필드, 드롭다운 메뉴에서 요청됨, 검색 단추가 강조 표시된 작업 요청 섹션입니다.](../images/user-guide/requested-on-dropdown-menu.png)

특정 작업 요청의 세부 정보를 보려면 목록에서 요청의 작업 ID를 선택하여 **[!UICONTROL 작업 세부 정보]** 페이지를 엽니다.

![GDPR UI 작업 세부 정보](../images/user-guide/job-details.png)

이 대화 상자에는 각 [!DNL Experience Cloud] 솔루션에 대한 상태 정보와 전체 작업과 관련된 현재 상태가 포함되어 있습니다. 모든 개인 정보 보호 작업은 비동기적으로 수행되므로, 일부는 요청을 처리하는 데 다른 작업보다 더 많은 시간이 필요하므로 페이지에는 각 솔루션의 최신 통신 날짜 및 시간(GMT)이 표시됩니다.

솔루션에서 추가 데이터가 제공된 경우 이 대화 상자에서 볼 수 있습니다. 개별 제품 행을 선택하여 이 데이터를 볼 수 있습니다.

전체 작업 데이터를 CSV 파일로 다운로드하려면 대화 상자의 오른쪽 상단에서 **[!UICONTROL CSV로 내보내기]**&#x200B;를 선택합니다.

## 새 개인정보 보호 작업 요청 만들기 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="지침"
>abstract="<ul><li>왼쪽 탐색 메뉴에서 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">요청</a>을 선택하여 Privacy Ul를 연 다음 <b>요청 만들기</b>를 선택합니다.</li><li>여기에서 요청 빌더를 사용하거나 데이터 주체의 JSON 파일을 업로드할 수 있습니다.</li><li>요청 빌더를 사용하는 경우 작업 유형(액세스 및/또는 삭제)을 선택한 다음 제공하는 자격 증명 유형(이메일, ECID 또는 AAID)을 선택하거나 사용자 정의 자격 증명 네임스페이스를 입력합니다. 고객에 대한 적절한 ID 값을 입력하고 완료되면 <b>만들기</b>를 선택합니다.</li><li>JSON 파일을 업로드하는 경우 요청 만들기 옆에 있는 화살표를 선택합니다. 옵션 목록에서 <b>JSON 업로드</b>를 선택하고 파일을 업로드합니다. 업로드할 JSON 파일이 없는 경우 <b>Adobe-GDPR-Request.json 다운로드</b>를 선택하여 작성할 수 있는 템플릿을 다운로드합니다. JSON을 업로드하고 완료되면 <b>만들기</b>를 선택합니다.</li><li>이 기능에 대한 자세한 내용은 Experience League의 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=ko">Privacy Service 사용 안내서</a>를 참조하십시오.</li></ul>"

>[!NOTE]
>
>개인 정보 작업 요청을 만들려면 데이터에 액세스하거나 삭제할 특정 고객에 대한 ID 정보를 제공해야 합니다. 이 섹션을 계속하기 전에 [개인 정보 보호 요청에 대한 ID 데이터](../identity-data.md)에 대한 문서를 검토하십시오.

[!DNL Privacy Service] UI는 새 작업 요청을 만드는 두 가지 방법을 제공합니다.

* [요청 빌더 사용](#request-builder)
* [JSON 파일 업로드](#json)

이러한 각 방법을 사용하는 단계는 다음 섹션에 나와 있습니다.

### 요청 빌더 사용 {#request-builder}

요청 빌더를 사용하여 사용자 인터페이스에서 새 개인 정보 보호 작업 요청을 수동으로 만들 수 있습니다. Request Builder는 요청을 사용자당 ID 유형만 갖도록 제한하므로 더 간단하고 작은 요청 세트에 가장 적절하게 사용됩니다. 더 복잡한 요청의 경우 대신 [JSON 파일을 업로드](#json)하는 것이 좋습니다.

요청 빌더를 사용하려면 화면 오른쪽의 상태 보고서 위젯 아래에서 **[!UICONTROL 요청 만들기]**&#x200B;를 선택하십시오.

![요청 만들기 선택](../images/user-guide/create-request.png)

**[!UICONTROL 요청 만들기]** 대화 상자가 열리고 현재 선택한 규정 유형에 대한 개인 정보 작업 요청을 제출하는 데 사용할 수 있는 옵션이 표시됩니다.

![](../images/user-guide/request-builder.png){width=500}

목록에서 요청의 **[!UICONTROL 작업 유형]**(&quot;삭제&quot; 또는 &quot;액세스&quot;) 및 사용 가능한 제품을 하나 이상 선택하십시오.

Privacy Service에서는 개인 데이터에 대한 두 종류의 작업 요청을 지원합니다. [!UICONTROL 액세스]&#x200B;(읽기) 및/또는 [!UICONTROL 삭제]. 조회 대상과 관련된 상품에 있는 모든 정보를 제공받도록 요청하거나 조회 대상과 관련된 모든 정보를 삭제하도록 요청할 수 있습니다.

![](../images/user-guide/type-and-products.png){width=500}

**[!UICONTROL 네임스페이스 유형]**&#x200B;에서 [!DNL Privacy Service]&#x200B;(으)로 전송되는 고객 ID에 적합한 네임스페이스 유형을 선택합니다.

![](../images/user-guide/namespace-type.png){width=500}

표준 네임스페이스 유형을 사용하는 경우 드롭다운 메뉴에서 네임스페이스(이메일, ECID 또는 AAID)를 선택한 다음 오른쪽에 있는 텍스트 상자에 ID 값을 입력하고 각 ID에 대해 **\&lt;enter>**&#x200B;을 눌러 목록에 추가합니다.

![](../images/user-guide/standard-namespace.png){width=500}

사용자 지정 네임스페이스 유형을 사용하는 경우, 아래 ID 값을 제공하기 전에 네임스페이스를 수동으로 입력해야 합니다.

![](../images/user-guide/custom-namespace.png){width=500}

완료되면 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

![](../images/user-guide/request-builder-create.png){width=500}

대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 작업 요청 위젯에 나열됩니다.

### JSON 파일 업로드 {#json}

처리되는 각 데이터 주체에 대해 여러 ID 유형을 사용하는 요청과 같이 보다 복잡한 요청을 만들 때 JSON 파일을 업로드하여 요청을 만들 수 있습니다.

화면 오른쪽의 상태 보고서 위젯 아래에 있는 **[!UICONTROL 요청 만들기]** 옆에 있는 화살표를 선택합니다. 표시되는 옵션 목록에서 **[!UICONTROL JSON 업로드]**&#x200B;를 선택합니다.

![만들기 옵션 요청](../images/user-guide/create-options.png)

JSON 파일을 드래그하여 놓을 수 있는 창을 제공하는 **[!UICONTROL JSON 업로드]** 대화 상자가 나타납니다.

![](../images/user-guide/upload-json.png){width=500}

업로드할 JSON 파일이 없는 경우 **[!UICONTROL Adobe-GDPR-Request.json 다운로드]**&#x200B;를 선택하여 데이터 주체에서 수집한 값에 따라 채울 수 있는 템플릿을 다운로드합니다.


![](../images/user-guide/privacy-template.png){width=500}


컴퓨터에서 JSON 파일을 찾아 대화 상자 창으로 드래그합니다. 업로드가 성공적으로 수행되면 대화 상자에 파일 이름이 표시됩니다. 필요에 따라 JSON 파일을 대화 상자로 끌어다 놓아 계속 추가할 수 있습니다.

완료되면 **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 대화 상자가 사라지고 새 작업(또는 작업)이 현재 처리 상태와 함께 작업 요청 위젯에 나열됩니다.

### 다음 단계

이 문서를 읽고 [!DNL Privacy Service] UI를 사용하여 개인 정보 작업을 만들고, 작업의 세부 정보를 보고, 처리 상태를 모니터링하고, 작업이 완료되면 결과를 다운로드하는 방법에 대해 알아보았습니다.

[!DNL Privacy Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [API 안내서](../api/overview.md)를 참조하십시오.
