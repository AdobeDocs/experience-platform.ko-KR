---
title: Twitter 사용자 지정 대상 연결
description: Twitter에서 기존 팔로워와 고객을 Target 하고 Adobe Experience Platform 내에 구축된 대상을 활성화하여 적절한 리마케팅 캠페인을 만듭니다
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---


# [!DNL Twitter Custom Audiences] 연결

## 개요 {#overview}

Twitter에서 기존 팔로워와 고객을 Target하고 Adobe Experience Platform 내에 내장된 대상을 활성화하여 적절한 리마케팅 캠페인을 만듭니다.

## 전제 조건 {#prerequisites}

[!DNL Twitter Custom Audiences] 대상을 구성하기 전에 충족해야 하는 다음 Twitter 사전 요구 사항을 검토하십시오.

1. [!DNL Twitter Ads] 계정을 광고할 수 있어야 합니다. 새 [!DNL Twitter Ads] 계정은 만든 후 처음 2주 내에 광고를 수행할 수 없습니다.
2. [!DNL Twitter Audience Manager]에서 액세스를 인증한 Twitter 사용자 계정에는 *[!DNL Partner Audience Manager]* 권한이 활성화되어 있어야 합니다.


## 지원되는 ID {#supported-identities}

[!DNL Twitter Custom Audiences] 은 아래 표에 설명된 id의 활성화를 지원합니다. [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform에서는 GAID(Google Advertising ID) 및 Apple ID for Advertising (IDFA)가 지원됩니다. 대상 활성화 워크플로우의 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에 따라 소스 스키마에서 이러한 네임스페이스 및/또는 속성을 매핑하십시오. |
| 이메일 | 사용자의 이메일 주소 | 일반 텍스트 이메일 주소와 SHA256 해시된 이메일 주소를 이 필드에 매핑하십시오. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. Adobe Experience Platform에 업로드하기 전에 고객 이메일 주소를 해시하는 경우, 소금 없이 SHA256을 사용하여 이러한 ID를 해시해야 합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - Twitter 사용자 지정 대상 대상에 사용된 식별자를 사용하여 세그먼트(대상)의 모든 구성원을 내보냅니다.

## 사용 사례 {#use-cases}

[!DNL Twitter Custom Audiences] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례가 여기에 있습니다.

### 사용 사례 #1

Twitter에서 기존 팔로워와 고객을 Target 하고 Twitter에서 [!DNL List Custom Audiences] 로 Adobe Experience Platform 내에 내장된 대상을 활성화하여 적절한 리마케팅 캠페인을 만듭니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 계정  [!DNL Twitter Ads] ID입니다. 이는 [!DNL Twitter Ads] 설정에서 찾을 수 있습니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)를 참조하십시오.

## 추가 리소스 {#additional-resources}

대상 세그먼트를 Twitter에 매핑할 때는 다음 세그먼트 이름 지정 요구 사항을 충족하는지 확인하십시오.

1. 사람이 읽을 수 있는 세그먼트 매핑 이름을 제공합니다. Experience Platform 세그먼트에 사용한 것과 동일한 이름을 사용하는 것이 좋습니다.
2. 특수 문자는 사용하지 마십시오 (+ &amp; , % : ; @ / = ? $)를 사용할 수 있습니다. Experience Platform 세그먼트 이름에 이러한 문자가 포함되어 있는 경우 세그먼트를 Twitter 대상에 매핑하기 전에 제거하십시오.

twitter의 [!DNL List Custom Audiences]에 대한 자세한 내용은 [Twitter 설명서](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)에서 확인할 수 있습니다.