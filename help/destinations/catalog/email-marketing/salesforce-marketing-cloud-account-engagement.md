---
title: Salesforce Marketing Cloud 계정 참여
description: Salesforce Marketing Cloud 계정 참여(이전의 Pardot) 대상을 사용하여 계정 데이터를 내보내고 비즈니스 요구 사항에 맞게 Salesforce Marketing Cloud 계정 참여 내에서 활성화하는 방법에 대해 알아봅니다.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 연결

[[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(이전 이름: [!DNL Pardot])* 대상을 사용하여 잠재 고객을 캡처, 추적, 점수 매기기 및 등급을 매기십시오. 또한 이메일 드립 캠페인 및 육성, 채점 및 캠페인 세분화를 통한 리드 관리를 통해 타겟팅된 시장 대상자 및 고객 그룹에 대한 파이프라인의 모든 단계에 대한 리드 트랙을 디자인할 수 있습니다.

**B2C** 마케팅을 지향하는 [!DNL Salesforce Marketing Cloud Engagement]과(와) 비교하여 [!DNL Marketing Cloud Account Engagement]은(는) 더 긴 영업 및 의사 결정 주기를 필요로 하는 여러 부서 및 의사 결정자를 포함하는 **B2B** 사용 사례에 이상적입니다. 또한 CRM과의 긴밀한 근접성과 통합을 유지하여 적절한 판매 및 마케팅 결정을 내릴 수 있습니다. *참고: Experience Platform에 [!DNL Salesforce Marketing Cloud Engagement]에 대한 연결도 있습니다. [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 및 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 페이지에서 확인할 수 있습니다.*

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) 새 [!DNL Marketing Cloud Account Engagement] 세그먼트 내에서 리드를 활성화한 후 **리드를 추가 또는 업데이트**&#x200B;하기 위해 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 끝점을 활용합니다.

[!DNL Marketing Cloud Account Engagement]은(는) 인증 코드 프로토콜이 있는 OAuth 2를 사용하여 [!DNL Account Engagement] API에 인증합니다. [!DNL Marketing Cloud Account Engagement] 인스턴스에 대한 인증 지침은 [대상에 대한 인증](#authenticate) 섹션에서 아래에 더 나와 있습니다.

## 사용 사례 {#use-cases}

[!DNL Marketing Cloud Account Engagement] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 마케팅 캠페인을 위해 연락처에 이메일 보내기 {#use-case-send-emails}

온라인 플랫폼의 마케팅 부서는 이메일 기반 마케팅 캠페인을 B2B 리드의 엄선된 대상자에게 브로드캐스트하려고 합니다. 플랫폼의 마케팅 팀은 Adobe Experience Platform을 통해 새 리드를 추가하거나 기존 리드 정보를 업데이트하고, 자체 오프라인 데이터에서 대상을 작성한 다음 해당 대상을 [!DNL Marketing Cloud Account Engagement]에 보낼 수 있습니다. 그런 다음 마케팅 캠페인 이메일을 보내는 데 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

Experience Platform 및 [!DNL Salesforce]에서 설정해야 하는 필수 구성 요소와 [!DNL Marketing Cloud Account Engagement] 대상으로 작업하기 전에 수집해야 하는 정보는 아래 섹션을 참조하십시오.

### Experience Platform의 사전 요구 사항 {#prerequisites-in-experience-platform}

[!DNL Marketing Cloud Account Engagement] 대상에 대한 데이터를 활성화하기 전에 [!DNL Experience Platform]에서 만든 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)가 있어야 합니다.

### [!DNL Marketing Cloud Account Engagement]의 필수 구성 요소 {#prerequisites-destination}

Experience Platform에서 [!DNL Marketing Cloud Account Engagement] 계정으로 데이터를 내보내려면 다음 전제 조건을 참고하십시오.

#### [!DNL Marketing Cloud Account Engagement] 계정이 있어야 합니다. {#prerequisites-account}

계속하려면 [Marketing Cloud 계정 참여](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 제품에 대한 구독이 있는 [!DNL Marketing Cloud Account Engagement] 계정이 필요합니다.

[!DNL Salesforce] 계정에 [!DNL Salesforce] `Account Engagement Administrator role`이(가) 있어야 합니다. [사용자 지정 잠재 고객 필드를 만들기](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5)하려면 필요합니다.

마지막으로, 계정에서도 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5)에 액세스할 수 있습니다.

계정이 없거나 계정에 [!DNL Marketing Cloud Account Engagement] 구독 또는 [!DNL Account Engagement Administrator role]이 없는 경우 [[!DNL Salesforce] 지원](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 또는 [!DNL Salesforce] 계정 관리자에게 문의하세요.

#### [!DNL Marketing Cloud Account Engagement] 자격 증명 수집 {#gather-credentials}

[!DNL Marketing Cloud Account Engagement] 대상에 인증하기 전에 아래 항목을 적어 두십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `Username` | [!DNL Marketing Cloud Account Engagement] 계정 사용자 이름입니다. |
| `Password` | [!DNL Marketing Cloud Account Engagement] 계정 암호입니다. |
| `Account Engagement Business Unit ID` | 계정 참여 비즈니스 단위 ID를 찾으려면 [!DNL Salesforce]에서 설정을 사용하십시오. 설정에서 [빠른 찾기] 상자에 *사업부 설정*&#x200B;을 입력합니다. 계정 참여 비즈니스 단위 ID는 `0Uv`부터 18자까지 사용할 수 있습니다. 사업부 설정 정보에 액세스할 수 없는 경우 [!DNL Salesforce] 계정 관리자에게 `Account Engagement Business Unit ID`을(를) 제공해 달라고 요청하십시오. 추가 지침이 필요한 경우 [[!DNL Salesforce] 인증](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 지침 페이지를 참조하세요. |

{style="table-layout:auto"}

### 가드레일 {#guardrails}

플랜에 의해 적용된 제한을 자세히 설명하고 Experience Platform 실행에도 적용되는 [!DNL Marketing Cloud Account Engagement] [비율 제한](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits)을 참조하세요.

>[!IMPORTANT]
>
>[!DNL Salesforce] 계정 관리자가 신뢰할 수 있는 IP 범위에 대한 액세스를 제한한 경우 해당 관리자에게 연락하여 [Experience Platform IP](/help/destinations/catalog/streaming/ip-address-allow-list.md)를 허용 목록에추가된으로 받아야 합니다. 추가 지침이 필요한 경우 [!DNL Salesforce] [연결된 앱에 대한 신뢰할 수 있는 IP 범위에 대한 액세스 제한](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 설명서를 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Marketing Cloud Account Engagement]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 잠재 고객 이메일 주소 | 필수 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화 번호, 성)*&#x200B;과(와) 함께 세그먼트의 모든 멤버를 내보냅니다.</li><li> Experience Platform에서 선택한 각 대상에 대해 해당 [!DNL Salesforce Marketing Cloud Account Engagement] 세그먼트 상태가 Experience Platform의 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL Salesforce Marketing Cloud Account Engagement]을(를) 검색합니다. 또는 **[!UICONTROL 이메일 마케팅]** 범주에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하세요. [!DNL Salesforce] 로그인 페이지로 이동합니다. [!DNL Marketing Cloud Account Engagement] 계정 자격 증명을 입력하고 [!DNL Log In]을(를) 선택하십시오.

![Marketing Cloud 계정 참여를 인증하는 방법을 보여 주는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

그런 다음 후속 창에서 [!UICONTROL 허용]을(를) 선택하여 **Adobe Experience Platform** 앱에 [!DNL Salesforce Marketing Cloud Account Engagement] 계정에 액세스할 수 있는 권한을 부여합니다. *이 작업은 한 번만 수행해야 합니다*.

![Salesforce 앱 스크린샷 확인 팝업으로 Marketing Cloud 계정에 대한 Experience Platform 앱 액세스 권한을 부여합니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

제공된 세부 정보가 유효하면 UI에 다음과 같은 메시지가 표시됩니다. *Salesforce Marketing Cloud 계정 참여 계정에 성공적으로 연결되었습니다* 메시지와 **[!UICONTROL 연결됨]** 상태를 녹색 확인 표시로 표시합니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다. 자세한 내용은 [수집 [!DNL Marketing Cloud Account Engagement] 자격 증명](#gather-credentials) 섹션을 참조하십시오.

대상 세부 정보를 표시하는 ![Experience Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 필드 | 설명 |
| --- | --- |
| **[!UICONTROL 이름]** | 나중에 이 대상을 인식할 수 있는 이름입니다. |
| **[!UICONTROL 설명]** | 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다. |
| **[!UICONTROL 계정 참여 사업부 ID]** | 내 [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 매핑 고려 사항 및 예제 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 [!DNL Marketing Cloud Account Engagement] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야합니다. 매핑은 Experience Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 스키마 필드 간에 링크를 작성하는 것으로 구성됩니다.

XDM 필드를 [!DNL Marketing Cloud Account Engagement] 대상 필드에 올바르게 매핑하려면 아래 단계를 따르십시오.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택합니다. 화면에 새 매핑 행이 표시됩니다.
1. **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 특성 선택]** 범주를 선택하고 XDM 특성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을 선택하고 ID를 선택합니다.
1. **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을(를) 선택하고 ID를 선택하거나 **[!UICONTROL 사용자 지정 특성 선택]** 범주를 선택하고 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 목록에서 사용 가능한 스키마를 지정합니다.

   * XDM 프로필 스키마와 [!DNL Marketing Cloud Account Engagement] 사이에 매핑을 추가하려면 다음 단계를 반복합니다.

     | 소스 필드 | 대상 필드 | 필수 |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | 예 |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * 위 매핑의 예가 아래에 나와 있습니다.
     ![Target 매핑을 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

대상 연결에 대한 매핑을 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택한 대상 중 하나로 이동합니다. **[!DNL Activation data]** 탭을 선택합니다. **[!UICONTROL 매핑 ID]** 열에 [!DNL Marketing Cloud Account Engagement Prospects] 페이지 내에서 생성된 사용자 지정 필드의 이름이 표시됩니다.
   ![선택한 세그먼트에 대한 매핑 ID를 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. [[!DNL Salesforce]](https://login.salesforce.com/) 웹 사이트에 로그인합니다. 그런 다음 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 페이지로 이동하여 대상자의 잠재 고객이 추가/업데이트되었는지 확인합니다. 또는 [[!DNL Salesforce Pardot]](https://pi.pardot.com/)에 액세스하고 **[!DNL Prospects]** 페이지에 액세스할 수도 있습니다.
   ![잠재 고객 페이지를 보여주는 Salesforce UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 잠재 고객이 업데이트되었는지 확인하려면 잠재 고객을 선택하고 사용자 지정 잠재 고객 필드가 Experience Platform 대상 상태로 업데이트되었는지 확인합니다.
   ![선택한 잠재 고객 페이지를 보여 주는 Salesforce UI 스크린샷입니다. 사용자 지정 잠재 고객 필드가 대상 상태로 업데이트됩니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API 설명서](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
