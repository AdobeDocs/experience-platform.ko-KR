---
keywords: linkedin 연결;linkedin 연결;linkedin 대상;linkedin;
title: Linkedin 일치하는 대상 연결
description: 해시된 이메일을 기반으로 대상 타겟팅, 개인화 및 억제에 대한 LinkedIn 캠페인용 프로필을 활성화합니다.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] 연결

## 개요 {#overview}

에 대한 프로필 활성화 [!DNL LinkedIn] 해시된 이메일 및 모바일 ID를 기반으로 한 대상자 타겟팅, 개인화 및 억제용 캠페인.

![Adobe Experience Platform UI의 linkedIn 대상](../../assets/catalog/social/linkedin/catalog.png)

## 사용 사례

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL LinkedIn Matched Audiences] 대상: 다음은 이 기능을 사용하여 Adobe Experience Platform 고객이 해결할 수 있는 사용 사례입니다.

소프트웨어 회사는 회의를 주관하며 참가자와 계속 연락하고, 회의 참석 상태에 따라 개인화된 오퍼를 표시하기를 원합니다. 회사는 자신의 이메일 주소 또는 모바일 장치 ID를 수집할 수 있습니다 [!DNL CRM] Adobe Experience Platform으로. 그런 다음 자체 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 [!DNL LinkedIn] 소셜 플랫폼, 광고 지출을 최적화.

## 지원되는 ID {#supported-identities}

[!DNL LinkedIn Matched Audiences] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 의 지침을 따르십시오. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 및 에서는 각각 일반 텍스트와 해시된 이메일에 적절한 네임스페이스를 사용합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에 사용된 식별자(이름, 전화번호 등)를 사용하여 세그먼트(대상자)의 모든 구성원을 내보냅니다. [!DNL LinkedIn Matched Audiences] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## LinkedIn 계정 사전 요구 사항 {#LinkedIn-account-prerequisites}

을(를) 사용하기 전에 [!UICONTROL LinkedIn 일치 대상] 대상, 다음을 확인하십시오. [!DNL LinkedIn Campaign Manager] 계정이 다음을 보유함: [!DNL Creative Manager] 권한 수준 이상입니다.

을(를) 편집하는 방법에 대해 알아보려면 [!DNL LinkedIn Campaign Manager] 사용자 권한, 참조 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753) linkedIn 설명서에서 확인할 수 있습니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL LinkedIn Matched Audiences] 키 사용 안 함 *해시됨* 이메일 주소 또는 모바일 디바이스 ID와 같은 식별자.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 이메일 해시 요구 사항 {#email-hashing-requirements}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 이메일 주소를 지우고 다음을 수행할 수 있습니다. [!DNL Platform] 활성화 시 해시합니다.

Experience Platform에서 이메일 주소 수집에 대한 자세한 내용은 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](/help/ingestion/streaming-ingestion/overview.md).

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 준수해야 합니다.

* 전자 메일 문자열에서 선행 및 후행 공백을 모두 트리밍합니다. 예: `johndoe@example.com`, 아님 `<space>johndoe@example.com<space>`;
* 이메일 문자열을 해시할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, 아님 `EXAMPLE@EMAIL.COM`;
* 해시된 문자열이 모두 소문자인지 확인합니다.
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, 아님 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 문자열에 소금을 뿌리지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 다음에 의해 자동으로 해시됩니다. [!DNL Platform] 활성화 시.
> 속성 소스 데이터는 자동으로 해시되지 않습니다.
> 
> 다음 기간 동안 [ID 매핑](../../ui/activate-segment-streaming-destinations.md#mapping) 단계: 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.
> 
> 다음 **[!UICONTROL 변환 적용]** 옵션은 속성을 소스 필드로 선택하는 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

아래 비디오에서는 을(를) 구성하는 단계도 보여 줍니다. [!DNL LinkedIn Matched Audiences] 대상 및 활성화 세그먼트를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며, 이 비디오 녹화 이후에 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md).

### 대상에 인증 {#authenticate}

1. 다음 찾기 [!DNL LinkedIn Matched Audiences] 대상 카탈로그의 대상 및 선택 **[!UICONTROL 설정]**.
2. 선택 **[!UICONTROL 대상에 연결]**.
   ![linkedIn 인증](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. linkedIn 자격 증명을 입력하고 다음을 선택합니다. **로그인**.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="계정 ID"
>abstract="linkedIn Campaign Manager 계정 ID. 이 ID는 LinkedIn Campaign Manager 계정에서 찾을 수 있습니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL LinkedIn Campaign Manager Account ID]. 이 ID는 [!DNL LinkedIn Campaign Manager] 계정입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 세그먼트 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

## 내보낸 데이터 {#exported-data}

활성화가 성공하면 [!DNL LinkedIn] 사용자 지정 대상은에서 프로그래밍 방식으로 만들어집니다. [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 사용자가 활성화된 세그먼트에 대해 자격이 부여되거나 자격을 상실하면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 의 통합 [!DNL LinkedIn Matched Audiences] 는 과거 대상자 채우기를 지원합니다. 모든 과거 세그먼트 자격 요건이 (으)로 전송됩니다. [!DNL LinkedIn] 대상 세그먼트를 활성화할 때.
