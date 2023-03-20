---
keywords: facebook 연결;facebook 연결;facebook 대상;facebook;instagram;messenger;facebook messenger
title: Facebook 연결
description: 해시된 이메일을 기반으로 대상 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인용 프로필을 활성화합니다.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 70670f7aec2ab6a5594f5e69672236c7bcc3ce81
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 1%

---

# [!DNL Facebook] 연결

## 개요 {#overview}

에 대한 프로필 활성화 [!DNL Facebook] 해시된 이메일을 기반으로 하는 대상 타깃팅, 개인화 및 제외를 위한 캠페인.

대상 타깃팅에 이 대상을 사용할 수 있습니다 [!DNL Facebook’s] 가 지원하는 앱 제품군 [!DNL Custom Audiences], 포함 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], 및 [!DNL Messenger]. 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

![Adobe Experience Platform UI의 facebook 대상](../../assets/catalog/social/facebook/catalog.png)

## 사용 사례

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Facebook] 대상 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 #1

온라인 소매업체는 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문에 따라 개인화된 오퍼를 제공하려고 합니다. 온라인 소매업체는 고유한 CRM의 이메일 주소를 Adobe Experience Platform에 수집하고, 자체 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 로 보낼 수 있습니다 [!DNL Facebook] 소셜 플랫폼, 광고 비용 최적화.

### 사용 사례 #2

항공사에는 다양한 고객 계층(청동, 실버, 골드)이 있으며, 소셜 플랫폼을 통해 각 계층에 개인화된 오퍼를 제공하려고 합니다. 그러나 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 일부 고객은 회사의 웹 사이트에 로그온하지 않았습니다. 이 고객에 대해 회사가 가지고 있는 유일한 식별자는 멤버십 ID 및 이메일 주소입니다.

소셜 미디어에서 타깃팅하기 위해 이메일 주소를 식별자로 사용하여 CRM에서 Adobe Experience Platform으로 고객 데이터를 온보딩할 수 있습니다.

다음으로, 연결된 멤버십 ID 및 고객 계층을 포함한 오프라인 데이터를 사용하여 를 통해 타깃팅할 수 있는 새로운 대상 세그먼트를 만들 수 있습니다 [!DNL Facebook] 대상.

## 지원되는 ID {#supported-identities}

[!DNL Facebook Custom Audiences] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. 다음 [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션에서 그리고 일반 텍스트와 해시된 전화 번호에 적합한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 다음 [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션에서 그리고 개별 텍스트 및 해시된 이메일 주소에 적절한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스이면 이 타겟 ID를 선택합니다. |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | facebook 대상에 사용되는 식별자(이름, 전화 번호 또는 기타 식별자)로 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상 세그먼트를 보내기 전에 [!DNL Facebook]를 채울 때는 다음 요구 사항을 충족하는지 확인하십시오.

* 사용자 [!DNL Facebook] 사용자 계정에는 **[!DNL Manage campaigns]** 사용하려는 광고 계정에 대해 사용 권한이 활성화되었습니다.
* 다음 **Adobe Experience Cloud** 비즈니스 계정을 귀사의 광고 파트너로서 추가해야 합니다 [!DNL Facebook Ad Account]. `business ID=206617933627973` 사용. 자세한 내용은 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897) 자세한 내용은 Facebook 설명서 을 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 **캠페인 관리** 권한. 에는 권한이 필요합니다. [!DNL Adobe Experience Platform] 통합.
* 읽기 및 서명 [!DNL Facebook Custom Audiences] 서비스 약관. 이렇게 하려면 로 이동하십시오. `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, 위치 `accountID` 은 [!DNL Facebook Ad Account ID].
   >[!IMPORTANT]
   >
   >서명 시 [!DNL Facebook Custom Audiences] 서비스 약관은 Facebook API에서 인증하는 데 사용한 것과 동일한 사용자 계정을 사용해야 합니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Facebook] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상이 [!DNL Facebook] 키오프 가능 *해시* 이메일 주소 또는 전화 번호와 같은 식별자.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 전화 번호 해싱 요구 사항 {#phone-number-hashing-requirements}

에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다 [!DNL Facebook]:

* **원시 전화 번호 수집**: 전화 번호를 [!DNL E.164] 포맷 [!DNL Platform]. 활성화 시 자동으로 해시됩니다. 이 옵션을 선택하는 경우 항상 원시 전화 번호를 `Phone_E.164` 네임스페이스.
* **해시된 전화 번호 수집**: 에 수집하기 전에 전화 번호를 미리 해시할 수 있습니다. [!DNL Platform]. 이 옵션을 선택하는 경우 해시된 휴대폰 번호를 항상 `Phone_SHA256` 네임스페이스.

>[!NOTE]
>
>에 수집된 전화 번호 `Phone` 네임스페이스는에서 활성화할 수 없습니다. [!DNL Facebook].

## 이메일 해싱 요구 사항 {#email-hashing-requirements}

전자 메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 명확히 전자 메일 주소를 사용하여 다음을 보유할 수 있습니다. [!DNL Platform] 활성화 시 해시합니다.

Experience Platform에서 이메일 주소 섭취에 대한 자세한 내용은 [배치 수집 개요](/help/ingestion/batch-ingestion/overview.md) 그리고 [스트리밍 수집 개요](/help/ingestion/streaming-ingestion/overview.md).

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 충족하는지 확인하십시오.

* 전자 메일 문자열에서 선행 및 후행 공백을 모두 잘라냅니다. 예: `johndoe@example.com`, 아님 `<space>johndoe@example.com<space>`;
* 이메일 문자열을 해시할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, 아님 `EXAMPLE@EMAIL.COM`;
* 해시된 문자열이 모두 소문자로 되어 있는지 확인하십시오
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, 아님 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 문자열의 소금을 치지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 [!DNL Platform] 활성화 시.
> 속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.
> 다음 **[!UICONTROL 변형 적용]** 옵션은 속성을 소스 필드로 선택하는 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 사용자 지정 네임스페이스 사용 {#custom-namespaces}

를 사용하기 전에 `Extern_ID` 데이터를에 보낼 네임스페이스 [!DNL Facebook]를 사용하여 고유한 식별자를 동기화해야 합니다. [!DNL Facebook Pixel]. 자세한 내용은 [Facebook 공식 설명서](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) 자세한 정보

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

아래 비디오에서는 을(를) 구성하는 단계를 보여줍니다 [!DNL Facebook] 대상 및 세그먼트 활성화

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며 이 비디오를 기록한 후 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md).

### 대상에 인증 {#authenticate}

1. 대상 카탈로그에서 Facebook 대상을 찾고 을(를) 선택합니다 **[!UICONTROL 설정]**.
2. 선택 **[!UICONTROL 대상에 연결]**.
   ![facebook 인증](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. facebook 자격 증명을 입력하고 을(를) 선택합니다 **로그인**.

### 대상 세부 사항 채우기 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="계정 ID"
>abstract="facebook 광고 계정 ID입니다. 이 ID는 Facebook Ads Manager 계정에서 찾을 수 있습니다. 이 ID를 입력할 때 항상 접두사로 붙입니다 `act_`."

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Facebook Ad Account ID]. 이 ID는 [!DNL Facebook Ads Manager] 계정이 필요합니다. 이 ID를 입력할 때 항상 접두사로 붙입니다 `act_`.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="대상의 기원"
>abstract="원래 세그먼트에서 고객 데이터를 수집한 방법을 선택합니다. 사용자가 세그먼트에 의해 타깃팅되면 데이터가 Facebook에 표시됩니다"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="대상의 기원"
>abstract="광고주는 고객으로부터 직접 데이터를 수집했습니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="대상의 기원"
>abstract="광고주는 파트너로부터 직접 데이터를 수집합니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="대상의 기원"
>abstract="광고주는 고객 및 파트너로부터 직접 데이터를 수집합니다."

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

에서 **[!UICONTROL 세그먼트 예약]** 단계에서는 다음을 제공해야 합니다 [!UICONTROL 대상의 기원] 세그먼트를 [!DNL Facebook Custom Audiences].

![대상의 facebook 기원](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 매핑 예: 의 대상 데이터 활성화 [!DNL Facebook Custom Audience] {#example-facebook}

아래는 의 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다 [!DNL Facebook Custom Audience].

소스 필드 선택:

* 을(를) 선택합니다 `Email` 사용 중인 이메일 주소가 해시되지 않은 경우 소스 ID로 네임스페이스 를 지정합니다.
* 을(를) 선택합니다 `Email_LC_SHA256` 데이터 수집 시 고객 이메일 주소를 해시한 경우 소스 ID로 네임스페이스 [!DNL Platform]에 따라 [!DNL Facebook] [이메일 해싱 요구 사항](#email-hashing-requirements).
* 을(를) 선택합니다 `PHONE_E.164` 네임스페이스 는 데이터가 해시되지 않은 전화 번호로 구성된 경우 소스 id로 사용됩니다. [!DNL Platform] 이(가) [!DNL Facebook] 요구 사항.
* 을(를) 선택합니다 `Phone_SHA256` 데이터 수집 시 해시된 전화번호를 소스 ID로 네임스페이스 [!DNL Platform]에 따라 [!DNL Facebook] [전화 번호 해싱 요구 사항](#phone-number-hashing-requirements).
* 을(를) 선택합니다 `IDFA` 데이터가 [!DNL Apple] 장치 ID.
* 을(를) 선택합니다 `GAID` 데이터가 [!DNL Android] 장치 ID.
* 을(를) 선택합니다 `Custom` 네임스페이스 는 데이터가 다른 유형의 식별자로 구성된 경우 소스 id로 사용됩니다.

대상 필드 선택:

* 을(를) 선택합니다 `Email_LC_SHA256` 소스 네임스페이스가 `Email` 또는 `Email_LC_SHA256`.
* 을(를) 선택합니다 `Phone_SHA256` 소스 네임스페이스가 `PHONE_E.164` 또는 `Phone_SHA256`.
* 을(를) 선택합니다 `IDFA` 또는 `GAID` 소스 네임스페이스가 타겟 ID인 경우 네임스페이스가 네임스페이스입니다 `IDFA` 또는 `GAID`.
* 을(를) 선택합니다 `Extern_ID` 네임스페이스 는 소스 네임스페이스가 사용자 지정 네임스페이스일 때 타겟 id로 사용됩니다.

>[!IMPORTANT]
>
>해시되지 않은 네임스페이스의 데이터는 [!DNL Platform] 활성화 시.
> 
>속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.

![ID 매핑](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 내보낸 데이터 {#exported-data}

대상 [!DNL Facebook]를 활성화한 후에는 [!DNL Facebook] 사용자 지정 대상은 프로그래밍 방식으로 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). 사용자가 활성화된 세그먼트에 대한 자격이 있거나 자격 미달되면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 의 통합 [!DNL Facebook] 이전 대상 채우기 기능을 지원합니다. 모든 이전 세그먼트 자격이 [!DNL Facebook] 세그먼트를 대상에 활성화하는 경우.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

이 오류는 고객이 새로 만든 계정을 사용하고 [!DNL Facebook] 사용 권한이 아직 활성 상태가 아닙니다.

받는 경우 `400 Bad Request` 다음 단계를 수행한 후 오류 메시지 [Facebook 계정 사전 요구 사항](#facebook-account-prerequisites)에 대해 며칠 동안 기다려 주십시오. [!DNL Facebook] 적용할 권한 .
