---
keywords: facebook 연결;facebook 연결;facebook 대상;facebook;instagram;messenger;facebook messenger;facebook 연결;facebook 연결;facebook 연결;facebook 연결;facebook destinagram;messenger;facebook messenger;messenger
title: Facebook 연결
description: 해시 처리된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 2%

---


# [!DNL Facebook] 연결

## 개요 {#overview}

해시 처리된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 [!DNL Facebook] 캠페인에 대한 프로파일을 활성화합니다.

[!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] 및 [!DNL Messenger]를 포함하여 [!DNL Custom Audiences] 제품군에서 대상 타깃팅에 이 대상을 사용할 수 있습니다. [!DNL Facebook’s] 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

![Adobe Experience Platform UI의 Facebook 대상](../../assets/catalog/social/facebook/catalog.png)

## 사용 사례

[!DNL Facebook] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 샘플 사용 사례를 소개합니다.

### 사용 사례 #1

온라인 소매업체는 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문에 따라 개인화된 제안을 제공하기를 원합니다. 온라인 소매업체는 자사의 CRM에서 Adobe Experience Platform으로 이메일 주소를 인제스트하고 자체 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 [!DNL Facebook] 소셜 플랫폼으로 보내 광고 지출을 최적화할 수 있습니다.

### 사용 사례 #2

항공사는 다양한 고객 계층(브론즈, 실버, 골드)을 가지며 소셜 플랫폼을 통해 각 계층에 맞춤형 제안을 제공하고 싶어합니다. 그러나 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 그들 중 일부는 회사의 웹사이트에 로그인하지 않았습니다. 회사가 이러한 고객에 대해 가지고 있는 유일한 식별자는 멤버십 ID 및 이메일 주소입니다.

소셜 미디어에서 이들을 타깃팅하기 위해 이메일 주소를 식별자로 사용하여 CRM의 고객 데이터를 Adobe Experience Platform으로 가져올 수 있습니다.

다음으로, 연결된 멤버십 ID 및 고객 계층을 비롯한 오프라인 데이터를 사용하여 [!DNL Facebook] 대상을 통해 타깃팅할 수 있는 새 대상 세그먼트를 만들 수 있습니다.

## [!DNL Facebook] 대상 {#data-governance}에 대한 데이터 거버넌스

>[!IMPORTANT]
>
>[!DNL Facebook]으로 전송된 데이터에는 연결된 ID가 포함될 수 없습니다. 귀하는 이러한 의무를 지킬 책임이 있으며, 활성화를 위해 선택한 세그먼트가 병합 정책에 봉합 옵션을 사용하지 않도록 하여 이를 수행할 수 있습니다. [병합 정책](/help/profile/ui/merge-policies.md)에 대해 자세히 알아보십시오.

## 지원되는 ID {#supported-identities}

[!DNL Facebook Custom Audiences] 에서는 아래 표에 설명된 ID 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| phone_sha256 | SHA256 알고리즘으로 전화 번호 해시됨 | 일반 텍스트와 SHA256 해시된 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침을 따르고 일반 텍스트 및 해시 전화 번호에 적합한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침을 따르고 일반 텍스트 및 해시된 이메일 주소에 적합한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - Facebook 대상에 사용된 식별자(이름, 전화 번호 또는 기타)를 사용하여 세그먼트(대상자)의 모든 구성원을 내보냅니다.

## Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상 세그먼트를 [!DNL Facebook]에 보내려면 먼저 다음 요구 사항을 충족해야 합니다.

- [!DNL Facebook] 사용자 계정은 사용하려는 광고 계정에 대해 **[!DNL Manage campaigns]** 권한이 활성화되어 있어야 합니다.
- **Adobe Experience Cloud** 비즈니스 계정을 [!DNL Facebook Ad Account]에서 광고 파트너로 추가해야 합니다.  `business ID=206617933627973`. 자세한 내용은 Facebook 설명서의 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897)를 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 **캠페인 관리** 권한을 활성화해야 합니다. [!DNL Adobe Experience Platform] 통합에 대한 권한이 필요합니다.
- [!DNL Facebook Custom Audiences] 서비스 약관을 읽고 서명합니다. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`으로 이동합니다. 여기서 `accountID`은 [!DNL Facebook Ad Account ID]입니다.

## 요구 사항 {#id-matching-requirements} 일치하는 ID

[!DNL Facebook] 는 PII(개인 식별 정보)가 명확하게 전송되지 않도록 요구합니다. 따라서 [!DNL Facebook]에 대해 활성화된 대상은 이메일 주소 또는 전화 번호와 같은 *해시된* 식별자에서 키잉할 수 있습니다.

Adobe Experience Platform에 인제스트하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 전화 번호 해싱 요구 사항 {#phone-number-hashing-requirements}

[!DNL Facebook]에는 전화 번호를 활성화하는 두 가지 방법이 있습니다.

- **원시 전화 번호 인제스트**:원시 전화 번호를 형식으로 인제스트할 수  [!DNL E.164] 있습니다 [!DNL Platform]. 활성화하면 자동으로 숨겨집니다. 이 옵션을 선택하는 경우 원시 전화 번호를 항상 `Phone_E.164` 네임스페이스로 인제스트해야 합니다.
- **해시된 전화 번호** 인제스트:수신 전에 전화 번호를 사전에 해시 처리할 수 있습니다 [!DNL Platform]. 이 옵션을 선택하는 경우 해시 처리된 전화 번호를 항상 `Phone_SHA256` 네임스페이스로 인제스트해야 합니다.

>[!NOTE]
>
>`Phone` 네임스페이스로 인제스트된 전화 번호는 [!DNL Facebook]에서 활성화할 수 없습니다.


## 전자 메일 해싱 요구 사항 {#email-hashing-requirements}

전자 메일 주소를 Adobe Experience Platform으로 인제스트하기 전에 해시하거나, Experience Platform에서 명확하게 전자 메일 주소를 사용하고 활성화 시 [!DNL Platform] 해시하도록 할 수 있습니다.

Experience Platform에서 이메일 주소 인제스트에 대한 자세한 내용은 [일괄 처리 통합 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 통합 개요](/help/ingestion/streaming-ingestion/overview.md)를 참조하십시오.

직접 이메일 주소를 해시하도록 선택한 경우 다음 요구 사항을 준수해야 합니다.

- 이메일 문자열에서 모든 행간 및 후행 공백을 트리밍합니다.예:`<space>johndoe@example.com<space>`;`johndoe@example.com`
- 이메일 문자열을 해싱할 때는 반드시 소문자 문자열을 해시해야 합니다.
   - 예:`EXAMPLE@EMAIL.COM`;`example@email.com`
- 해시된 문자열이 모두 소문자인지 확인
   - 예:`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`
- 문자열에 소금을 넣지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Platform]에 의해 자동으로 해시됩니다.
> 속성 소스 데이터가 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.
> **[!UICONTROL Apply transformation]** 옵션은 속성을 소스 필드로 선택할 때만 표시됩니다. 네임스페이스를 선택할 때 표시되지 않습니다.

![ID 매핑 변형](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 사용자 정의 네임스페이스 사용 {#custom-namespaces}

`Extern_ID` 네임스페이스를 사용하여 데이터를 [!DNL Facebook]에 보내려면 [!DNL Facebook Pixel]을(를) 사용하여 자체 식별자를 동기화해야 합니다. 자세한 내용은 [공식 설명서](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)를 참조하십시오.

## 대상 {#connect-destination}에 연결

[!DNL Facebook] 대상에 연결하려면 [소셜 네트워크 대상 인증 워크플로](./workflow.md)를 참조하십시오.

## 세그먼트를 [!DNL Facebook] {#activate-segments}에 활성화

세그먼트를 [!DNL Facebook]에 활성화하는 방법에 대한 지침은 [대상에 데이터 활성화](../../ui/activate-destinations.md)를 참조하십시오.

**[!UICONTROL Segment schedule]** 단계에서 세그먼트를 [!DNL Facebook Custom Audiences]에 보낼 때 [!UICONTROL Origin of audience]을 제공해야 합니다.

![대상자의 Facebook 출처](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## 내보낸 데이터 {#exported-data}

[!DNL Facebook]의 경우 [!DNL Facebook] 사용자 지정 대상이 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)에서 프로그래밍 방식으로 만들어진다는 의미입니다. 활성화된 세그먼트에 대해 자격이 부여되거나 자격이 부여되지 않으면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 [!DNL Facebook] 간의 통합은 이전 대상 채우기를 지원합니다. 세그먼트를 대상으로 활성화하면 모든 내역 세그먼트 자격 조건은 [!DNL Facebook]으로 전송됩니다.