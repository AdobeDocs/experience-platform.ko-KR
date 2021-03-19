---
keywords: linkedin 연결;linkedin 연결;linkedin 대상;linkedin 대상;linkedin
title: Linkedin 일치된 대상 연결
description: 해시 처리된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 LinkedIn 캠페인의 프로필을 활성화합니다.
translation-type: tm+mt
source-git-commit: fd95357f3e3533fe6b7b9752798dd99eb1cc0eb5
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# [!DNL LinkedIn Matched Audiences] 연결

해시 처리된 이메일 및 모바일 ID를 기반으로 고객 타깃팅, 개인화 및 억제를 위해 [!DNL LinkedIn] 캠페인에 대한 프로파일을 활성화합니다.

![Adobe Experience Platform UI의 LinkedIn 대상](../../assets/catalog/social/linkedin/catalog.png)

## 사용 사례

Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 사용 방법은 [!DNL LinkedIn Matched Audiences] 대상을 사용하는 방법과 시기를 이해하는 데 도움이 됩니다.

소프트웨어 업체는 컨퍼런스를 조직하여 참가자와 계속 연락하고 컨퍼런스 참석 상태를 기반으로 개인화된 제안을 제공합니다. 회사는 자신의 [!DNL CRM]에서 Adobe Experience Platform으로 이메일 주소 또는 모바일 장치 ID를 인제스트할 수 있습니다. 그런 다음 자체 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 [!DNL LinkedIn] 소셜 플랫폼으로 보내 광고 지출을 최적화할 수 있습니다.

## 대상 세부 사항 {#destination-specs}

[!DNL LinkedIn Matched Audiences] 에서는 다음 ID 활성화를 지원합니다.해시된 이메일,  [!DNL GAID]및  [!DNL IDFA]

### 지원되는 ID {#supported-identities}

[!DNL LinkedIn Matched Audiences] 에서는 아래 표에 설명된 ID 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침을 따르고 일반 텍스트 및 해시 이메일에 적합한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |


### 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - 대상에 사용된 식별자(이름, 전화 번호 등)를 사용하여 세그먼트(대상)의 모든 구성원을  [!DNL LinkedIn Matched Audiences] 내보냅니다.

### LinkedIn 계정 사전 요구 사항 {#LinkedIn-account-prerequisites}

[!UICONTROL LinkedIn Matched Audience] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인합니다.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대한 자세한 내용은 LinkedIn 문서에서 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거를 참조하십시오.](https://www.linkedin.com/help/lms/answer/5753)

### 요구 사항 {#id-matching-requirements} 일치하는 ID

[!DNL LinkedIn Matched Audiences] 는 PII(개인 식별 정보)가 명확하게 전송되지 않도록 요구합니다. 따라서 [!DNL LinkedIn Matched Audiences]에 대해 활성화된 대상은 이메일 주소 또는 모바일 장치 ID와 같이 *해시* 식별자를 해제할 수 있습니다.

Adobe Experience Platform에 인제스트하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

#### 전자 메일 해싱 요구 사항 {#email-hashing-requirements}

전자 메일 주소를 Adobe Experience Platform으로 인제스트하기 전에 해시하거나, Experience Platform에서 명확하게 전자 메일 주소를 사용하고 활성화 시 [!DNL Platform] 해시하도록 할 수 있습니다.

Experience Platform에서 이메일 주소 인제스트에 대한 자세한 내용은 [일괄 처리 통합 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 통합 개요](/help/ingestion/streaming-ingestion/overview.md)를 참조하십시오.

직접 이메일 주소를 해시하도록 선택한 경우 다음 요구 사항을 준수해야 합니다.

- 이메일 문자열에서 모든 선행 및 후행 공백을 트리밍합니다. 예:`<space>johndoe@example.com<space>`;`johndoe@example.com`
- 이메일 문자열을 해싱할 때는 반드시 소문자 문자열을 해시해야 합니다.
   - 예:`EXAMPLE@EMAIL.COM`;`example@email.com`
- 해시된 문자열이 모두 소문자인지 확인
   - 예:`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`
- 문자열에 소금을 넣지 마십시오.

>[!NOTE]
>
>해시되지 않은 네임스페이스의 데이터는 활성화 시 [!DNL Platform]에 의해 자동으로 해시됩니다.
> 속성 소스 데이터가 자동으로 해시되지 않습니다.
> 
> [ID 매핑](../../ui/activate-destinations.md#identity-mapping) 단계 동안 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Platform]에서 활성화 데이터를 자동으로 해시하도록 하십시오.
> 
> **[!UICONTROL Apply transformation]** 옵션은 속성을 소스 필드로 선택할 때만 표시됩니다. 네임스페이스를 선택할 때 표시되지 않습니다.

![ID 매핑 변형](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 대상 {#connect-destination}에 연결

[!DNL LinkedIn Matched Audiences] 대상에 연결하려면 [소셜 네트워크 대상 인증 워크플로](./workflow.md)를 참조하십시오.

## 세그먼트를 [!DNL LinkedIn Matched Audiences] {#activate-segments}에 활성화

세그먼트를 [!DNL LinkedIn Matched Audiences]에 활성화하는 방법에 대한 지침은 [대상에 데이터 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

활성화가 성공하면 [!DNL LinkedIn] 사용자 지정 대상이 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)에서 프로그래밍 방식으로 작성된다는 의미입니다. 활성화된 세그먼트에 대해 자격이 부여되거나 자격이 부여되지 않으면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 [!DNL LinkedIn Matched Audiences] 간의 통합은 이전 대상 채우기를 지원합니다. 세그먼트를 대상으로 활성화하면 모든 내역 세그먼트 자격 조건은 [!DNL LinkedIn]으로 전송됩니다.