---
keywords: crm;CRM;crm 대상;Microsoft Dynamics 365;Microsoft Dynamics 365 crm 대상
title: Microsoft Dynamics 365 연결
description: Microsoft Dynamics 365 대상을 사용하면 계정 데이터를 내보내고 비즈니스 요구 사항에 맞게 Microsoft Dynamics 365 내에서 활성화할 수 있습니다.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics 365] 연결

## 개요 {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/)은(는) 생산성 응용 프로그램 및 AI 도구와 함께 ERP(전사적 자원 관리) 및 CRM(고객 관계 관리)을 결합하여 전체적인 더 유연하고 통제된 운영, 더 나은 성장 가능성 및 비용 절감을 제공하는 클라우드 기반의 비즈니스 응용 프로그램 플랫폼입니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) 대상 내의 ID를 [!DNL Dynamics 365](으)로 업데이트할 수 있는 [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)을(를) 활용합니다.

[!DNL Dynamics 365]은(는) 인증 메커니즘으로 권한 부여가 있는 OAuth 2를 사용하여 [!DNL Contact Entity Reference API]과(와) 통신합니다. [!DNL Dynamics 365] 인스턴스에 대한 인증 지침은 [대상에 대한 인증](#authenticate) 섹션에서 아래에 더 나와 있습니다.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성에 따라 개인화된 경험을 사용자에게 제공할 수 있습니다. Adobe Experience Platform에서 대상 및 프로필이 업데이트되는 즉시 사용자 피드에 표시하기 위해 오프라인 데이터에서 대상을 작성하고 이 대상을 [!DNL Dynamics 365](으)로 보낼 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

[!DNL Dynamics 365] 대상에 대한 데이터를 활성화하기 전에 [!DNL Experience Platform]에서 만든 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) 및 [대상](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html)이 있어야 합니다.

대상 상태에 대한 지침이 필요한 경우 [대상 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md)에 대한 Adobe 설명서를 참조하세요.

### [!DNL Microsoft Dynamics 365]개 필수 구성 요소 {#prerequisites-destination}

플랫폼에서 [!DNL Dynamics 365] 계정으로 데이터를 내보내려면 [!DNL Dynamics 365]의 다음 필수 구성 요소를 참고하십시오.

#### [!DNL Microsoft Dynamics 365] 계정이 있어야 합니다. {#prerequisites-account}

아직 계정이 없는 경우 [!DNL Dynamics 365] [평가판](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) 페이지로 이동하여 등록하고 계정을 만드십시오.

#### [!DNL Dynamics 365] 내에 필드 만들기 {#prerequisites-custom-field}

[!DNL Dynamics 365] 내의 대상 상태를 업데이트하는 데 사용할 필드 데이터 형식을 `Single Line of Text`(으)로 하는 `Simple` 유형의 Experience Platform 정의 필드를 만드십시오.

추가 지침이 필요한 경우 [!DNL Dynamics 365] [필드(특성) 만들기 또는 편집](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 설명서를 참조하십시오.

[!DNL Dynamics 365]에서 만든 사용자 지정 필드의 **[!UICONTROL 사용자 지정 접두사]**&#x200B;을(를) 기록하십시오. [대상 세부 정보를 입력하십시오](#destination-details) 단계 동안 이 접두사가 필요합니다. 자세한 내용은 [!DNL Dynamics 365] 설명서의 [필드 만들기 및 편집](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) 섹션을 참조하십시오.
사용자 지정 접두사를 표시하는 ![Dynamics 365 UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

[!DNL Dynamics 365] 내의 예제 설정이 아래에 표시되어 있습니다.
사용자 지정 필드를 보여주는 ![Dynamics 365 UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Azure Active Directory 내에서 응용 프로그램 및 응용 프로그램 사용자 등록 {#prerequisites-app-user}

[!DNL Dynamics 365]이(가) 리소스에 액세스할 수 있도록 하려면 [!DNL Azure Account](으)로 [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal)에 로그인하고 다음을 만들어야 합니다.
* [!DNL Azure Active Directory] 응용 프로그램
* 서비스 주체
* 애플리케이션 암호

[!DNL Azure Active Directory]에서 [응용 프로그램 사용자를 만들고](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user)을(를) 새로 만든 응용 프로그램과 연결해야 합니다.

#### [!DNL Dynamics 365] 자격 증명 수집 {#gather-credentials}

[!DNL Dynamics 365] CRM 대상에 인증하기 전에 아래 항목을 적어 두십시오.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `Client ID` | [!DNL Azure Active Directory] 응용 프로그램에 대한 [!DNL Dynamics 365] 클라이언트 ID입니다. 자세한 내용은 [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in)를 참조하세요. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | [!DNL Azure Active Directory] 응용 프로그램에 대한 [!DNL Dynamics 365] 클라이언트 암호입니다. [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options)에서 #2 옵션을 사용합니다. | 지침을 위한 `abcde~abcdefghijklmnopqrstuvwxyz12345678`. |
| `Tenant ID` | [!DNL Azure Active Directory] 응용 프로그램에 대한 [!DNL Dynamics 365] 테넌트 ID입니다. 자세한 내용은 [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in)를 참조하세요. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | 환경 URL과 연결된 Microsoft 영역입니다.<br> 지침은 [[!DNL Dynamics 365] 설명서](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions)를 참조하세요. | 도메인이 아래와 같은 경우 [대상](#authenticate).<br>에 인증할 때 드롭다운 선택기에서 CRM 필드에 강조 표시된 값을 제공해야 합니다. *org57771b33.`crm`.dynamics.com*<br> 예: 회사가 북미(NAM) 지역에서 프로비저닝된 경우 URL은 `crm.dynamics.com`이고 `crm`을(를) 선택해야 합니다. 회사가 캐나다(CAN) 지역에서 프로비저닝된 경우 URL은 `crm3.dynamics.com`이고 `crm3`을(를) 선택해야 합니다. |
| `Environment URL` | 자세한 내용은 [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1)를 참조하세요. | [!DNL Dynamics 365] 도메인이 아래와 같은 경우 강조 표시된 값이 필요합니다.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## 가드레일 {#guardrails}

[요청 제한 및 할당](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) 페이지에서 [!DNL Dynamics 365] 라이선스와 연결된 [!DNL Dynamics 365] API 제한을 자세히 설명합니다. 데이터와 페이로드가 이러한 제한 내에 있는지 확인해야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Dynamics 365]은(는) 아래 표에 설명된 ID 업데이트를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 예 | 설명 | 고려 사항 |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | 연락처에 대한 고유 식별자. | **필수**. 자세한 내용은 [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)를 참조하세요. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 모든 대상에 대해 설명합니다.

이 대상은 Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 모든 대상의 활성화를 지원합니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화번호, 성)*&#x200B;과(와) 함께 대상자의 모든 구성원을 내보냅니다.</li><li> [!DNL Dynamics 365]의 각 대상 상태는 [대상 예약](#schedule-audience-export-example) 단계 동안 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 플랫폼에서 해당 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요.</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL Dynamics 365] 검색 또는 **[!UICONTROL CRM]** 범주 아래에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 **[!UICONTROL 대상에 연결]**을 선택하세요.
인증 방법을 보여 주는 ![플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

아래의 필수 필드를 입력하십시오. 자세한 내용은 [Dynamics 365 자격 증명 수집](#gather-credentials) 섹션을 참조하십시오.
* **[!UICONTROL 클라이언트 ID]**: [!DNL Azure Active Directory] 응용 프로그램의 [!DNL Dynamics 365] 클라이언트 ID입니다.
* **[!UICONTROL 테넌트 ID]**: [!DNL Azure Active Directory] 응용 프로그램의 [!DNL Dynamics 365] 테넌트 ID입니다.
* **[!UICONTROL 클라이언트 암호]**: [!DNL Azure Active Directory] 응용 프로그램에 대한 [!DNL Dynamics 365] 클라이언트 암호입니다.
* **[!UICONTROL 지역]**: [[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) 지역. 예를 들어 회사가 북미(NAM) 지역에 프로비저닝된 경우 URL은 `crm.dynamics.com`이고 `crm`을(를) 선택해야 합니다. 회사가 캐나다(CAN) 지역에서 프로비저닝된 경우 URL은 `crm3.dynamics.com`이고 `crm3`을(를) 선택해야 합니다.
* **[!UICONTROL 환경 URL]**: [!DNL Dynamics 365] 환경 URL.

제공된 세부 정보가 유효하면 UI에 녹색 확인 표시와 함께 **[!UICONTROL 연결됨]** 상태가 표시됩니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 정보를 표시하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 사용자 지정 접두사]**: [!DNL Dynamics 365]에서 만든 사용자 지정 필드의 `Customization prefix`. 자세한 내용은 [!DNL Dynamics 365] 설명서의 [필드 만들기 및 편집](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) 섹션을 참조하십시오.

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

대상 데이터를 Adobe Experience Platform에서 [!DNL Dynamics 365] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다. XDM 필드를 [!DNL Dynamics 365] 대상 필드에 올바르게 매핑하려면 다음 단계를 따르십시오.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**를 선택합니다. 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑 추가를 위한 플랫폼 UI 스크린샷 예](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. **[!UICONTROL 원본 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]** 범주를 선택하고 `contactid`을(를) 선택합니다.
   ![Source 매핑에 대한 플랫폼 UI 스크린샷 예](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. **[!UICONTROL 대상 필드 선택]** 창에서 원본 필드를 매핑할 대상 필드 유형을 선택합니다.
   * **[!UICONTROL ID 네임스페이스 선택]**: 소스 필드를 목록의 ID 네임스페이스에 매핑하려면 이 옵션을 선택하십시오.
     ![Contactid에 대한 Target 매핑을 보여 주는 Platform UI 스크린샷](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * XDM 프로필 스키마와 [!DNL Dynamics 365] 인스턴스 간에 다음 매핑을 추가합니다.
|XDM 프로필 스키마|[!DNL Dynamics 365] 인스턴스| 필수|
|—|—|
|`contactid`|`contactid`| 예 |

   * **[!UICONTROL 사용자 지정 특성 선택]**: 소스 필드를 **[!UICONTROL 특성 이름]** 필드에 정의한 사용자 지정 특성에 매핑하려면 이 옵션을 선택하십시오. 지원되는 특성의 전체 목록은 [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties)를 참조하세요.
     ![이메일에 대한 대상 매핑을 보여 주는 플랫폼 UI 스크린샷](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)

     >[!IMPORTANT]
     >
     > * 대상 필드 이름은 `lowercase`에 있어야 합니다.
     > * 또한 [!DNL Dynamics 365] [날짜 또는 타임스탬프](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) 대상 필드에 매핑된 날짜 또는 타임스탬프 원본 필드가 있는 경우 매핑된 값이 비어 있지 않은지 확인하십시오. 내보낸 필드 값이 비어 있으면 *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* 오류 메시지가 표시되고 데이터가 업데이트되지 않습니다. [!DNL Dynamics 365] 제한입니다.

   * 예를 들어 업데이트할 값에 따라 XDM 프로필 스키마와 [!DNL Dynamics 365] 인스턴스 사이에 다음 매핑을 추가합니다.
|XDM 프로필 스키마|[!DNL Dynamics 365] 인스턴스|
|—|—|
|`person.name.firstName`|`firstname`|
|`person.name.lastName`|`lastname`|
|`personalEmail.address`|`emailaddress1`|

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
     ![Target 매핑을 보여 주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### 대상자 내보내기 예약 및 예제 {#schedule-audience-export-example}

활성화 워크플로의 [[!UICONTROL 대상 내보내기 예약]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계에서 플랫폼 대상을 [!DNL Dynamics 365]의 사용자 지정 필드 특성에 수동으로 매핑해야 합니다.

이렇게 하려면 각 대상을 선택한 다음 **[!UICONTROL 매핑 ID]** 필드에 [!DNL Dynamics 365]의 해당 사용자 지정 필드 특성을 입력하십시오.

>[!IMPORTANT]
>
>**[!UICONTROL 매핑 ID]**&#x200B;에 사용된 값은 [!DNL Dynamics 365] 내에 만든 사용자 지정 필드 특성의 이름과 정확히 일치해야 합니다. 사용자 지정 필드 특성을 찾는 방법에 대한 지침이 필요한 경우 [[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1)를 참조하세요.

예제는 아래에 나와 있습니다.
대상자 내보내기 일정을 보여 주는 ![Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 대상 목록으로 이동하려면 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**를 선택하십시오.
   ![검색 대상을 표시하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. 대상을 선택하고 상태가 **[!UICONTROL 활성화됨]**인지 확인하십시오.
   ![대상 데이터 흐름이 실행되는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. **[!DNL Activation data]** 탭으로 전환한 다음 대상 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 플랫폼 UI 스크린샷 예입니다.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. 대상자 요약을 모니터링하고 프로필 수가 대상자 내에서 만든 수에 해당하는지 확인합니다.
   대상을 표시하는 ![Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. [!DNL Dynamics 365] 웹 사이트에 로그인한 다음 [!DNL Customers] > [!DNL Contacts] 페이지로 이동하여 대상자의 프로필이 추가되었는지 확인합니다. [대상 예약](#schedule-audience-export-example) 단계 동안 제공된 **[!UICONTROL 매핑 ID]** 값을 기반으로 [!DNL Dynamics 365]의 각 대상 상태가 플랫폼의 해당 대상 상태로 업데이트되었음을 확인할 수 있습니다.
   대상 상태가 업데이트된 연락처 페이지를 표시하는 ![Dynamics 365 UI 스크린샷.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### 이벤트를 대상으로 푸시하는 동안 알 수 없는 오류 발생 {#unknown-errors}

데이터 흐름 실행을 확인할 때 다음 오류 메시지가 나타나면 `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![잘못된 요청 오류를 표시하는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

이 오류를 수정하려면 Platform 대상에 대해 [!DNL Dynamics 365]에서 제공한 **[!UICONTROL 매핑 ID]**&#x200B;이(가) 유효하고 [!DNL Dynamics 365] 내에 있는지 확인하십시오.

## 추가 리소스 {#additional-resources}

[[!DNL Dynamics 365] 설명서](https://docs.microsoft.com/en-us/dynamics365/)의 추가 유용한 정보는 다음과 같습니다.
* [IOrorganizationService.Update(Entity) 메서드](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [웹 API를 사용하여 테이블 행 업데이트 및 삭제](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### 변경 로그

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 10월 | 설명서 업데이트 | [매핑 고려 사항 및 예제](#mapping-considerations-example) 단계에서 모든 대상 특성 이름이 소문자여야 함을 나타내는 지침을 업데이트했습니다. |
| 2023년 8월 | 기능 및 설명서 업데이트 | [!DNL Dynamics 365]의 기본 솔루션 내에서 만들어지지 않은 사용자 지정 필드에 대한 [!DNL Dynamics 365] 사용자 지정 필드 접두사에 대한 지원을 추가했습니다. [대상 세부 정보를 채우기](#destination-details) 단계에서 새 입력 필드 **[!UICONTROL 사용자 지정 접두사]**&#x200B;을(를) 추가했습니다. (PLATIR-31602). |
| 2022년 11월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서 게시. |

{style="table-layout:auto"}

+++