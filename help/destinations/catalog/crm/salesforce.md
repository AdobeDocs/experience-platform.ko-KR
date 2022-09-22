---
keywords: crm;CRM;crm 대상;salesforce crm;salesforce crm 대상
title: Salesforce CRM 연결
description: Salesforce CRM 대상을 사용하면 계정 데이터를 내보내고 Salesforce CRM 내에서 활성화하여 비즈니스 요구 사항을 충족할 수 있습니다.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: b243a5f88cadc238ac3edd3bf45a54564598bbf0
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 1%

---

# [!DNL Salesforce CRM] 연결

## 개요 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) 는 널리 사용되는 CRM(고객 관계 관리) 플랫폼이며 다음을 지원합니다.

* [리드](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - 리드는 판매하는 제품이나 서비스에 관심이 있거나 관심이 없을 수 있는 사람 또는 회사의 이름입니다.
* [연락처](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - 연락처는 귀하의 대리인 중 한 명이 관계를 설정하고 잠재적 고객으로 자격을 부여받은 개인입니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)은 위에서 설명한 두 유형의 프로필을 모두 지원합니다.

When [세그먼트 활성화](#activate)로 지정하는 경우, 잠재 고객 또는 연락처 중에서 선택하고 속성 업데이트 및 세그먼트 데이터를으로 업데이트할 수 있습니다. [!DNL Salesforce CRM].

[!DNL Salesforce CRM] 에서는 Salesforce REST API와 통신하기 위해 암호 부여와 OAuth 2를 인증 메커니즘으로 사용합니다. 인증 지침 [!DNL Salesforce CRM] 인스턴스는 아래에 있습니다. [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성에 따라 사용자에게 개인화된 경험을 제공할 수 있습니다. 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 Salesforce CRM에 보내 Adobe Experience Platform에서 세그먼트와 프로필이 업데이트되는 즉시 사용자의 피드에 표시할 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

Salesforce CRM 대상에 데이터를 활성화하기 전에 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

### 의 사전 요구 사항 [!DNL Salesforce CRM] {#prerequisites-destination}

에서 다음 전제 조건을 확인합니다. [!DNL Salesforce CRM]를 입력하여 Platform에서 Salesforce 계정으로 데이터를 내보냅니다.

#### Salesforce 계정이 있어야 합니다. {#prerequisites-account}

Salesforce로 이동 [재판](https://www.salesforce.com/in/form/signup/freetrial-sales/) Salesforce 계정이 아직 없는 경우 등록하고 만들 페이지입니다.

#### 연결된 앱 구성 {#prerequisites-connected-app}

다음으로, [연결된 앱](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) Salesforce 계정 내에서, 아직 계정이 없는 경우

연결된 앱 내에서 [OAuth 설정](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 이 활성화되어 있습니다.

또한 [범위](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 아래에 언급된 항목이 선택되어 있습니다.

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

#### Salesforce 내에서 사용자 지정 필드 만들기 {#prerequisites-custom-field}

유형의 사용자 지정 필드 만들기 `Text Area Long`: 내에서 세그먼트 상태를 업데이트하는 데 사용할 Experience Platform [!DNL Salesforce CRM].
자세한 내용은 Salesforce 설명서 를 참조하십시오. [사용자 지정 필드 만들기](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) 추가 지침이 필요한 경우

>[!IMPORTANT]
>
>필드 이름에 공백 문자가 없는지 확인합니다. 대신 밑줄을 사용하십시오 `(_)` 문자를 구분 기호로 사용합니다.

>[!NOTE]
>
>* Salesforce의 개체는 25개의 외부 필드로 제한됩니다. 자세한 내용은 [사용자 지정 필드 속성](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* 이 제한은 언제든지 최대 25개의 Experience Platform 세그먼트 멤버십만 활성화할 수 있음을 의미합니다.
>* Salesforce 내에서 이 제한에 도달한 경우, 새 항목 전에 Experience Platform 내의 이전 세그먼트에 대한 세그먼트 상태를 저장하는 데 사용된 사용자 지정 특성을 Salesforce에서 제거해야 합니다 **[!UICONTROL 매핑 ID]** 사용할 수 있습니다.


자세한 내용은 Adobe Experience Platform 설명서 을 참조하십시오. [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

#### Salesforce 자격 증명 수집 {#gather-credentials}

를 인증하기 전에 아래 항목을 참고하십시오 [!DNL Salesforce CRM] 대상:

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| <ul><li>Salesforce 도메인 접두사</li></ul> | 자세한 내용은 [Salesforce 도메인 접두사](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 추가 지침 | <ul><li>도메인이 다음과 같은 경우 강조 표시된 값이 필요합니다.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>소비자 키</li><li>소비자 비밀</li></ul> | 자세한 내용은 [Salesforce 설명서](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 추가 지침이 필요한 경우 | <ul><li>r23kxxxxxxxx0z05xxxxxx</code></li><li>ipxxxxxxxxxxT4xxxxxxxxxx</code></li></ul> |

### 가드레일 {#guardrails}

Salesforce는 요청, 비율 및 시간 제한 제한을 적용하여 트랜잭션 로드 잔액을 조정합니다. 자세한 내용은 [API 요청 제한 및 할당](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 자세한 내용

>[!IMPORTANT]
>
>When [세그먼트 활성화](#activate) 다음 중 하나를 선택해야 합니다. *연락처* 또는 *리드* 유형. 세그먼트에 선택한 유형에 따라 적절한 데이터 매핑이 있는지 확인해야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Salesforce CRM] 은 아래 표에 설명된 id 업데이트를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| `SalesforceId` | 다음 [!DNL Salesforce CRM] 세그먼트를 통해 내보내거나 업데이트하는 연락처 또는 리드 ID의 식별자입니다. | 필수입니다 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> 의 각 세그먼트 상태 [!DNL Salesforce CRM] 은(는) **[!UICONTROL 매핑 ID]** 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example) 단계.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL Salesforce CRM]. 또는 **[!UICONTROL CRM]** 카테고리.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

![인증 방법을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL 암호]**: Salesforce 계정 암호입니다.
* **[!UICONTROL 사용자 지정 도메인]**: Salesforce 도메인입니다.
* **[!UICONTROL 클라이언트 ID]**: Salesforce에 연결된 앱 소비자 키입니다.
* **[!UICONTROL 클라이언트 암호]**: Salesforce가 연결된 앱 소비자 암호입니다.
* **[!UICONTROL 사용자 이름]**: Salesforce 계정 사용자 이름입니다.

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태에서 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 Platform UI 스크린샷.](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Salesforce ID 유형]**: 선택 **[!UICONTROL 연락처]** 내보내거나 업데이트하려는 ID가 유형인 경우 *연락처*. 선택 **[!UICONTROL 리드]** 내보내거나 업데이트하려는 ID가 유형인 경우 *리드*.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 매핑 고려 사항 및 예 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 로 올바로 보내려면 [!DNL Salesforce CRM] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다. XDM 필드를 [!DNL Salesforce CRM] 대상 필드: 다음 단계를 수행합니다.

1. 에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**이면 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑 추가에 대한 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. 에서 **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]** 또는 **[!UICONTROL 속성 선택]** 카테고리를 선택하고 `crmID`.
   ![소스 매핑에 대한 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/source-mapping.png)

1. 에서 **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]** 카테고리를 선택하고 `SalesforceId`.
   ![SalesforceId에 대한 Target 매핑을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

   * XDM 프로필 스키마와 프로필 스키마 사이에 다음 매핑을 추가합니다 [!DNL Salesforce CRM] 인스턴스:
   | XDM 프로필 스키마 | [!DNL Salesforce CRM] 인스턴스 | 필수입니다 |
   |---|---|---|
   | `crmID` | `SalesforceId` | 예 |

   * **[!UICONTROL 사용자 지정 속성 선택]**: 소스 필드를 **[!UICONTROL 속성 이름]** 필드. 자세한 내용은 [[!DNL Salesforce CRM] 설명서](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) 를 참조하십시오.
      ![LastName에 대한 Target 매핑을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

   * 작업 중인 경우 *연락처* 세그먼트 내에서 Salesforce의 개체 참조 를 참조하십시오 [연락처](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 업데이트할 필드에 대한 매핑을 정의하려면
   * 단어를 검색하여 필수 필드를 식별할 수 있습니다 *필수 여부*- 위의 링크에 있는 필드 설명에 나와 있습니다.
   * 내보내거나 업데이트할 필드에 따라 XDM 프로필 스키마와 사용자 간에 매핑을 추가합니다 [!DNL Salesforce CRM] 인스턴스:

   | XDM 프로필 스키마 | [!DNL Salesforce CRM] 인스턴스 | 참고 |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required` 질문에 답합니다. 연락처의 성은 최대 80자입니다. |
   | `person.name.firstName` | `FirstName` | 연락처의 이름은 최대 40자입니다. |
   | `personalEmail.address` | `Email` | 연락처의 이메일 주소입니다. |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
      ![Target 매핑을 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   * 작업 중인 경우 *리드* 세그먼트 내에서 Salesforce의 개체 참조 를 참조하십시오 [리드](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 업데이트할 필드에 대한 매핑을 정의하려면
   * 단어를 검색하여 필수 필드를 식별할 수 있습니다 *필수 여부*- 위의 링크에 있는 필드 설명에 나와 있습니다.
   * 내보내거나 업데이트할 필드에 따라 XDM 프로필 스키마와 사용자 간에 매핑을 추가합니다 [!DNL Salesforce CRM] 인스턴스:

   | XDM 프로필 스키마 | [!DNL Salesforce CRM] 인스턴스 | 참고 |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required` 질문에 답합니다. 연락처의 성은 최대 80자입니다. |
   | `b2b.companyName` | `Company` | `Required` 질문에 답합니다. 납의 회사입니다. |
   | `personalEmail.address` | `Email` | 연락처의 이메일 주소입니다. |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
      ![Target 매핑을 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/mappings-leads.png)




### 세그먼트 내보내기 예약 및 예제 {#schedule-segment-export-example}

다음을 수행할 때 [세그먼트 내보내기 예약](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계는 Platform 세그먼트를 Salesforce의 사용자 지정 필드 속성에 수동으로 매핑해야 합니다.

이렇게 하려면 각 세그먼트를 선택한 다음 Salesforce의 해당 사용자 지정 필드 속성을 **[!UICONTROL 매핑 ID]** 필드.

>[!IMPORTANT]
>
>* 에 사용되는 값 **[!UICONTROL 매핑 ID]** 는 Salesforce 내에서 만든 사용자 지정 필드 속성의 이름과 정확히 일치해야 합니다.
>* Salesforce에서 만든 사용자 지정 필드 특성의 이름이 공백 문자를 사용하지 않는지 확인합니다.


예는 다음과 같습니다.
![Platform UI 스크린샷 예 - 세그먼트 내보내기 예약](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
   ![찾아보기 대상을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 대상을 선택하고 상태가 맞는지 확인합니다 **[!UICONTROL 활성화됨]**.
   ![대상 데이터 흐름 실행을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 로 전환 **[!UICONTROL 활성화 데이터]** 탭을 클릭한 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내에서 생성된 수에 해당하는지 확인합니다.
   ![세그먼트를 보여주는 Platform UI 스크린샷 예.](../../assets/catalog/crm/salesforce/segment.png)

1. 마지막으로 Salesforce 웹 사이트에 로그인하고 세그먼트의 프로필이 추가되었는지 또는 업데이트되었는지 확인합니다.
   * 만약 *연락처* platform 세그먼트 내에서 **[!DNL Apps]** > **[!DNL Contacts]** 페이지.
      ![Salesforce CRM 스크린샷에서는 세그먼트의 프로필이 있는 연락처 페이지를 보여줍니다.](../../assets/catalog/crm/salesforce/contacts.png)

   * 선택 *연락처* 및 필드가 업데이트되었는지 확인합니다. 에서 각 세그먼트 상태를 확인할 수 있습니다. [!DNL Salesforce CRM] 이(가) **[!UICONTROL 매핑 ID]** 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example).
      ![업데이트된 세그먼트 상태가 있는 연락처 세부 사항 페이지를 보여주는 Salesforce CRM 스크린샷입니다.](../../assets/catalog/crm/salesforce/contact-info.png)

   * 만약 *리드* platform 세그먼트 내에서 **[!DNL Apps]** > **[!DNL Leads]** 페이지.
      ![세그먼트의 프로필이 있는 리드 페이지를 보여주는 Salesforce CRM 스크린샷입니다.](../../assets/catalog/crm/salesforce/leads.png)

   * 선택 *리드* 및 필드가 업데이트되었는지 확인합니다. 에서 각 세그먼트 상태를 확인할 수 있습니다. [!DNL Salesforce CRM] 이(가) **[!UICONTROL 매핑 ID]** 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example).
      ![업데이트된 세그먼트 상태가 있는 리드 세부 사항 페이지를 보여주는 Salesforce CRM 스크린샷입니다.](../../assets/catalog/crm/salesforce/lead-info.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### 이벤트를 대상으로 푸시하는 동안 알 수 없는 오류가 발생했습니다. {#unknown-errors}

데이터 흐름 실행을 확인할 때 다음 오류 메시지가 표시되는 경우 `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![오류를 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/error.png)

이 오류를 해결하려면 **[!UICONTROL 매핑 ID]** 에 제공됨 [!DNL Salesforce CRM] 플랫폼 세그먼트가 유효하며 다음 내에 있음 [!DNL Salesforce CRM].

## 추가 리소스 {#additional-resources}

유용한 추가 정보는 [Salesforce 개발자 포털](https://developer.salesforce.com/) 아래와 같습니다.
* [빠른 시작](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [레코드 만들기](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [사용자 지정 권장 사항 대상](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [복합 리소스 사용](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 이 대상은 [여러 레코드 업로드](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API 대신 [단일 레코드 업데이트](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API 호출.