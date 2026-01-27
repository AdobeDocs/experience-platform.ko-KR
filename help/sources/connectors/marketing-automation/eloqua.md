---
title: Oracle Eloqua (V2) Source 개요
description: Oracle Eloqua를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 2%

---

# [!DNL Oracle Eloqua]&#x200B;(V2) 소스 개요

>[!IMPORTANT]
>
>원래 [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md) 원본은 2026년 1월부터 더 이상 사용되지 않습니다. 더 이상 사용되지 않는 이 원본에 대해 사용할 수 있는 마이그레이션이 없으므로 새 [!DNL Oracle Eloqua]&#x200B;(V2) 원본을 사용하여 데이터를 다시 구현해야 합니다.

[!DNL Oracle Eloqua]은(는) 주로 B2B 공간에 있는 조직에서 리드를 관리하고 구매자 여정을 조정하는 복잡한 프로세스를 자동화하고 개인화할 수 있도록 설계된 강력한 엔터프라이즈급 마케팅 자동화 플랫폼입니다. 마케팅 팀이 여러 디지털 채널에서 정교한 캠페인을 정의, 배포 및 측정할 수 있는 중앙 허브 역할을 하므로 잠재 고객이 가장 참여하는 시점에 올바른 콘텐츠를 받을 수 있습니다. [!DNL Eloqua]을(를) 통한 수집에 지원되는 개체는 **연락처**, **계정**, **캠페인** 및 **활동**&#x200B;입니다. 초기 수집이 완료되면 예약된 증분 프로세스를 사용하여 변경된 데이터를 가져옵니다.

[!DNL Eloqua] 소스를 사용하여 [!DNL Eloqua] 계정을 Adobe Experience Platform에 연결할 수 있습니다. 시작하는 방법을 알려면 아래 설명서를 읽어 보십시오.

## 사용 사례 예 {#use-case-examples}

다음은 Adobe Experience Platform과의 [!DNL Eloqua]&#x200B;(V2) 통합에서 지원하는 마케팅 개체에 대해 간략히 설명하는 표입니다. 각 개체에 대해 [!DNL Eloqua] 데이터를 Real-Time CDP과 통합하여 마케팅 효율성 및 캠페인 결과를 높이는 방법을 설명하는 샘플 사용 사례와 함께 설명이 제공됩니다.

| 오브젝트 | 설명 | 사용 사례 예 |
| --- | --- | --- |
| 연락처 | 연락처 데이터(예: 이름, 이메일, 전화번호, 직책)를 Real-Time CDP에 수집하여 각 개별 연락처와의 모든 상호 작용 및 참여를 통합하는 세분화된 통합 고객 프로필을 만듭니다. | **캠페인 최적화:** 마케팅 팀은 [!DNL Eloqua]의 연락처 데이터를 통합하여 이메일 열기, 양식 제출, 이벤트 등록과 같은 최근 활동을 기반으로 우선 순위가 높은 잠재 고객을 식별할 수 있습니다. Real-Time CDP은 이메일, 웹 사이트 및 기타 마케팅 접점 전반에 걸쳐 각 연락처의 동작을 360° 방식으로 볼 수 있으므로 마케팅 팀이 캠페인을 조정하고 메시지를 최적화하여 보다 나은 참여와 전환을 수행할 수 있습니다. |
| 계정 | 계정 수준 데이터(예: 회사 이름, 업계, 회사 규모, 수익, 위치)를 수집하여 Real-Time CDP에서 계정 기반 마케팅(ABM) 전략을 수립하고 팀이 적절한 조직을 타깃팅하고 관련 메시징을 통해 참여할 수 있도록 합니다. | **ABM 캠페인:** [!DNL Eloqua]에서 계정 데이터를 통합하면 타깃팅된 ABM 캠페인을 빌드할 수 있습니다. 예를 들어 소프트웨어 회사는 계정 데이터를 사용하여 금융 분야의 회사 의사결정자에게 맞춤형 이메일 캠페인을 세분화하고 전송하여 업계에 맞는 새로운 솔루션을 홍보할 수 있습니다. |
| 캠페인 | 캠페인 데이터(예: 캠페인 이름, 유형, 목표, 공개 비율, CTR과 같은 성과 지표)를 Real-Time CDP에 수집하여 여러 채널에서 캠페인 성과를 추적하고 최적화할 수 있습니다. 이 데이터를 사용하여 ROI를 측정하고 전략을 세웁니다. | **크로스 채널 속성:** [!DNL Eloqua]이(가) Real-Time CDP에 캠페인 데이터를 전송하는 경우 마케팅 팀은 다양한 채널(이메일, 소셜 미디어, 광고 등)에서 캠페인의 성과를 보고, 올바른 접점으로 전환을 기여하고 해당 insight을 기반으로 향후 전략을 구체화할 수 있습니다. |
| 활동 | 활동 데이터(예: 이메일 열기, 클릭 수, 웹 사이트 방문, 양식 제출, 웨비나 참석)를 수집하여 다양한 채널에서 실시간 행동 및 연락처를 추적하여 실시간 개인화된 참여를 위한 기회를 만듭니다. | **실시간 교육:** Real-Time CDP은 [!DNL Eloqua]의 활동 데이터를 통합하여 연락처가 콘텐츠를 사용할 때(백서 다운로드 또는 이메일 링크 클릭 등) 영업 팀에 개인화된 이메일 또는 알림을 트리거하여 적시에 후속 조치를 취하고 더 나은 전환 기회를 제공할 수 있습니다. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

소스를 Experience Platform에 연결하기 전에 완료해야 하는 필수 구성 요소 설정에 대해서는 아래 섹션을 참조하십시오.

### 인증을 위한 애플리케이션 설정

[!DNL Eloqua] 계정을 설정하고 기본 인증을 사용하여 Experience Platform에 연결하는 방법을 배우려면 아래 단계를 따르십시오.

시작하려면 [!DNL Eloqua] 인스턴스에 관리자(또는 사용자, 보안 그룹 및 앱을 만들 수 있는 액세스 권한이 있는 사용자)로 로그인합니다.

![내 Eloqua 대시보드입니다.](../../images/tutorials/create/eloqua/admin.png)

**설정** > **플랫폼 확장** > **앱 클라우드 개발자** > **앱 만들기**&#x200B;로 이동합니다. 이름, 설명, 아이콘 및 OAuth 콜백 URL을 포함하여 앱에 대한 세부 사항을 제공합니다. 완료되면 **저장**&#x200B;을 선택합니다.

![앱 개발자 패널 및 Eloqua 대시보드의 앱 만들기 단추](../../images/tutorials/create/eloqua/create-app.png)

| 속성 | 설명 |
| --- | --- |
| 이름 | 앱의 이름입니다. |
| 설명 | 앱에 대한 간략한 설명입니다. |
| 아이콘 | 아이콘의 URL입니다. |
| OAuth 콜백 URL | 앱을 설치하고 [!DNL Eloqua]&#x200B;(으)로 인증한 후 사용자를 리디렉션해야 하는 URL. |

![Eloqua의 앱 만들기 창](../../images/tutorials/create/eloqua/new-app.png)

앱을 만든 상태에서 [!DNL Authentication to Eloqua]&#x200B;(으)로 이동하여 새로 만든 앱에서 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;를 검색합니다. 이러한 값은 나중에 Experience Platform에 연결할 때 사용됩니다.

![Eloqua의 클라이언트 ID 및 클라이언트 암호](../../images/tutorials/create/eloqua/credentials.png)

보안 그룹을 사용하면 관리자가 자산, 기능, 인터페이스 등에 대한 사용자의 액세스 수준을 제어할 수 있습니다. 보안 그룹을 만들려면 **설정** > **사용자**(으)로 이동합니다. 그런 다음 왼쪽 패널의 **그룹** 탭을 선택한 다음 **새 보안 그룹 만들기**&#x200B;를 선택합니다.

![Eloqua의 사용자 관리 대시보드입니다.](../../images/tutorials/create/eloqua/user-management.png)

**[!DNL Security Group Overview]** 창을 사용하여 보안 그룹의 이름과 약어를 입력합니다. 만든 후에는 [!DNL Action Permissions]&#x200B;(으)로 이동하여 목록에서 [!DNL Consume] API 권한을 추가하고 **저장**&#x200B;을(를) 선택합니다.

![Eloqua의 보안 그룹 개요 창](../../images/tutorials/create/eloqua/security-group-overview.png)

![API 사용을 위한 선택 창](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>[!DNL Consume] API는 필수 권한이지만 앱 사용에 따라 더 많은 권한을 추가할 수 있습니다.

캠페인 데이터를 수집하려면 **사용자 편집** 인터페이스로 이동하여 선택한 보안 그룹에 [!DNL Guided Campaigns]을(를) 추가하십시오.

![안내 캠페인이 포함된 보안 그룹이 추가되었습니다.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

선택적으로 추가 사용자를 생성하고 해당 사용자를 보안 그룹에 추가할 수 있습니다. 자세한 단계는 [!DNL Eloqua]사용자 만들기[&#x200B; 및 &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm)보안 그룹에 사용자 할당[에 대한 &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm) 설명서를 참조하십시오.

### 필요한 자격 증명 수집

[!DNL Eloqua]을(를) Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 클라이언트 ID | Experience Platform 인증 시 계정을 식별하기 위해 [!DNL Eloqua]에서 사용하는 공개적으로 노출된 식별자입니다. |
| 클라이언트 암호 | 클라이언트 응용 프로그램 및 인증 서버에만 알려진 비밀 키입니다. 이 키는 클라이언트 ID와 함께 있어야 계정을 인증할 수 있습니다. |
| 사용자 이름 | [!DNL Eloqua] 계정과 연결된 사용자 이름. 액세스 확인 및 권한 부여에 사용됩니다. 사용자 이름은 `CompanyName\Username` 형식을 따릅니다. |
| 암호 | [!DNL Eloqua] 계정과 연결된 암호입니다. 사용자 이름과 함께 Eloqua 환경에 대한 액세스 권한을 부여합니다. |
| 기본 엔드포인트 | [!DNL Eloqua]에 대한 인증 기본 URI의 접두사입니다. 인증할 때 기본 끝점에 `http://` 또는 `https://`이(가) 포함되지 않아야 합니다. |

## [!DNL Eloqua] 매핑 안내서

>[!NOTE]
>
>다음은 증분 데이터 로드를 위해 내부적으로 사용되는 델타 필드입니다.
>
>- **연락처:** `C_DateModified`
>- **계정:** `M_DateModified`
>- **활동:** `CreatedAt`
>- **사용자 지정 개체:** `UpdatedAt`
>- **캠페인:** `updatedAt`

다음 표에서는 [!DNL Eloqua] 소스 필드와 Experience Platform의 해당 XDM(Experience Data Model) 대상 필드 간의 자세한 매핑을 제공합니다. 각 행에서는 필드를 변경할 수 없는지 여부에 대한 변환 논리에 대해 간략하게 설명하고 Experience Platform에서 [!DNL Eloqua] 데이터를 수집하고 구조화하는 방법을 이해하는 데 도움이 되는 추가 메모를 제공합니다.

### 계정

| Eloqua Source 열 | XDM 대상 경로 | 참고 |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | 이 필드는 항상 고정 값 &quot;Eloqua&quot;로 설정됩니다. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | account점수 | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | 커넥터가 CRM 인스턴스 ID를 자동으로 검색할 수 없습니다. `${CRM_INSTANCE_ID}`을(를) 실제 CRM 인스턴스 ID(Salesforce 또는 Dynamics 인스턴스 ID)로 수동으로 바꾸어야 합니다. 수집 중에 `M_SFDCAccountID`이(가) 있으면 커넥터가 해당 값을 사용하여 외부 키를 생성하고 `\@CRM_INSTANCE_ID.Salesforce`을(를) 추가합니다. 이 필드가 비어 있으면 커넥터가 `M_MSCRMAccountID`을(를) 사용하고 대신 `\@CRM_INSTANCE_ID.Dynamics`을(를) 추가합니다. 두 필드가 모두 비어 있으면 이 필드는 null로 설정됩니다. |

{style="table-layout:auto"}

### 활동

| Eloqua Source 열 | XDM 대상 경로 | 참고 |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | 이 필드는 항상 고정 값 &quot;Eloqua&quot;로 설정됩니다. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `ExternalId` | _ID |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | ActivityType을 기반으로 해당 Experience Platform eventType 값이 채워집니다. ExternalActivities의 경우 Experience Platform에 eventType이 없습니다. 이 매핑을 수정하여 더 많은 유형을 처리할 수 있습니다. |
| `ActivityDate` | 타임스탬프 | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### 캠페인

| Eloqua Source 열 | XDM 대상 경로 | 참고 |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | 이 필드는 항상 고정 값 &quot;Eloqua&quot;로 설정됩니다. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `name` | campaignName | |
| `endAt` | 캠페인 종료일 | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | 캠페인 유형 | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### 연락처

| Eloqua Source 열 | XDM 대상 경로 | 참고 |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | 이 필드는 항상 고정 값 &quot;Eloqua&quot;로 설정됩니다. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID`은(는) 커넥터로 자동 교체됩니다. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | [!DNL Eloqua] 인스턴스가 Salesforce과 동기화되는 경우 이 매핑을 유지합니다. 그렇지 않으면 제거합니다. 커넥터에 CRM_INSTANCE_ID를 확인할 수 있는 방법이 없으므로 ${CRM_INSTANCE_ID}을(를) 동기화된 Salesforce 인스턴스 ID로 바꾸어야 합니다. 이와 동일한 매핑은 personComponents와 extSourceSystemAudit에 적용되므로 둘 다 유지하십시오. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | [!DNL Eloqua] 인스턴스가 Dynamics와 동기화되는 경우 이 매핑을 유지합니다. 그렇지 않으면 제거합니다. 커넥터에 CRM_INSTANCE_ID를 확인할 방법이 없으므로 ${CRM_INSTANCE_ID}을(를) 동기화된 Dynamics 인스턴스 ID로 바꾸어야 합니다. 이와 동일한 매핑은 personComponents와 extSourceSystemAudit에 적용되므로 둘 다 유지하십시오. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | [!DNL Eloqua] 인스턴스가 Salesforce과 동기화되는 경우 이 매핑을 유지합니다. 그렇지 않으면 제거합니다. 커넥터에 CRM_INSTANCE_ID를 확인할 수 있는 방법이 없으므로 ${CRM_INSTANCE_ID}을(를) 동기화된 Salesforce 인스턴스 ID로 바꾸어야 합니다. 이와 동일한 매핑은 personComponents와 extSourceSystemAudit에 적용되므로 둘 다 유지하십시오. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | [!DNL Eloqua] 인스턴스가 Dynamics와 동기화되는 경우 이 매핑을 유지합니다. 그렇지 않으면 제거합니다. 커넥터에 CRM_INSTANCE_ID를 확인할 방법이 없으므로 ${CRM_INSTANCE_ID}을(를) 동기화된 Dynamics 인스턴스 ID로 바꾸어야 합니다. 이와 동일한 매핑은 personComponents와 extSourceSystemAudit에 적용되므로 둘 다 유지하십시오. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | 커넥터에 CRM_INSTANCE_ID를 확인할 방법이 없으므로 ${CRM_INSTANCE_ID}을(를) 동기화된 CRM 인스턴스 ID(Salesforce 인스턴스 ID 또는 Dynamics 인스턴스 ID)로 바꾸어야 합니다. 이 동일한 매핑은 b2b.accountKey 및 personComponents.sourceAccountKey 모두에 적용되므로 둘 다 유지합니다. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | 커넥터에 CRM_INSTANCE_ID를 확인할 방법이 없으므로 ${CRM_INSTANCE_ID}을(를) 동기화된 CRM 인스턴스 ID(Salesforce 인스턴스 ID 또는 Dynamics 인스턴스 ID)로 바꾸어야 합니다. 이 동일한 매핑은 b2b.accountKey 및 personComponents.sourceAccountKey 모두에 적용되므로 둘 다 유지합니다. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### 활동 유형 매핑 참조

| Eloqua ActivityType | XDM eventType |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | 있는 그대로 통과 |

{style="table-layout:auto"}

### 변수 자리 표시자

매핑 템플릿은 데이터 흐름이 실행되면 대체되는 다음 변수 자리 표시자를 사용합니다.

| 자리 표시자 | 설명 | 사용 |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | Eloqua 소스 인스턴스의 고유 ID | 소스 키에 사용됨 |
| `${CRM_INSTANCE_ID}` | CRM 시스템에 대한 고유 ID(Salesforce/Dynamics) | 외부 키에 사용됨 |

## Experience Platform에 [!DNL Eloqua] 연결

Experience Platform 내에서 [!DNL Eloqua] 소스 연결을 구성하십시오. UI를 통해 연결을 설정하는 방법에 대한 단계별 안내서는 [튜토리얼 여기](../../tutorials/ui/create/marketing-automation/eloqua.md)를 참조하십시오. 이 튜토리얼을 참조하여 [!DNL Eloqua] 계정 연결, 데이터 선택, 필드 매핑, 수집 예약 및 데이터 흐름 모니터링에 대해 알아보십시오.

