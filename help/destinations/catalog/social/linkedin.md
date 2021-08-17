---
keywords: linkedin 연결;linkedin 연결;linkedin 대상;linkedin
title: Linkedin 일치하는 대상 연결
description: 해시된 이메일을 기반으로 대상 타깃팅, 개인화 및 억제를 위해 LinkedIn 캠페인용 프로필을 활성화합니다.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# [!DNL LinkedIn Matched Audiences] 연결

## 개요 {#overview}

해시된 이메일 및 모바일 ID를 기반으로 대상 타깃팅, 개인화 및 억제를 위해 [!DNL LinkedIn] 캠페인에 대한 프로필을 활성화합니다.

![Adobe Experience Platform UI의 linkedIn 대상](../../assets/catalog/social/linkedin/catalog.png)

## 사용 사례

[!DNL LinkedIn Matched Audiences] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

한 소프트웨어 회사는 회의를 조직하고 참가자들과 계속 연락을 취하고, 회의 참석 상태에 따라 개인화된 오퍼를 제공합니다. 이 회사는 고유한 [!DNL CRM]의 이메일 주소 또는 모바일 장치 ID를 Adobe Experience Platform으로 수집할 수 있습니다. 그런 다음 자체 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 [!DNL LinkedIn] 소셜 플랫폼으로 전송하여 광고 비용을 최적화할 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL LinkedIn Matched Audiences] 은 아래 표에 설명된 id의 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침에 따라 일반 텍스트와 해시된 이메일에 적절한 네임스페이스를 각각 사용하십시오. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |


## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - 대상에 사용된 식별자(이름, 전화 번호 및 기타)로 세그먼트(대상)의 모든 멤버를  [!DNL LinkedIn Matched Audiences] 내보냅니다.

## linkedIn 계정 사전 요구 사항 {#LinkedIn-account-prerequisites}

[!UICONTROL LinkedIn Matched Audience] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인하십시오.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대한 자세한 내용은 LinkedIn 설명서에서 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753)를 참조하십시오.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 [!DNL LinkedIn Matched Audiences]에 활성화된 대상은 이메일 주소 또는 모바일 장치 ID와 같이 *해시된* 식별자를 사용할 수 있습니다.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

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
> 속성 소스 데이터는 자동으로 해시되지 않습니다.
> 
> [ID 매핑](../../ui/activate-segment-streaming-destinations.md#mapping) 단계에서 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오.
> 
> **[!UICONTROL 변환 적용]** 옵션은 속성을 소스 필드로 선택한 경우에만 표시됩니다. 네임스페이스를 선택하면 표시되지 않습니다.

![ID 매핑 변환](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

아래 비디오에서는 [!DNL LinkedIn Matched Audiences] 대상을 구성하고 세그먼트를 활성화하는 단계를 보여줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며 이 비디오를 기록한 후 변경되었을 수 있습니다. 최신 정보는 [대상 구성 자습서](../../ui/connect-destination.md)를 참조하십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자  [!DNL LinkedIn Campaign Manager Account ID]. 이 ID는 [!DNL LinkedIn Campaign Manager] 계정에서 찾을 수 있습니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

성공적인 활성화는 [!DNL LinkedIn] 사용자 지정 대상이 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)에서 프로그래밍 방식으로 만들어짐을 의미합니다. 사용자가 활성화된 세그먼트에 대한 자격이 있거나 자격 미달되면 대상의 세그먼트 멤버십이 추가 및 제거됩니다.

>[!TIP]
>
>Adobe Experience Platform과 [!DNL LinkedIn Matched Audiences] 간의 통합은 이전 대상 채우기 기능을 지원합니다. 세그먼트를 대상으로 활성화하면 모든 이전 세그먼트 자격이 [!DNL LinkedIn]으로 전송됩니다.
