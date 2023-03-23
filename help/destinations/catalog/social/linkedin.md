---
keywords: linkedin 연결;linkedin 연결;linkedin 대상;linkedin
title: Linkedin 일치하는 대상 연결
description: 해시된 이메일을 기반으로 대상 타깃팅, 개인화 및 억제를 위해 LinkedIn 캠페인용 프로필을 활성화합니다.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] 연결

## 개요 {#overview}

에 대한 프로필 활성화 [!DNL LinkedIn] 해시된 이메일 및 모바일 ID를 기반으로 하는 대상 타깃팅, 개인화 및 억제를 위한 캠페인.

![Adobe Experience Platform UI의 linkedIn 대상](../../assets/catalog/social/linkedin/catalog.png)

## 사용 사례

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL LinkedIn Matched Audiences] 대상. Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 사용 사례입니다.

한 소프트웨어 회사는 회의를 조직하고 참가자들과 계속 연락을 취하고, 회의 참석 상태에 따라 개인화된 오퍼를 제공합니다. 이 회사는 자체 이메일 주소 또는 모바일 장치 ID를 수집할 수 있습니다 [!DNL CRM] Adobe Experience Platform으로 전환합니다. 그런 다음 고유한 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 [!DNL LinkedIn] 소셜 플랫폼, 광고 비용 최적화.

## 지원되는 ID {#supported-identities}

[!DNL LinkedIn Matched Audiences] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 다음 [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션에서 그리고 일반 텍스트와 해시된 이메일에 각각 적절한 네임스페이스를 사용합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에서 사용되는 식별자(이름, 전화번호 등)로 세그먼트(대상)의 모든 구성원을 내보냅니다 [!DNL LinkedIn Matched Audiences] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## linkedIn 계정 사전 요구 사항 {#LinkedIn-account-prerequisites}

를 사용하기 전에 [!UICONTROL linkedIn 대응 대상] 대상, [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상

편집 방법을 배우려면 [!DNL LinkedIn Campaign Manager] 사용자 권한 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753) ( LinkedIn 설명서)를 참조하십시오.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상이 [!DNL LinkedIn Matched Audiences] 키오프 가능 *해시* 이메일 주소 또는 모바일 장치 ID와 같은 식별자.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

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
> 속성 소스 데이터는 자동으로 해시되지 않습니다.
> 
> 다음 기간 동안 [ID 매핑](../../ui/activate-segment-streaming-destinations.md#mapping) 단계, 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.
> 
> 다음 **[!UICONTROL 변형 적용]** 옵션은 속성을 소스 필드로 선택하는 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

아래 비디오에서는 을(를) 구성하는 단계를 보여줍니다 [!DNL LinkedIn Matched Audiences] 대상 및 세그먼트 활성화

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며 이 비디오를 기록한 후 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md).

### 대상에 인증 {#authenticate}

1. 를 찾습니다. [!DNL LinkedIn Matched Audiences] 대상 카탈로그의 대상을 선택하고 을(를) 선택합니다. **[!UICONTROL 설정]**.
2. 선택 **[!UICONTROL 대상에 연결]**.
   ![LinkedIn 인증](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. LinkedIn 자격 증명을 입력하고 을(를) 선택합니다 **로그인**.

### 대상 세부 사항 채우기 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="계정 ID"
>abstract="LinkedIn Campaign Manager 계정 ID. LinkedIn Campaign Manager 계정에서 이 ID를 찾을 수 있습니다."

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL LinkedIn Campaign Manager Account ID]. 이 ID는 [!DNL LinkedIn Campaign Manager] 계정이 필요합니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

성공적인 활성화는 [!DNL LinkedIn] 사용자 지정 대상은 프로그래밍 방식으로 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 사용자가 활성화된 세그먼트에 대한 자격이 있거나 자격 미달되면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 의 통합 [!DNL LinkedIn Matched Audiences] 이전 대상 채우기 기능을 지원합니다. 모든 이전 세그먼트 자격이 [!DNL LinkedIn] 세그먼트를 대상에 활성화하는 경우.
