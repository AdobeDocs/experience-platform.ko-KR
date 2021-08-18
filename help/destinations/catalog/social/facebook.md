---
keywords: facebook 연결;facebook 연결;facebook 대상;facebook;instagram;messenger;facebook messenger
title: Facebook 연결
description: 해시된 이메일을 기반으로 대상 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인용 프로필을 활성화합니다.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 183aff5a3b6bcc1635ae7b4b0e503a9d4b6d4d31
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 1%

---

# [!DNL Facebook] 연결

## 개요 {#overview}

해시된 이메일을 기반으로 대상 타깃팅, 개인화 및 억제를 위해 [!DNL Facebook] 캠페인에 대한 프로필을 활성화합니다.

[!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] 및 [!DNL Messenger]를 포함하여 [!DNL Custom Audiences]에서 지원하는 앱 제품군에서 대상 타깃팅에 이 대상을 사용할 수 있습니다. [!DNL Facebook’s] 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

![Adobe Experience Platform UI의 facebook 대상](../../assets/catalog/social/facebook/catalog.png)

## 사용 사례

[!DNL Facebook] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 샘플 사용 사례가 있습니다.

### 사용 사례 #1

온라인 소매업체는 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문에 따라 개인화된 오퍼를 제공하려고 합니다. 온라인 소매점은 자체 CRM의 이메일 주소를 Adobe Experience Platform에 수집하고, 자체 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 [!DNL Facebook] 소셜 플랫폼으로 전송하여 광고 비용을 최적화할 수 있습니다.

### 사용 사례 #2

항공사에는 다양한 고객 계층(청동, 실버, 골드)이 있으며, 소셜 플랫폼을 통해 각 계층에 개인화된 오퍼를 제공하려고 합니다. 그러나 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 일부 고객은 회사의 웹 사이트에 로그온하지 않았습니다. 이 고객에 대해 회사가 가지고 있는 유일한 식별자는 멤버십 ID 및 이메일 주소입니다.

소셜 미디어에서 타깃팅하기 위해 이메일 주소를 식별자로 사용하여 CRM에서 Adobe Experience Platform으로 고객 데이터를 온보딩할 수 있습니다.

그런 다음 연결된 멤버십 ID 및 고객 계층을 포함한 오프라인 데이터를 사용하여 [!DNL Facebook] 대상을 통해 타깃팅할 수 있는 새로운 대상 세그먼트를 만들 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL Facebook Custom Audiences] 은 아래 표에 설명된 id의 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침에 따라 일반 텍스트 및 해시된 전화 번호에 적합한 네임스페이스를 각각 사용하십시오. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침에 따라 일반 텍스트 및 해시된 이메일 주소에 적합한 네임스페이스를 각각 사용하십시오. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스이면 이 타겟 ID를 선택합니다. |

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - Facebook 대상에 사용되는 식별자(이름, 전화번호 또는 기타)로 세그먼트(대상)의 모든 구성원을 내보냅니다.

## Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상 세그먼트를 [!DNL Facebook]에 보내려면 먼저 다음 요구 사항을 충족하는지 확인하십시오.

* 사용하려는 광고 계정에 대해 **[!DNL Manage campaigns]** 사용 권한이 활성화되어 있어야 합니다.[!DNL Facebook]
* **Adobe Experience Cloud** 비즈니스 계정은 [!DNL Facebook Ad Account]에서 광고 파트너로서 추가해야 합니다.  `business ID=206617933627973`. 자세한 내용은 Facebook 설명서의 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897)를 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 **캠페인 관리** 권한을 활성화해야 합니다. [!DNL Adobe Experience Platform] 통합에 대한 권한이 필요합니다.
* [!DNL Facebook Custom Audiences] 서비스 약관을 읽고 서명하십시오. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` 로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Facebook] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 [!DNL Facebook]에 활성화된 대상은 이메일 주소 또는 전화 번호와 같이 *해시된* 식별자를 사용할 수 있습니다.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 전화 번호 해싱 요구 사항 {#phone-number-hashing-requirements}

[!DNL Facebook]에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다.

* **원시 전화 번호 수집**: 원시 전화 번호를 형식으로  [!DNL E.164] 수집할 수  [!DNL Platform]있습니다. 활성화 시 자동으로 해시됩니다. 이 옵션을 선택하는 경우 반드시 원시 전화 번호를 항상 `Phone_E.164` 네임스페이스에 수집하십시오.
* **해시된 전화 번호 수집**: 에 수집하기 전에 전화 번호를 미리 해시할 수 있습니다 [!DNL Platform]. 이 옵션을 선택하는 경우 해시된 전화 번호를 항상 `Phone_SHA256` 네임스페이스에 수집해야 합니다.

>[!NOTE]
>
>`Phone` 네임스페이스에 수집된 전화 번호는 [!DNL Facebook]에서 활성화할 수 없습니다.


## 이메일 해싱 요구 사항 {#email-hashing-requirements}

전자 메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 명확히 전자 메일 주소를 사용할 수 있으며 [!DNL Platform] 해시 처리할 수 있습니다.

Experience Platform에서 이메일 주소를 수집하는 방법에 대한 자세한 내용은 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](/help/ingestion/streaming-ingestion/overview.md)를 참조하십시오.

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 충족하는지 확인하십시오.

* 전자 메일 문자열에서 선행 및 후행 공백을 모두 잘라냅니다. 예: `<space>johndoe@example.com<space>`;이 아닌 `johndoe@example.com`
* 이메일 문자열을 해시할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `EXAMPLE@EMAIL.COM`;이 아닌 `example@email.com`
* 해시된 문자열이 모두 소문자로 되어 있는지 확인하십시오
   * 예: `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;이 아닌 `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`
* 문자열의 소금을 치지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Platform]에 의해 자동으로 해시됩니다.
> 속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오.
> **[!UICONTROL 변환 적용]** 옵션은 속성을 소스 필드로 선택한 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 사용자 지정 네임스페이스 사용 {#custom-namespaces}

`Extern_ID` 네임스페이스를 사용하여 데이터를 [!DNL Facebook]에 보내려면 먼저 [!DNL Facebook Pixel]를 사용하여 자체 식별자를 동기화해야 합니다. 자세한 내용은 [Facebook 공식 설명서](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)를 참조하십시오.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

아래 비디오에서는 [!DNL Facebook] 대상을 구성하고 세그먼트를 활성화하는 단계를 보여줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며 이 비디오를 기록한 후 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md)를 참조하십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자  [!DNL Facebook Ad Account ID]. 이 ID는 [!DNL Facebook Ads Manager] 계정에서 찾을 수 있습니다. 이 ID를 입력할 때 항상 `act_` 접두사로 붙입니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

**[!UICONTROL 세그먼트 일정]** 단계에서 세그먼트를 [!DNL Facebook Custom Audiences]에 보낼 때 [!UICONTROL 대상]의 출처를 제공해야 합니다.

![대상의 facebook 기원](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 매핑 예: [!DNL Facebook Custom Audience]에서 대상 데이터 활성화 {#example-facebook}

다음은 [!DNL Facebook Custom Audience]에서 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* 사용 중인 전자 메일 주소가 해시되지 않은 경우 `Email` 네임스페이스를 소스 ID로 선택합니다.
* [!DNL Facebook] [이메일 해싱 요구 사항](#email-hashing-requirements)에 따라 [!DNL Platform]로 데이터 처리에 대한 고객 이메일 주소를 해시한 경우 `Email_LC_SHA256` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 해시되지 않은 전화 번호로 구성된 경우 `PHONE_E.164` 네임스페이스를 소스 ID로 선택합니다. [!DNL Platform] 은 요구 사항을 준수하도록 전화 번호를 해시합니다 [!DNL Facebook] .
* [!DNL Facebook] [전화 번호 해싱 요구 사항](#phone-number-hashing-requirements)에 따라 데이터 처리에 대한 전화 번호를 해시하면 `Phone_SHA256` 네임스페이스를 소스 ID로 선택합니다.[!DNL Platform]
* 데이터가 [!DNL Apple] 장치 ID로 구성된 경우 `IDFA` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 [!DNL Android] 장치 ID로 구성된 경우 `GAID` 네임스페이스를 소스 ID로 선택합니다.
* 데이터가 다른 유형의 식별자로 구성된 경우 `Custom` 네임스페이스를 소스 ID로 선택합니다.

대상 필드 선택:

* 소스 네임스페이스가 `Email` 또는 `Email_LC_SHA256`인 경우 `Email_LC_SHA256` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 `PHONE_E.164` 또는 `Phone_SHA256`인 경우 `Phone_SHA256` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 `IDFA` 또는 `GAID`인 경우 `IDFA` 또는 `GAID` 네임스페이스를 대상 ID로 선택합니다.
* 소스 네임스페이스가 사용자 지정 네임스페이스일 때 `Extern_ID` 네임스페이스를 대상 ID로 선택합니다.

>[!IMPORTANT]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Platform]에 의해 자동으로 해시됩니다.
> 
>속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오.

![ID 매핑](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 내보낸 데이터 {#exported-data}

[!DNL Facebook]의 경우 성공적인 활성화는 [!DNL Facebook] 사용자 지정 대상이 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)에서 프로그래밍 방식으로 생성됨을 의미합니다. 사용자가 활성화된 세그먼트에 대한 자격이 있거나 자격 미달되면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 [!DNL Facebook] 간의 통합은 이전 대상 채우기 기능을 지원합니다. 세그먼트를 대상으로 활성화하면 모든 이전 세그먼트 자격이 [!DNL Facebook]으로 전송됩니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

세그먼트를 [!DNL Facebook]에 활성화할 때 다음 오류가 발생할 수 있습니다.

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

이 오류는 고객이 새로 만든 계정을 사용하고 있으며 [!DNL Facebook] 권한이 아직 활성 상태가 아닌 경우에 발생합니다.

[Facebook 계정 사전 요구 사항](#facebook-account-prerequisites)의 단계를 수행한 후 `400 Bad Request` 오류 메시지를 받는 경우 [!DNL Facebook] 권한이 적용되려면 며칠 동안 기다리십시오.