---
keywords: 대상; 질문 FAQ faq; 대상 faq
title: 자주 묻는 질문
seo-title: Frequently asked questions
description: Adobe Experience Platform 대상에 대해 자주 묻는 질문과 대답(FAQ)입니다
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 8f9a601a833149c83d465f68d16ca362ed730b8a
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 4%

---

# 자주 묻는 질문 {#faq}

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 대상에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 기타 관련 질문 및 문제 해결 [!DNL Platform] 모든 곳에서 발생한 서비스 포함 [!DNL Platform] API는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

## 일반 대상 질문 {#general}

**Experience Platform UI와 내보낸 CSV 파일에 다른 프로필 카운트가 표시되는 이유는 무엇입니까?**

이는 Experience Platform이 세그먼테이션을 수행하는 방식에 따른 일반적인 동작입니다.

스트리밍 세그먼테이션은 하루 종일 스트리밍 세그먼트에 대한 프로필 수를 업데이트하는 반면, 일괄 처리 세그먼테이션은 24시간마다 한 번 배치 세그먼트에 대한 프로필 수를 업데이트합니다.

세그먼트 내보내기 일정이 세그먼테이션 일정과 다른 경우, 프로필은 UI와 내보낸 세그먼트 간에 계산됩니다 [!DNL CSV] 특히 스트리밍 세그먼트와 관련하여 파일이 다릅니다.

자세한 내용은 [Segmentation Service 설명서](../segmentation/home.md) 자세한 내용

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**에서 대상을 활성화하기 전에 필요한 작업 [!DNL Facebook Custom Audiences]?**

대상 세그먼트를 보내기 전에 [!DNL Facebook]를 채울 때는 다음 요구 사항을 충족하는지 확인하십시오.

* 사용자 [!DNL Facebook] 사용자 계정에는 **[!DNL Manage campaigns]** 사용하려는 광고 계정에 대해 사용 권한이 활성화되었습니다.
* 다음 **Adobe Experience Cloud** 비즈니스 계정을 귀사의 광고 파트너로서 추가해야 합니다 [!DNL Facebook Ad Account].  `business ID=206617933627973`. 자세한 내용은 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897) 자세한 내용은 Facebook 설명서 을 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 **캠페인 관리** 권한. 이 단계는 [!DNL Adobe Experience Platform] 통합에 필요합니다.
* 읽기 및 서명 [!DNL Facebook Custom Audiences] 서비스 약관. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.

**내 앱에 앱이나 픽셀을 추가해야 합니까? [!DNL Facebook] 광고주 계정?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**facebook은 Adobe Experience Platform에서 정보를 처리하는 데 얼마나 걸립니까?**

2021년 3월 현재 [!DNL Facebook Custom Audiences] 에서 받은 정보를 처리하려면 최대 1시간이 필요합니다. [!DNL Platform].

**사용할 수 있나요 [!DNL Facebook Custom Audiences] 대상 타깃팅에 대해 다음을 수행합니다 [!DNL Facebook] 앱과 같은 [!DNL Instagram]?**

를 사용할 수 있습니다 [!DNL Facebook Custom Audiences] 에서 지원하는 Facebook의 앱 제품군에서의 대상 타깃팅 대상 [!DNL Facebook Custom Audiences], 포함 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], 및 [!DNL Messenger]. 광고주가 캠페인을 실행할 앱의 선택은 의 배치 수준에서 표시됩니다. [!DNL Facebook Ads Manager].

**그 사이의 차이점은 무엇입니까 [!DNL Facebook Custom Audiences] 연결 및 [!DNL Facebook Pixel] 확장을 사용할 수 있습니까?**

다음 [!DNL Facebook Custom Audiences] 연결 사용 [!DNL Platform] 대상을 [!DNL Facebook], [[!DNL Facebook Pixel] 연결](../destinations/catalog/advertising/facebook-pixel.md) 사용 [!DNL Facebook] 웹 사이트에 통합된 픽셀.

이 두 가지 통합은 상호 보완적입니다. 두 가지 모두를 사용하여 대상 범위를 개선할 수 있습니다. 예를 들어 [!DNL Facebook Pixel] 계정을 만들지 않은 웹 사이트 방문자를 위한 확장 [!DNL Facebook Custom Audiences] 을 기반으로 기존 고객을 타겟팅하는 데 도움이 될 수 있습니다. [!DNL Platform] ID입니다.

**Adobe Experience Platform과 통합됩니까? [!DNL Facebook Custom Audiences] 더 이상 대상의 자격을 박탈하는 사용자를 지원합니까?**

예, 통합은 [!DNL Facebook Custom Audiences] 자격 조건을 충족하지 않는 경우

**전송하기 전에 대상 데이터를 해시하려면 어떻게 해야 합니까? [!DNL Facebook]?**

[!DNL Facebook] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상이 [!DNL Facebook] 키오프 가능 *해시* 이메일 주소 또는 전화 번호와 같은 식별자.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/facebook.md#id-matching-requirements).

**어떤 종류의 ID를 활성화할 수 있습니까? [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 은 다음 ID의 활성화를 지원합니다. 해시된 이메일, 해시된 전화 번호, [!DNL GAID], [!DNL IDFA], 및 사용자 지정 외부 ID .

**별도의 Facebook 계정에 대해 Platform UI에서 여러 Facebook 대상을 만들 수 있습니까?**

Experience Platform의 Facebook 대상은 Facebook의 광고 계정에 1:1입니다. 회사의 각 Facebook 광고 계정에 대해 별도의 Facebook 대상을 만들 수 있습니다. 다음을 수행합니다 [대상 연결 자습서](/help/destinations/ui/connect-destination.md) 플랫폼 UI에서 새로운 각 Facebook 대상에 대해 별도의 Facebook 계정에 연결합니다.

## linkedIn 일치하는 대상 {#linkedin}

**내 앱에 앱이나 픽셀을 추가해야 합니까? [!DNL LinkedIn] 광고주 계정?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**에서 대상을 활성화하기 전에 필요한 작업 [!DNL LinkedIn Matched Audiences]?**

를 사용하기 전에 [!UICONTROL linkedIn 대응 대상] 대상, [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상

편집 방법을 배우려면 [!DNL LinkedIn Campaign Manager] 사용자 권한 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753) ( LinkedIn 설명서)를 참조하십시오.

**전송하기 전에 대상 데이터를 해시하려면 어떻게 해야 합니까? [!DNL LinkedIn]?**

[!DNL LinkedIn] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상이 [!DNL LinkedIn] 키오프 가능 *해시* 이메일 주소 또는 전화 번호와 같은 식별자.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/linkedin.md#id-matching-requirements).

**어떤 종류의 ID를 활성화할 수 있습니까? [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 은 다음 ID의 활성화를 지원합니다. 해시된 이메일, [!DNL GAID], 및 [!DNL IDFA].
