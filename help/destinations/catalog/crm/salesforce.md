---
keywords: crm;CRM;crm 대상;salesforce crm;salesforce crm 대상
title: Salesforce CRM 연결
description: Salesforce CRM 대상을 사용하면 계정 데이터를 내보내고 Salesforce CRM 내에서 활성화하여 비즈니스 요구 사항을 충족할 수 있습니다.
source-git-commit: 154cca31c5b434a2f036773ef9cda088f84eb1e5
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 2%

---


# [!DNL Salesforce CRM] 연결

## 개요 {#overview}

[Salesforce CRM](https://www.salesforce.com/) 는 자주 사용하는 CRM(고객 관계 관리) 플랫폼입니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts): 세그먼트 내의 ID를 Salesforce CRM으로 업데이트할 수 있습니다.

Salesforce CRM은 Salesforce REST API와 통신하기 위해 암호 부여와 OAuth 2를 인증 메커니즘으로 사용합니다. Salesforce CRM 인스턴스를 인증하는 지침은 아래에 나와 있습니다. [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성에 따라 사용자에게 개인화된 경험을 제공할 수 있습니다. 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 Salesforce CRM에 보내 Adobe Experience Platform에서 세그먼트와 프로필이 업데이트되는 즉시 사용자의 피드에 표시할 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

Salesforce CRM 대상에 데이터를 활성화하기 전에 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

### Salesforce CRM의 사전 요구 사항 {#prerequisites-destination}

Platform에서 Salesforce 계정으로 데이터를 내보내려면 Salesforce에서 다음 사전 요구 사항을 참고하십시오.

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

유형의 사용자 지정 필드 만들기 `Text Area Long` Salesforce CRM 내에서 세그먼트 상태를 업데이트하는 데 사용할 Experience Platform입니다.
자세한 내용은 Salesforce 설명서 를 참조하십시오. [사용자 지정 필드 만들기](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) 추가 지침이 필요한 경우

>[!IMPORTANT]
>
> 필드 이름에 공백 문자가 없는지 확인합니다. 대신 밑줄을 사용하십시오 `(_)` 문자를 구분 기호로 사용합니다.

>[!NOTE]
>
> * Salesforce의 개체는 25개의 외부 필드로 제한됩니다. 자세한 내용은 [사용자 지정 필드 속성](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
> * 이 제한은 언제든지 최대 25개의 Experience Platform 세그먼트 멤버십을 활성화할 수 있음을 의미합니다.
> * Salesforce 내에서 이 제한에 도달한 경우, 새 mappingId를 사용하기 전에 Experience Platform 내의 이전 세그먼트에 대해 세그먼트 상태를 저장하는 데 사용된 사용자 지정 특성을 Salesforce에서 제거해야 합니다.


자세한 내용은 Adobe Experience Platform 설명서 을 참조하십시오. [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

#### Salesforce 자격 증명 수집 {#gather-credentials}

Salesforce CRM 대상을 인증하기 전에 아래 항목을 참고하십시오.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| <ul><li>Salesforce 도메인 접두사</li></ul> | 자세한 내용은 [Salesforce 도메인 접두사](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 추가 지침 | <ul><li>도메인이 다음과 같은 경우 강조 표시된 값이 필요합니다.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>소비자 키</li><li>소비자 비밀</li></ul> | 자세한 내용은 [Salesforce 설명서](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 추가 지침이 필요한 경우 | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxx</li></ul> |

## 지원되는 ID {#supported-identities}

Salesforce CRM은 아래 표에 설명된 ID 업데이트를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| SalesforceId | 모든 ID의 매핑을 지원하는 사용자 지정 Salesforce CRM 식별자입니다. | 필수입니다. 임의의 [id](../../../identity-service/namespaces.md) 변환 후 [!DNL Salesforce CRM] 대상에 매핑하기만 하면 됩니다 `SalesforceId`. |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> 플랫폼 세그먼트 상태는 로 내보내집니다 [!DNL Salesforce CRM] 에 해당 사용자 지정 필드 속성을 지정합니다. [!DNL Salesforce CRM] 에서 **[!UICONTROL 대상 활성화]** > **[!UICONTROL 세그먼트 내보내기 예약]** > **[!UICONTROL 매핑 ID]** 필드.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

![카탈로그](../../assets/catalog/crm/salesforce/catalog.png)

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

![Salesforce CRM에 인증하는 방법을 보여주는 샘플 스크린샷](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL 암호]**: Salesforce 계정 암호입니다.
* **[!UICONTROL 클라이언트 ID]**: Salesforce에 연결된 앱 소비자 키입니다.
* **[!UICONTROL 클라이언트 암호]**: Salesforce가 연결된 앱 소비자 암호입니다.
* **[!UICONTROL 사용자 이름]**: Salesforce 계정 사용자 이름입니다.

제공된 세부 정보가 유효한 경우 UI에 **연결됨** 녹색 확인 표시가 있는 상태에서 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![Salesforce CRM에 대한 세부 사항을 채우는 방법을 보여주는 샘플 스크린샷](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 사용자 지정 도메인]**: Salesforce 도메인입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 매핑 고려 사항 및 예 {#mapping-considerations-example}

Adobe Experience Platform에서 Salesforce CRM 대상으로 대상 데이터를 올바르게 전송하려면 필드 매핑 단계를 수행해야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다. XDM 필드를 Salesforce CRM 대상 필드에 올바르게 매핑하려면 다음 단계를 수행합니다.

1. 매핑 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;이면 화면에 새 매핑 행이 표시됩니다.

   ![새 매핑 추가](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. 소스 필드 선택 창에서 소스 필드를 선택할 때 **[!UICONTROL 속성 선택]** 카테고리를 추가하고 원하는 매핑을 추가합니다.

   ![소스 매핑](../../assets/catalog/crm/salesforce/source-mapping.png)

1. 대상 선택 필드 창에서 대상 필드를 선택하고 **[!UICONTROL ID 네임스페이스 선택]** 카테고리를 추가하고 원하는 매핑을 추가합니다.

   ![SalesforceId를 사용한 Target 매핑](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

1. 사용자 지정 속성의 경우 대상 필드 선택 창에서 대상 필드를 선택하고 **[!UICONTROL 사용자 지정 속성 선택]** 카테고리에서 원하는 대상 속성 이름을 제공하고 원하는 매핑을 추가합니다.

   ![LastName을 사용한 대상 매핑](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

1. 예를 들어 XDM 프로필 스키마와 프로필 스키마 사이에 다음 매핑을 추가할 수 있습니다 [!DNL Salesforce CRM] 인스턴스:

   |  | XDM 프로필 스키마 | [!DNL Salesforce CRM] 인스턴스 | 필수입니다 |
   |---|---|---|---|
   | 속성 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>이메일</code></li></ul> |
   | ID | <ul><li>crmID</code></li></ul> | <ul><li>SalesforceId</code></li></ul> | 예 |

1. 이러한 매핑을 사용하는 예는 다음과 같습니다.

   ![대상 매핑](../../assets/catalog/crm/salesforce/mappings.png)

### 세그먼트 내보내기 예약 및 예제 {#schedule-segment-export-example}

다음을 수행할 때 [세그먼트 내보내기 예약](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계는 Platform 세그먼트를 Salesforce의 사용자 지정 필드 속성에 수동으로 매핑해야 합니다.

이렇게 하려면 각 세그먼트를 선택한 다음 Salesforce의 해당 사용자 지정 필드 속성을 **[!UICONTROL 매핑 ID]** 필드.

>[!IMPORTANT]
>
>* 에 사용되는 값 **[!UICONTROL 매핑 ID]** 는 Salesforce 내에서 만든 사용자 지정 필드 속성의 이름과 정확히 일치해야 합니다.
>* Salesforce에서 만든 사용자 지정 필드 특성의 이름이 공백 문자를 사용하지 않는지 확인합니다.


예는 다음과 같습니다.
![세그먼트 내보내기 예약](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
   ![찾아보기 대상](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 대상을 선택하고 상태가 맞는지 확인합니다 **[!UICONTROL 활성화됨]**.
   ![대상 데이터 흐름 실행](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 로 전환 **[!DNL Activation data]** 탭을 클릭한 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내에서 생성된 수에 해당하는지 확인합니다.
   ![세그먼트](../../assets/catalog/crm/salesforce/segment.png)

1. Salesforce 웹 사이트에 로그인한 다음 **[!DNL Apps]** > **[!DNL Contacts]** 페이지를 방문하여 세그먼트의 프로필이 추가되었는지 확인합니다.
   ![Salesforce 연락처](../../assets/catalog/crm/salesforce/contacts.png)

1. 연락처를 클릭하고 필드가 업데이트되었는지 확인합니다. Experience Platform의 세그먼트 상태가 **매핑 ID** 다음 기간 중 필드 **[!UICONTROL 대상 활성화]** > **[!UICONTROL 세그먼트 내보내기 예약]** 단계.
   ![Salesforce 연락처](../../assets/catalog/crm/salesforce/contact-info.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### 이벤트를 대상으로 푸시하는 동안 알 수 없는 오류가 발생했습니다. {#unknown-errors}

데이터 흐름 실행을 확인할 때 아래에 오류 메시지가 표시되면 제공한 매핑 ID가 있는지 확인하십시오 [!DNL Salesforce CRM] 플랫폼 세그먼트가 유효하며 다음 내에 있음 [!DNL Salesforce CRM].
![오류](../../assets/catalog/crm/salesforce/error.png)

## 추가 리소스 {#additional-resources}

유용한 추가 정보는 [Salesforce 개발자 포털](https://developer.salesforce.com/) 아래와 같습니다.
* [레코드 만들기](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [사용자 지정 권장 사항 대상](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [복합 리소스 사용](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* [빠른 시작](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)

### 제한 {#limits}

Salesforce는 요청, 비율 및 시간 제한 제한을 적용하여 트랜잭션 로드 잔액을 조정합니다. 자세한 내용은 [API 요청 제한 및 할당](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 자세한 내용