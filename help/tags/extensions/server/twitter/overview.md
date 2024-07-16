---
keywords: 이벤트 전달 확장;twitter;twitter 이벤트 전달 확장
title: Twitter 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장을 사용하면 비즈니스 요구 사항에 맞게 이벤트를 Twitter으로 수집할 수 있습니다.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# [!DNL Twitter] 이벤트 전달 확장 기능

[[!DNL Twitter]](https://twitter.com/i/flow/login)은(는) 사용자가 트윗이라고 하는 280자 길이의 메시지를 게시하고 상호 작용하는 온라인 소셜 미디어 및 소셜 네트워킹 서비스입니다. 사용자는 브라우저, 모바일 프론트엔드 소프트웨어를 사용하거나 [API](https://developer.twitter.com/en/docs/twitter-api)를 통해 프로그래밍 방식으로 Twitter과 상호 작용할 수 있습니다

[!DNL Twitter] 웹 전환 API [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하여 [!DNL Twitter]에 보낼 수 있습니다. 이 문서에서는 확장의 사용 사례, 설치 방법 및 해당 기능을 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)에 통합하는 방법에 대해 설명합니다.

[!DNL Twitter]은(는) [!DNL Twitter] [!DNL Web Conversions] API를 사용한 인증을 위해 [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a)이(가) 필요합니다.

## 사용 사례

[!DNL Twitter]에 있는 Edge Network의 데이터를 사용하여 고객 분석 및 타깃팅 기능을 이용하려면 이 확장을 사용해야 합니다.

예를 들어 조직의 마케팅 팀을 생각해 보십시오. 팀은 웹 사이트의 사용자 인터랙션 이벤트 데이터를 웹 사이트의 이벤트 데이터로 캡처하고 이 이벤트 전달 확장을 사용하여 [!DNL Twitter]에 로드합니다.

그런 다음 마케팅 및 분석 팀은 [!DNL Twitter's] 기능을 활용하여 추가 분석을 수행하고 이러한 사용자를 타겟팅된 광고 캠페인으로 타겟팅할 수 있습니다.

[!DNL Twitter]과(와) 관련된 사용 사례에 대한 자세한 내용은 [[!DNL Twitter] 사용 사례](https://developer.twitter.com/en/use-cases/build-for-businesses) 설명서를 참조하세요.

## [!DNL Twitter]개의 필수 구성 요소 및 보호 기능 {#prerequisites}

이 확장을 사용하려면 올바른 [!DNL Twitter] 계정이 있어야 합니다. 아직 계정이 없는 경우 [[!DNL Twitter] 등록 페이지](https://help.twitter.com/en/using-twitter/create-twitter-account)(으)로 이동하여 등록하고 계정을 만드십시오.

계정을 [!DNL Twitter] 개발자 계정으로 설정해야 합니다. 개발자로 등록하는 방법은 [[!DNL Twitter] 개발자 계정](https://developer.twitter.com/en/support/twitter-api/developer-account1)을 참조하세요.

### API 보호 기능 {#guardrails}

[!DNL Twitter] 웹 전환 API의 속도 제한은 15분 간격당 60,000개이며, 각 요청에서 500개의 이벤트를 허용합니다.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Twitter]에 연결하려면 다음 입력이 필요합니다.

| 키 유형 | 설명 |
| --- | --- |
| 소비자 키 | {&#x200B;0} API에 액세스하기 위한 앱의 API 키. [!DNL Twitter] 지침은 [api 키 및 암호](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)의 [!DNL Twitter] 설명서를 참조하십시오. | |
| 소비자 암호 | API 암호를 사용하면 앱이 [!DNL Twitter] API에 액세스할 수 있습니다. 지침은 [api 키 및 암호](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)의 [!DNL Twitter] 설명서를 참조하십시오. |
| 토큰 암호 | OAuth를 통해 [!DNL Twitter] API에 인증하는 데 사용되는 앱의 만료되지 않는 토큰 암호입니다. 지침은 [사용 액세스 토큰 가져오기](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)에 대한 [!DNL Twitter] 설명서를 참조하세요. |
| 액세스 토큰 | OAuth를 통해 [!DNL Twitter] API 인증에 사용되는 앱의 만료되지 않는 액세스 토큰입니다. 지침은 [사용 액세스 토큰 가져오기](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)에 대한 [!DNL Twitter] 설명서를 참조하세요. |
| 픽셀 ID | [!DNL Twitter] 픽셀은 사이트 작업 또는 전환을 추적하기 위해 웹 사이트에 구현된 웹 사이트 태그입니다. 지침은 [웹 사이트에 대한 전환 추적](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)에 대한 [!DNL Twitter] 설명서를 참조하십시오. |

## [!DNL Twitter] 확장 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 대신 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 [!DNL Twitter] 확장의 카드에서 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![설치를 강조 표시하는 [!DNL Twitter] 확장을 표시하는 카탈로그.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>구현 요구 사항에 따라 확장을 구성하기 전에 스키마, 데이터 요소 및 데이터 세트를 만들어야 할 수 있습니다. 사용 사례에 대해 설정해야 하는 엔터티를 결정하려면 시작하기 전에 모든 구성 단계를 검토하십시오.

다음 화면에서는 이전에 [!DNL Twitter]에서 수집한 다음 [구성 값](#configuration-details)을 입력합니다.

* **[!UICONTROL 픽셀 ID]**
* **[!UICONTROL 소비자 키]**
* **[!UICONTROL 소비자 암호]**
* **[!UICONTROL 토큰]**
* **[!UICONTROL 토큰 암호]**

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

[!DNL Twitter] 확장에 대한 ![[!DNL Twitter] 구성 화면입니다.](../../../images/extensions/server/twitter/configure.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 [!DNL Twitter]에 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙을 만들 수 있습니다.

이벤트 전달 속성에 새 [규칙](../../../ui/managing-resources/rules.md)을(를) 만듭니다. **[!UICONTROL 작업]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL Twitter]**(으)로 설정합니다. Edge Network 이벤트를 [!DNL Twitter]에 보내려면 **[!UICONTROL 작업 유형]**&#x200B;을(를) **[!UICONTROL 웹 전환 보내기].**(으)로 설정하십시오.

선택 후 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다. [!DNL Twitter] 이벤트 속성을 이전에 만든 데이터 요소에 매핑해야 합니다. 자세한 내용은 [[!DNL Twitter] 웹 전환 API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)를 참조하세요.

![전환 이벤트 규칙을 만드는 [!DNL Twitter]입니다.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL 사용자 식별]**

| 필드 이름 | 설명 | 예 | 필수 여부 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] 클릭 ID] | 클릭스루 URL에서 구문 분석된 [!DNL Twitter] 클릭 ID입니다. | 26l6412g5p4iyj65a2oic2ayg2 | 다른 식별자가 추가되지 않는 경우 필수입니다. |
| [!UICONTROL 이메일] | SHA256으로 해시된 이메일 주소. 텍스트는 소문자여야 하며 해시 전에 후행 또는 선행 공백을 제거해야 합니다. | eventforwarding@example.com | 다른 식별자가 추가되지 않는 경우 필수입니다. |
| [!UICONTROL 전화] | 전화기는 전환 이벤트와 일치하는 식별자 역할을 합니다. 해싱하기 전에 전화번호는 E164 형식 [+][국가 코드][지역 코드][local phone number]여야 합니다. | +911234567875 | 다른 식별자가 추가되지 않는 경우 필수입니다. |

**[!UICONTROL 전환 데이터]**

| 필드 이름 | 설명 | 예 | 필수 여부 |
| --- | --- | --- | --- |
| [!UICONTROL 전환 시간] | ISO 8601 또는 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 형식의 문자열로 표시된 날짜-시간입니다. | 2022-02-18T01:14:00.603Z | 예 |
| [!UICONTROL 이벤트 ID] | 특정 이벤트의 base-36 ID입니다. 이 ID는 [!DNL Twitter] 광고 계정에 포함된 사전 구성된 이벤트와 일치해야 합니다. 이를 이벤트 관리자의 해당 이벤트에 대한 ID라고 합니다. | o87ne 또는 tw-o8z6j-o87ne (tw-pixel_id-event-id) | 예 |
| [!UICONTROL 항목 수] | 이벤트에서 구매 중인 항목 수입니다. 0보다 큰 양수여야 합니다. | 4 | 아니요 |
| [!UICONTROL 통화] | 이벤트에서 구매 중인 항목의 통화입니다. 이는 ISO-4217로 표시되며, 제공되지 않을 경우 기본값은 USD입니다. | 미국 달러 | 아니요 |
| [!UICONTROL 값] | 이벤트에서 구매 중인 항목의 가격 값. | 100.00 | 아니요 |
| [!UICONTROL 전환 ID] | 동일한 이벤트 태그에서 웹 픽셀과 전환 API 전환 간의 중복 제거에 사용할 수 있는 전환 이벤트의 식별자입니다. | 23294827 | 아니요 |
| [!UICONTROL 설명] | 변환에 대한 추가 정보가 포함된 설명입니다. | 전환 테스트 | 아니요 |

## [!DNL Twitter] 내의 데이터 유효성 검사

이벤트 전달 규칙이 만들어지고 실행되면 [!DNL Twitter] API로 전송된 이벤트가 [!DNL Twitter] UI에 예상대로 표시되는지 확인합니다.

이벤트 컬렉션 및 [!DNL Experience Platform] 통합이 성공하면 [!DNL Twitter] [!UICONTROL 이벤트 관리자] 내에 이벤트가 표시됩니다.

![[!DNL Twitter] 이벤트 관리자](../../../images/extensions/server/twitter/event-manager.png)

## 다음 단계

이 안내서에서는 이벤트 전달을 사용하여 전환 이벤트를 [!DNL Twitter]에 보내는 방법에 대해 설명합니다. 이러한 기본 기술에 대한 자세한 내용은 공식 설명서를 참조하십시오.

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] 웹 전환 API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 사용자 액세스 토큰](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [픽셀 ID 및 전환 추적](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
