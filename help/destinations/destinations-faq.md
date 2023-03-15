---
keywords: 대상; 질문; faq; faq; 대상 faq
title: 자주 묻는 질문
description: Adobe Experience Platform 대상에 대해 가장 자주 묻는 질문에 대한 답변
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 자주 묻는 질문 {#faq}

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 대상에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 기타 관련 질문 및 문제 해결 [!DNL Platform] 모든 상황에서 발생하는 서비스를 포함한 서비스 [!DNL Platform] API입니다. 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

## 일반 대상 질문 {#general}

**Experience Platform UI와 내보낸 CSV 파일에서 다른 프로필 수가 표시되는 이유는 무엇입니까?**

이는 Experience Platform이 세그먼테이션을 수행하는 방식으로 인해 발생하는 일반적인 비헤이비어입니다.

스트리밍 세그먼테이션은 하루 종일 스트리밍 세그먼트의 프로필 수를 업데이트하는 반면, 배치 세그먼테이션은 24시간마다 한 번씩 배치 세그먼트의 프로필 수를 업데이트합니다.

세그먼트 내보내기 일정이 세분화 일정과 다른 경우 프로필은 UI와 내보낸 프로필 간에 계산됩니다 [!DNL CSV] 파일은 특히 세그먼트 스트리밍과 관련하여 달라집니다.

다음을 참조하십시오. [세그먼테이션 서비스 설명서](../segmentation/home.md) 을 참조하십시오.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**에서 대상자를 활성화하려면 먼저 무엇을 해야 합니까 [!DNL Facebook Custom Audiences]?**

대상 세그먼트를 보낼 수 있으려면 먼저 [!DNL Facebook], 다음 요구 사항을 충족하는지 확인하십시오.

* 사용자 [!DNL Facebook] 사용자 계정에는 **[!DNL Manage campaigns]** 사용하려는 광고 계정에 대해 권한이 활성화되었습니다.
* 다음 **Adobe Experience Cloud** 비즈니스 계정을 의 광고 파트너로 추가해야 합니다. [!DNL Facebook Ad Account]. `business ID=206617933627973` 사용. 다음을 참조하십시오 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897) 자세한 내용은 Facebook 설명서 를 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 다음을 활성화해야 합니다 **캠페인 관리** 권한. 이 단계는 [!DNL Adobe Experience Platform] 통합에 필요합니다.
* 읽기 및 서명 [!DNL Facebook Custom Audiences] 서비스 약관. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.

**에 앱 또는 픽셀을 추가해야 합니까? [!DNL Facebook] 광고주 계정이요?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**facebook에서 Adobe Experience Platform의 정보를 처리하는 데 시간이 얼마나 걸립니까?**

2021년 3월 현재 [!DNL Facebook Custom Audiences] 에서 받은 정보를 처리하려면 최대 1시간이 필요합니다. [!DNL Platform].

**사용할 수 있습니까 [!DNL Facebook Custom Audiences] 기타 대상의 대상 타깃팅 [!DNL Facebook] 앱, 예 [!DNL Instagram]?**

다음을 사용할 수 있습니다. [!DNL Facebook Custom Audiences] 에서 지원하는 Facebook 앱 제품군의 대상 타겟팅 [!DNL Facebook Custom Audiences], 포함 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], 및 [!DNL Messenger]. 광고주가 캠페인을 실행할 앱의 선택은 의 배치 수준에서 표시됩니다. [!DNL Facebook Ads Manager].

**차이점이 무엇입니까 [!DNL Facebook Custom Audiences] 연결 및 [!DNL Facebook Pixel] 확장?**

다음 [!DNL Facebook Custom Audiences] 연결 사용 [!DNL Platform] 대상자를 (으)로 보낼 때 ID [!DNL Facebook], 반면에 [[!DNL Facebook Pixel] 연결](../destinations/catalog/advertising/facebook-pixel.md) 를 사용합니다. [!DNL Facebook] 웹 사이트에 통합된 픽셀.

이 두 가지 통합은 상호 보완적입니다. 두 가지 모두를 사용하여 대상 범위를 개선할 수 있습니다. 예를 들어 [!DNL Facebook Pixel] 계정을 만들지 않은 웹 사이트 방문자를 예견하는 데 사용되는 확장 프로그램입니다. [!DNL Facebook Custom Audiences] 을(를) 통해 다음을 기반으로 기존 고객을 타겟팅할 수 있습니다. [!DNL Platform] id입니다.

**Adobe Experience Platform 통합 대상 [!DNL Facebook Custom Audiences] 더 이상 자격이 없는 경우 대상에서 자격을 박탈하는 사용자를 지원합니까?**

예. 통합은에서 사용자 제거를 지원합니다. [!DNL Facebook Custom Audiences] 더 이상 자격이 없을 때.

**대상 데이터를에 보내기 전에 해시하려면 어떻게 해야 합니까? [!DNL Facebook]?**

[!DNL Facebook] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL Facebook] 키 사용 안 함 *해시됨* 이메일 주소 또는 전화번호 등 식별자.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/facebook.md#id-matching-requirements).

**에서 활성화할 수 있는 ID 종류 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 은(는) 해시된 이메일, 해시된 전화번호, [!DNL GAID], [!DNL IDFA]및 사용자 지정 외부 ID입니다.

**별도의 Facebook 계정에 대해 Platform UI에서 여러 Facebook 대상을 만들 수 있습니까?**

예. Experience Platform의 Facebook 대상은 Facebook의 광고 계정으로 1:1입니다. 회사의 각 Facebook 광고 계정에 대해 별도의 Facebook 대상을 만들 수 있습니다. 다음 [대상 연결 자습서](/help/destinations/ui/connect-destination.md) 플랫폼 UI에서 각각의 새로운 Facebook 대상에 대한 별도의 Facebook 계정에 연결합니다. 연결할 수 있는 Facebook 광고 계정 수에는 제한이 없습니다.

## Google Customer Match {#google-customer-match}

**세그먼트를 Google Customer Match로 내보낼 때 Google 인터페이스에 세그먼트 이름의 끝에 추가된 숫자가 표시되는 이유는 무엇입니까?**

Google을 사용하려면 세그먼트 이름이 고유해야 합니다. 지금 보시는 숫자는 다음과 같습니다 [UNIX 타임스탬프](https://www.unixtimestamp.com/) 또한 동일한 세그먼트를 여러 Google 대상에 매핑한 경우 세그먼트 이름을 고유하게 유지하기 위해 추가됩니다.

## LinkedIn과 일치하는 대상 {#linkedin}

**에 앱 또는 픽셀을 추가해야 합니까? [!DNL LinkedIn] 광고주 계정이요?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**에서 대상자를 활성화하려면 먼저 무엇을 해야 합니까 [!DNL LinkedIn Matched Audiences]?**

을(를) 사용하기 전에 [!UICONTROL LinkedIn 일치 대상] 대상, 다음을 확인하십시오. [!DNL LinkedIn Campaign Manager] 계정이 다음을 보유함: [!DNL Creative Manager] 권한 수준 이상입니다.

을(를) 편집하는 방법에 대해 알아보려면 [!DNL LinkedIn Campaign Manager] 사용자 권한, 참조 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753) linkedIn 설명서에서 확인할 수 있습니다.

**대상 데이터를에 보내기 전에 해시하려면 어떻게 해야 합니까? [!DNL LinkedIn]?**

[!DNL LinkedIn] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL LinkedIn] 키 사용 안 함 *해시됨* 이메일 주소 또는 전화번호 등 식별자.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/linkedin.md#id-matching-requirements).

**에서 활성화할 수 있는 ID 종류 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 은(는) 해시된 이메일, [!DNL GAID], 및 [!DNL IDFA].
