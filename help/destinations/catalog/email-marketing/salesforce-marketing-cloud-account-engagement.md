---
title: Salesforce Marketing Cloud 계정 참여
description: Salesforce Marketing Cloud 계정 참여(이전의 Pardot) 대상을 사용하여 계정 데이터를 내보내고 Salesforce Marketing Cloud 계정 참여 내에서 비즈니스 요구 사항에 맞게 활성화하는 방법을 알아봅니다.
last-substantial-update: 2023-04-14T00:00:00Z
source-git-commit: 65feb905bfa7d663d1d463d94af428a04dc55b01
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 연결

를 사용하십시오 [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(이전에는 [!DNL Pardot])* 리드 캡처, 추적, 점수 및 등급 지정 대상. 또한 이메일 드립 캠페인 및 교육, 점수 책정 및 캠페인 세그멘테이션을 통해 타겟팅된 시장 세그먼트 및 고객 그룹에 대한 파이프라인의 모든 단계에 대한 리드 트랙을 디자인할 수 있습니다.

비교 대상 [!DNL Salesforce Marketing Cloud Engagement] 어느 쪽이 더 **B2C** 마케팅, [!DNL Marketing Cloud Account Engagement] 에 이상적입니다. **B2B** 판매 및 의사 결정 주기를 더 오래 필요로 하는 여러 부서 및 의사 결정자와 관련된 사용 사례 또한 CRM과 보다 가까운 근접성 및 통합을 유지하여 적절한 판매 및 마케팅 결정을 내릴 수 있습니다. *참고: Experience Platform에 [!DNL Salesforce Marketing Cloud Engagement]로 이동하여 [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 및 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 페이지.*

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 엔드포인트, 종료 **리드 추가 또는 업데이트** 활성화한 후 [!DNL Marketing Cloud Account Engagement] 세그먼트.

[!DNL Marketing Cloud Account Engagement] 는 인증 코드 프로토콜을 사용하여 OAuth 2를 사용하여 [!DNL Account Engagement] API. 인증 지침 [!DNL Marketing Cloud Account Engagement] 인스턴스는 아래에 있습니다. [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Marketing Cloud Account Engagement] 대상은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 마케팅 캠페인을 위해 연락처에 전자 메일 보내기 {#use-case-send-emails}

온라인 플랫폼의 마케팅 부서는 이메일 기반 마케팅 캠페인을 B2B 리드의 선별된 대상자에게 방송하려고 합니다. 플랫폼의 마케팅 팀은 Adobe Experience Platform을 통해 새로운 리드를 추가하거나 기존 리드 정보를 업데이트하고 고유한 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 로 보낼 수 있습니다 [!DNL Marketing Cloud Account Engagement]: 마케팅 캠페인 이메일을 전송하는 데 사용할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

Experience Platform에서 설정해야 하는 사전 요구 사항에 대해서는 아래 섹션을 참조하십시오. [!DNL Salesforce] 작업 전에 수집해야 하는 정보를 [!DNL Marketing Cloud Account Engagement] 대상.

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

데이터를 로 활성화하기 전에 [!DNL Marketing Cloud Account Engagement] 대상, [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

### 의 사전 요구 사항 [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Platform에서 사용자 [!DNL Marketing Cloud Account Engagement] 계정:

#### 다음을 수행해야 합니다 [!DNL Marketing Cloud Account Engagement] account {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] 을 구독하는 계정 [Marketing Cloud 계정 참여](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 제품을 계속 진행해야 합니다.

사용자 [!DNL Salesforce] 계정에는 [!DNL Salesforce] `Account Engagement Administrator role`. 이것은 다음 경우에 필요합니다 [사용자 지정 잠재 고객 필드 만들기](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

마지막으로 계정에 액세스할 수도 있어야 합니다 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

에 연결 [[!DNL Salesforce] 지원](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 또는 [!DNL Salesforce] 계정이 없거나 계정에 [!DNL Marketing Cloud Account Engagement] 구독 또는 [!DNL Account Engagement Administrator role].

#### 수집 [!DNL Marketing Cloud Account Engagement] 자격 증명 {#gather-credentials}

를 인증하기 전에 아래 항목을 참고하십시오 [!DNL Marketing Cloud Account Engagement] 대상.

| 자격 증명 | 설명 |
| --- | --- |
| `Username` | 사용자 [!DNL Marketing Cloud Account Engagement] 계정 사용자 이름. |
| `Password` | 사용자 [!DNL Marketing Cloud Account Engagement] 계정 암호입니다. |
| `Account Engagement Business Unit ID` | 계정 참여 비즈니스 단위 ID를 찾으려면 [!DNL Salesforce]. 설정에서 을 입력합니다. *비즈니스 단위 설정* 를 클릭합니다. 계정 참여 비즈니스 단위 ID는 `0Uv` 은 18자입니다. 비즈니스 단위 설정 정보에 액세스할 수 없는 경우 [!DNL Salesforce] 계정 관리자가 `Account Engagement Business Unit ID`. 추가 지침이 필요한 경우 [[!DNL Salesforce] 인증](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 지침 페이지. |

{style="table-layout:auto"}

### 가드레일 {#guardrails}

자세한 내용은 [!DNL Marketing Cloud Account Engagement] [비율 제한](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) 계획에 의해 적용되는 제한을 자세히 설명하고 Experience Platform 실행에도 적용됩니다.

>[!IMPORTANT]
>
>만약 [!DNL Salesforce] 계정 관리자가 신뢰할 수 있는 IP 범위에 대한 액세스 권한을 제한하므로 액세스 권한을 받으려면 해당 관리자에게 문의해야 합니다 [Experience Platform IP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 허용 목록에추가된. 자세한 내용은 [!DNL Salesforce] [연결된 앱에 대한 신뢰할 수 있는 IP 범위에 대한 액세스 제한](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 추가 지침이 필요한 경우 설명서

## 지원되는 ID {#supported-identities}

[!DNL Marketing Cloud Account Engagement] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 잠재 고객 이메일 주소 | 필수입니다 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> Platform에서 선택한 각 세그먼트에 대해 해당 [!DNL Salesforce Marketing Cloud Account Engagement] 세그먼트 상태는 Platform의 세그먼트 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**, 검색 [!DNL Salesforce Marketing Cloud Account Engagement]. 또는 **[!UICONTROL 이메일 마케팅]** 카테고리.

### 대상에 인증 {#authenticate}

대상을 인증하려면 **[!UICONTROL 대상에 연결]**. 로 이동합니다. [!DNL Salesforce] 로그인 페이지. 을(를) 입력합니다. [!DNL Marketing Cloud Account Engagement] 계정 자격 증명 및 [!DNL Log In].

![Marketing Cloud 계정 참여를 인증하는 방법을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

다음, 선택 [!UICONTROL 허용] 다음에 대한 권한을 제공하는 다음 창에서 **Adobe Experience Platform** 앱 액세스 [!DNL Salesforce Marketing Cloud Account Engagement] 계정이 필요합니다. *이 작업은 한 번만 수행해야 합니다*.

![Salesforce 앱 스크린샷 확인 팝업을 통해 Experience Platform 앱에 Marketing Cloud 계정 참여에 대한 액세스 권한을 제공합니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

제공된 세부 정보가 유효한 경우 UI에 메시지가 표시됩니다. *Salesforce Marketing Cloud 계정 참여 계정에 연결했습니다* 메시지 및 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태에서 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다. 자세한 내용은 [수집 [!DNL Marketing Cloud Account Engagement] 자격 증명](#gather-credentials) 섹션을 참조하십시오.

![대상 세부 사항을 보여주는 Platform UI 스크린샷.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 필드 | 설명 |
| --- | --- |
| **[!UICONTROL 이름]** | 나중에 이 대상을 인식하는 이름입니다. |
| **[!UICONTROL 설명]** | 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다. |
| **[!UICONTROL 계정 참여 비즈니스 단위 ID]** | 사용자 [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 매핑 고려 사항 및 예 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 로 올바로 보내려면 [!DNL Marketing Cloud Account Engagement] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다.

XDM 필드를 [!DNL Marketing Cloud Account Engagement] 대상 필드에서 아래 단계를 수행합니다.

1. 에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 화면에 새 매핑 행이 표시됩니다.
1. 에서 **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 속성 선택]** 카테고리를 선택하고 XDM 속성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]** id를 선택합니다.
1. 에서 **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]** ID를 선택하거나 **[!UICONTROL 사용자 지정 속성 선택]** 카테고리 및 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 사용 가능한 스키마에서 확인하십시오.

   * XDM 프로필 스키마와 [!DNL Marketing Cloud Account Engagement]: | 소스 필드 | Target 필드 | 필수 | | — | — | — | |`IdentityMap: Email`|`Identity: email`| 예 | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * 위의 매핑에 대한 예는 다음과 같습니다.
      ![Target 매핑을 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

대상 연결에 대한 매핑 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택한 세그먼트 중 하나로 이동합니다. **[!DNL Activation data]** 탭을 선택합니다. 다음 **[!UICONTROL 매핑 ID]** 열에는 [!DNL Marketing Cloud Account Engagement Prospects] 페이지.
   ![선택한 세그먼트에 대한 매핑 ID를 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 에 로그인합니다. [[!DNL Salesforce]](https://login.salesforce.com/) 웹 사이트입니다. 그런 다음 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 페이지의 잠재 고객을 확인하고 세그먼트의 잠재 고객이 추가/업데이트되었는지 확인합니다. 또는 액세스 권한도 있습니다 [[!DNL Salesforce Pardot]](https://pi.pardot.com/) 액세스 **[!DNL Prospects]** 페이지.
   ![Salesforce UI 스크린샷으로 Represents 페이지를 표시합니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 잠재 고객이 업데이트되었는지 확인하려면 잠재 고객을 선택하고 사용자 지정 잠재 고객 필드가 Experience Platform 세그먼트 상태로 업데이트되었는지 확인합니다.
   ![선택한 Prospect 페이지를 보여주는 Salesforce UI 스크린샷에서는 사용자 지정 Prospect 필드가 세그먼트 상태로 업데이트됩니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API 설명서](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).