---
title: 트레이드 데스크 - CRM 연결
description: CRM 데이터를 기반으로 대상 타기팅 및 억제에 대한 프로필을 트레이드 데스크 계정에 활성화합니다.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 2%

---

# [!DNL Trade Desk] - CRM 연결

>[!IMPORTANT]
>
>[대상 카탈로그](/help/destinations/catalog/overview.md)에 두 개의 Trade Desk(CRM 대상)가 있습니다.
>
>* EU에서 데이터를 원본으로 사용하는 경우 **[!DNL The Trade Desk - CRM (EU)]** 대상을 사용하십시오.
>* APAC 또는 NAMER 영역에서 데이터를 소싱할 경우 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 대상을 사용합니다.
>
>이 대상 커넥터 및 설명서 페이지는 *[!DNL Trade Desk]* 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 [!DNL Trade Desk] 담당자에게 문의하십시오.

## 개요 {#overview}

CRM 데이터를 기반으로 대상 타기팅 및 제외를 위해 [!DNL Trade Desk] 계정에 프로필을 활성화하는 방법을 이해합니다.

이 커넥터는 자사 데이터 활성화를 위해 데이터를 [!DNL The Trade Desk]에 보냅니다. [!DNL The Trade Desk]은(는) 해시되지 않은 원시 전자 메일과 전화 번호를 저장합니다.

>[!TIP]
>
>[!DNL The Trade Desk - CRM] 대상을 사용하여 CRM 데이터(전자 메일 및 전화 번호 등)와 쿠키 및 장치 ID와 같은 기타 자사 데이터 식별자를 보냅니다. 쿠키 및 장치 ID 매핑을 위해 Experience Platform 카탈로그의 [Trade Desk 대상](/help/destinations/catalog/advertising/tradedesk.md)을(를) 계속 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>트레이드 데스크에 대상자를 활성화하려면 먼저 [!DNL Trade Desk] 계정 관리자에게 문의하여 기능을 활성화해야 합니다. 전자 메일, 전화 번호 및 UID2/EUID를 보내는 경우 서명된 UID2/EUID 계약을 [!DNL The Trade Desk]과(와) 공유해야 합니다.

## ID 일치 요구 사항 {#id-matching-requirements}

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다. 자세한 내용은 [ID 네임스페이스 개요](/help/identity-service/features/namespaces.md)를 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL The Trade Desk]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

Adobe Experience Platform은 해시되지 않은 이메일 주소와 전화번호를 모두 지원합니다. ID 일치 요구 사항 섹션의 지침에 따라 일반 텍스트 및 해시된 이메일 주소에 적절한 네임스페이스를 각각 사용하십시오.

| 대상 ID | 설명 |
|---|---|
| 이메일 | 이메일 주소(텍스트 지우기) |
| Email_LC_SHA256 | 이메일 주소는 SHA256 및 소문자를 사용하여 해시해야 합니다. 나중에 이 설정을 변경할 수 없습니다. |
| 전화(E.164) | E.164 형식으로 정규화해야 하는 전화번호. E.164 형식에는 더하기 기호(+), 국제 국가 호출 코드, 지역 번호 및 전화 번호가 포함됩니다. 예: (+)(국가 코드)(지역 코드)(전화 번호). 이 식별자는 Trade Desk - 자사 데이터(EU)에서 사용할 수 없습니다. |
| 전화(SHA256_E.164) | E.164 형식으로 이미 표준화된 다음 SHA-256을 사용하여 해시된 전화 번호로, 해시 Base64가 인코딩되었습니다. 이 식별자는 Trade Desk - 자사 데이터(EU)에서 사용할 수 없습니다. |
| TDID | 트레이드 데스크의 쿠키 ID |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | 광고주용 Apple ID |
| UID2 | 원시 UID2 값 |
| UID2 토큰 | 광고 토큰이라고도 하는 암호화된 UID2 토큰. |
| EUID | 원시 유럽 연합 ID 값 |
| EUIDToken | 광고 토큰이라고도 하는 암호화된 EUID 토큰. |
| 램프 ID | 49자 또는 70자 RampID(이전에는 IdentityLink 또는 IDL이라고 함). Trade Desk에 대해 특별히 매핑된 LiveRamp의 RampID여야 합니다. |
| netID | 70자의 base64로 인코딩된 문자열인 사용자의 netID입니다. 이 ID는 유럽에서만 지원됩니다. |
| FirstID | 사용자의 First-id로, 일반적으로 프랑스의 게시자가 설정합니다. 이 ID는 유럽에서만 지원됩니다. |

{style="table-layout:auto"}

## 이메일 해시 요구 사항 {#email-hashing}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 원시 이메일 주소를 사용할 수 있습니다.

Experience Platform에서 전자 메일 주소를 수집하는 방법에 대해 알아보려면 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md)를 읽어 보십시오.

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 준수해야 합니다.

* 선행 및 후행 공백을 제거합니다.
* 모든 ASCII 문자를 소문자로 변환합니다.
* `gmail.com` 전자 메일 주소의 사용자 이름 부분에서 다음 문자를 제거하십시오.

      * 기간(`.`) 문자(ASCII 코드 46). 예를 들어 &#39;jane.doe@gmail.com&#39;을 &#39;janedoe@gmail.com&#39;으로 정규화합니다.
     * 더하기 기호(`+`) 문자(ASCII 코드 43) 및 모든 후속 문자입니다. 예를 들어 &#39;janedoe+home@gmail.com&#39;을 &#39;janedoe@gmail.com&#39;으로 정규화합니다.
  
## 전화번호 표준화 및 해시 요구 사항 {#phone-hashing}

다음은 전화번호 업로드에 대해 알아야 할 사항입니다.

* 요청에서 해시했거나 해시하지 않은 전화번호는 요청에서 보내기 전에 정상화해야 합니다.
* 표준화되고 해시되고 인코딩된 데이터를 업로드하려면 전화 번호를 표준화된 전화 번호의 Base64 인코딩 SHA-256 해시로 보내야 합니다.

원시 전화 번호든 해시된 전화 번호든 업로드하려면 정상화해야 합니다.

>[!IMPORTANT]
>
>해시 전에 표준화를 수행하면 생성된 ID 값이 항상 동일해지고 데이터가 정확하게 일치할 수 있습니다.

다음은 전화 번호 표준화 요구 사항에 대해 알고 있어야 하는 사항입니다.

* UID2 운영자는 글로벌 고유성을 보장하는 국제 전화 번호 형식인 E.164 형식의 전화 번호를 수락합니다.
* E.164 전화 번호는 최대 15자리까지 사용할 수 있습니다.
* 정규화된 E.164 전화 번호에서는 공백, 하이픈, 괄호 또는 기타 특수 문자가 없는 `[+][country code][subscriber number including area code]` 구문을 사용합니다. 다음은 몇 가지 예입니다.

      * US: 1 (234) 567-8901이 +12345678901으로 표준화되었습니다.
     * 싱가포르: 65 1243 5678이 +6512345678으로 표준화되었습니다.
     * 오스트레일리아: 휴대폰 번호 0491 570 006이 국가 코드를 추가하고 앞에 있는 0을 삭제하도록 표준화되었습니다. +61491570006.
     * 영국: 휴대폰 번호 07812 345678은 국가 코드를 추가하고 선행 0을 삭제하도록 표준화되었습니다. +447812345678.
  
정규화된 전화 번호가 UTF-16과 같은 다른 인코딩 시스템이 아닌 UTF-8인지 확인하십시오.

전화번호 해시는 정규화된 전화번호의 Base64 인코딩 SHA-256 해시입니다. 전화번호는 먼저 정규화되고 SHA-256 해시 알고리즘을 사용하여 해시된 다음, 해시 값의 결과 바이트는 Base64 인코딩을 사용하여 인코딩됩니다. Base64 인코딩은 16진수로 인코딩된 문자열 표현이 아니라 해시 값의 바이트에 적용됩니다.
다음 표는 간단한 입력 전화 번호의 예를 보여 주며, 각 단계가 안전하고 불투명한 값에 도달하기 위해 적용됨에 따른 결과를 보여 줍니다.

| 유형 | 예 | 댓글 및 사용 |
|---|---|---|
| 원시 전화 번호 | 1 (234) 567-8901 | 이것이 시작점입니다. |
| 표준화된 전화번호 | +12345678901 | 표준화는 항상 첫 번째 단계입니다. |
| 정규화된 전화 번호의 SHA-256 해시 | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | 이 64자 문자열은 32바이트 SHA-256을 16진수로 인코딩한 것입니다. |
| 정규화된 전화번호 및 해시된 전화번호의 16진수를 Base64 SHA-256으로 인코딩 | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | 이 44자 문자열은 32바이트 SHA-256의 Base64로 인코딩된 표현입니다. SHA-256 해시는 16진수 값입니다. 16진수 값을 입력으로 사용하는 Base64 인코더를 사용해야 합니다. 요청 본문에 전송된 phone_hash 값에 이 인코딩을 사용합니다. |

>[!IMPORTANT]
>
>Base64 인코딩을 적용할 때는 16진수 값을 입력으로 사용하는 함수를 사용해야 합니다. 텍스트를 입력으로 가져오는 함수를 사용하는 경우 결과는 UID2의 목적에 적합하지 않은 더 긴 문자열입니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | Trade Desk 대상에 사용된 식별자(이메일 또는 해시된 이메일)로 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Daily Batch]** | 대상 평가를 기반으로 Experience Platform에서 프로필이 업데이트되면 프로필(ID)은 대상 플랫폼으로 하루에 한 번 업데이트됩니다. [일괄 내보내기](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

### 대상에 인증 {#authenticate}

[!DNL The Trade Desk] CRM 대상은 일일 일괄 처리 파일 업로드이며, 사용자의 인증이 필요하지 않습니다.

### 대상 세부 사항 입력 {#fill-in-details}

대상 데이터를 대상으로 보내거나 활성화하려면 먼저 고유한 대상 플랫폼에 대한 연결을 설정해야 합니다. [이 대상을 설정](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL Account Type]**: **[!UICONTROL Existing Account]** 옵션을 선택하십시오.
* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Advertiser ID]**: [!DNL Trade Desk Advertiser ID] 계정 관리자가 공유하거나 [!DNL Trade Desk] UI의 [!DNL Advertiser Preferences]에서 찾을 수 있는 [!DNL Trade Desk].

대상 세부 정보를 채우는 방법을 보여 주는 ![Experience Platform UI 스크린샷입니다.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

대상에 연결할 때 데이터 거버넌스 정책을 설정하는 것은 완전히 선택 사항입니다. 자세한 내용은 Experience Platform [데이터 거버넌스 개요](/help/data-governance/policies/overview.md)를 검토하십시오.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

대상을 대상으로 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

**[!UICONTROL Scheduling]** 페이지에서 내보내는 각 대상에 대해 일정 및 파일 이름을 구성할 수 있습니다. 예약을 구성해야 하지만, 파일 이름을 구성하는 것은 선택 사항입니다.

대상자 활성화를 예약하기 위한 ![Experience Platform UI 스크린샷](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>[!DNL The Trade Desk] CRM 대상에 대해 활성화된 모든 대상은 자동으로 일일 빈도 및 전체 파일 내보내기로 설정됩니다.

대상자 활성화를 예약하기 위한 ![Experience Platform UI 스크린샷](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

**[!UICONTROL Mapping]** 페이지의 원본 열에서 특성 또는 ID 네임스페이스를 선택하고 대상 열에 매핑해야 합니다.

대상 활성화를 매핑할 수 있는 ![Experience Platform UI 스크린샷](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

다음은 대상을 [!DNL The Trade Desk] CRM 대상으로 활성화할 때 올바른 ID 매핑의 예입니다.

소스 및 대상 필드 선택:

| 소스 필드 | 대상 필드 |
|---|---|
| 이메일 | 이메일 |
| Email_LC_SHA256 | hashed_email |
| 전화(E.164) | 전화 |
| 전화(SHA256_E.164) | hashed_phone |
| TDID | tdid |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2 토큰 | uid2_token |
| EUID | euid |
| EUIDToken | euid_token |
| 램프 ID | idl |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## 데이터 내보내기 유효성 검사 {#validate}

데이터가 Experience Platform에서 [!DNL The Trade Desk]&#x200B;(으)로 올바르게 내보내졌는지 확인하려면 [!DNL The Trade Desk] &quot;Advertiser Data and ID&quot; 라이브러리의 Adobe 1PD 탭에서 대상을 찾으십시오. [!DNL Trade Desk] UI 내에서 해당 ID를 찾는 단계는 다음과 같습니다.

1. 먼저 **[!UICONTROL Libraries]** 탭을 선택하고 **[!UICONTROL Advertiser data and identity]** 섹션을 검토합니다.
2. **[!UICONTROL Adobe 1PD]**&#x200B;을(를) 클릭하면 [!DNL The Trade Desk]에 대해 활성화된 모든 대상이 나열됩니다.
3. Experience Platform의 세그먼트 이름 또는 세그먼트 ID가 [!DNL Trade Desk] UI에서 세그먼트 이름으로 표시됩니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
