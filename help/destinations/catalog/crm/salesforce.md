---
keywords: crm;CRM;CRM 대상;salesforce crm;salesforce crm 대상
title: Salesforce CRM 연결
description: Salesforce CRM 대상을 사용하면 계정 데이터를 내보내고 비즈니스 요구 사항에 맞게 Salesforce CRM 내에서 활성화할 수 있습니다.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 1%

---

# [!DNL Salesforce CRM] 연결

## 개요 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/)은(는) 인기 있는 CRM(고객 관계 관리) 플랫폼이며 아래에 설명된 프로필 유형을 지원합니다.

* [리드](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - 리드는 판매하는 제품이나 서비스에 관심이 있는(또는 관심이 없는) 사람 또는 회사의 이름입니다.
* [연락처](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - 연락처는 담당자 중 한 명이 관계를 맺고 잠재 고객으로 자격을 얻은 개인입니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) 위에서 설명한 두 유형의 프로필을 모두 지원하는 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)을(를) 활용합니다.

[세그먼트를 활성화](#activate)할 때 리드 또는 연락처 중 하나를 선택하고 특성 및 대상 데이터를 [!DNL Salesforce CRM]&#x200B;(으)로 업데이트할 수 있습니다.

[!DNL Salesforce CRM]은(는) 암호 부여가 있는 OAuth 2를 인증 메커니즘으로 사용하여 Salesforce REST API와 통신합니다. [!DNL Salesforce CRM] 인스턴스에 대한 인증 지침은 [대상에 대한 인증](#authenticate) 섹션에서 아래에 더 나와 있습니다.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성에 따라 개인화된 경험을 사용자에게 제공할 수 있습니다. 오프라인 데이터에서 대상을 작성하고 이 대상을 Salesforce CRM으로 보내면 Adobe Experience Platform에서 대상 및 프로필이 업데이트되는 즉시 CRM 멤버십을 업데이트할 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform의 사전 요구 사항 {#prerequisites-in-experience-platform}

Salesforce CRM 대상으로 데이터를 활성화하기 전에 [!DNL Experience Platform]에서 만든 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko) 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)가 있어야 합니다.

### [!DNL Salesforce CRM]의 필수 구성 요소 {#prerequisites-destination}

Experience Platform에서 Salesforce 계정으로 데이터를 내보내려면 [!DNL Salesforce CRM]에서 다음 사전 요구 사항을 참고하십시오.

#### [!DNL Salesforce] 계정이 있어야 합니다. {#prerequisites-account}

아직 계정이 없는 경우 [!DNL Salesforce] [평가판](https://www.salesforce.com/in/form/signup/freetrial-sales/) 페이지로 이동하여 등록하고 [!DNL Salesforce] 계정을 만드십시오.

#### [!DNL Salesforce] 내에서 연결된 앱 구성 {#prerequisites-connected-app}

먼저 [!DNL Salesforce] 계정 내에 [[!DNL Salesforce] 연결된 앱](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5)이 없는 경우 구성해야 합니다. [!DNL Salesforce CRM]은(는) 연결된 앱을 활용하여 [!DNL Salesforce]에 연결합니다.

그런 다음 [!DNL Salesforce connected app]에 대해 [!DNL OAuth Settings for API Integration]을(를) 사용하도록 설정합니다. 자세한 내용은 [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 설명서를 참조하세요.

또한 [!DNL Salesforce connected app]에 대해 아래에 언급된 [범위](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US)를 선택해야 합니다.

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

마지막으로 [!DNL Salesforce] 계정 내에서 `password` 부여가 활성화되었는지 확인하십시오. 지침이 필요한 경우 [!DNL Salesforce] [특별 시나리오에 대한 OAuth 2.0 사용자 이름 암호 흐름](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) 설명서를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Salesforce] 계정 관리자가 신뢰할 수 있는 IP 범위에 대한 액세스를 제한한 경우 해당 관리자에게 연락하여 [Experience Platform IP](/help/destinations/catalog/streaming/ip-address-allow-list.md)를 허용 목록에추가된으로 받아야 합니다. 추가 지침이 필요한 경우 [!DNL Salesforce] [연결된 앱에 대한 신뢰할 수 있는 IP 범위에 대한 액세스 제한](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 설명서를 참조하십시오.

#### [!DNL Salesforce] 내에 사용자 지정 필드 만들기 {#prerequisites-custom-field}

대상을 [!DNL Salesforce CRM] 대상으로 활성화할 때 **[대상 일정](#schedule-segment-export-example)** 단계에서 활성화된 각 대상에 대해 **[!UICONTROL 매핑 ID]** 필드에 값을 입력해야 합니다.

[!DNL Salesforce CRM]에서는 Experience Platform에서 들어오는 대상을 올바르게 읽고 해석하고 [!DNL Salesforce] 내에서 대상 상태를 업데이트하려면 이 값이 필요합니다. 대상 상태에 대한 지침이 필요한 경우 [대상 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md)에 대한 Experience Platform 설명서를 참조하십시오.

Experience Platform에서 [!DNL Salesforce CRM]&#x200B;(으)로 활성화하는 각 대상에 대해 [!DNL Salesforce] 내에 `Text Area (Long)` 유형의 사용자 지정 필드를 만들어야 합니다. 비즈니스 요구 사항에 따라 256~131,072자 사이의 모든 크기의 필드 문자 길이를 정의할 수 있습니다. 사용자 지정 필드 형식에 대한 자세한 내용은 [!DNL Salesforce] [사용자 지정 필드 형식](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) 설명서 페이지를 참조하세요. 필드 만들기에 대한 지원이 필요한 경우 [!DNL Salesforce] 설명서를 참조하여 [사용자 지정 필드 만들기](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US)를 참조하십시오.

>[!IMPORTANT]
>
>필드 이름에 공백 문자를 포함하지 마십시오. 대신 밑줄 `(_)` 문자를 구분 기호로 사용하십시오.
>[!DNL Salesforce] 내에서 활성화된 각 Experience Platform 세그먼트에 대해 **[!UICONTROL 매핑 ID]** 내에 지정된 값과 정확히 일치하는 **[!UICONTROL 필드 이름]**&#x200B;을(를) 가진 사용자 정의 필드를 만들어야 합니다. 예를 들어 아래 스크린샷에는 이름이 `crm_2_seg`인 사용자 지정 필드가 표시됩니다. 대상을 이 대상으로 활성화할 때 `crm_2_seg`을(를) **[!UICONTROL 매핑 ID]**(으)로 추가하여 Experience Platform의 대상 대상을 이 사용자 정의 필드에 채웁니다.

[!DNL Salesforce], *1단계 - 데이터 형식 선택*에서 사용자 지정 필드를 만드는 예는 다음과 같습니다.
![사용자 지정 필드 만들기, 1단계 - 데이터 형식 선택을 보여 주는 Salesforce UI 스크린샷](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

[!DNL Salesforce], *2단계 - 사용자 정의 필드에 대한 세부 정보를 입력*하는 사용자 정의 필드 생성의 예는 다음과 같습니다.
![사용자 지정 필드 만들기, 2단계를 보여주는 Salesforce UI 스크린샷 - 사용자 지정 필드에 대한 세부 정보를 입력합니다.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Experience Platform 대상에 사용되는 사용자 정의 필드와 [!DNL Salesforce] 내의 다른 사용자 정의 필드를 구분하려면 사용자 정의 필드를 만들 때 인식 가능한 접두사 또는 접미사를 포함할 수 있습니다. 예를 들어 `test_segment` 대신 `Adobe_test_segment` 또는 `test_segment_Adobe`을(를) 사용합니다.
>* [!DNL Salesforce]에 이미 다른 사용자 정의 필드가 만들어져 있는 경우 Experience Platform 세그먼트와 동일한 이름을 사용하여 [!DNL Salesforce]의 대상자를 쉽게 식별할 수 있습니다.

>[!NOTE]
>
>* Salesforce의 개체는 25개의 외부 필드로 제한됩니다. [사용자 지정 필드 특성](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5)을 참조하십시오.
>* 이 제한은 언제든지 최대 25개의 Experience Platform 대상 멤버십을 활성화할 수 있음을 의미합니다.
>* Salesforce 내에서 이 제한에 도달한 경우 새 **[!UICONTROL 매핑 ID]**&#x200B;을(를) 사용하기 전에 Experience Platform 내의 이전 대상에 대해 대상 상태를 저장하는 데 사용된 Salesforce에서 사용자 지정 특성을 제거해야 합니다.

#### [!DNL Salesforce CRM] 자격 증명 수집 {#gather-credentials}

[!DNL Salesforce CRM] 대상에 인증하기 전에 아래 항목을 적어 두십시오.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `Username` | [!DNL Salesforce] 계정 사용자 이름입니다. | |
| `Password` | [!DNL Salesforce] 계정 암호입니다. | |
| `Security Token` | [대상에 대한 인증](#authenticate)을(를) 수행할 때 **[!UICONTROL 암호]**(으)로 사용할 연결된 문자열을 만들기 위해 나중에 [!DNL Salesforce] 암호 끝에 추가할 [!DNL Salesforce] 보안 토큰입니다.<br> 보안 토큰이 없는 경우 [!DNL Salesforce] 인터페이스에서 다시 생성하는 방법에 대해 알아보려면 [!DNL Salesforce] 설명서를 참조하여 [보안 토큰을 다시 설정](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5)하십시오. |  |
| `Custom Domain` | [!DNL Salesforce] 도메인 접두사입니다. <br> [!DNL Salesforce] 인터페이스에서 이 값을 가져오는 방법을 알아보려면 [[!DNL Salesforce] 설명서](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5)를 참조하세요. | [!DNL Salesforce] 도메인이 <br>인 경우 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> 값으로 `d5i000000isb4eak-dev-ed`이(가) 필요합니다. |
| `Client ID` | Salesforce `Consumer Key`. <br> [!DNL Salesforce] 인터페이스에서 이 값을 가져오는 방법에 대해 알아보려면 [[!DNL Salesforce] 설명서](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5)를 참조하세요. | |
| `Client Secret` | Salesforce `Consumer Secret`. <br> [!DNL Salesforce] 인터페이스에서 이 값을 가져오는 방법에 대해 알아보려면 [[!DNL Salesforce] 설명서](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5)를 참조하세요. | |

### 가드레일 {#guardrails}

[!DNL Salesforce]은(는) 요청, 속도 및 시간 제한을 적용하여 트랜잭션 로드 균형을 조정합니다. 자세한 내용은 [API 요청 제한 및 할당](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm)을 참조하세요.

[!DNL Salesforce] 계정 관리자가 IP 제한을 적용한 경우 [!DNL Salesforce] 계정의 신뢰할 수 있는 IP 범위에 [Experience Platform IP 주소](/help/destinations/catalog/streaming/ip-address-allow-list.md)를 추가해야 합니다. 추가 지침이 필요한 경우 [!DNL Salesforce] [연결된 앱에 대한 신뢰할 수 있는 IP 범위에 대한 액세스 제한](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 설명서를 참조하십시오.

>[!IMPORTANT]
>
>[세그먼트를 활성화](#activate)할 때 *연락처* 또는 *리드* 유형 중 하나를 선택해야 합니다. 대상자에게 선택한 유형에 따라 적절한 데이터 매핑이 있는지 확인해야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Salesforce CRM]은(는) 아래 표에 설명된 ID 업데이트를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| `SalesforceId` | 세그먼트를 통해 내보내거나 업데이트하는 연락처 또는 잠재 고객 ID에 대한 [!DNL Salesforce CRM] 식별자입니다. | 필수 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화 번호, 성)*&#x200B;과(와) 함께 세그먼트의 모든 멤버를 내보냅니다.</li><li> [!DNL Salesforce CRM]의 각 대상 상태는 [대상 예약](#schedule-segment-export-example) 단계 동안 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 Experience Platform의 해당 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요.</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL Salesforce CRM] 검색 또는 **[!UICONTROL CRM]** 범주 아래에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 아래의 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오. 자세한 내용은 [수집 [!DNL Salesforce CRM] 자격 증명](#gather-credentials) 섹션을 참조하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| **[!UICONTROL 사용자 이름]** | [!DNL Salesforce] 계정 사용자 이름입니다. |
| **[!UICONTROL 암호]** | [!DNL Salesforce] 보안 토큰과 함께 추가된 [!DNL Salesforce] 계정 암호로 구성된 연결된 문자열.<br>연결된 값은 `{PASSWORD}{TOKEN}` 형식입니다.<br> 참고: 중괄호나 공백을 사용하지 마십시오.<br>예를 들어 [!DNL Salesforce] 암호가 `MyPa$$w0rd123`이고 [!DNL Salesforce] 보안 토큰이 `TOKEN12345....0000`인 경우 **[!UICONTROL 암호]** 필드에서 사용할 연결된 값은 `MyPa$$w0rd123TOKEN12345....0000`입니다. |
| **[!UICONTROL 사용자 지정 도메인]** | [!DNL Salesforce] 도메인 접두사입니다. <br>예를 들어 도메인이 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*&#x200B;이면 `d5i000000isb4eak-dev-ed`을(를) 값으로 제공해야 합니다. |
| **[!UICONTROL 클라이언트 ID]** | [!DNL Salesforce]이(가) 앱 `Consumer Key`에 연결했습니다. |
| **[!UICONTROL 클라이언트 암호]** | [!DNL Salesforce]이(가) 앱 `Consumer Secret`에 연결했습니다. |

인증 방법을 보여 주는 ![Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

제공된 세부 정보가 유효하면 UI에 녹색 확인 표시와 함께 **[!UICONTROL 연결됨]** 상태가 표시됩니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Salesforce ID 유형]**:
   * 내보내거나 업데이트하려는 ID가 *연락처* 유형인 경우 **[!UICONTROL 연락처]**&#x200B;을(를) 선택하십시오.
   * 내보내거나 업데이트하려는 ID가 *리드* 유형인 경우 **[!UICONTROL 리드]**&#x200B;를 선택하십시오.

대상 세부 정보를 표시하는 ![Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/destination-details.png)

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

대상 데이터를 Adobe Experience Platform에서 [!DNL Salesforce CRM] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야합니다. 매핑은 Experience Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 스키마 필드 간에 링크를 작성하는 것으로 구성됩니다.

**[!UICONTROL 대상 필드]**&#x200B;에 지정된 특성은 요청 본문을 형성하므로 특성 매핑 표에 설명된 대로 정확히 이름을 지정해야 합니다.

**[!UICONTROL Source 필드]**&#x200B;에 지정된 특성은 이러한 제한을 따르지 않습니다. 필요에 따라 매핑할 수 있지만 [[!DNL Salesforce] 설명서](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5)에 따라 입력 데이터 형식이 유효한지 확인합니다. 입력 데이터가 올바르지 않으면 [!DNL Salesforce]에 대한 업데이트 호출이 실패하고 연락처/잠재 고객이 업데이트되지 않습니다.

XDM 필드를 [!DNL (API) Salesforce CRM] 대상 필드에 올바르게 매핑하려면 다음 단계를 따르십시오.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택하면 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑 추가를 위한 Experience Platform UI 스크린샷 예](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 특성 선택]** 범주를 선택하고 XDM 특성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을 선택하고 ID를 선택합니다.
1. **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을(를) 선택하고 ID를 선택하거나 **[!UICONTROL 사용자 지정 특성 선택]** 범주를 선택하고 필요에 따라 특성을 선택하거나 **[!UICONTROL 특성 이름]** 필드를 사용하여 특성을 정의합니다. 지원되는 특성에 대한 지침은 [[!DNL Salesforce CRM] 설명서](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5)를 참조하세요.
   * XDM 프로필 스키마와 [!DNL (API) Salesforce CRM] 사이에 다음 매핑을 추가하려면 다음 단계를 반복합니다.

   **연락처 작업**

   * 세그먼트 내에서 *연락처*&#x200B;와 함께 작업하는 경우 [연락처](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm)에 대한 Salesforce의 개체 참조를 참조하여 업데이트할 필드에 대한 매핑을 정의하십시오.
   * 위의 링크에서 필드 설명에 언급된 단어 *Required*&#x200B;을(를) 검색하여 필수 필드를 식별할 수 있습니다.
   * 내보내거나 업데이트할 필드에 따라 XDM 프로필 스키마와 [!DNL (API) Salesforce CRM] 사이에 매핑을 추가합니다.

     | 소스 필드 | 대상 필드 | 참고 |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory` 질문에 답합니다. 연락처의 성(최대 80자). |
     | `xdm: person.name.firstName` | `Attribute: FirstName` | 연락처의 이름은 최대 40자입니다. |
     | `xdm: personalEmail.address` | `Attribute: Email` | 연락처의 이메일 주소입니다. |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.

     ![Target 매핑을 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **잠재 고객 작업**

   * 세그먼트 내에서 *리드*&#x200B;로 작업하는 경우 [리드](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm)에 대한 Salesforce의 개체 참조를 참조하여 업데이트할 필드에 대한 매핑을 정의하십시오.
   * 위의 링크에서 필드 설명에 언급된 단어 *Required*&#x200B;을(를) 검색하여 필수 필드를 식별할 수 있습니다.
   * 내보내거나 업데이트할 필드에 따라 XDM 프로필 스키마와 [!DNL (API) Salesforce CRM] 사이에 매핑을 추가합니다.

     | 소스 필드 | 대상 필드 | 참고 |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory` 질문에 답합니다. 리드 최대 80자의 성. |
     | `xdm: b2b.companyName` | `Attribute: Company` | `Mandatory` 질문에 답합니다. 리드의 회사. |
     | `xdm: personalEmail.address` | `Attribute: Email` | 잠재 고객의 이메일 주소입니다. |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.

     ![Target 매핑을 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/mappings-leads.png)

대상 연결에 대한 매핑을 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

### 대상자 내보내기 예약 및 예제 {#schedule-segment-export-example}

[대상 내보내기 예약](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계를 수행할 때 Experience Platform에서 활성화된 대상을 [!DNL Salesforce]의 해당 사용자 정의 필드에 수동으로 매핑해야 합니다.

이렇게 하려면 각 세그먼트를 선택한 다음 [!DNL Salesforce CRM] **[!UICONTROL 매핑 ID]** 필드의 [!DNL Salesforce]에서 사용자 지정 필드 이름을 입력하십시오. [!DNL Salesforce]에서 사용자 지정 필드를 만드는 방법에 대한 지침 및 모범 사례를 보려면 [다음 섹션 내에서 사용자 지정 필드 만들기 [!DNL Salesforce]](#prerequisites-custom-field)를 참조하세요.

예를 들어 [!DNL Salesforce] 사용자 지정 필드가 `crm_2_seg`인 경우 [!DNL Salesforce CRM] **[!UICONTROL 매핑 ID]**&#x200B;에 이 값을 지정하여 Experience Platform의 대상 대상을 이 사용자 지정 필드로 채웁니다.

[!DNL Salesforce]의 사용자 지정 필드 예가 아래에 표시되어 있습니다.
사용자 지정 필드를 표시하는 ![[!DNL Salesforce] UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

[!DNL Salesforce CRM] **[!UICONTROL 매핑 ID]**&#x200B;의 위치를 나타내는 예는 다음과 같습니다.
![대상자 내보내기 일정을 보여 주는 Experience Platform UI 스크린샷 예](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

위에 표시된 대로 [!DNL Salesforce] **[!UICONTROL 필드 이름]**&#x200B;은(는) [!DNL Salesforce CRM] **[!UICONTROL 매핑 ID]** 내에 지정된 값과 정확히 일치합니다.

사용 사례에 따라 활성화된 모든 대상을 동일한 [!DNL Salesforce] 사용자 정의 필드 또는 [!DNL Salesforce CRM]의 다른 **[!UICONTROL 필드 이름]**&#x200B;에 매핑할 수 있습니다. 위에 표시된 이미지를 기반으로 한 일반적인 예는 다음과 같을 수 있습니다.

| [!DNL Salesforce CRM] 세그먼트 이름 | [!DNL Salesforce] **[!UICONTROL 필드 이름]** | [!DNL Salesforce CRM] **[!UICONTROL 매핑 ID]** |
| --- | --- | --- |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

활성화된 각 Experience Platform 세그먼트에 대해 이 섹션을 반복합니다.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 대상 목록으로 이동하려면 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.
   ![찾아보기 대상을 표시하는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 대상을 선택하고 상태가 **[!UICONTROL 활성화됨]**&#x200B;인지 확인하십시오.
   ![대상 데이터 흐름이 실행되는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. **[!UICONTROL 활성화 데이터]** 탭으로 전환한 다음 대상 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 대상자 요약을 모니터링하고 프로필 수가 세그먼트 내에서 만든 수에 해당하는지 확인합니다.
   ![세그먼트를 표시하는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/salesforce/segment.png)

1. 마지막으로 Salesforce 웹 사이트에 로그인하여 대상자의 프로필이 추가 또는 업데이트되었는지 확인합니다.

   **연락처 작업**

   * Experience Platform 세그먼트 내에서 *연락처*&#x200B;를 선택한 경우 **[!DNL Apps]** > **[!DNL Contacts]** 페이지로 이동합니다.

     ![세그먼트의 프로필이 있는 연락처 페이지를 표시하는 Salesforce CRM 스크린샷입니다.](../../assets/catalog/crm/salesforce/contacts.png)

   * *연락처*&#x200B;를 선택하고 필드가 업데이트되었는지 확인하십시오. [대상 예약](#schedule-segment-export-example) 중에 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 [!DNL Salesforce CRM]의 각 대상 상태가 Experience Platform의 해당 대상 상태로 업데이트되었음을 확인할 수 있습니다.

     ![대상자 상태가 업데이트된 연락처 세부 정보 페이지를 표시하는 Salesforce CRM 스크린샷](../../assets/catalog/crm/salesforce/contact-info.png)

   **잠재 고객 작업**

   * Experience Platform 세그먼트 내에서 *리드*&#x200B;를 선택한 경우 **[!DNL Apps]** > **[!DNL Leads]** 페이지로 이동합니다.

     ![세그먼트의 프로필이 있는 리드 페이지를 표시하는 Salesforce CRM 스크린샷입니다.](../../assets/catalog/crm/salesforce/leads.png)

   * *잠재 고객*&#x200B;을 선택하고 필드가 업데이트되었는지 확인하십시오. [대상 예약](#schedule-segment-export-example) 중에 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 [!DNL Salesforce CRM]의 각 대상 상태가 Experience Platform의 해당 대상 상태로 업데이트되었음을 확인할 수 있습니다.

     대상 상태가 업데이트된 잠재 고객 세부 정보 페이지를 표시하는 ![Salesforce CRM 스크린샷입니다.](../../assets/catalog/crm/salesforce/lead-info.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### 이벤트를 대상으로 푸시하는 동안 알 수 없는 오류 발생 {#unknown-errors}

* 데이터 흐름 실행을 확인할 때 다음 오류 메시지가 표시될 수 있습니다. `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![오류를 표시하는 Experience Platform UI 스크린샷](../../assets/catalog/crm/salesforce/error.png)

   * 이 오류를 수정하려면 활성화 워크플로에서 [!DNL Salesforce CRM] 대상에 제공한 **[!UICONTROL 매핑 ID]**&#x200B;이(가) [!DNL Salesforce]에서 만든 사용자 지정 필드 형식의 값과 정확히 일치하는지 확인하십시오. 지침은  [!DNL Salesforce][&#128279;](#prerequisites-custom-field) 섹션 내에서 사용자 지정 필드 만들기를 참조하세요.

* 세그먼트를 활성화할 때 다음 오류 메시지가 표시될 수 있습니다. `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 이 오류를 해결하려면 [!DNL Salesforce] 계정 관리자에게 문의하여 [!DNL Salesforce] 계정의 신뢰할 수 있는 IP 범위에 [Experience Platform IP 주소](/help/destinations/catalog/streaming/ip-address-allow-list.md)를 추가하십시오. 추가 지침이 필요한 경우 [!DNL Salesforce] [연결된 앱에 대한 신뢰할 수 있는 IP 범위에 대한 액세스 제한](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 설명서를 참조하십시오.

## 추가 리소스 {#additional-resources}

[Salesforce 개발자 포털](https://developer.salesforce.com/)의 추가 유용한 정보는 다음과 같습니다.
* [빠른 시작](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [레코드 만들기](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [사용자 지정 권장 사항 대상](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [복합 리소스 사용](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 이 대상은 [단일 레코드 업데이트](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API 호출 대신 [여러 레코드 업데이트](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API를 활용합니다.
