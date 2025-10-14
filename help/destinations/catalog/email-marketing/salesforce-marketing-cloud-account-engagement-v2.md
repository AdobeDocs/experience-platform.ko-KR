---
title: (V2) Salesforce Marketing Cloud 계정 참여
description: (V2) Salesforce Marketing Cloud 계정 참여(이전의 Pardot) 대상을 사용하여 비즈니스 요구 사항에 대한 일괄 처리를 사용하여 프로필 데이터를 내보내고 Salesforce Marketing Cloud 계정 참여 내에서 활성화하는 방법에 대해 알아봅니다.
badge: label="Alpha" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: d1405237698271607fa672ccae1ac731d66df263
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 3%

---

# [!DNL (V2) Salesforce Marketing Cloud Account Engagement] 연결

[[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/)&#x200B;(이전의 [!DNL Pardot]) 대상을 사용하면 Adobe Experience Platform 프로필 데이터를 Salesforce의 B2B 마케팅 자동화 플랫폼으로 내보낼 수 있습니다.

이 통합을 통해 Adobe Experience Platform의 고객 프로필과 [!DNL Salesforce Marketing Cloud Account Engagement]의 마케팅 캠페인 간에 데이터를 원활하게 동기화할 수 있습니다.

이 대상은 [[!DNL Salesforce Import API v5]](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)을(를) 사용하여 배치 데이터 내보내기를 효율적으로 처리합니다.


>[!IMPORTANT]
> 
> [Salesforce Marketing Cloud 계정 참여](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) 대상의 V2 버전입니다. 이 버전은 이전 대상을 대체하며 현재 Alpha 릴리스에 있습니다.
> &#x200B;> <br>
> &#x200B;> 현재 이전 버전의 [Salesforce Marketing Cloud 계정 참여](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) 대상을 사용하는 경우 **2026년 1월** 전에 이 V2 버전으로 마이그레이션해야 합니다. 2026년 1월 이후 Adobe은 이전 버전을 중단하고 더 이상 사용할 수 없습니다.


## 사용 사례 {#use-cases}

[!DNL (V2) Marketing Cloud Account Engagement] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### B2B 리드 관리 {#use-case-lead-management}

포괄적인 잠재 고객 양성과 점수를 얻으려면 Adobe Experience Platform의 잠재 고객 데이터를 [!DNL Salesforce Marketing Cloud Account Engagement]과(와) 동기화하십시오. 마케팅 팀은 Experience Platform에서 풍부한 대상 프로필을 빌드하고 자동화된 B2B 마케팅 캠페인을 위해 [!DNL Salesforce Marketing Cloud Account Engagement]&#x200B;(으)로 내보낼 수 있습니다.

### 캠페인 자동화 {#use-case-campaign-automation}

Adobe Experience Platform에서 정의한 대상을 사용하여 [!DNL Salesforce Marketing Cloud Account Engagement]에서 마케팅 캠페인을 트리거할 수 있습니다. 타겟팅된 대상을 [!DNL Salesforce]&#x200B;(으)로 내보낸 후 이를 사용하여 이메일 캠페인을 실행하고 양성, 채점 및 캠페인 세분화를 통해 잠재 고객을 관리할 수 있습니다.

### 프로필 보강 {#use-case-profile-enrichment}

Adobe Experience Platform의 풍부한 고객 데이터를 통해 [!DNL Salesforce Marketing Cloud Account Engagement] 잠재 고객 프로필을 개선합니다. [!DNL Salesforce Marketing Cloud Account Engagement]에서 더 자세한 잠재 고객 레코드를 만들어 개선된 타기팅 및 개인화를 위해 포괄적인 프로필 특성을 내보냅니다.

## 전제 조건 {#prerequisites}

Experience Platform 및 [!DNL Salesforce]에서 설정해야 하는 필수 구성 요소와 [!DNL (V2) Marketing Cloud Account Engagement] 대상으로 작업하기 전에 수집해야 하는 정보는 아래 섹션을 참조하십시오.

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

[!DNL (V2) Marketing Cloud Account Engagement] 대상에 대한 데이터를 활성화하기 전에 [에서 만든 &#x200B;](/help/xdm/schema/composition.md)스키마[, &#x200B;](../../../catalog/datasets/overview.md)데이터 세트[&#x200B; 및 &#x200B;](../../../segmentation/types/overview.md)대상[!DNL Experience Platform]이 있어야 합니다.

### [!DNL Salesforce Marketing Cloud Account Engagement]개 필수 구성 요소 {#prerequisites-destination}

Experience Platform에서 [!DNL Marketing Cloud Account Engagement] 계정으로 데이터를 내보내려면 다음 전제 조건을 참고하십시오.

#### [!DNL Marketing Cloud Account Engagement] 계정이 있어야 합니다. {#prerequisites-account}

계속하려면 [!DNL Marketing Cloud Account Engagement]Marketing Cloud 계정 참여[&#x200B; 제품에 대한 구독이 있는 &#x200B;](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 계정이 필요합니다.

#### [!DNL Marketing Cloud Account Engagement] 자격 증명 수집 {#gather-credentials}

[!DNL (V2) Marketing Cloud Account Engagement] 대상에 인증하기 전에 아래 항목을 기록하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| **[!UICONTROL 계정 참여 사업부 ID]** | [!DNL Salesforce] 계정 참여 사업부 ID입니다. ID를 찾는 방법에 대해 알아보려면 Salesforce [설명서](https://help.salesforce.com/s/articleView?id=000381973&type=1)를 참조하세요. |

{style="table-layout:auto"}

## 지원되는 ID {#supported-identities}

[!DNL (V2) Marketing Cloud Account Engagement]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

이러한 식별자 중 하나를 사용하여 일치하는 항목이 발견되면 기존 Account Engagement 잠재 고객 레코드가 Adobe Experience Platform의 데이터로 업데이트됩니다. 일치하는 항목이 없으면 Account Engagement에서 새 Prospect Record 가 생성됩니다.

| 타겟 ID | 설명 | 고려 사항 |
|---|---|---|
| `matchId` | 계정 참여의 잠재 고객 ID | 이 세 가지 ID 중 하나 이상이 필요합니다 |
| `matchSalesforceId` | 잠재 고객의 Salesforce 리드/연락처 ID | 이 세 가지 ID 중 하나 이상이 필요합니다 |
| `matchEmail` | 잠재 고객의 이메일 주소 | 이 세 가지 ID 중 하나 이상이 필요합니다 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화번호, 성)*&#x200B;과(와) 함께 대상자의 모든 구성원을 내보냅니다.</li><li>이 대상은 Salesforce Import API v5를 사용하여 프로필 데이터의 일괄 내보내기를 지원합니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | <ul><li>**초기 내보내기**: 매핑 후 즉시 전체 내보내기</li><li>**후속 내보내기**: 3시간마다 증분 내보내기</li><li>이 일정은 수정되었으며 Alpha에서 사용자 지정할 수 없습니다.</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하세요.

![Salesforce Marketing Cloud 계정 참여 V2 대상 연결 워크플로](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/connect-to-destination.png "Salesforce Marketing Cloud 계정 참여 V2 대상 연결 워크플로")

[!DNL Salesforce] 로그인 페이지로 리디렉션됩니다. [!DNL Marketing Cloud Account Engagement] 계정 자격 증명을 입력하고 **[!UICONTROL 로그인]**&#x200B;을 선택합니다.

![Salesforce 로그인 페이지](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/salesforce-auth.png "Salesforce 로그인 페이지.")

**[!UICONTROL 허용]**&#x200B;을(를) 선택하여 **Adobe Experience Platform** 앱에 권한을 부여하여 [!DNL Salesforce Marketing Cloud Account Engagement] 계정에 액세스하세요. *한 번만 수행해야 합니다*.

![Salesforce 앱 스크린샷 확인 팝업으로 Marketing Cloud 계정에 대한 Experience Platform 앱 액세스 권한을 부여합니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/allow-app.png)

제공된 세부 정보가 유효하면 UI에 다음과 같은 메시지가 표시됩니다. *Salesforce Marketing Cloud 계정 참여 계정에 성공적으로 연결되었습니다* 및 **[!UICONTROL 연결됨]** 상태와 녹색 확인 표시가 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 참여 사업부 ID]**: [!DNL Salesforce] `Account Engagement Business Unit ID`.
* **[!UICONTROL 계정 참여 API]**: 계정 참여 API의 프로덕션(`https://pi.pardot.com`) 또는 데모(`https://pi.demo.pardot.com`) 끝점을 사용할지 여부를 선택합니다.
* **[!UICONTROL 계정 참여 캠페인 ID]**: 모든 [!DNL Account Engagement] 잠재 고객은 캠페인과 연결해야 합니다. 캠페인 ID를 설정하지 않은 경우, 기본값이 Salesforce 계정에 있으면 계정 참여에서 자동으로 ID를 할당하려고 시도합니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 매핑 고려 사항 및 예제 {#mapping-considerations-example}

Adobe Experience Platform에서 [!DNL (V2) Marketing Cloud Account Engagement] 대상으로 대상 데이터를 보내려면 XDM(Experience Data Model) 스키마 필드를 대상의 해당 필드에 매핑해야 합니다.

지원되는 필드의 전체 목록은 [Salesforce Prospect API v5 설명서](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)를 참조하십시오. [사용자 지정 필드](https://developer.salesforce.com/docs/marketing/pardot/guide/custom-field-v5.html)은(는) Alpha 릴리스에서 지원되지 않습니다.

#### 지원되는 속성 {#supported-attributes}

Salesforce Marketing Cloud 계정 참여 대상은 아래 표에 설명된 타겟 속성을 지원합니다.

| 속성 | 유형 | 설명 |
|---------|----------|----------|
| `salesforceId` | 문자열 | 잠재 고객의 Salesforce ID |
| `salesforceOwnerId` | 정수 | 잠재 고객 소유자의 Salesforce 사용자 ID |
| `salutation` | 문자열 | 잠재 고객의 인사말(예: Mr., Ms., Dr.) |
| `score` | 정수 | 고객 참여에서의 잠재 고객 점수 |
| `source` | 문자열 | 잠재 고객 레코드의 소스 |
| `state` | 문자열 | 잠재 고객의 시/도 |
| `territory` | 문자열 | 잠재 고객에게 할당된 지역 |
| `userId` | 정수 | 잠재 고객과 연관된 사용자 ID |
| `website` | 문자열 | 잠재 고객의 웹 사이트 URL |
| `yearsInBusiness` | 문자열 | 잠재 고객이 사업을 시작한 연도 수 |
| `zip` | 문자열 | 잠재 고객의 ZIP/우편 번호 |

#### 필수 매핑 {#required-mappings}

데이터 매핑을 시작하기 전에 아래의 필수 필드 매핑을 검토하십시오.

| 대상 필드 | 유형 | 필수 여부 | 사용 시기 |
|---|---|---|---|
| `email` | 속성 | 항상 필요함 | 잠재 고객의 이메일 주소입니다. `matchId` 또는 `matchSalesforceId`이(가) 없는 경우 계정 참여에서 잠재 고객 레코드를 찾아 일치시키기 위한 기본 식별자입니다. <br> **참고:** Account Engagement의 &quot;전자 메일 주소가 같은 여러 잠재 고객 허용&quot; 기능을 사용하면 전자 메일이 같은 잠재 고객이 여러 개 있는 경우 전자 메일에만 의존하면 모호해질 수 있습니다. 일반적으로 Account Engagement 는 이러한 경우 가장 최근 활동으로 잠재 고객을 업데이트하는 것으로 기본 설정됩니다. |
| `matchId` | ID | 이 세 가지 ID 중 하나 이상이 필요합니다 | Account Engagement에서 각 개별 잠재 고객 레코드에 대해 생성한 고유 식별자입니다. 계정 참여 잠재 고객 ID가 이미 있고, 특히 여러 잠재 고객이 동일한 이메일 주소를 공유하는 경우 업데이트가 올바른 잠재 고객에게 적용되도록 하려는 경우 이 ID를 사용하십시오. |
| `matchSalesforceId` | ID | 이 세 가지 ID 중 하나 이상이 필요합니다 | Salesforce 잠재 고객 또는 연락처의 Salesforce ID입니다. 잠재 고객이 이미 Salesforce과 동기화되어 계정 참여와 Salesforce 간에 데이터 일관성을 유지할 때 사용합니다. |
| `matchEmail` | ID | 이 세 가지 ID 중 하나 이상이 필요합니다 | 일치에 사용되는 잠재 고객의 이메일 주소입니다. 특정 계정 참여 잠재 고객 ID 또는 Salesforce ID가 없는 경우 대체 식별자로 사용하십시오. 참고: 여러 잠재 고객이 동일한 이메일 주소를 공유하는 경우 일반적으로 계정 참여는 가장 최근 활동으로 잠재 고객을 업데이트하는 것으로 기본 설정됩니다. |

아래 단계에 따라 올바른 필드를 매핑하십시오.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택합니다. 화면에 새 매핑 행이 표시됩니다.
1. **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 특성 선택]** 범주를 선택하고 XDM 특성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을 선택하고 ID를 선택합니다.
1. **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을(를) 선택하고 ID를 선택하거나 **[!UICONTROL 사용자 지정 특성 선택]** 범주를 선택하고 표준 계정 참여 잠재 필드 목록에서 지정합니다.

![XDM 필드 및 ID를 Salesforce Marketing Cloud 계정 참여 V2 필드에 매핑](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/mapping.png "XDM 필드 및 ID를 Salesforce Marketing Cloud 계정 참여 V2 필드에 매핑하는 예제")

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택한 대상 중 하나로 이동합니다. **[!DNL Activation data]** 탭을 선택합니다. **[!UICONTROL 매핑 ID]** 열에 [!DNL Marketing Cloud Account Engagement Prospects] 페이지 내에서 생성된 사용자 지정 필드의 이름이 표시됩니다.
   ![선택한 세그먼트에 대한 매핑 ID를 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/selected-segment-mapping-id.png)

1. [[!DNL Salesforce]](https://login.salesforce.com/) 웹 사이트에 로그인합니다. 그런 다음 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 페이지로 이동하여 대상자의 잠재 고객이 추가/업데이트되었는지 확인합니다. 또는 [[!DNL Account Engagement]](https://pi.pardot.com/)에 액세스하고 **[!DNL Prospects]** 페이지에 액세스할 수도 있습니다.
   ![잠재 고객 페이지를 보여주는 Salesforce UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospects.png)

1. 잠재 고객이 업데이트되었는지 확인하려면 잠재 고객을 선택하고 사용자 지정 잠재 고객 필드가 Experience Platform 대상 상태로 업데이트되었는지 확인합니다.
   ![선택한 잠재 고객 페이지를 보여 주는 Salesforce UI 스크린샷입니다. 사용자 지정 잠재 고객 필드가 대상 상태로 업데이트됩니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospect.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API 설명서](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)
* [Salesforce Import API v5 설명서](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)
* [Salesforce Prospect API v5 설명서](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)