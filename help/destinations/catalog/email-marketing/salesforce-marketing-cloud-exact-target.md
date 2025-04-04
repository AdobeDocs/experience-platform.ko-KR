---
title: (API) Salesforce Marketing Cloud 연결
description: Salesforce Marketing Cloud(이전의 ExactTarget) 대상을 사용하면 계정 데이터를 내보내고 비즈니스 요구 사항에 맞게 Salesforce Marketing Cloud 내에서 활성화할 수 있습니다.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 2%

---

# [!DNL (API) Salesforce Marketing Cloud] 연결

## 개요 {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/)&#x200B;(이전 이름: [!DNL ExactTarget])은(는) 방문자와 고객이 자신의 경험을 개인화할 수 있도록 여정을 만들고 사용자 지정할 수 있는 디지털 마케팅 세트입니다.

>[!IMPORTANT]
>
> 이 연결과 전자 메일 마케팅 카탈로그 섹션 내에 있는 다른 [[!DNL Salesforce Marketing Cloud] 연결](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 간의 차이점을 참고하십시오. 다른 Salesforce Marketing Cloud 연결을 사용하면 파일을 지정된 저장소 위치로 내보낼 수 있지만 이 연결은 API 기반 스트리밍 연결입니다.

**B2B** 마케팅을 지향하는 [!DNL Salesforce Marketing Cloud Account Engagement]과(와) 비교하여 [!DNL (API) Salesforce Marketing Cloud] 대상은 트랜잭션 의사 결정 주기가 짧은 **B2C** 사용 사례에 이상적입니다. 타겟 대상의 행동을 나타내는 더 큰 데이터 세트를 통합하여 연락처, 특히 [!DNL Salesforce] 외부의 데이터 세트에서 우선 순위를 지정하고 세그먼트화하여 마케팅 캠페인을 조정하고 개선할 수 있습니다. *참고: Experience Platform에도 [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)에 대한 연결이 있습니다.*

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) [!DNL Salesforce Marketing Cloud] [연락처 업데이트](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API를 사용하므로 새 [!DNL Salesforce Marketing Cloud] 세그먼트 내에서 연락처를 활성화한 후 비즈니스 요구 사항에 대해 **연락처를 추가하고 연락처 데이터를 업데이트**&#x200B;할 수 있습니다.

[!DNL Salesforce Marketing Cloud]은(는) 클라이언트 자격 증명이 포함된 OAuth 2를 인증 메커니즘으로 사용하여 [!DNL Salesforce Marketing Cloud] API와 통신합니다. [!DNL Salesforce Marketing Cloud] 인스턴스에 대한 인증 지침은 [대상에 대한 인증](#authenticate) 섹션에서 아래에 더 나와 있습니다.

## 사용 사례 {#use-cases}

[!DNL (API) Salesforce Marketing Cloud] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 마케팅 캠페인을 위해 연락처에 이메일 보내기 {#use-case-send-emails}

홈 임대 플랫폼의 판매 부서에서 마케팅 이메일을 타겟팅된 고객 대상자에게 브로드캐스트하려고 합니다. 플랫폼의 마케팅 팀은 Adobe Experience Platform을 통해 새 연락처를 추가하고 기존 연락처 *(및 해당 이메일 주소)*&#x200B;을(를) 업데이트하고, 자신의 오프라인 데이터에서 대상을 만들고, 이러한 대상을 [!DNL Salesforce Marketing Cloud]에 보낼 수 있습니다. 그런 다음 마케팅 캠페인 이메일을 보내는 데 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform의 사전 요구 사항 {#prerequisites-in-experience-platform}

[!DNL (API) Salesforce Marketing Cloud] 대상에 대한 데이터를 활성화하기 전에 [!DNL Experience Platform]에서 만든 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)가 있어야 합니다.

### [!DNL (API) Salesforce Marketing Cloud]의 필수 구성 요소 {#prerequisites-destination}

Experience Platform에서 [!DNL Salesforce Marketing Cloud] 계정으로 데이터를 내보내려면 다음 전제 조건을 참고하십시오.

#### [!DNL Salesforce Marketing Cloud] 계정이 있어야 합니다. {#prerequisites-account}

계속하려면 [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) 제품에 대한 구독이 있는 [!DNL Salesforce Marketing Cloud] 계정이 필요합니다.

[!DNL Salesforce Marketing Cloud] 계정이 없거나 계정에 [!DNL Marketing Cloud Engagement] 제품 구독이 없는 경우 [[!DNL Salesforce] 지원](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10)에 문의하세요.

#### [!DNL Salesforce Marketing Cloud] 내 특성 만들기 {#prerequisites-attribute}

대상을 [!DNL (API) Salesforce Marketing Cloud] 대상으로 활성화할 때 **[대상 일정](#schedule-segment-export-example)** 단계에서 활성화된 각 대상에 대해 **[!UICONTROL 매핑 ID]** 필드에 값을 입력해야 합니다.

[!DNL Salesforce]에서는 Experience Platform에서 들어오는 대상을 올바르게 읽고 해석하고 [!DNL Salesforce Marketing Cloud] 내에서 대상 상태를 업데이트하려면 이 값이 필요합니다. 대상 상태에 대한 지침이 필요한 경우 [대상 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md)에 대한 Experience Platform 설명서를 참조하십시오.

Experience Platform에서 [!DNL Salesforce]까지 활성화하는 각 대상에 대해 [!DNL Salesforce Marketing Cloud] 내의 [!DNL Email Demographics] 데이터 확장에 연결된 `Text` 유형의 특성이 있어야 합니다. 특성을 만들려면 [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder]을(를) 사용합니다. 특성 만들기에 대한 지침이 필요한 경우 [!DNL Salesforce Marketing Cloud] 설명서를 참조하여 [특성 만들기](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US)를 참조하세요.

특성 필드 이름은 **[!UICONTROL 매핑]** 단계 동안 [!DNL (API) Salesforce Marketing Cloud] 대상 필드에 사용됩니다. 비즈니스 요구 사항에 따라 최대 4000자로 필드 문자를 정의할 수 있습니다. 특성 유형에 대한 자세한 내용은 [!DNL Salesforce Marketing Cloud] [데이터 확장 데이터 유형](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) 설명서 페이지를 참조하십시오.

특성을 추가할 [!DNL Salesforce Marketing Cloud]의 데이터 디자이너 화면의 예는 다음과 같습니다.
![Salesforce Marketing Cloud UI 데이터 디자이너](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

[!DNL Email Demographics] 데이터 확장 내의 대상 상태에 해당하는 특성이 있는 [!DNL Salesforce Marketing Cloud] [!DNL Email Data] 특성 그룹의 보기가 아래에 표시되어 있습니다.
![Salesforce Marketing Cloud UI 전자 메일 데이터 특성 그룹](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

[!DNL (API) Salesforce Marketing Cloud] 대상은 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html)를 사용하여 [!DNL Salesforce Marketing Cloud] 내에 정의된 데이터 확장과 연결된 특성을 동적으로 검색합니다.

워크플로우에서 [매핑](#mapping-considerations-example)을(를) [대상에 대한 대상을 활성화](#activate)(으)로 설정할 때 **[!UICONTROL 대상 필드]** 선택 창에 표시됩니다.

>[!IMPORTANT]
>
> [!DNL Salesforce Marketing Cloud] 내에서 활성화된 각 Experience Platform 세그먼트에 대해 **[!UICONTROL 매핑 ID]** 내에 지정된 값과 정확히 일치하는 **[!UICONTROL 필드 이름]**&#x200B;을(를) 가진 특성을 만들어야 합니다. 예를 들어 아래 스크린샷에는 이름이 `salesforce_mc_segment_1`인 특성이 표시됩니다. 대상을 이 대상으로 활성화할 때 `salesforce_mc_segment_1`을(를) **[!UICONTROL 매핑 ID]**(으)로 추가하여 Experience Platform의 대상 대상을 이 특성에 채웁니다.

[!DNL Salesforce Marketing Cloud]에서 특성을 만든 예는 다음과 같습니다.
![특성을 표시하는 Salesforce Marketing Cloud UI 스크린샷.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * 속성을 만들 때 필드 이름에 공백 문자를 포함하지 마십시오. 대신 밑줄 `(_)` 문자를 구분 기호로 사용하십시오.
> * Experience Platform 대상에 사용되는 특성과 [!DNL Salesforce Marketing Cloud] 내의 다른 특성을 구별하기 위해 Adobe 세그먼트에 사용되는 특성에 인식 가능한 접두사 또는 접미사를 포함할 수 있습니다. 예를 들어 `test_segment` 대신 `Adobe_test_segment` 또는 `test_segment_Adobe`을(를) 사용합니다.
> * [!DNL Salesforce Marketing Cloud]에 다른 특성이 이미 만들어져 있는 경우 Experience Platform 세그먼트와 동일한 이름을 사용하여 [!DNL Salesforce Marketing Cloud]의 대상자를 쉽게 식별할 수 있습니다.

#### [!DNL Salesforce Marketing Cloud] 내에서 사용자 역할 및 권한 할당 {#prerequisites-roles-permissions}

[!DNL Salesforce Marketing Cloud]은(는) 사용 사례에 따라 사용자 지정 역할을 지원하므로 [!DNL Salesforce Marketing Cloud] 내에서 특성을 업데이트하려면 사용자에게 관련 역할을 할당해야 합니다. 사용자에게 할당된 역할의 예는 다음과 같습니다.
![할당된 역할을 표시하는 선택한 사용자에 대한 Salesforce Marketing Cloud UI.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

[!DNL Salesforce Marketing Cloud] 사용자가 할당된 역할에 따라 업데이트하려는 필드에 연결된 [!DNL Salesforce Marketing Cloud] 데이터 확장에 대한 권한도 할당해야 합니다.

이 대상을 사용하려면 `[!DNL data extension]`에 액세스해야 하므로 이를 허용해야 합니다. 예를 들어 `Email` [!DNL data extension]의 경우 아래와 같이 허용해야 합니다.

![허용된 사용 권한을 가진 전자 메일 데이터 확장을 표시하는 Salesforce Marketing Cloud UI](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

액세스 수준을 제한하려면 세분화된 권한을 사용하여 개별 액세스를 재정의할 수도 있습니다.
![세분화된 권한을 가진 전자 메일 데이터 확장을 표시하는 Salesforce Marketing Cloud UI](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

자세한 지침은 [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) 및 [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) 페이지를 참조하세요.

#### [!DNL Salesforce Marketing Cloud] 자격 증명 수집 {#gather-credentials}

[!DNL (API) Salesforce Marketing Cloud] 대상에 인증하기 전에 아래 항목을 적어 두십시오.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 하위 도메인 | [!DNL Salesforce Marketing Cloud] 인터페이스에서 이 값을 가져오는 방법을 알아보려면 [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html)을(를) 참조하세요. | [!DNL Salesforce Marketing Cloud] 도메인이 <br>인 경우 *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>값으로 `mcq4jrssqdlyc4lph19nnqgzzs84`을(를) 제공해야 합니다. |
| 클라이언트 ID | [!DNL Salesforce Marketing Cloud] 인터페이스에서 이 값을 가져오는 방법을 알아보려면 [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html)를 참조하세요. | r23kxxxxxxxx0z05xxxxxx |
| 클라이언트 암호 | [!DNL Salesforce Marketing Cloud] 인터페이스에서 이 값을 가져오는 방법을 알아보려면 [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html)를 참조하세요. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### 가드레일 {#guardrails}

* Salesforce은 특정 [등급 제한](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html)을 적용합니다.
   * 실행 중에 발생할 수 있는 가능한 제한을 해결하고 오류를 줄이려면 [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html)를 참조하세요.
   * *전체 버전 비교 차트를 다운로드*&#x200B;하려면 [[!DNL Salesforce Marketing Cloud] 참여 가격](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 페이지를 참조하세요. 이 PDF는 플랜에 의해 적용된 제한에 대해 자세히 설명합니다.
   * [API 개요](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 페이지에서 추가 제한을 자세히 설명합니다.
   * 이러한 세부 정보를 대조하는 페이지에 대해서는 [여기](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits)를 참조하세요.
* 오브젝트당 허용되는 *사용자 정의 필드*&#x200B;의 수는 Salesforce 버전에 따라 다릅니다.
   * 자세한 지침은 [!DNL Salesforce] [설명서](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5)를 참조하세요.
   * [!DNL Salesforce Marketing Cloud] 내의 *개체 당 허용되는 사용자 정의 필드*&#x200B;에 대해 정의된 한도에 도달한 경우 다음을 수행해야 합니다.
      * [!DNL Salesforce Marketing Cloud]에 새 특성을 추가하기 전에 이전 특성을 제거하십시오.
      * [대상 예약](#schedule-segment-export-example) 단계 동안 이러한 이전 특성 이름을 **[!UICONTROL 매핑 ID]**&#x200B;에 제공된 값으로 사용하는 Experience Platform 대상에서 활성화된 대상을 업데이트하거나 제거합니다.

## 지원되는 ID {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] 연락처 키. 추가 지침이 필요한 경우 [!DNL Salesforce Marketing Cloud] [설명서](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5)를 참조하세요. | 필수 |

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화 번호, 성)*&#x200B;과(와) 함께 세그먼트의 모든 멤버를 내보냅니다.</li><li> [대상 예약](#schedule-segment-export-example) 단계 동안 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 [!DNL Salesforce Marketing Cloud]의 각 세그먼트 상태가 Experience Platform의 해당 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
> 대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL (API) Salesforce Marketing Cloud]을(를) 검색합니다. 또는 **[!UICONTROL 이메일 마케팅]** 범주에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 아래의 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오. 자세한 내용은 [수집 [!DNL Salesforce Marketing Cloud] 자격 증명](#gather-credentials) 섹션을 참조하십시오.

| [!DNL (API) Salesforce Marketing Cloud] 대상 | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL 하위 도메인]** | [!DNL Salesforce Marketing Cloud] 도메인 접두사입니다. <br>예를 들어 도메인이 <br>인 경우 *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> 값으로 `mcq4jrssqdlyc4lph19nnqgzzs84`을(를) 제공해야 합니다. |
| **[!UICONTROL 클라이언트 ID]** | 내 [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL 클라이언트 암호]** | 내 [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Salesforce Marketing Cloud에 인증하는 방법을 보여 주는 Experience Platform UI 스크린샷](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

제공된 세부 정보가 유효하면 UI에 녹색 확인 표시와 함께 **[!UICONTROL 연결됨]** 상태가 표시됩니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
대상 세부 정보를 표시하는 ![Experience Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
> * 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
> * *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 매핑 고려 사항 및 예제 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 [!DNL (API) Salesforce Marketing Cloud] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야합니다. 매핑은 Experience Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 스키마 필드 간에 링크를 작성하는 것으로 구성됩니다.

XDM 필드를 [!DNL (API) Salesforce Marketing Cloud] 대상 필드에 올바르게 매핑하려면 아래 단계를 따르십시오.

>[!IMPORTANT]
>
> * 특성 이름은 [!DNL Salesforce Marketing Cloud] 계정에 따라 다르지만 `contactKey` 및 `personalEmail.address`에 대한 매핑은 필수입니다.
>
> * [!DNL Salesforce Marketing Cloud] API와의 통합에는 Experience Platform이 Salesforce에서 검색할 수 있는 특성 수에 대한 페이지 매김 제한이 적용됩니다. 즉, **[!UICONTROL 매핑]** 단계 동안 대상 필드 스키마에 Salesforce 계정의 최대 2000개의 특성이 표시될 수 있습니다.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**를 선택합니다. 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑 추가를 위한 Experience Platform UI 스크린샷 예](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 특성 선택]** 범주를 선택하고 XDM 특성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을 선택하고 ID를 선택합니다.
1. **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을(를) 선택하고 ID를 선택하거나 **[!UICONTROL 특성 선택]** 범주를 선택하고 필요에 따라 표시되는 데이터 확장에서 특성을 선택합니다. [!DNL (API) Salesforce Marketing Cloud] 대상은 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html)를 사용하여 [!DNL Salesforce Marketing Cloud] 내에 정의된 데이터 확장과 연결된 특성을 동적으로 검색합니다. [대상 활성화 워크플로](#activate)에서 [매핑](#mapping-considerations-example)을(를) 설정할 때 **[!UICONTROL 대상 필드]** 팝업에 표시됩니다.

   * XDM 프로필 스키마와 [!DNL (API) Salesforce Marketing Cloud] 사이에 다음 매핑을 추가하려면 다음 단계를 반복합니다.

     | 소스 필드 | 대상 필드 | 필수 |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses] 데이터 확장의 `Attribute: Email Address`. | 새 연락처를 추가할 때 `Mandatory`. |
     | `xdm: person.name.firstName` | 원하는 [!DNL Salesforce Marketing Cloud] 데이터 확장의 `Attribute: First Name`. | - |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
     ![Target 매핑을 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

대상 연결에 대한 매핑을 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

### 대상자 내보내기 예약 및 예제 {#schedule-segment-export-example}

[대상 내보내기 예약](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계를 수행할 때 Experience Platform 대상을 [!DNL Salesforce Marketing Cloud]의 [특성](#prerequisites-attribute)에 수동으로 매핑해야 합니다.

이렇게 하려면 각 세그먼트를 선택한 다음 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 매핑 ID]** 필드에 [!DNL Salesforce Marketing Cloud]의 특성 이름을 입력하십시오. [!DNL Salesforce Marketing Cloud]에서 특성을 만드는 방법에 대한 지침과 모범 사례를 보려면 [다음 항목 내에서 특성 만들기 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 섹션을 참조하십시오.

예를 들어 [!DNL Salesforce Marketing Cloud] 특성이 `salesforce_mc_segment_1`인 경우 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 매핑 ID]**&#x200B;에 이 값을 지정하여 Experience Platform의 대상 대상을 이 특성으로 채웁니다.

[!DNL Salesforce Marketing Cloud]의 예제 특성이 아래에 표시되어 있습니다.
![특성을 표시하는 Salesforce Marketing Cloud UI 스크린샷.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

[!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 매핑 ID]**&#x200B;의 위치를 나타내는 예는 다음과 같습니다.

대상자 내보내기 일정을 보여 주는 ![Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

표시된 대로 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 매핑 ID]**&#x200B;는 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 필드 이름]** 내에 지정된 값과 정확히 일치해야 합니다.

활성화된 각 Experience Platform 세그먼트에 대해 이 섹션을 반복합니다.

위에 표시된 이미지를 기반으로 한 일반적인 예는 다음과 같을 수 있습니다.

| [!DNL (API) Salesforce Marketing Cloud] 세그먼트 이름 | [!DNL Salesforce Marketing Cloud] **[!UICONTROL 필드 이름]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 매핑 ID]** |
| --- | --- | --- |
| salesforce mc 대상 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| salesforce mc 대상 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 대상 목록으로 이동하려면 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**를 선택하십시오.
   ![찾아보기 대상을 표시하는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. 대상을 선택하고 상태가 **[!UICONTROL 활성화됨]**인지 확인하십시오.
   ![대상 데이터 흐름이 실행되는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. **[!DNL Activation data]** 탭으로 전환한 다음 대상 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. 대상자 요약을 모니터링하고 프로필 수가 세그먼트 내에서 만든 수에 해당하는지 확인합니다.
   ![세그먼트를 표시하는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) 웹 사이트에 로그인합니다. 그런 다음 **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** 페이지로 이동하여 대상자의 프로필이 추가되었는지 확인합니다.
   ![세그먼트에서 사용된 프로필이 있는 연락처 페이지를 보여 주는 Salesforce Marketing Cloud UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. 프로필이 업데이트되었는지 확인하려면 **[!UICONTROL 이메일]** 페이지로 이동하여 대상자의 프로필에 대한 특성 값이 업데이트되었는지 확인하십시오. 성공하면 [대상 예약](#schedule-segment-export-example) 단계에서 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 [!DNL Salesforce Marketing Cloud]의 각 대상 상태가 Experience Platform의 해당 대상 상태로 업데이트되었음을 확인할 수 있습니다.
   ![선택한 연락처 전자 메일 페이지에 업데이트된 대상 상태를 표시하는 Salesforce Marketing Cloud UI 스크린샷](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### 이벤트를 Salesforce Marketing Cloud에 푸시하는 동안 알 수 없는 오류 발생 {#unknown-errors}

* 데이터 흐름 실행을 확인할 때 다음 오류 메시지가 표시될 수 있습니다. `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![오류를 표시하는 Experience Platform UI 스크린샷](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * 이 오류를 수정하려면 활성화 워크플로에서 [!DNL (API) Salesforce Marketing Cloud] 대상에 제공한 **[!UICONTROL 매핑 ID]**&#x200B;이(가) [!DNL Salesforce Marketing Cloud]에서 만든 특성의 이름과 정확히 일치하는지 확인하십시오. 자세한 내용은  [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 섹션 내의 [특성 만들기를 참조하세요.

* 세그먼트를 활성화할 때 다음 오류 메시지가 표시될 수 있습니다. `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 이 오류를 해결하려면 [!DNL Salesforce Marketing Cloud] 계정 관리자에게 문의하여 [!DNL Salesforce Marketing Cloud] 계정의 신뢰할 수 있는 IP 범위에 [Experience Platform IP 주소](/help/destinations/catalog/streaming/ip-address-allow-list.md)를 추가하십시오. 추가 지침이 필요한 경우 [!DNL Salesforce Marketing Cloud] [Marketing Cloud의 허용 목록에 포함할 IP 주소](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) 설명서를 참조하십시오.

## 추가 리소스 {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* 연락처가 지정된 정보로 업데이트되는 방법을 설명하는 [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html).

### 변경 로그 {#changelog}

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 10월 | 설명서 업데이트 | <ul><li>(API) Salesforce Marketing Cloud](#prerequisites-destination)의 [필수 구성 요소 섹션을 업데이트했으며 일반적으로 문서에서 특성 그룹에 대한 불필요한 참조를 제거했습니다.</li> <li>대상 상태에 대한 특성을 [!DNL Email Demographics] 데이터 확장 내의 [!DNL Salesforce Marketing Cloud] 내에서만 만들어야 함을 나타내도록 설명서를 업데이트했습니다.</li> <li>[매핑 고려 사항 및 예제](#mapping-considerations-example) 섹션 내의 매핑 테이블을 업데이트했습니다. `Email Addresses` 데이터 확장 내의 `Email Address` 특성에 대한 매핑은 필수로 표시되어 있습니다. 이 요구 사항은 중요로 표시된 호출에서 언급되었지만 테이블에서 생략되었습니다.</li></ul> |
| 2023년 4월 | 설명서 업데이트 | <ul><li>[!DNL Salesforce Marketing Cloud Engagement]이(가) 이 대상을 사용하기 위한 필수 구독임을 호출하기 위해 [API(Salesforce Marketing Cloud)의 필수 구성 요소](#prerequisites-destination) 섹션의 문 및 참조 링크를 수정했습니다. 계속하려면 사용자가 Marketing Cloud **Account** Engagement에 대한 구독이 필요하다는 섹션이 잘못 호출되었습니다.</li> <li>[역할 및 권한](#prerequisites-roles-permissions)을(를) [필수 구성 요소](#prerequisites) 아래에 이 대상의 [!DNL Salesforce] 사용자에게 할당할 섹션을 추가했습니다. (PLATIR-26299)</li></ul> |
| 2023년 2월 | 설명서 업데이트 | [!DNL Salesforce Marketing Cloud Engagement]이(가) 이 대상을 사용하기 위한 필수 구독임을 호출하는 참조 링크를 포함하도록 (API) Salesforce Marketing Cloud](#prerequisites-destination)의 [필수 구성 요소 섹션을 업데이트했습니다. |
| 2023년 2월 | 기능 업데이트 | 대상에서 잘못된 구성으로 인해 잘못된 포맷의 JSON이 Salesforce으로 전송되는 문제가 해결되었습니다. 이로 인해 일부 사용자는 활성화 시 많은 ID가 실패했음을 보게 되었습니다. (PLATIR-26299) |
| 2023년 1월 | 설명서 업데이트 | <ul><li>[!DNL Salesforce]측에서 특성을 만들어야 함을 호출하기 위해  [!DNL Salesforce]](#prerequisites-destination)의 [필수 구성 요소 섹션을 업데이트했습니다. 이제 이 섹션에는 [!DNL Salesforce]에서 특성 이름을 지정하는 방법에 대한 자세한 지침과 모범 사례가 포함되어 있습니다. (PLATIR-25602)</li><li>[대상 예약](#schedule-segment-export-example) 단계에서 활성화된 각 대상에 대해 매핑 ID를 사용하는 방법에 대한 명확한 지침을 추가했습니다. (PLATIR-25602)</li></ul> |
| 2022년 10월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서 게시. |

{style="table-layout:auto"}

+++
