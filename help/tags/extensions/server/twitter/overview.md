---
keywords: 이벤트 전달 확장;twitter;twitter 이벤트 전달 확장
title: Twitter 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장을 사용하면 비즈니스 요구 사항에 맞게 이벤트를 Twitter으로 수집할 수 있습니다.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 3%

---

# [!DNL Twitter] 이벤트 전달 확장 기능

[[!DNL Twitter]](https://twitter.com/i/flow/login) 은 사용자가 트윗으로 알려진 280자 길이의 메시지를 게시하고 상호 작용하는 온라인 소셜 미디어 및 소셜 네트워킹 서비스입니다. 사용자는 브라우저, 모바일 프론트엔드 소프트웨어를 사용하거나 프로그래밍 방식으로 Twitter과 상호 작용할 수 있습니다 [API](https://developer.twitter.com/en/docs/twitter-api)

다음 [!DNL Twitter] 웹 전환 API [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장을 사용하면 Adobe Experience Platform Edge Network에 캡처된 데이터를 활용하여 로 전송할 수 있습니다. [!DNL Twitter]. 이 문서에서는 확장의 사용 사례, 설치 방법 및 해당 기능을 이벤트 전달에 통합하는 방법에 대해 설명합니다 [규칙](../../../ui/managing-resources/rules.md).

[!DNL Twitter] 필수 [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) 을 사용한 인증용 [!DNL Twitter] [!DNL Web Conversions] API.

## 사용 사례

에서 Edge Network의 데이터를 사용하려면 이 확장 기능을 사용해야 합니다 [!DNL Twitter] customer analytics 및 타깃팅 기능을 활용하십시오.

예를 들어 조직의 마케팅 팀을 생각해 보십시오. 팀은 웹 사이트의 사용자 상호 작용 이벤트 데이터를 웹 사이트의 이벤트 데이터로 캡처하여 로 로드합니다 [!DNL Twitter] 이 이벤트 전달 확장 사용.

그런 다음 마케팅 및 분석 팀은 [!DNL Twitter's] 추가 분석을 수행하고 타겟팅된 광고 캠페인을 위해 이러한 사용자를 타겟팅하는 기능.

에만 해당되는 사용 사례에 대한 자세한 내용은 [!DNL Twitter]을(를) 참조하십시오. [[!DNL Twitter] 사용 사례](https://developer.twitter.com/en/use-cases/build-for-businesses) 설명서를 참조하십시오.

## [!DNL Twitter] 사전 요구 사항 및 보호 기능 {#prerequisites}

유효한 권한이 있어야 합니다. [!DNL Twitter] 이 확장을 사용하려면 계정을 사용하십시오. 로 이동 [[!DNL Twitter] 등록 페이지](https://help.twitter.com/en/using-twitter/create-twitter-account) 아직 계정이 없는 경우 등록하고 계정을 만듭니다.

다음으로 계정을 설정해야 합니다. [!DNL Twitter] 개발자 계정입니다. 개발자로 등록하는 방법에 대한 자세한 내용은 [[!DNL Twitter] 개발자 계정](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API 보호 기능 {#guardrails}

다음 [!DNL Twitter] 웹 전환 API의 속도 제한은 15분 간격당 60,000개의 요청이며, 각 요청에서 500개의 이벤트를 허용합니다.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Twitter]를 사용하려면 다음 입력이 필요합니다.

| 키 유형 | 설명 |
| --- | --- |
| 소비자 키 | 액세스&#x200B;을 위한 앱의 API 키 [!DNL Twitter] API. 다음을 참조하십시오. [!DNL Twitter] 설명서 [api 키 및 암호](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 지침을 참조하십시오. | |
| 소비자 암호 | API 보안을 사용하면 앱에서 [!DNL Twitter] API. 다음을 참조하십시오. [!DNL Twitter] 설명서 [api 키 및 암호](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 지침을 참조하십시오. |
| 토큰 암호 | 에 인증하는 데 사용되는 앱의 만료되지 않는 토큰 암호 [!DNL Twitter] OAuth를 통한 API. 다음을 참조하십시오. [!DNL Twitter] 설명서 [사용 액세스 토큰 가져오기](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 지침을 참조하십시오. |
| 액세스 토큰 | 앱의 만료되지 않는 액세스 토큰, 인증용 [!DNL Twitter] OAuth를 통한 API. 다음을 참조하십시오. [!DNL Twitter] 설명서 [사용 액세스 토큰 가져오기](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 지침을 참조하십시오. |
| 픽셀 ID | 다음 [!DNL Twitter] Pixel은 사이트 작업 또는 전환을 추적하기 위해 웹 사이트에 구현된 웹 사이트 태그입니다. 다음을 참조하십시오. [!DNL Twitter] 설명서 [웹 사이트에 대한 전환 추적](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) 지침을 참조하십시오. |

## 설치 및 구성 [!DNL Twitter] 확장 {#install}

확장을 설치하려면 [이벤트 전달 속성 만들기](../../../ui/event-forwarding/overview.md#properties) 또는 편집할 기존 속성을 대신 선택하십시오.

선택 **[!UICONTROL 확장]** 왼쪽 탐색. 다음에서 **[!UICONTROL 카탈로그]** 탭, 선택 **[!UICONTROL 설치]** 카드 사용 [!DNL Twitter] 확장명.

![다음을 표시하는 카탈로그 [!DNL Twitter] 확장 강조 표시 설치.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>구현 요구 사항에 따라 확장을 구성하기 전에 스키마, 데이터 요소 및 데이터 세트를 만들어야 할 수 있습니다. 사용 사례에 대해 설정해야 하는 엔터티를 결정하려면 시작하기 전에 모든 구성 단계를 검토하십시오.

다음 화면에서 다음을 입력합니다 [구성 값](#configuration-details) 이전에 수집한 항목 [!DNL Twitter]:

* **[!UICONTROL 픽셀 ID]**
* **[!UICONTROL 소비자 키]**
* **[!UICONTROL 소비자 암호]**
* **[!UICONTROL 토큰]**
* **[!UICONTROL 토큰 암호]**

완료되면 다음을 선택합니다. **[!UICONTROL 저장]**.

![[!DNL Twitter] 구성 화면 [!DNL Twitter] 확장명.](../../../images/extensions/server/twitter/configure.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙 만들기를 시작할 수 있습니다 [!DNL Twitter].

새로 만들기 [규칙](../../../ui/managing-resources/rules.md) 이벤트 전달 속성에서 다음을 수행합니다. 아래 **[!UICONTROL 작업]**, 새 작업을 추가하고 확장을 로 설정합니다. **[!UICONTROL Twitter]**. Adobe Experience Edge 네트워크 이벤트를 [!DNL Twitter], 를 설정합니다. **[!UICONTROL 작업 유형]** 끝 **[!UICONTROL 웹 전환 보내기].**

선택 후 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다. 다음을 매핑해야 합니다. [!DNL Twitter] 이전에 만든 데이터 요소에 대한 이벤트 속성입니다. 자세한 내용은 [[!DNL Twitter] 웹 전환 API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![다음 [!DNL Twitter] 전환 이벤트 규칙 만들기](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL 사용자 식별]**

| 필드 이름 | 설명 | 예 | 필수 여부 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] 클릭 ID] | [!DNL Twitter] 클릭스루 URL에서 구문 분석된 클릭 ID입니다. | 26l6412g5p4iyj65a2oic2ayg2 | 다른 식별자가 추가되지 않는 경우 필수입니다. |
| [!UICONTROL 이메일] | SHA256으로 해시된 이메일 주소. 텍스트는 소문자여야 하며 해시 전에 후행 또는 선행 공백을 제거해야 합니다. | eventforwarding@example.com | 다른 식별자가 추가되지 않는 경우 필수입니다. |
| [!UICONTROL 전화] | 전화기는 전환 이벤트와 일치하는 식별자 역할을 합니다. 전화번호는 E164 형식 [+][국가 코드]여야 합니다.[지역 번호][local phone number] 해싱하기 전에 | +911234567875 | 다른 식별자가 추가되지 않는 경우 필수입니다. |

**[!UICONTROL 전환 데이터]**

| 필드 이름 | 설명 | 예 | 필수 여부 |
| --- | --- | --- | --- |
| [!UICONTROL 전환 시간] | ISO 8601 또는 yyyy-MM-dd&#39;T&#39;HH의 문자열로 표시된 날짜-시간:mm:ss:SSSZ 형식입니다. | 2022년 2월 18일:14:00.603Z | 예 |
| [!UICONTROL 이벤트 ID] | 특정 이벤트의 base-36 ID입니다. 이 ID는 내에 포함된 사전 구성된 이벤트와 일치해야 합니다 [!DNL Twitter] 광고 계정입니다. 이를 이벤트 관리자의 해당 이벤트에 대한 ID라고 합니다. | o87ne 또는 tw-o8z6j-o87ne (tw-pixel_id-event-id) | 예 |
| [!UICONTROL 항목 수] | 이벤트에서 구매 중인 항목 수입니다. 0보다 큰 양수여야 합니다. | 4 | 아니요 |
| [!UICONTROL 통화] | 이벤트에서 구매 중인 항목의 통화입니다. 이는 ISO-4217로 표시되며, 제공되지 않을 경우 기본값은 USD입니다. | 미국 달러 | 아니요 |
| [!UICONTROL 값] | 이벤트에서 구매 중인 항목의 가격 값. | 100.00 | 아니요 |
| [!UICONTROL 전환 ID] | 동일한 이벤트 태그에서 웹 픽셀과 전환 API 전환 간의 중복 제거에 사용할 수 있는 전환 이벤트의 식별자입니다. | 23294827 | 아니요 |
| [!UICONTROL 설명] | 변환에 대한 추가 정보가 포함된 설명입니다. | 전환 테스트 | 아니요 |

## 내에서 데이터 유효성 검사 [!DNL Twitter]

이벤트 전달 규칙이 생성되고 실행되면 로 전송된 이벤트인지 확인합니다. [!DNL Twitter] API는 의 예상대로 표시됩니다. [!DNL Twitter] UI.

이벤트 컬렉션 및 [!DNL Experience Platform] 통합에 성공했습니다. 다음 내에서 이벤트가 표시됩니다. [!DNL Twitter] [!UICONTROL 이벤트 관리자].

![다음 [!DNL Twitter] 이벤트 관리자](../../../images/extensions/server/twitter/event-manager.png)

## 다음 단계

이 안내서에서는 전환 이벤트를에 보내는 방법을 다룹니다. [!DNL Twitter] 이벤트 전달을 사용합니다. 이러한 기본 기술에 대한 자세한 내용은 공식 설명서를 참조하십시오.

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] 웹 전환 API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 사용자 액세스 토큰](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [픽셀 ID 및 전환 추적](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
