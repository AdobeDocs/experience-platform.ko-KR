---
keywords: facebook 연결;facebook 연결;facebook 대상;facebook;instagram;메신저;facebook 메신저
title: Facebook 연결
description: 해시된 이메일을 기반으로 한 대상자 타겟팅, 개인화 및 억제에 대한 Facebook 캠페인용 프로필을 활성화합니다.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 37e8d36d89bf984673345743b371c31b4bb1f94d
workflow-type: tm+mt
source-wordcount: '1926'
ht-degree: 6%

---

# [!DNL Facebook] 연결

## 개요 {#overview}

에 대한 프로필 활성화 [!DNL Facebook] 해시된 이메일을 기반으로 한 대상자 타겟팅, 개인화 및 억제용 캠페인

대상 타깃팅에 이 대상을 사용할 수 있습니다. [!DNL Facebook's] 에서 지원하는 앱 제품군 [!DNL Custom Audiences], 포함 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], 및 [!DNL Messenger]. 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

![Adobe Experience Platform UI의 facebook 대상](../../assets/catalog/social/facebook/catalog.png)

## 사용 사례

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Facebook] 대상: Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 샘플 사용 사례입니다.

### 사용 사례 #1

온라인 소매업체는 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문을 기반으로 개인화된 오퍼를 표시하려고 합니다. 온라인 소매업체는 자신의 CRM에서 Adobe Experience Platform으로 이메일 주소를 수집하고 자신의 오프라인 데이터에서 대상을 빌드하여 이러한 대상을 로 보낼 수 있습니다. [!DNL Facebook] 소셜 플랫폼, 광고 지출을 최적화.

### 사용 사례 #2

항공사에는 다양한 고객 계층(브론즈, 실버 및 골드)이 있으며 소셜 플랫폼을 통해 각 계층에 개인화된 오퍼를 제공하려고 합니다. 다만 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 이들 중 일부는 회사 홈페이지에 로그인하지 않은 상태다. 회사에 이러한 고객에 대한 유일한 식별자는 멤버십 ID와 이메일 주소입니다.

소셜 미디어에서 고객을 타깃팅하기 위해 이메일 주소를 식별자로 사용하여 CRM의 고객 데이터를 Adobe Experience Platform에 온보딩할 수 있습니다.

그런 다음 관련 멤버십 ID 및 고객 계층을 비롯한 오프라인 데이터를 사용하여 를 통해 타깃팅할 수 있는 새 대상을 구축할 수 있습니다. [!DNL Facebook] 대상.

## 지원되는 ID {#supported-identities}

[!DNL Facebook Custom Audiences] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 의 지침을 따르십시오. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 일반 텍스트와 해시된 전화 번호에 대해 각각 적절한 네임스페이스를 선택하고 사용하십시오. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 의 지침을 따르십시오. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 일반 텍스트와 해시된 이메일 주소에 각각 적절한 네임스페이스를 섹션으로 지정하고 사용하십시오. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 모든 대상에 대해 설명합니다.

이 대상은 Experience Platform을 통해 생성된 모든 대상의 활성화를 지원합니다 [세분화 서비스](../../../segmentation/home.md).

*추가로*, 이 대상은 아래 표에 설명된 대상의 활성화도 지원합니다.

| 대상자 유형 | 설명 |
---------|----------|
| 사용자 정의 업로드 | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | facebook 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상자를 다음으로 보내기 전 [!DNL Facebook], 다음 요구 사항을 충족하는지 확인하십시오.

* 사용자 [!DNL Facebook] 사용자 계정에 대한 전체 액세스 권한이 있어야 함 [!DNL Facebook Business Account] 사용할 광고 계정을 소유하는 계정입니다.
* 사용자 [!DNL Facebook] 사용자 계정에는 **[!DNL Manage campaigns]** 사용하려는 광고 계정에 대해 권한이 활성화되었습니다.
* 다음 **Adobe Experience Cloud** 비즈니스 계정을 의 광고 파트너로 추가해야 합니다. [!DNL Facebook Ad Account]. `business ID=206617933627973` 사용. 다음을 참조하십시오 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897) 자세한 내용은 Facebook 설명서 를 참조하십시오.
  >[!IMPORTANT]
  >
  > Adobe Experience Cloud에 대한 권한을 구성할 때 다음을 활성화해야 합니다 **캠페인 관리** 권한. 다음에 대한 권한이 필요합니다. [!DNL Adobe Experience Platform] 통합.
* 읽기 및 서명 [!DNL Facebook Custom Audiences] 서비스 약관. 이렇게 하려면 다음으로 이동합니다. `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, 여기서 `accountID` 본인 [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >서명 시 [!DNL Facebook Custom Audiences] 서비스 약관에서 Facebook API에서 인증하는 데 사용한 것과 동일한 사용자 계정을 사용해야 합니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Facebook] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL Facebook] 키 사용 안 함 *해시됨* 이메일 주소 또는 전화번호 등 식별자.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 전화번호 해시 요구 사항 {#phone-number-hashing-requirements}

에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다 [!DNL Facebook]:

* **원시 전화번호 수집**: 에서 원시 전화 번호를 수집할 수 있습니다. [!DNL E.164] 서식 [!DNL Platform]. 활성화 시 자동으로 해시됩니다. 이 옵션을 선택하는 경우 항상 원시 전화 번호를 `Phone_E.164` 네임스페이스입니다.
* **해시된 전화번호 수집**: 로 수집하기 전에 전화 번호를 사전 해시할 수 있습니다. [!DNL Platform]. 이 옵션을 선택하는 경우 해시된 전화 번호를 항상 `Phone_SHA256` 네임스페이스입니다.

>[!NOTE]
>
>에 수집된 전화번호 `Phone` 네임스페이스를에서 활성화할 수 없음 [!DNL Facebook].

## 이메일 해시 요구 사항 {#email-hashing-requirements}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 이메일 주소를 지우고 다음을 수행할 수 있습니다. [!DNL Platform] 활성화 시 해시합니다.

Experience Platform에서 이메일 주소 수집에 대한 자세한 내용은 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](/help/ingestion/streaming-ingestion/overview.md).

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 준수해야 합니다.

* 이메일 문자열에서 선행 및 후행 공백을 모두 트리밍합니다. 예: `johndoe@example.com`, 아님 `<space>johndoe@example.com<space>`;
* 이메일 문자열을 해시할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, 아님 `EXAMPLE@EMAIL.COM`;
* 해시된 문자열이 모두 소문자인지 확인합니다.
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, 아님 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 문자열에 소금을 뿌리지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 다음에 의해 자동으로 해시됩니다. [!DNL Platform] 활성화 시.
> 속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.
> 다음 **[!UICONTROL 변환 적용]** 옵션은 속성을 소스 필드로 선택하는 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 사용자 정의 네임스페이스 사용 {#custom-namespaces}

을(를) 사용하기 전에 `Extern_ID` 데이터를 보낼 네임스페이스 [!DNL Facebook]를 사용하여 자체 식별자를 동기화해야 합니다 [!DNL Facebook Pixel]. 다음을 참조하십시오. [Facebook 공식 설명서](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) 을 참조하십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

아래 비디오에서는 을(를) 구성하는 단계도 보여 줍니다. [!DNL Facebook] 대상 및 대상자 활성화

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며, 이 비디오 녹화 이후에 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md).

### 대상에 인증 {#authenticate}

1. 대상 카탈로그에서 Facebook 대상을 찾고 을 선택합니다. **[!UICONTROL 설정]**.
2. 선택 **[!UICONTROL 대상에 연결]**.
   ![facebook 인증](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. facebook 자격 증명을 입력하고 다음을 선택합니다. **로그인**.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="계정 ID"
>abstract="Facebook 광고 계정 ID. Facebook Ads Manager 계정에서 이 ID를 찾을 수 있습니다. 이 ID를 입력할 때 항상 `act_`로 접두사가 붙습니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Facebook Ad Account ID]. 이 ID는 [!DNL Facebook Ads Manager] 계정입니다. 이 ID를 입력할 때 항상 `act_`로 접두사가 붙습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대상자 활성화 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="대상자 원본"
>abstract="원래 대상자의 고객 데이터를 수집하는 방법을 선택합니다. 사용자가 세그먼트에 타겟팅되면 데이터가 Facebook에 표시됩니다."

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
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

다음에서 **[!UICONTROL 세그먼트 일정]** 단계, 다음을 제공해야 합니다. [!UICONTROL 대상자 원본] 대상자를 (으)로 보낼 때 [!DNL Facebook Custom Audiences].

![Facebook 대상자 기원](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 매핑 예:에서 대상 데이터 활성화 [!DNL Facebook Custom Audience] {#example-facebook}

아래는에서 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다 [!DNL Facebook Custom Audience].

소스 필드 선택:

* 다음 항목 선택 `Email` 사용 중인 이메일 주소가 해시되지 않은 경우 소스 id로서의 네임스페이스.
* 다음 항목 선택 `Email_LC_SHA256` 데이터 수집에 대한 고객 이메일 주소를 해시한 경우 소스 id로서의 네임스페이스 [!DNL Platform]에 따라 [!DNL Facebook] [이메일 해시 요구 사항](#email-hashing-requirements).
* 다음 항목 선택 `PHONE_E.164` 데이터가 해시되지 않은 전화 번호로 구성된 경우 소스 id로 네임스페이스입니다. [!DNL Platform] 은(는) 다음을 준수하기 위해 전화번호를 해시합니다. [!DNL Facebook] 요구 사항.
* 다음 항목 선택 `Phone_SHA256` 데이터 수집 시 전화번호를 해시한 경우 소스 id로 네임스페이스 [!DNL Platform]에 따라 [!DNL Facebook] [전화번호 해시 요구 사항](#phone-number-hashing-requirements).
* 다음 항목 선택 `IDFA` 네임스페이스 를 소스 id로 사용 [!DNL Apple] 장치 ID.
* 다음 항목 선택 `GAID` 네임스페이스 를 소스 id로 사용 [!DNL Android] 장치 ID.
* 다음 항목 선택 `Custom` 데이터가 다른 유형의 식별자로 구성된 경우 네임스페이스 를 소스 id로 사용합니다.

대상 필드 선택:

* 다음 항목 선택 `Email_LC_SHA256` 소스 네임스페이스가 다음 중 하나일 때 타겟 ID로서의 네임스페이스 `Email` 또는 `Email_LC_SHA256`.
* 다음 항목 선택 `Phone_SHA256` 소스 네임스페이스가 다음 중 하나일 때 타겟 ID로서의 네임스페이스 `PHONE_E.164` 또는 `Phone_SHA256`.
* 다음 항목 선택 `IDFA` 또는 `GAID` 소스 네임스페이스가 다음과 같을 때 타겟 ID로서의 네임스페이스 `IDFA` 또는 `GAID`.
* 다음 항목 선택 `Extern_ID` 소스 네임스페이스가 사용자 정의 네임스페이스인 경우 네임스페이스를 타겟 ID로.

>[!IMPORTANT]
>
>해시되지 않은 네임스페이스의 데이터는 다음에 의해 자동으로 해시됩니다. [!DNL Platform] 활성화 시.
> 
>속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.

![ID 매핑](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 내보낸 데이터 {#exported-data}

대상 [!DNL Facebook], 활성화가 성공하면 [!DNL Facebook] 사용자 지정 대상은에서 프로그래밍 방식으로 만들어집니다. [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). 사용자가 활성화된 대상자에 대해 자격이 부여되거나 자격을 상실하면 대상자 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 의 통합 [!DNL Facebook] 는 과거 대상자 채우기를 지원합니다. 모든 과거 대상 자격 요건이 (으)로 전송됩니다. [!DNL Facebook] 대상을 대상에 대해 활성화하면

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

이 오류는 고객이 새로 만든 계정을 사용할 때 발생합니다. [!DNL Facebook] 사용 권한이 아직 활성화되지 않았습니다.

다음을 받는 경우 `400 Bad Request` 의 단계를 수행한 후 오류 메시지 표시 [Facebook 계정 사전 요구 사항](#facebook-account-prerequisites), 며칠간 을(를) 허용하십시오. [!DNL Facebook] 적용할 권한입니다.
