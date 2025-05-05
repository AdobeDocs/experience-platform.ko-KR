---
keywords: linkedin 연결;linkedin 연결;linkedin 대상;linkedin;
title: Linkedin 일치하는 대상 연결
description: 해시된 이메일을 기반으로 대상자 타겟팅, 개인화 및 억제에 대한 LinkedIn 캠페인에 대한 프로필을 활성화합니다.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 3%

---

# [!DNL LinkedIn Matched Audiences] 연결

## 개요 {#overview}

해시된 이메일과 모바일 ID를 기반으로 대상자 타겟팅, 개인화 및 제외를 위해 [!DNL LinkedIn] 캠페인에 대한 프로필을 활성화합니다.

Adobe Experience Platform UI의 ![LinkedIn 대상](../../assets/catalog/social/linkedin/catalog.png)

## 사용 사례

[!DNL LinkedIn Matched Audiences] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

소프트웨어 회사는 회의를 주관하며 참가자와 계속 연락하고, 회의 참석 상태에 따라 개인화된 오퍼를 표시하기를 원합니다. 회사는 자신의 [!DNL CRM]에서 Adobe Experience Platform으로 이메일 주소 또는 모바일 장치 ID를 수집할 수 있습니다. 그런 다음 자신의 오프라인 데이터로 대상자를 만들어 [!DNL LinkedIn] 소셜 플랫폼으로 보내어 광고 지출을 최적화할 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL LinkedIn Matched Audiences]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침을 따라 일반 텍스트와 해시된 이메일에 각각 적절한 네임스페이스를 사용하십시오. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 하십시오. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | [!DNL LinkedIn Matched Audiences] 대상에 사용된 식별자(이름, 전화번호 등)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## LinkedIn 계정 사전 요구 사항 {#LinkedIn-account-prerequisites}

[!UICONTROL LinkedIn 일치하는 대상] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인하십시오.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대해 알아보려면 LinkedIn 설명서에서 [Advertising 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753)를 참조하십시오.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences]을(를) 사용하려면 PII(개인 식별 정보)를 명확하게 보내지 않아야 합니다. 따라서 [!DNL LinkedIn Matched Audiences]에 대해 활성화된 대상은 이메일 주소 또는 모바일 장치 ID와 같은 *hashed* 식별자에서 벗어날 수 있습니다.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 이메일 해시 요구 사항 {#email-hashing-requirements}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 이메일 주소를 지우고 활성화 시 [!DNL Experience Platform]에게 해시하도록 할 수 있습니다.

Experience Platform에서 전자 메일 주소를 수집하는 방법에 대한 자세한 내용은 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](/help/ingestion/streaming-ingestion/overview.md)를 참조하십시오.

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 준수해야 합니다.

* 전자 메일 문자열에서 선행 및 후행 공백을 모두 트리밍합니다. 예: `<space>johndoe@example.com<space>`이(가) 아닌 `johndoe@example.com`;
* 이메일 문자열을 해시할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, `EXAMPLE@EMAIL.COM` 아님;
* 해시된 문자열이 모두 소문자인지 확인합니다.
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149` 아님;
* 문자열에 소금을 뿌리지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Experience Platform]에 의해 자동으로 해시됩니다.
> 속성 소스 데이터는 자동으로 해시되지 않습니다.
> 
> [ID 매핑](../../ui/activate-segment-streaming-destinations.md#mapping) 단계 동안 소스 필드에 해시되지 않은 특성이 포함되어 있으면 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다.
> 
> **[!UICONTROL 변환 적용]** 옵션은 특성을 소스 필드로 선택하는 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

아래 비디오에서는 [!DNL LinkedIn Matched Audiences] 대상을 구성하고 대상을 활성화하는 단계도 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/3411788/?quality=12&learn=on&captions=kor)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며, 이 비디오 녹화 이후 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md)를 참조하세요.

### 대상으로 인증 {#authenticate}

1. 대상 카탈로그에서 [!DNL LinkedIn Matched Audiences] 대상을 찾은 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.
2. **[!UICONTROL 대상에 연결]**&#x200B;을 선택합니다.
   ![LinkedIn 인증](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. LinkedIn 자격 증명을 입력하고 **로그인**&#x200B;을 선택합니다.

### 인증 자격 증명 새로 고침 {#refresh-authentication-credentials}

LinkedIn 토큰은 60일마다 만료됩니다. 토큰이 만료되면 대상으로의 데이터 내보내기가 더 이상 작동하지 않습니다. 이러한 상황을 방지하려면 다음 단계를 수행하여 다시 인증하십시오.

1. **[!UICONTROL 대상]** > **[!UICONTROL 계정]**(으)로 이동
2. (선택 사항) 페이지에서 사용할 수 있는 필터를 사용하여 LinkedIn 계정만 표시합니다.
   ![LinkedIn 계정만 표시하도록 필터링](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. 새로 고침할 계정을 선택하고 줄임표를 선택한 다음 **[!UICONTROL 세부 정보 편집]**&#x200B;을 선택합니다.
   ![세부 정보 편집 컨트롤 선택](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. 모달 창에서 **[!UICONTROL OAuth 다시 연결]**&#x200B;을 선택하고 LinkedIn 자격 증명으로 다시 인증합니다.
   ![다시 연결 OAuth 옵션이 있는 모달 창](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>인증 자격 증명이 새로 고쳐지고 만료 시간이 60일로 재설정됩니다.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="계정 ID"
>abstract="LinkedIn Campaign Manager 계정 ID. LinkedIn Campaign Manager 계정에서 이 ID를 찾을 수 있습니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 내 [!DNL LinkedIn Campaign Manager Account ID]. 이 ID는 [!DNL LinkedIn Campaign Manager] 계정에서 찾을 수 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

활성화가 성공하면 [!DNL LinkedIn] 사용자 지정 대상자가 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)에서 프로그래밍 방식으로 만들어집니다. 사용자가 활성화된 대상에 대해 자격이 부여되거나 자격을 상실함에 따라 대상 멤버십이 조정됩니다.

>[!TIP]
>
>Adobe Experience Platform과 [!DNL LinkedIn Matched Audiences] 간의 통합은 과거 대상 다시 채우기를 지원합니다. 대상에 대해 대상을 활성화하면 기존의 모든 대상 자격이 [!DNL LinkedIn]&#x200B;(으)로 전송됩니다.
