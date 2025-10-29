---
keywords: facebook 연결;facebook 연결;facebook 대상;facebook;instagram;messenger;facebook messenger
title: Facebook 연결
description: 해시된 이메일을 기반으로 한 대상자 타겟팅, 개인화 및 억제에 대한 Facebook 캠페인을 위한 프로필을 활성화합니다.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2636'
ht-degree: 5%

---

# [!DNL Facebook] 연결

## 개요 {#overview}

해시된 이메일을 기반으로 한 대상자 타겟팅, 개인화 및 제외를 위해 [!DNL Facebook] 캠페인에 대한 프로필을 활성화합니다.

[!DNL Facebook's], [!DNL Custom Audiences], [!DNL Facebook] 및 [!DNL Instagram]을(를) 포함하여 [!DNL Audience Network]에서 지원하는 [!DNL Messenger] 앱 제품군의 대상 타깃팅에 이 대상을 사용할 수 있습니다. 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

![Adobe Experience Platform UI의 Facebook 대상입니다.](../../assets/catalog/social/facebook/catalog.png)

## 사용 사례

[!DNL Facebook] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 사용 사례를 소개합니다.

### 사용 사례 #1

온라인 retailer은 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문을 기반으로 개인화된 오퍼를 표시하려고 합니다. 온라인 retailer은 자체 CRM에서 Adobe Experience Platform으로 전자 메일 주소를 수집하고, 자체 오프라인 데이터에서 대상을 만들고, 이러한 대상을 [!DNL Facebook] 소셜 플랫폼으로 보내어 광고 지출을 최적화할 수 있습니다.

### 사용 사례 #2

항공사에는 다양한 고객 계층(브론즈, 실버 및 골드)이 있으며 소셜 플랫폼을 통해 각 계층에 개인화된 오퍼를 제공하려고 합니다. 다만 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 이들 중 일부는 회사 홈페이지에 로그인하지 않은 상태다. 회사에서 이러한 고객에 대해 가지고 있는 유일한 식별자는 멤버십 ID와 이메일 주소입니다.

소셜 미디어에서 고객을 타깃팅하기 위해 이메일 주소를 식별자로 사용하여 CRM의 고객 데이터를 Adobe Experience Platform에 온보딩할 수 있습니다.

다음으로 연결된 멤버십 ID 및 고객 계층을 포함한 오프라인 데이터를 사용하여 [!DNL Facebook] 대상을 통해 타깃팅할 수 있는 새 대상을 만들 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL Facebook Custom Audiences]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| `IDFA` | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| `phone_sha256` | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침을 따르고 일반 텍스트와 해시된 전화 번호에 각각 적절한 네임스페이스를 사용하십시오. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| `email_lc_sha256` | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침에 따라 일반 텍스트와 해시된 이메일 주소에 각각 적절한 네임스페이스를 사용하십시오. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| `extern_id` | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| `gender` | 성별 | 허용된 값: <ul><li>남성의 경우 `m`</li><li>여성용 `f`</li></ul> Experience Platform으로 보내기 전에 이 값을 **자동으로 해싱**&#x200B;합니다. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `date_of_birth` | 생년월일 | 허용되는 형식: `yyyy-MM-DD`. <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `last_name` | 성 | 허용되는 형식: 소문자, `a-z`자만 허용되며 구두점이 없습니다. 특수 문자에는 UTF-8 인코딩을 사용하십시오.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `first_name` | 이름 | 허용되는 형식: 소문자, `a-z`자만, 구두점 없음, 공백 없음. 특수 문자에는 UTF-8 인코딩을 사용하십시오.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `first_name_initial` | 이름 이니셜 | 허용되는 형식: 소문자, `a-z`자만. 특수 문자에는 UTF-8 인코딩을 사용하십시오.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `state` | 주/도 | 소문자로 [2자 ANSI 약어 코드](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code)을(를) 사용하십시오. 미국 이외의 주에서는 소문자, 구두점 없음, 특수 문자 및 공백을 사용하지 마십시오.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `city` | 구/군/시 | 허용되는 형식: 소문자, `a-z`자만, 구두점 없음, 특수 문자 없음, 공백 없음.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `zip` | 우편 번호 | 허용된 형식: 소문자, 공백 없음. 미국 우편번호의 경우 처음 5자리만 사용하십시오. 영국에서는 `Area/District/Sector` 형식을 사용합니다.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |
| `country` | 국가 | 허용되는 형식: [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 형식의 소문자, 두 글자로 된 국가 코드입니다.  <br>Experience Platform **이 값을 Facebook으로 보내기 전에 자동으로 해시합니다**. 이 자동 해싱은 Facebook의 보안 및 개인정보 보호 요구 사항을 준수하는 데 필요합니다. **not**&#x200B;은(는) 이 필드에 사전 해시된 값을 제공하지 마십시오. 그러면 일치 프로세스가 실패합니다. |

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
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | Facebook 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상자를 [!DNL Facebook]&#x200B;(으)로 보내려면 먼저 다음 요구 사항을 충족하는지 확인하십시오.

* [!DNL Facebook] 사용자 계정에는 사용 중인 광고 계정을 소유한 [!DNL Facebook Business Account]에 대한 전체 액세스 권한이 있어야 합니다.
* [!DNL Facebook] 사용자 계정에는 사용할 광고 계정에 대해 **[!DNL Manage campaigns]** 권한이 활성화되어 있어야 합니다.
* **Adobe Experience Cloud** 비즈니스 계정을 [!DNL Facebook Ad Account]의 광고 파트너로 추가해야 합니다. `business ID=206617933627973` 사용. 자세한 내용은 Facebook 설명서의 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897)를 참조하십시오.

  >[!IMPORTANT]
  >
  > Adobe Experience Cloud에 대한 권한을 구성할 때는 **캠페인 관리** 권한을 활성화해야 합니다. [!DNL Adobe Experience Platform] 통합에는 권한이 필요합니다.

* [!DNL Facebook Custom Audiences] 서비스 약관을 읽고 서명합니다. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]&business_id=206617933627973`(으)로 이동하십시오. 여기서 `accountID`은(는) 내 [!DNL Facebook Ad Account ID]입니다. 서비스 약관에 서명할 때 `business_id=206617933627973` 섹션이 URL에 있는지 확인하십시오.

  >[!IMPORTANT]
  >
  >[!DNL Facebook Custom Audiences] 서비스 약관에 서명할 때 Facebook API에서 인증하는 데 사용한 것과 동일한 사용자 계정을 사용해야 합니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Facebook]을(를) 사용하려면 PII(개인 식별 정보)를 명확하게 보내지 않아야 합니다. 따라서 [!DNL Facebook]에 대해 활성화된 대상은 이메일 주소 또는 전화 번호와 같은 *hashed* 식별자에서 벗어날 수 있습니다.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 대상자 일치율 최대화 {#match-rates}

[!DNL Facebook]에서 가장 높은 대상 일치율을 달성하려면 `phone_sha256` 및 `email_lc_sha256` 대상 ID를 사용하는 것이 좋습니다.

이러한 식별자는 [!DNL Facebook]이(가) 플랫폼 간 대상을 일치시키기 위해 사용하는 기본 식별자입니다. 소스 데이터가 이러한 대상 ID에 올바르게 매핑되고 [!DNL Facebook's] 해시 요구 사항을 준수하는지 확인하십시오.

## 전화번호 해시 요구 사항 {#phone-number-hashing-requirements}

[!DNL Facebook]에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다.

* **원시 전화 번호 수집**: [!DNL E.164] 형식의 원시 전화 번호를 [!DNL Experience Platform]&#x200B;(으)로 수집할 수 있습니다. 활성화 시 자동으로 해시됩니다. 이 옵션을 선택하는 경우 항상 원시 전화 번호를 `Phone_E.164` 네임스페이스로 수집해야 합니다.
* **해시된 전화번호 수집**: [!DNL Experience Platform]에 수집하기 전에 전화번호를 미리 해시할 수 있습니다. 이 옵션을 선택하는 경우 해시된 전화 번호를 항상 `Phone_SHA256` 네임스페이스로 수집해야 합니다.

>[!NOTE]
>
>`Phone` 네임스페이스로 수집된 전화 번호는 [!DNL Facebook]에서 활성화할 수 없습니다.

## 이메일 해시 요구 사항 {#email-hashing-requirements}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 이메일 주소를 지우고 활성화 시 [!DNL Experience Platform]에게 해시하도록 할 수 있습니다.

Experience Platform에서 전자 메일 주소를 수집하는 방법에 대한 자세한 내용은 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](/help/ingestion/streaming-ingestion/overview.md)를 참조하십시오.

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 준수해야 합니다.

* 전자 메일 문자열에서 선행 및 후행 공백을 모두 트리밍합니다. 예: `johndoe@example.com`이(가) 아닌 `<space>johndoe@example.com<space>`;
* 이메일 문자열을 해시할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, `EXAMPLE@EMAIL.COM` 아님;
* 해시된 문자열이 모두 소문자인지 확인합니다.
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149` 아님;
* 문자열에 소금을 뿌리지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Experience Platform]에 의해 자동으로 해시됩니다.
>&#x200B;> 속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다.
>&#x200B;> **[!UICONTROL Apply transformation]** 옵션은 특성을 소스 필드로 선택하는 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![매핑 단계에서 강조 표시된 변환 컨트롤을 적용합니다.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 사용자 정의 네임스페이스 사용 {#custom-namespaces}

`Extern_ID` 네임스페이스를 사용하여 [!DNL Facebook]&#x200B;(으)로 데이터를 보내려면 먼저 [!DNL Facebook Pixel]을(를) 사용하여 자신의 식별자를 동기화해야 합니다. 자세한 내용은 [Facebook 공식 설명서](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)를 참조하세요.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

아래 비디오에서는 [!DNL Facebook] 대상을 구성하고 대상을 활성화하는 단계도 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/3411788/?quality=12&learn=on&captions=kor)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며, 이 비디오 녹화 이후 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md)를 참조하세요.

### 대상으로 인증 {#authenticate}

1. 대상 카탈로그에서 Facebook 대상을 찾고 **[!UICONTROL Set Up]**&#x200B;을(를) 선택합니다.
2. **[!UICONTROL Connect to destination]**&#x200B;를 선택합니다.
   ![활성화 워크플로에 표시된 Facebook 인증 단계입니다.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Facebook 자격 증명을 입력하고 **로그인**&#x200B;을 선택합니다.

### 인증 자격 증명 새로 고침 {#refresh-authentication-credentials}

Facebook 인증 토큰은 60일마다 만료됩니다. 토큰이 만료되면 대상으로의 데이터 내보내기가 더 이상 작동하지 않습니다.

**[!UICONTROL Account expiration date]** 또는 **[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)** 탭의 **[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)** 열에서 토큰 만료 날짜를 모니터링할 수 있습니다.

![찾아보기 탭의 Facebook 계정 토큰 만료 날짜 열](../../assets/catalog/social/facebook/account-expiration-browse.png)

![계정 탭의 Facebook 계정 토큰 만료 날짜 열](../../assets/catalog/social/facebook/account-expiration-accounts.png)

토큰 만료로 인해 활성화 데이터 흐름이 중단되지 않도록 하려면 다음 단계를 수행하여 다시 인증하십시오.

1. **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**(으)로 이동
2. (선택 사항) 페이지에서 사용할 수 있는 필터를 사용하여 Facebook 계정만 표시합니다.
   ![Facebook 계정만 표시하도록 필터링](/help/destinations/assets/catalog/social/facebook/refresh-oauth-filters.png)
3. 새로 고침할 계정을 선택하고 줄임표를 선택한 다음 **[!UICONTROL Edit details]**&#x200B;을(를) 선택하십시오.
   ![세부 정보 편집 컨트롤 선택](/help/destinations/assets/catalog/social/facebook/refresh-oauth-edit-details.png)
4. 모달 창에서 **[!UICONTROL Reconnect OAuth]**&#x200B;을(를) 선택하고 Facebook 자격 증명으로 다시 인증합니다.
   ![다시 연결 OAuth 옵션이 있는 모달 창](/help/destinations/assets/catalog/social/facebook/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>인증 자격 증명이 새로 고쳐지고 만료 시간이 60일로 재설정됩니다.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="계정 ID"
>abstract="Facebook 광고 계정 ID. Facebook Ads Manager 계정에서 이 ID를 찾을 수 있습니다. 이 ID를 입력할 때 항상 `act_`로 접두사가 붙습니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Account ID]**: 내 [!DNL Facebook Ad Account ID]. 이 ID는 [!DNL Facebook Ads Manager] 계정에서 찾을 수 있습니다. 이 ID를 입력할 때 항상 `act_`로 접두사가 붙습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="대상자 원본"
>abstract="원래 대상자의 고객 데이터를 수집하는 방법을 선택합니다. 사용자가 세그먼트에 타기팅되면 데이터가 Facebook에 표시됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="대상자 원본"
>abstract="광고주는 고객으로부터 직접 데이터를 수집했습니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="대상자 원본"
>abstract="광고주는 파트너로부터 직접 데이터를 수집했습니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="대상자 원본"
>abstract="광고주는 고객과 파트너로부터 직접 데이터를 수집했습니다."

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

**[!UICONTROL Segment schedule]** 단계에서는 대상자를 [!UICONTROL Origin of audience]에 보낼 때 [!DNL Facebook Custom Audiences]을(를) 제공해야 합니다.

![Facebook 활성화 단계에 표시된 대상자 원본 드롭다운입니다.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 매핑 예: [!DNL Facebook Custom Audience]에서 대상 데이터 활성화 {#example-facebook}

다음은 [!DNL Facebook Custom Audience]에서 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* 사용 중인 전자 메일 주소가 해시되지 않은 경우 `Email` 네임스페이스를 원본 ID로 선택하십시오.
* `Email_LC_SHA256` [!DNL Experience Platform]전자 메일 해시 요구 사항[!DNL Facebook]에 따라 데이터 수집 시 고객 전자 메일 주소를 [(으)로 해시했다면 &#x200B;](#email-hashing-requirements) 네임스페이스를 원본 ID로 선택하십시오.
* 데이터가 해시되지 않은 전화 번호로 구성된 경우 `PHONE_E.164` 네임스페이스를 원본 ID로 선택하십시오. [!DNL Experience Platform]이(가) [!DNL Facebook] 요구 사항을 준수하기 위해 전화 번호를 해시합니다.
* `Phone_SHA256` [!DNL Experience Platform]전화 번호 해시 요구 사항[!DNL Facebook]에 따라 데이터 수집 시 전화 번호를 [(으)로 해시했다면 &#x200B;](#phone-number-hashing-requirements) 네임스페이스를 원본 ID로 선택하십시오.
* 데이터가 `IDFA` 장치 ID로 구성된 경우 [!DNL Apple] 네임스페이스를 원본 ID로 선택하십시오.
* 데이터가 `GAID` 장치 ID로 구성된 경우 [!DNL Android] 네임스페이스를 원본 ID로 선택하십시오.
* 데이터가 다른 유형의 식별자로 구성된 경우 `Custom` 네임스페이스를 소스 ID로 선택하십시오.

대상 필드 선택:

* 원본 네임스페이스가 `Email_LC_SHA256` 또는 `Email`인 경우 `Email_LC_SHA256` 네임스페이스를 대상 ID로 선택하십시오.
* 원본 네임스페이스가 `Phone_SHA256` 또는 `PHONE_E.164`인 경우 `Phone_SHA256` 네임스페이스를 대상 ID로 선택하십시오.
* 원본 네임스페이스가 `IDFA` 또는 `GAID`인 경우 `IDFA` 또는 `GAID` 네임스페이스를 대상 ID로 선택하십시오.
* 소스 네임스페이스가 사용자 지정 네임스페이스인 경우 `Extern_ID` 네임스페이스를 대상 ID로 선택하십시오.

>[!IMPORTANT]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Experience Platform]에 의해 자동으로 해시됩니다.
> 
>속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다.

![매핑 단계에서 강조 표시된 변환 컨트롤을 적용합니다.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 내보낸 데이터 {#exported-data}

[!DNL Facebook]의 경우 활성화가 성공하면 [!DNL Facebook] 사용자 지정 대상자가 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)에서 프로그래밍 방식으로 만들어집니다. 사용자가 활성화된 대상자에 대해 자격이 부여되거나 자격을 상실하면 대상자 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 [!DNL Facebook] 간의 통합은 과거 대상 다시 채우기를 지원합니다. 대상에 대해 대상을 활성화하면 기존의 모든 대상 자격이 [!DNL Facebook]&#x200B;(으)로 전송됩니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

이 오류는 고객이 새로 만든 계정을 사용하고 있으며 [!DNL Facebook] 권한이 아직 활성화되지 않은 경우에 발생합니다.

>[!IMPORTANT]
>
>[!DNL Facebook Custom Audience Terms of Service]계정 필수 구성 요소`business ID 206617933627973` 섹션의 URL 템플릿에 표시된 대로 [에서 &#x200B;](#facebook-account-prerequisites)을(를) 수락해야 합니다.

`400 Bad Request`Facebook 계정 필수 구성 요소[의 단계를 수행한 후 &#x200B;](#facebook-account-prerequisites) 오류 메시지가 표시되면 [!DNL Facebook] 권한이 적용될 수 있는 기간을 며칠으로 허용하십시오.


