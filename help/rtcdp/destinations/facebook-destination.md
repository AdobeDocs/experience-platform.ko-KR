---
title: Facebook 대상
seo-title: Facebook 대상
description: 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
seo-description: 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
translation-type: tm+mt
source-git-commit: 522014f8e5f3de0f553a69763d3a37482953b7c4
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# Facebook 대상

## 개요 {#overview}

해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.

![실시간 CDP UI의 Facebook 대상](/help/rtcdp/destinations/assets/facebook-destination.png)

## 사용 사례

Facebook 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe 실시간 고객 데이터 플랫폼 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 샘플 사용 사례를 소개합니다.


### 사용 사례 #1


온라인 소매업체는 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문에 따라 개인화된 제안을 제공하고자 합니다. 온라인 리테일 업체는 자사의 CRM에서 Adobe Real-time CDP로 이메일 주소를 인제스트하고, 자체 오프라인 데이터를 기반으로 세그먼트를 작성하고, 이러한 세그먼트를 Facebook 소셜 플랫폼으로 보내 광고 지출을 최적화할 수 있습니다.


### 사용 사례 #2


항공사는 다양한 고객 계층(브론즈, 실버, 골드)을 보유하고 있으며 소셜 플랫폼을 통해 각 계층에 맞춤형 제안을 제공하려고 합니다. 그러나 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 그들 중 일부는 회사의 웹사이트에 로그인하지 않았다. 회사가 이러한 고객에 대해 가지고 있는 유일한 식별자는 멤버십 ID와 이메일 주소입니다.
소셜 미디어에서 고객 데이터를 타깃팅하기 위해 해시된 이메일 주소를 식별자로 사용하여 CRM의 고객 데이터를 Adobe Real-time CDP로 가져올 수 있습니다.
그런 다음 오프라인 데이터와 기존 온라인 활동 데이터를 결합하여 Facebook 대상을 통해 타깃팅할 수 있는 새로운 고객 세그먼트를 만들 수 있습니다.

## 대상 세부 사항 {#destination-specs}

### Facebook 대상을 위한 데이터 거버넌스 {#data-governance}

>[!IMPORTANT]
>
>Facebook으로 보낸 데이터에는 연결된 ID가 포함되지 않아야 합니다. 귀하는 본 의무 사항을 지킬 책임이 있으며, 활성화를 위해 선택한 세그먼트가 병합 정책에 연결 옵션을 사용하지 않도록 함으로써 이에 대응할 수 있습니다. 병합 정책에 대한 자세한 [내용을 살펴보십시오](/help/profile/ui/merge-policies.md).

### 활성화 유형 {#activation-type}

**세그먼트 내보내기** - 식별자(이름, 전화 번호 등)를 사용하여 세그먼트(대상)의 모든 멤버를 내보냅니다. Facebook 대상에 사용됩니다.

### Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상 세그먼트를 다음으로 보내기 전에 다음 요구 사항 [!DNL Facebook]을 충족해야 합니다.

1. 사용자 [!DNL Facebook] 계정에는 사용할 광고 계정에 대해 **[!DNL Manage campaigns]** 사용 권한이 활성화되어 있어야 합니다.
2. 광고 파트너로 **Adobe Experience Cloud** 비즈니스 계정을 추가합니다 [!DNL Facebook Ad Account].  `business ID=206617933627973`. 자세한 내용은 [Facebook 설명서의 비즈니스](https://www.facebook.com/business/help/1717412048538897) 관리자에 파트너 추가를 참조하십시오.
   >[!IMPORTANT]
   > Adobe Experience Cloud에 대한 권한을 구성할 때 캠페인 **관리 권한을 활성화해야** 합니다. 통합하려면 이 [!DNL Adobe Real-time CDP] 값이 필요합니다.
3. 서비스 약관을 읽고 [!DNL Facebook Custom Audiences] 서명합니다. 이렇게 하려면, `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`어디로 `accountID` 가 [!DNL Facebook Ad Account ID].

### 이메일 해싱 요구 사항 {#email-hashing-requirements}

Facebook에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 Facebook에 대해 활성화된 대상은 해시된 *이메일* 주소에서 키잉되어야 합니다. 이메일 주소를 Adobe Experience Platform으로 인제스트하기 전에 해시하도록 선택하거나, 경험 플랫폼에서 이메일 주소를 명확히 사용하여 작업하고 알고리즘으로 활성화하여 해시 처리하도록 선택할 수 있습니다.

Experience Platform의 이메일 주소 인제팅에 대한 자세한 내용은 [배치 인제스트 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 인제스트 개요를 참조하십시오](/help/ingestion/streaming-ingestion/overview.md).

직접 이메일 주소를 해시하도록 선택한 경우 다음 요구 사항을 준수해야 합니다.

* 이메일 문자열에서 모든 선행 및 후행 공백을 트리밍합니다. 예: `johndoe@example.com`, not `<space>johndoe@example.com<space>`
* 이메일 문자열을 해싱할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, not `EXAMPLE@EMAIL.COM`
* 해시된 문자열이 모두 소문자인지 확인하십시오.
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`
* 끈에 소금을 치지 마라.


>[!IMPORTANT]
>
>이메일 주소를 해시하지 않기로 선택하면 Facebook에 세그먼트를 활성화하면 Adobe 실시간 CDP가 자동으로 수행됩니다. [활성화 워크플로우](/help/rtcdp/destinations/activate-destinations.md#activate-data) (5단계 참조)에서 `Email` raw 이메일 주소 *및 해시된 이메일 주소* 에 대해 아래 `Email_LC_SHA256` 와 같은 옵션을 **&#x200B;선택합니다.


![활성화 시 해싱](/help/rtcdp/destinations/assets/identity-mapping.png)

## 대상에 연결 {#connect-destination}

Facebook 대상에 연결하려면 [소셜 네트워크 대상 인증 워크플로우를 참조하십시오](/help/rtcdp/destinations/social-network-destinations-workflow.md).


## Facebook에 세그먼트 활성화 {#activate-segments}

Facebook에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).