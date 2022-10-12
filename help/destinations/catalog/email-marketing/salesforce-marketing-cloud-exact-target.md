---
keywords: 이메일;이메일;이메일;이메일 대상;salesforce;api salesforce marketing cloud 대상
title: (API) Salesforce Marketing Cloud 연결
description: Salesforce Marketing Cloud(이전의 ExactTarget) 대상을 사용하면 계정 데이터를 내보내고 Salesforce Marketing Cloud 내에서 활성화하여 비즈니스 요구 사항을 충족할 수 있습니다.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2c778fe087a04261c79b9daf8579666cd0794eb4
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] 연결

## 개요 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (이전에는 [!DNL ExactTarget])은 방문자 및 고객이 자신의 경험을 개인화할 수 있는 여정을 작성하고 사용자 지정할 수 있는 디지털 마케팅 세트입니다.

>[!IMPORTANT]
>
>이 연결과 다른 연결의 차이점을 확인합니다 [[!DNL Salesforce Marketing Cloud] 연결](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 이메일 마케팅 카탈로그 섹션에 있습니다. 다른 Salesforce Marketing Cloud 연결을 사용하면 파일을 지정된 저장소 위치로 내보낼 수 있지만 API 기반 스트리밍 연결입니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [!DNL Salesforce Marketing Cloud] [연락처 업데이트](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API: 새로운 기능 내에서 연락처 데이터를 활성화한 후 비즈니스 요구에 대한 연락처 데이터를 추가/업데이트할 수 있습니다 [!DNL Salesforce Marketing Cloud] 세그먼트.

[!DNL Salesforce Marketing Cloud] 는 와 통신하기 위해 클라이언트 자격 증명과 함께 OAuth 2를 인증 메커니즘으로 사용합니다 [!DNL Salesforce Marketing Cloud] API. 인증 지침 [!DNL Salesforce Marketing Cloud] 인스턴스는 아래에 있습니다. [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Salesforce Marketing Cloud] 대상은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 마케팅 캠페인을 위해 연락처에 전자 메일 보내기 {#use-case-send-emails}

주택 임대 플랫폼의 판매부에서는 대상 고객 대상으로 마케팅 이메일을 방송하려고 합니다. 플랫폼의 마케팅 팀은 새 연락처를 추가하거나 기존 연락처를 업데이트할 수 있습니다 *(및 해당 이메일 주소)* Adobe Experience Platform을 통해 고유한 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 로 보냅니다 [!DNL Salesforce Marketing Cloud]: 마케팅 캠페인 이메일을 전송하는 데 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

데이터를 로 활성화하기 전에 [!DNL Salesforce Marketing Cloud] 대상, [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

### 의 사전 요구 사항 [!DNL Salesforce Marketing Cloud] {#prerequisites-destination}

Platform에서 사용자 [!DNL Salesforce Marketing Cloud] 계정:

#### 다음을 수행해야 합니다 [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

연락하여 [!DNL Salesforce Account Executive] 에 가입하다 [!DNL Salesforce Marketing Cloud Account Engagement] 아직 가지고 있지 않다면 제품을 선택하십시오.

#### 내에서 사용자 지정 필드 만들기 [!DNL Salesforce Marketing Cloud] {#prerequisites-custom-field}

유형의 사용자 지정 속성을 만들어야 합니다 `Text Area Long`: 내에서 세그먼트 상태를 업데이트하는 데 사용할 Experience Platform [!DNL Salesforce Marketing Cloud]. 세그먼트를 대상에 활성화하는 워크플로우에서 **[세그먼트 예약](#schedule-segment-export-example)** 1단계에서는 사용자 지정 속성을 **[!UICONTROL 매핑 ID]** 각 세그먼트에 대해 을 활성화하면 됩니다.

자세한 내용은 [!DNL Salesforce Marketing Cloud] 설명서 [사용자 지정 필드 만들기](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 추가 지침이 필요한 경우

>[!IMPORTANT]
>
> 에서 사용자 지정 속성을 만들어야 합니다 `Email Demographics` 사용자 내에서 속성 설정 [!DNL Salesforce Marketing Cloud] 계정이 필요합니다.

자세한 내용은 Adobe Experience Platform 설명서 을 참조하십시오. [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

#### Salesforce 자격 증명 수집 {#gather-credentials}

를 인증하기 전에 아래 항목을 참고하십시오 [!DNL Salesforce Marketing Cloud] 대상.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| <ul><li>[!DNL Salesforce Marketing Cloud] prefix로 인해 영구적으로 지정되는 Mbox 매개 변수입니다</li></ul> | 자세한 내용은 [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) 추가 지침 | <ul><li>도메인이 다음과 같은 경우 강조 표시된 값이 필요합니다.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com</i></li></ul> |
| <ul><li>클라이언트 ID</li><li>클라이언트 암호</li></ul> | 자세한 내용은 [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 추가 지침이 필요한 경우 | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 의 제한 [!DNL Salesforce Marketing Cloud] {#limits}

* Salesforce에서는 [비율 제한](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * 자세한 내용은 [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) 발생할 수 있는 모든 가능한 제한을 해결하고 실행 중에 오류를 줄일 수 있습니다.
   * 자세한 내용은 [[!DNL Salesforce Marketing Cloud] 참여 가격 책정](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 페이지 대상 *전체 버전 비교 차트 다운로드* 계획에 의해 적용되는 제한을 자세히 설명하는 pdf입니다.
   * 다음 [API 개요](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 페이지 세부 사항 추가 제한.
   * 참조 [여기](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) 를 입력합니다.
* 개수 *개체당 허용되는 사용자 지정 필드* 는 Salesforce 버전에 따라 다릅니다.
   * 자세한 내용은 [!DNL Salesforce] [설명서](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) 추가 지침
   * 에 정의된 제한에 도달한 경우 *개체당 허용되는 사용자 지정 필드* within [!DNL Salesforce Marketing Cloud] 다음을 수행해야 합니다.
      * 에서 새 사용자 지정 필드를 추가하기 전에 이전 사용자 지정 필드를 제거합니다. [!DNL Salesforce Marketing Cloud].
      * 이러한 이전 사용자 지정 필드 이름을 에 제공된 값으로 사용하는 Platform의 대상을 업데이트하거나 제거합니다 **[!UICONTROL 매핑 ID]** 그 동안 [세그먼트 예약](#schedule-segment-export-example) 단계.

## 지원되는 ID {#supported-identities}

[!DNL Salesforce Marketing Cloud] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] 연락처 키 자세한 내용은 [!DNL Salesforce Marketing Cloud] [설명서](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) 추가 지침이 필요한 경우 | 필수입니다 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> 의 각 세그먼트 상태 [!DNL Salesforce Marketing Cloud] 은(는) **[!UICONTROL 매핑 ID]** 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example) 단계.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**, 검색 [!DNL (API) Salesforce Marketing Cloud]. 또는 **[!UICONTROL 이메일 마케팅]** 카테고리.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.
![Salesforce Marketing Cloud 인증 방법을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL 하위 도메인]**: 사용자 [!DNL Salesforce Marketing Cloud] 도메인 접두사. 예를 들어 도메인이 *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*&#x200B;를 채울 때는 강조 표시된 값이 필요합니다.
* **[!UICONTROL 클라이언트 ID]**: 사용자 [!DNL Salesforce Marketing Cloud] 클라이언트 ID.
* **[!UICONTROL 클라이언트 암호]**: 사용자 [!DNL Salesforce Marketing Cloud] 클라이언트 암호.

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태에서 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 Platform UI 스크린샷.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 매핑 고려 사항 및 예 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 로 올바로 보내려면 [!DNL Salesforce Marketing Cloud] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다. XDM 필드를 [!DNL Salesforce Marketing Cloud] 대상 필드에서 아래 단계를 수행합니다.

>[!IMPORTANT]
>
>하지만 속성 이름은 [!DNL Salesforce Marketing Cloud] 계정, 두 계정 모두에 대한 매핑 `contactKey` 및 `personalEmail.address` 는 필수입니다.

1. 에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑 추가에 대한 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. 에서 **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 속성 선택]** 카테고리를 선택하고 `contactKey`.
   ![소스 매핑에 대한 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. 에서 **[!UICONTROL 대상 필드 선택]** 창에서 소스 필드를 매핑할 대상 필드의 유형을 선택합니다.
   * **[!UICONTROL ID 네임스페이스 선택]**: 목록에서 소스 필드를 id 네임스페이스에 매핑하려면 이 옵션을 선택합니다.
      ![salesforceContactKey에 대한 Target 매핑을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

   * XDM 프로필 스키마와 프로필 스키마 사이에 다음 매핑을 추가합니다 [!DNL Salesforce Marketing Cloud] 인스턴스: |XDM 프로필 스키마|[!DNL Salesforce Marketing Cloud] 인스턴스| 필수| |—|—|—| |`contactKey`|`salesforceContactKey`| 예 |

   * **[!UICONTROL 사용자 지정 속성 선택]**: 소스 필드를 **[!UICONTROL 속성 이름]** 필드. 을(를) 참조하십시오. [!DNL Salesforce Marketing Cloud] [설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) 를 참조하십시오. 또한 대상에서 [Salesforce 검색 속성 집합 정의 REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) Salesforce 내에 정의된 연락처 및 계정별 특성을 검색하려면
      ![Target 매핑을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

   * 예를 들어 업데이트할 값에 따라 XDM 프로필 스키마와 프로필 스키마 사이에 다음 매핑을 추가합니다 [!DNL Salesforce Marketing Cloud] 인스턴스: |XDM 프로필 스키마|[!DNL Salesforce Marketing Cloud] 인스턴스| |—|—| |`person.name.firstName`|`Email Demographics.First Name`| |`personalEmail.address`|`Email Addresses.Email Address`|

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
      ![Target 매핑을 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### 세그먼트 내보내기 예약 및 예제 {#schedule-segment-export-example}

다음을 수행할 때 [세그먼트 내보내기 예약](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계별로 Platform 세그먼트를 [사용자 지정 속성](#prerequisites-custom-field) Salesforce에서

이렇게 하려면 각 세그먼트를 선택한 다음 Salesforce의 해당 사용자 지정 속성을 **[!UICONTROL 매핑 ID]** 필드.

>[!IMPORTANT]
>
>매핑 ID에 사용된 값은 &quot;이메일 인구 통계&quot; 속성 세트 아래의 Salesforce 내에서 생성된 사용자 지정 속성의 이름과 정확히 일치해야 합니다.

예는 다음과 같습니다.
![Platform UI 스크린샷 예 - 세그먼트 내보내기 예약](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
   ![찾아보기 대상을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. 대상을 선택하고 상태가 맞는지 확인합니다 **[!UICONTROL 활성화됨]**.
   ![대상 데이터 흐름 실행을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. 로 전환 **[!DNL Activation data]** 탭을 클릭한 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내에서 생성된 수에 해당하는지 확인합니다.
   ![세그먼트를 보여주는 Platform UI 스크린샷 예.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. 에 로그인합니다. [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) 웹 사이트입니다. 그런 다음 **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** 페이지를 방문하여 세그먼트의 프로필이 추가되었는지 확인합니다.
   ![Salesforce Marketing Cloud UI 스크린샷에서는 세그먼트에 사용된 프로필이 있는 연락처 페이지를 보여줍니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. 업데이트된 프로필이 있는지 확인하려면 **[!UICONTROL 이메일]** 페이지를 표시하고 세그먼트의 프로필에 대한 속성 값이 업데이트되었는지 확인합니다. 성공하면 다음을 통해 각 세그먼트 상태를 확인할 수 있습니다 [!DNL Salesforce Marketing Cloud] 이(가) **[!UICONTROL 매핑 ID]** 에 제공된 값 [세그먼트 예약](#schedule-segment-export-example) 단계.
   ![Salesforce Marketing Cloud UI 스크린샷에서는 업데이트된 세그먼트 상태가 있는 선택한 연락처 이메일 페이지를 보여줍니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### Salesforce Marketing Cloud에 이벤트를 푸시하는 동안 알 수 없는 오류가 발생했습니다 {#unknown-errors}

데이터 흐름 실행을 확인할 때 다음 오류 메시지가 표시될 수 있습니다. `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![오류를 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

이 오류를 해결하려면 **[!UICONTROL 매핑 ID]** 당신이 [!DNL Salesforce Marketing Cloud] 플랫폼 세그먼트가 유효하며 다음 내에 있음 [!DNL Salesforce Marketing Cloud].

## 추가 리소스 {#additional-resources}

* [[!DNL Salesforce Marketing Cloud] API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
