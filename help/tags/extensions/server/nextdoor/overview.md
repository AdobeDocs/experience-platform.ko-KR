---
title: Nextdoor 변환 API 확장
description: Nextdoor 전환 API 확장을 사용하여 전환 이벤트를 전송하여 광고 캠페인의 성능을 추적하는 방법에 대해 알아봅니다.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 8%

---


# [!DNL Nextdoor] 전환 API 확장 - 사용 안내서

## 개요

[!DNL Nextdoor]은(는) 지역 주민과 지역 커뮤니티를 연결하는 지역에 대한 소셜 네트워킹 서비스입니다. 이웃들이 소통하고 정보를 공유하며 지역 행사나 뉴스에 대한 최신 정보를 유지하고 자신이 사는 지역의 다른 사람들과 물건을 사고팔 수 있는 플랫폼이다.

[[!DNL Nextdoor] 전환 API 확장](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API)을(를) 사용하여 전환 이벤트를 [!DNL Nextdoor's] 전환 API로 직접 보냅니다. 이 확장을 사용하면 서버측 전환 데이터를 전송하여 [!DNL Nextdoor] 광고 캠페인의 성능을 추적하고 측정할 수 있습니다.

이 안내서에서는 이벤트 전달 [!DNL Nextdoor]규칙[에서 &#x200B;](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/ui/rules) 전환 API 확장을 설치, 구성 및 사용하는 방법을 보여 줍니다.

## 전제 조건 {#prerequisites}

이 확장을 사용하려면 유효한 [!DNL Nextdoor] Ads Manager 계정이 필요합니다. 아직 계정이 없는 경우 [[!DNL Nextdoor Ads] 등록 페이지](https://ads.nextdoor.com/v2/signup)&#x200B;(으)로 이동하여 등록하고 계정을 만드십시오.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Nextdoor]에 연결하려면 다음 정보가 필요합니다.

| 자격 증명 | 설명 | 보안 정보 |
| --- | --- | --- |
| 데이터 Source ID | [!DNL Nextdoor]의 고유한 데이터 원본 식별자입니다. 이 식별자는 Assets > 픽셀 페이지에 액세스하고 Nextdoor 픽셀을 생성하여 [!DNL Nextdoor Ads Manager] 계정에서 찾을 수 있습니다. | 조직 내에서 공유해도 안전합니다. |
| 액세스 토큰 | 보안 통신을 위한 API 인증 액세스 토큰입니다. [!DNL Nextdoor Ads Manager] 계정에 로그인하고 API 설정에 액세스하여 이 토큰을 생성할 수 있습니다. | 이 토큰은 계정에 대한 액세스를 제공하므로 보안을 유지합니다. |

## [!DNL Nextdoor] 확장 설치 및 구성 {#install}

확장을 설치하려면 왼쪽 탐색에서 **[!UICONTROL Extensions]**&#x200B;을(를) 선택합니다. **[!UICONTROL Catalog]** 탭에서 **[!UICONTROL Nextdoor Conversion API Extension]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Install]**&#x200B;을(를) 선택합니다.

![설치를 강조 표시하는 [!DNL Nextdoor] 확장 카드를 표시하는 확장 카탈로그입니다.](../../../images/extensions/server/nextdoor/install-extension.png)

다음 화면에서는 [!DNL Nextdoor Ads Manager]에서 생성한 구성 값을 입력합니다.

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

완료되면 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

![[!DNL Nextdoor] 전환 API 확장에 대한 [!DNL Nextdoor] 구성 화면입니다.](../../../images/extensions/server/nextdoor/configure.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 [!DNL Nextdoor]&#x200B;(으)로 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙을 만들 수 있습니다.

이벤트 전달 속성에 새 [규칙](../../../ui/managing-resources/rules.md)을(를) 만듭니다. **[!UICONTROL Actions]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL Nextdoor Conversion API Extension]**(으)로 설정합니다. Edge Network 이벤트를 [!DNL Nextdoor]에 보내려면 **[!UICONTROL Action Type]**&#x200B;을(를) **[!UICONTROL Report Web Conversions]**(으)로 설정하십시오.

![데이터 수집 UI에서 [!UICONTROL Report Web Conversions] 규칙에 대해 [!DNL Nextdoor] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/nextdoor/select-action.png)

이 옵션을 선택하면 아래 설명된 대로 이벤트를 추가로 구성할 수 있는 추가 제어 기능이 나타납니다. 완료되면 **[!UICONTROL Keep Changes]**&#x200B;을(를) 선택하여 규칙을 저장합니다.

**본문 매개 변수**

다음 핵심 매개 변수는 전환 이벤트를 정의합니다.

| 매개변수 | 설명 | 데이터 유형 | 필수 여부 | 옵션/형식 | 예 |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | 추적 중인 전환 이벤트의 유형을 지정합니다. | 문자열(드롭다운) | 필수 여부 | <ul><li>구매</li><li>리드</li><li>등록</li><li>장바구니에 추가</li><li>체크아웃 시작</li><li>페이지 보기</li><li>검색</li><li>컨텐츠 보기</li><li>위시리스트에 추가</li><li>구독</li><li>사용자 정의</li></li>전환 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | 중복 이벤트 보고를 방지하는 고유 식별자입니다. 비어 있는 경우 자동으로 생성됩니다. | 문자열 | 선택 사항입니다 | 고유 문자열 식별자 | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | 전환 이벤트가 발생한 타임스탬프. 비워 두면 기본값은 현재 시간으로 설정됩니다. | 정수 | 선택 사항입니다 | Unix 타임스탬프(초) | `1703980800`(2023년 12월 30일) |
| [!UICONTROL Action Source] | 전환이 발생한 채널 또는 플랫폼입니다. | 문자열(드롭다운) | 필수 여부 | <ul><li>웹 사이트</li><li>이메일</li><li>앱</li><li>phone_call</li><li>채팅</li><li>physical_store</li><li>system_generated</li><li>기타</li></ul> | `website` |
| [!UICONTROL Data Source ID] | 특정 이벤트에 대한 글로벌 데이터 소스 ID를 재정의합니다. 비워 두면 구성에서 상속합니다. | 문자열 | 선택 사항입니다 | 영숫자 문자열 | `12345` |
| [!UICONTROL Action Source URL] | 전환이 발생한 특정 URL입니다. | 문자열 | 선택 사항입니다 | 프로토콜을 포함한 전체 URL | https://example.com/checkout/success |

**개인 정보 및 준수 매개 변수**

다음 매개 변수를 사용하여 개인 정보 보호 규정을 준수하십시오.

| 매개변수 | 설명 | 데이터 유형 | 필수 여부 | 값/형식 | 예 |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | 개인 정보 보호 규정 준수를 위해 데이터 사용을 제한하는 플래그. | 정수 | 선택 사항입니다 | <ul><li>0 = 제한 없음</li><li>1 = 제한</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | 국가별 데이터 처리 제한 사항. | 정수 | 선택 사항입니다 | 1 = USA(다른 코드가 지원될 수 있음) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | 미국 사용자에 대한 주별 제한 사항. | 정수 | 선택 사항입니다 | 1000 = CA, 1001 = CO 등 | `1000` |
| [!UICONTROL Test Event] | 이벤트를 개발/디버깅에 대한 테스트로 표시합니다. | 문자열 | 선택 사항입니다 | 비어 있지 않은 모든 문자열 | `test` |

**고객 정보 매개 변수**

>[!IMPORTANT]
>
>적절한 이벤트 속성 및 일치를 위해 하나 이상의 고객 정보 매개 변수를 제공해야 합니다.

| 매개변수 | 설명 | 데이터 유형 | 필수 여부 | 형식 | 예 |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | ID 일치를 위한 고객의 이메일 주소. | 문자열 | 최소 1개의 고객 필드 필요 | 일반 텍스트 또는 SHA-256 해시 | `user@example.com` |
| [!UICONTROL Phone Number] | ID 일치를 위한 고객 전화번호. | 문자열 | 최소 1개의 고객 필드 필요 | E.164 형식(SHA-256으로 해시됨) | `+15551234567` |
| [!UICONTROL First Name] | 향상된 일치를 위한 고객의 이름. | 문자열 | 최소 1개의 고객 필드 필요 | 일반 텍스트 또는 SHA-256 해시 | `John` |
| [!UICONTROL Last Name] | 향상된 일치를 위한 고객의 성. | 문자열 | 최소 1개의 고객 필드 필요 | 일반 텍스트 또는 SHA-256 해시 | `Smith` |
| [!UICONTROL Date of Birth] | 인구 통계 일치를 위한 고객의 생년월일. | 문자열 | 선택 사항입니다 | YYYYMMDD (SHA-256 해시) | `19900115` |
| [!UICONTROL Gender] | 인구 통계학적 타겟팅에 대한 고객의 성별. | 문자열 | 선택 사항입니다 | M/F/O(SHA-256 해시) | `M` |
| [!UICONTROL External ID] | 내부 고객 식별자. | 문자열 | 선택 사항입니다 | 모든 고유 문자열 | `customer_12345` |
| [!UICONTROL Street Address] | 고객의 주소입니다. | 문자열 | 선택 사항입니다 | SHA-256 해시 | `123 Main Street`(해시됨) |
| [!UICONTROL City] | 고객의 도시입니다. | 문자열 | 선택 사항입니다 | SHA-256 해시 | `San Francisco`(해시됨) |
| [!UICONTROL State] | 고객의 시/도. | 문자열 | 선택 사항입니다 | 두 글자 코드(SHA-256 해시) | `CA`(해시됨) |
| [!UICONTROL Zip Code] | 고객의 우편 번호입니다. | 문자열 | 선택 사항입니다 | 처음 5자리 미국(SHA-256 해시) | `94102`(해시됨) |
| [!UICONTROL Country] | 고객의 국가입니다. | 문자열 | 선택 사항입니다 | ISO-3166-1 alpha-2(SHA-256 해시) | `US`(해시됨) |
| [!UICONTROL Click ID] | 속성을 위한 다음 클릭 식별자. | 문자열 | 선택 사항입니다 | `ndclid` URL 매개 변수에서 캡처됨 | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | 사용자 디바이스의 IP 주소입니다. | 문자열 | 선택 사항입니다 | IPv4 또는 IPv6 주소 | `192.168.1.1` |
| [!UICONTROL Client User Agent] | 브라우저 사용자 에이전트 문자열입니다. | 문자열 | 선택 사항입니다 | 원시 브라우저 사용자 에이전트 문자열 | `Mozilla/5.0 (Windows...)` |

**사용자 정의 매개변수**

이러한 매개 변수는 전환 이벤트에 대한 추가 컨텍스트를 제공합니다.

| 매개변수 | 설명 | 데이터 유형 | 필수 여부 | 형식 | 예 |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | 구매 트랜잭션의 총 값입니다. | 문자열 | **구매 이벤트에 필요** | ISO 4217 통화 + 금액(공백 없음) | `USD123.45` |
| [!UICONTROL Order ID] | 고유 거래 또는 주문 식별자. | 문자열 | 선택 사항입니다 | 모든 고유 문자열 | `order_12345` |
| [!UICONTROL Delivery Category] | 제품/서비스 제공 방법. | 문자열 | 선택 사항입니다 | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | 구매한 제품에 대한 자세한 정보. | 문자열(JSON 배열) | 선택 사항입니다 | 제품 개체의 JSON 배열 | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**모바일 앱 매개 변수**

`Action Source = 'APP'`할 때 다음 매개 변수를 포함해야 합니다.

| 매개변수 | 설명 | 데이터 유형 | 필수 여부 | 형식 | 예 |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | 모바일 애플리케이션 식별자. | 문자열 | **앱 이벤트에 필요** | <ul><li>번들 ID (iOS)</li><li>패키지 이름(Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | iOS 앱 추적 투명도 동의 상태. | 문자열 | **앱 이벤트에 필요** | 부울 문자열 | `true` |
| [!UICONTROL Platform] | 모바일 운영 체제. | 문자열 | **앱 이벤트에 필요** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | 모바일 애플리케이션 버전. | 문자열 | **앱 이벤트에 필요** | 앱에서 정의한 버전 문자열 | `2.0.0-beta` |

## 이벤트 유형 {#event-types}

다양한 전환 시나리오에 대해 지원되는 이벤트 유형은 다음과 같습니다.

| 이벤트 이름 | 이벤트 유형 | 설명 | 사용 사례 | 필수 필드 | 참고 |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | 표준 | 구매 트랜잭션이 완료되었습니다. | 전자 상거래 전환 | <ul><li>이벤트 이름</li><li>주문 값</li><li>고객 정보</li></ul> | ROAS 최적화에 가장 중요 |
| [!UICONTROL Lead] | 표준 | 리드 생성 또는 조회. | 양식 제출, 연락처 요청 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | B2B를 위한 고가치 전환 |
| [!UICONTROL Sign Up] | 표준 | 사용자 등록 또는 계정 만들기. | 뉴스레터 등록, 계정 등록 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 최상위 funnel 전환 추적 |
| [!UICONTROL Add to Cart] | 표준 | 장바구니에 제품이 추가되었습니다. | E-commerce funnel 추적 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 중간 funnel 참여 신호 |
| [!UICONTROL Initiate Checkout] | 표준 | 체크아웃 프로세스가 시작되었습니다. | 구매 의도 추적 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 강력한 구매 의도 지표 |
| [!UICONTROL Page View] | 표준 | 중요한 페이지를 방문했습니다. | 콘텐츠 참여, 랜딩 페이지 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 고가치 페이지에만 사용 |
| [!UICONTROL Search] | 표준 | 사이트에서 검색이 수행되었습니다. | 제품/컨텐츠 검색 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 활성 사용자 참여를 나타냅니다. |
| [!UICONTROL View Content] | 표준 | 본 컨텐츠 또는 제품 | 제품 페이지 보기 수, 콘텐츠 참여 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 리마케팅 대상자에 유용함 |
| [!UICONTROL Add to Wishlist] | 표준 | 위시리스트에 제품이 추가되었습니다. | 향후 구매 의도 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 강력한 제품 관심을 나타냅니다. |
| [!UICONTROL Subscribe] | 표준 | 서비스/뉴스레터 구독. | 반복 매출, 참여 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 높은 라이프타임 값 표시기 |
| [!UICONTROL Custom Conversion 1 - 10] | 사용자 정의 | 비즈니스별 전환 이벤트. | 자체 전환 유형 정의 | <ul><li>이벤트 이름</li><li>고객 정보</li></ul> | 고유한 비즈니스 작업에 대해 사용자 지정 |

## 데이터 요소 통합 {#data-element}

모든 필드는 Adobe 이벤트 전달 데이터 요소를 지원합니다. 필드 옆에 있는 데이터 요소 아이콘 ![데이터 요소](../../../images/extensions/server/nextdoor/data-element-icon.png)을(를) 선택하여 다음 작업을 수행합니다.

* **기존 데이터 요소 선택**: 이미 만들어진 데이터 요소 중에서 선택합니다.
* **새 데이터 요소 추가**: 필요에 따라 새 데이터 요소를 만들고 정의합니다.
* **동적 값 적용**: 웹 사이트에서 가져온 동적 콘텐츠로 필드를 채웁니다.

## 모범 사례 {#best-practices}

정확한 전환 추적을 보장하고 데이터 품질을 개선하며 개인 정보 보호 규정을 준수하려면 다음 모범 사례를 따르십시오. 이러한 권장 사항을 통해 [!DNL Nextdoor] 전환 API 통합의 효과를 극대화하고 광고 성능을 최적화할 수 있습니다.

### 데이터 품질 및 개인 정보 보호 규정 준수

적절한 데이터 처리는 사용자 개인 정보 보호 및 규정 준수를 유지하면서 전환 속성 정확도를 최대화하는 데 필수적입니다. 이러한 사례는 고객 데이터의 형식이 올바르게 지정되고, 안전하게 처리되고, 개인 정보 보호 규정에 따라 처리되도록 하는 데 도움이 됩니다.

* **일관된 데이터 서식 사용**: 전자 메일, 전화 번호 및 기타 데이터를 일관되게 서식 지정:

   * **전자 메일 정규화**: 전자 메일을 소문자로 변환하고, 공백을 트리밍하고, [!DNL Gmail] 주소에서 점을 제거합니다.
   * **전화 번호 표준화**: 국제 호환성을 위해 E.164 형식(+1234567890)을 사용하십시오.
   * **주소 정규화**: 거리 약어(St., Ave., Rd.)를 표준화하고 추가 공백을 제거합니다.
   * **이름 서식**: 이름을 소문자로 변환하고, 추가 공백을 제거하고, 특수 문자를 일관되게 처리합니다.

* **중요 데이터 해시**: 중요 고객 데이터를 전송하기 전에 해시하는 것이 좋습니다. 해시 전에 항상 데이터를 정규화하여 일관된 해시 값을 유지합니다.

   * 전화번호, 주소 및 기타 PII에 대해 SHA-256 해싱을 사용합니다.
   * 확장 프로그램은 일반 텍스트 이메일을 자동으로 해시합니다. 두 형식 중 하나를 보낼 수 있습니다.
   * 모든 추적 구현에서 데이터를 일관되게 해시합니다.
      * **예**: 해싱하기 전에 &quot;John@Example.COM&quot; → &quot;john@example.com&quot;을 정규화합니다.

* **전체 정보 제공**: 더 나은 일치를 위해 가능한 한 많은 고객 정보를 포함하십시오.

   * 사용 가능한 경우 여러 식별자(이메일 + 전화 또는 이메일 + 이름 + 주소)를 포함합니다.
   * 외부 고객 ID를 사용하여 전환 이벤트를 CRM 데이터에 연결합니다.
   * 개인 정보 보호 법률을 준수하고 사용 가능한 경우 인구 통계 데이터(연령, 성별)를 제공합니다.

* **동의 관리**: 데이터 수집에 대한 적절한 동의가 있는지 확인하십시오.

   * 고객 데이터를 수집하기 전에 적절한 동의 메커니즘을 구현합니다.
   * 사용자 옵트아웃 환경 설정 및 데이터 삭제 요청을 준수합니다.
   * 옵트아웃한 사용자의 제한된 데이터 사용 매개변수를 사용합니다.
   * **리소스**:
      * [GDPR 준수 안내서](https://gdpr.eu/compliance/)
      * [CCPA 개인 정보 보호 요구 사항](https://oag.ca.gov/privacy/ccpa)

* **데이터 최소화**: 전환 추적에 필요한 데이터만 보냅니다.

   * 속성 및 최적화에 필수적인 데이터만 수집하고 전송합니다.
   * 보내는 데이터 필드를 정기적으로 검토하고 감사하십시오.
   * 불필요한 고객 정보를 제거하여 개인 정보 위험을 줄입니다.

* **정확한 타임스탬프 사용**: 이벤트 타임스탬프가 적절한 속성에 대해 정확한지 확인합니다.
   * 데이터를 처리할 때가 아니라 전환이 발생한 실제 시간을 사용합니다.
   * 타임스탬프가 Unix epoch 형식(1970년 1월 1일 이후 경과한 초)인지 확인합니다.
   * 타임스탬프 계산에서 시간대 차이를 고려합니다.

### 이벤트 중복 제거

중복 전환 이벤트를 방지하여 정확한 캠페인 측정을 보장하고 부풀려진 성능 지표를 방지합니다. 각 전환이 한 번만 카운트되도록 적절한 중복 제거를 구현하여 최적화 결정에 신뢰할 수 있는 데이터를 제공합니다.

* **고유 이벤트 ID 제공**: 중복 전환을 방지하려면 항상 고유 이벤트 ID를 사용하십시오.
* **일관된 이름 지정 사용**: 구현 전반에 일관된 이벤트 이름 지정을 적용합니다.

### 속도 제한

[!DNL Nextdoor] 전환 API는 속도 제한을 받습니다. 현재 속도 제한은 광고주당 **100개 요청/분**&#x200B;입니다. 속도 제한을 초과하면 API에서 `HTTP 429 Too Many Requests` 오류 코드를 반환합니다.

## 결론 {#conclusion}

[!DNL Nextdoor] 전환 API 확장은 전환을 추적하고 [!DNL Nextdoor] 광고 캠페인의 효과를 측정하는 강력한 방법을 제공합니다. 이 안내서를 따르고 모범 사례를 구현하면 정확한 전환 추적을 보장하고 광고 성능을 최적화할 수 있습니다.

최신 정보 및 추가 리소스를 보려면 [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com)을(를) 방문하세요.

## 다음 단계 {#next-steps}

이 안내서에서는 [!DNL Nextdoor] 전환 API 확장을 사용하여 서버측 이벤트 데이터를 [!DNL Nextdoor]에 보내는 방법을 보여 줍니다. [!DNL Adobe Experience Platform]의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
