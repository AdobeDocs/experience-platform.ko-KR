---
keywords: facebook extensions;facebook extension;facebook destinations;facebook;instagram;messenger;facebook messenger
title: Facebook 대상
seo-title: Facebook 대상
description: 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
seo-description: 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
translation-type: tm+mt
source-git-commit: c66fb4cf0a414e02ceb58becc9d9b59db3fe987b
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 4%

---


# [!DNL Facebook] 대상

## 개요 {#overview}

해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 캠페인에 대한 프로필을 활성화합니다. [!DNL Facebook]

이 대상을 사용하여, [!DNL Facebook’s][!DNL Custom Audiences]및 [!DNL Facebook]등 [!DNL Instagram]에서 지원하는 앱 제품군 [!DNL Audience Network] [!DNL Messenger]에서 대상을 타깃팅할 수 있습니다. 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

![실시간 CDP UI의 Facebook 대상](/help/rtcdp/destinations/assets/facebook-destination.png)


## 사용 사례

대상을 사용하는 방법과 시기를 보다 잘 이해할 수 있도록 Adobe의 실시간 고객 데이터 플랫폼 고객이 이 기능을 사용하여 해결할 수 있는 두 가지 샘플 사용 사례를 소개합니다. [!DNL Facebook]


### 사용 사례 #1


온라인 소매업체는 소셜 플랫폼을 통해 기존 고객에게 도달하고 이전 주문에 따라 개인화된 제안을 제공하고자 합니다. 온라인 리테일 업체는 자사의 CRM에서 Adobe으로 이메일 주소를 인제스트하고, 오프라인 데이터를 기반으로 세그먼트를 작성하고, 이러한 세그먼트를 [!DNL Facebook] 소셜 플랫폼으로 보내 광고 지출을 최적화할 수 있습니다.


### 사용 사례 #2


항공사는 다양한 고객 계층(브론즈, 실버, 골드)을 보유하고 있으며 소셜 플랫폼을 통해 각 계층에 맞춤형 제안을 제공하려고 합니다. 그러나 모든 고객이 항공사의 모바일 앱을 사용하는 것은 아니며, 그들 중 일부는 회사의 웹사이트에 로그인하지 않았다. 회사가 이러한 고객에 대해 가지고 있는 유일한 식별자는 멤버십 ID와 이메일 주소입니다.

다양한 소셜 미디어에서 고객 데이터를 타깃팅하기 위해 이메일 주소를 식별자로 사용하여 CRM의 고객 데이터를 Adobe 실시간 CDP로 가져올 수 있습니다.

또한 관련 멤버십 ID 및 고객 계층을 비롯한 오프라인 데이터를 사용하여 대상을 통해 타깃팅할 수 있는 새로운 고객 세그먼트를 만들 수 [!DNL Facebook] 있습니다.

## 대상 세부 사항 {#destination-specs}

### 대상을 위한 데이터 [!DNL Facebook] 거버넌스 {#data-governance}

>[!IMPORTANT]
>
>전송된 데이터에는 연결된 ID가 포함되지 [!DNL Facebook] 않아야 합니다. 귀하는 본 의무 사항을 지킬 책임이 있으며, 활성화를 위해 선택한 세그먼트가 병합 정책에 연결 옵션을 사용하지 않도록 함으로써 이에 대응할 수 있습니다. 병합 정책에 대한 자세한 [내용을 살펴보십시오](/help/profile/ui/merge-policies.md).

### 내보내기 유형 {#export-type}

**세그먼트 내보내기** - 식별자(이름, 전화 번호 등)를 사용하여 세그먼트(대상)의 모든 멤버를 내보냅니다. Facebook 대상에 사용됩니다.

### Facebook 계정 사전 요구 사항 {#facebook-account-prerequisites}

대상 세그먼트를 다음으로 보내기 전에 다음 요구 사항 [!DNL Facebook]을 충족해야 합니다.

1. 사용자 [!DNL Facebook] 계정에는 사용할 광고 계정에 대해 **[!DNL Manage campaigns]** 사용 권한이 활성화되어 있어야 합니다.
2. Add the **Adobe Experience Cloud** business account as an advertising partner in your [!DNL Facebook Ad Account].  `business ID=206617933627973`. 자세한 내용은 [Facebook 설명서의 비즈니스](https://www.facebook.com/business/help/1717412048538897) 관리자에 파트너 추가를 참조하십시오.
   >[!IMPORTANT]
   >
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. 이 단계는 [!DNL Adobe Real-time CDP] 통합에 필요합니다.
3. 서비스 약관을 읽고 [!DNL Facebook Custom Audiences] 서명합니다. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.

### 이메일 해싱 요구 사항 {#email-hashing-requirements}

[!DNL Facebook] 는 PII(개인 식별 정보)가 명확하게 전송되지 않도록 요구합니다. 따라서, 활성화한 대상이 해시된 이메일 주소 [!DNL Facebook] 에서 *키잉되어야* 합니다. 이메일 주소를 Adobe Experience Platform으로 인제스트하기 전에 해시하도록 선택하거나, Experience Platform에서 명확하게 이메일 주소를 사용하여 작업하도록 선택하고 알고리즘이 활성화하면 해당 이메일 주소를 해시하도록 할 수 있습니다.

Experience Platform에서 이메일 주소 인제스트에 대한 자세한 내용은 [일괄 처리 개요](/help/ingestion/batch-ingestion/overview.md) 및 [스트리밍 통합 개요를 참조하십시오](/help/ingestion/streaming-ingestion/overview.md).

직접 이메일 주소를 해시하도록 선택한 경우 다음 요구 사항을 준수해야 합니다.

* 이메일 문자열에서 모든 선행 및 후행 공백을 트리밍합니다.예: `johndoe@example.com`, not `<space>johndoe@example.com<space>`
* 이메일 문자열을 해싱할 때는 소문자 문자열을 해시해야 합니다.
   * 예: `example@email.com`, not `EXAMPLE@EMAIL.COM`
* 해시된 문자열이 모두 소문자인지 확인하십시오.
   * 예: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`
* 끈에 소금을 치지 마라.


>[!IMPORTANT]
>
>이메일 주소를 해시하지 않기로 선택하면 세그먼트를 활성화할 때 Adobe 실시간 CDP가 자동으로 수행됩니다 [!DNL Facebook]. [활성화 워크플로우](/help/rtcdp/destinations/activate-destinations.md#activate-data) (5단계 참조)에서 `Email` raw 이메일 주소 *및 해시된 이메일 주소* 에 대해 아래 `Email_LC_SHA256` 와 같은 옵션을 **&#x200B;선택합니다.


![활성화 시 해싱](/help/rtcdp/destinations/assets/identity-mapping.png)

## 대상에 연결 {#connect-destination}

대상에 [!DNL Facebook] 연결하려면 [소셜 네트워크 대상 인증 워크플로우를 참조하십시오](/help/rtcdp/destinations/social-network-destinations-workflow.md).


## 세그먼트 활성화 [!DNL Facebook] {#activate-segments}

세그먼트를 활성화할 방법에 대한 지침 [!DNL Facebook]은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).

## 내보낸 데이터 {#exported-data}

활성화 [!DNL Facebook]를 성공적으로 수행하면 사용자 [!DNL Facebook] 지정 대상이 [[!DNL Facebook 광고 관리자]에서 프로그램 방식으로 생성된다는 의미입니다](https://www.facebook.com/adsmanager/manage/). 사용자가 활성화된 세그먼트에 대해 자격이 부여되거나 자격이 부여되면 대상의 세그먼트 멤버십이 추가되고 제거됩니다.

>[!TIP]
>
>Adobe 실시간 CDP를 통합하고 이전 고객 채우기를 [!DNL Facebook] 지원합니다. 세그먼트를 대상에 활성화하면 모든 내역 세그먼트 자격 [!DNL Facebook] 이 전송됩니다.