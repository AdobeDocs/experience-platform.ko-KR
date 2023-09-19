---
keywords: 이벤트 전달 확장;pinterest;pinterest 이벤트 전달 확장
title: Pinterest 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장을 사용하면 비즈니스 요구 사항에 맞게 이벤트를 Pinterest에 수집할 수 있습니다.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 4%

---

# [!DNL Pinterest] 이벤트 전달 확장 기능

[!DNL Pinterest] 은 레시피, 홈 데코, 스타일 영감 등과 같은 아이디어를 찾는 시각적 검색 엔진입니다. 에 수십억 개의 핀이 있습니다. [!DNL Pinterest], 다른 사용자와 공유할 수도 있습니다. [!DNL Pinterest]. 사용자 상호 작용 이벤트를 대조하고 를 활용할 수 있습니다 [!DNL Pinterest Analytics] 사용자 행동을 이해하고 타깃팅된 광고를 실행합니다.

다음 [[!DNL Pinterest] 전환](https://developers.pinterest.com/docs/conversions/conversion-management/) API [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장을 사용하면 Adobe Experience Platform Edge Network에 캡처된 데이터를 활용하여 로 전송할 수 있습니다. [!DNL Pinterest]. 이 문서에서는 확장의 사용 사례, 설치 방법 및 해당 기능을 이벤트 전달에 통합하는 방법에 대해 설명합니다 [규칙](../../../ui/managing-resources/rules.md).

전환 액세스 토큰은에서 사용하는 인증 방법입니다. [!DNL Pinterest] 와 상호 작용할 때 [!DNL Pinterest] API.

## 사용 사례

에서 Edge Network의 데이터를 사용하려면 이 확장 기능을 사용해야 합니다 [!DNL Pinterest] customer analytics 기능을 활용하십시오.

예를 들어 조직의 마케팅 팀을 생각해 보십시오. 팀은 웹 사이트에서 사용자 상호 작용 이벤트 데이터를 캡처하여 로 로드합니다 [!DNL Pinterest] 이 이벤트 전달 확장 사용.

그런 다음 마케팅 및 분석 팀은 [!DNL Pinterest] 주요 사용자 상호 작용 및 동작을 이해하는 Analytics 기능을 통해 사용자를 더 잘 이해하고 타깃팅된 광고 캠페인을 타깃팅할 수 있습니다.

에만 해당되는 사용 사례에 대한 자세한 내용은 [!DNL Pinterest]을(를) 참조하십시오. [[!DNL Pinterest] 사용 사례](https://business.pinterest.com/en/success-stories) 설명서를 참조하십시오.

## [!DNL Pinterest] 전제 조건 {#prerequisites}

유효한 권한이 있어야 합니다. [!DNL Pinterest] [비즈니스 계정](https://help.pinterest.com/en/business/article/get-a-business-account) 이 확장을 사용하려면 로 이동 [[!DNL Pinterest] 등록 페이지](https://www.pinterest.com/business/create/) 아직 계정이 없는 경우 등록하고 계정을 만듭니다.

다음 항목도 필요합니다. [!DNL Pinterest] 개발자 계정( 와 연결되어야 함) [!DNL Pinterest] 비즈니스 계정입니다. 개발자 계정을 비즈니스 계정과 연결하려면 [[!DNL Pinterest ] 개발자 계정](https://developers.pinterest.com/account-setup/).

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Pinterest]를 사용하려면 다음 입력이 필요합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 광고 계정 ID | 사용자 [!DNL Pinterest] 광고 계정 ID. 다음을 참조하십시오. [[!DNL Pinterest] 설명서](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) 지침을 참조하십시오. | 123456789012 |
| 전환 액세스 토큰 | 사용자 [!DNL Pinterest] 전환 액세스 토큰. 다음을 참조하십시오. [[!DNL Pinterest] 전환 API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) 설명서를 참조하십시오. <br> **이 토큰이 만료되지 않으므로 이 작업을 한 번만 수행하면 됩니다.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## 설치 및 구성 [!DNL Pinterest] 확장 {#install}

확장을 설치하려면 [이벤트 전달 속성 만들기](../../../ui/event-forwarding/overview.md#properties) 또는 편집할 기존 속성을 대신 선택하십시오.

왼쪽 탐색에서 을 선택합니다. **[!UICONTROL 확장]**. 선택 **[!UICONTROL 설치]** 카드 사용 [!DNL Pinterest] 의 확장 **[!UICONTROL 카탈로그]** 탭.

![다음을 표시하는 카탈로그 [!DNL Pinterest] 확장 프로그램 [!UICONTROL 설치] 강조 표시됨.](../../../images/extensions/server/pinterest/install.png)

### [!DNL Pinterest] 확장 구성

>[!IMPORTANT]
>
>구현 요구 사항에 따라 확장을 구성하기 전에 스키마, 데이터 요소 및 데이터 세트를 만들어야 할 수 있습니다. 사용 사례에 대해 설정해야 하는 엔터티를 결정하려면 시작하기 전에 모든 구성 단계를 검토하십시오.

왼쪽 탐색에서 을 선택합니다. **[!UICONTROL 확장]**. 선택 **[!UICONTROL 구성]** 카드 사용 [!DNL Pinterest] 의 확장 [!UICONTROL 설치됨]**을 클릭합니다.

![[!DNL Pinterest] 에 표시된 확장 [!UICONTROL 설치] 탭 [!UICONTROL 구성] 강조 표시됨.](../../../images/extensions/server/pinterest/configure.png)

다음 화면에서 [!UICONTROL 광고 계정 ID] 및 [!UICONTROL 전환 액세스 토큰] 이전에 수집한 [구성 세부 정보](#configuration-details) 섹션. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![다음 [!DNL Pinterest] [!UICONTROL 구성] 을 강조 표시하는 화면 [!UICONTROL 광고 계정 ID] 및 [!UICONTROL 전환 액세스 토큰] 입력 필드.](../../../images/extensions/server/pinterest/input.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙 만들기를 시작할 수 있습니다 [!DNL Pinterest].

새로 만들기 [규칙](../../../ui/managing-resources/rules.md) 이벤트 전달 속성에서 다음을 수행합니다. 아래 **[!UICONTROL 작업]**, 새 작업을 추가하고 확장을 로 설정합니다. **[!UICONTROL Pinterest]**. Edge Network 이벤트를 로 보내려면 [!DNL Pinterest], 를 설정합니다. **[!UICONTROL 작업 유형]** 끝 **[!UICONTROL 이벤트 보내기].**

![다음 [!DNL Pinterest] [!UICONTROL 이벤트 보내기] 규칙 만들기.](../../../images/extensions/server/pinterest/rule.png)

선택 후 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다. 다음을 매핑해야 합니다. [!DNL Pinterest] 이전에 만든 데이터 요소에 대한 이벤트 속성입니다.

### [!UICONTROL 이벤트 데이터]

새 규칙을 만들려면 다음 이벤트 데이터가 필요합니다.

| 필드 이름 | 설명 | 예 |
| --- | --- | --- | 
| [!UICONTROL 이벤트 이름] | 사용자 이벤트의 유형입니다. 그러나 활용하려면 모든 이벤트 유형이 가능합니다. [!DNL Pinterest Analytics] 다음을 사용하는 것이 좋습니다. [[!DNL Pinterest] 이벤트 코드](https://help.pinterest.com/en/business/article/add-event-codes) | * 체크아웃 <br> * add_to_cart <br> * page_visit <br> * 등록 <br> * [사용자 정의 이벤트] |
| [!UICONTROL 작업 소스] | 전환 이벤트가 발생한 위치를 나타내는 소스. | * app_android <br> * app_ios <br> * 웹 <br> * 오프라인 |
| [!UICONTROL 이벤트 시간] | 이벤트 시간을 나타냅니다. 사용되는 기본 시간 형식은 UNIX이며 형식으로 사용됩니다 `<seconds>.<miliseconds>` 현지 시간대에 따라 다릅니다. 자세한 내용은 [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500은 epoch 후 또는 2015년 6월 1일 월요일 7시 1433188255초 및 500밀리초를 나타냅니다:50:55 오후 GMT. |
| [!UICONTROL 이벤트 ID] | 이 이벤트를 식별하고 전환 API 및 Pinterest 추적을 통해 수집된 이벤트 간에 중복 제거하는 데 사용할 수 있는 고유한 ID 문자열입니다. 이 기능이 없으면 이벤트 데이터가 두 번 계산되고 지표 인플레이션을 보고할 가능성이 높습니다. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL 이벤트 속성] | 이벤트의 사용자 지정 속성이 포함된 JSON 개체입니다. 원시 JSON을 제공하거나 간소화된 키-값 입력 세트를 사용하여 선택하십시오. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![다음 [!DNL Pinterest] [!UICONTROL 이벤트 데이터] 에서는 규칙 작업에 강조 표시되어 있습니다.](../../../images/extensions/server/pinterest/event-data.png)

다음 이벤트 속성을 구성할 수 있습니다.

| 필드 이름 | 설명 |
| --- | --- |
| 이벤트 소스 URL | 웹 전환 이벤트의 URL. |
| 애플리케이션 저장소 ID | 앱스토어 앱 ID입니다. |
| 애플리케이션 이름 | 애플리케이션 이름. |
| Application Version | 애플리케이션의 버전입니다. |
| 장치 브랜드 | 사용자가 사용 중인 장치의 브랜드입니다. |
| 장치 캐리어 | 해당 디바이스에 대한 사용자의 이동통신사입니다. |
| 장치 모델 | 사용자 디바이스의 모델입니다. |
| 장치 유형 | 사용자가 사용 중인 장치의 유형입니다. |
| OS 버전 | 장치의 운영 체제 버전입니다. |
| 사용자 언어 | 사용자의 언어를 나타내는 두 문자 ISO-639-1 언어 코드. |

### [!UICONTROL 사용자 데이터]

에서 입력할 수 있는 다음 사용자 데이터는 필수 필드가 아닙니다.

| 필드 이름 | 설명 | 예 |
| --- | --- | --- | 
| [!UICONTROL 이메일] | 사용자 이메일 주소 또는 사용자 주소 이메일의 SHA256 해시입니다. | ebd543592...f2b7e1 |
| [!UICONTROL 모바일 광고 ID] | 사용자의 &quot;Google Advertising ID&quot;(GAID) 또는 &quot;Apple 광고주의 식별자&quot;(IDFA)의 Sha256 해시 | ebd543592...f2b7e1 |
| [!UICONTROL 클라이언트 IP 주소] | IPv4 또는 IPv6 형식일 수 있는 사용자의 IP 주소입니다. 일치에 사용됩니다. | 192.168.0.1 |
| [!UICONTROL 클라이언트 사용자 에이전트] | 사용자 웹 브라우저의 사용자 에이전트 문자열입니다. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL 고객 정보 데이터] | 다른 고객 정보가 포함된 JSON 개체입니다. 원시 JSON을 제공하거나 간소화된 키-값 입력 세트를 사용하여 선택하십시오. | { &quot;ph&quot;: &quot;122333445&quot; } |

![다음 [!DNL Pinterest] [!UICONTROL 사용자 데이터] 에서는 규칙 작업에 강조 표시되어 있습니다.](../../../images/extensions/server/pinterest/user-data.png)

구성할 수 있는 고객 정보 속성은 다음과 같습니다.

| 필드 이름 | 설명 |
| --- | --- |
| 전화 | 사용자 연락처 번호. 숫자만 허용되며 국가 코드, 지역 코드 및 번호로 입력해야 합니다. |
| 성별 | 성별은 여성의 경우 &quot;f&quot;, 남성의 경우 &quot;m&quot; 또는 이진이 아닌 경우 &quot;n&quot;으로 입력할 수 있습니다. |
| 생일 | 연도, 월, 일로 입력된 생년월일. |
| 성 | 사용자의 성. |
| 이름 | 사용자의 이름. |
| 구/군/시 | 사용자의 상주 도시입니다. 이는 주로 청구 목적으로 사용됩니다. |
| 주/도 | 소문자로 된 두 자리 코드로 제공되는 사용자 상태. |
| 우편번호 | 주로 청구 용도로 사용되는 사용자의 우편 번호입니다. |
| 국가 | 사용자의 국가를 나타내는 두 문자 ISO-3166 국가 코드. |
| 외부 ID | 스페이스에서 사용자를 식별하는 광고주의 고유 ID. 예: 사용자 ID, 충성도 ID 등. |
| 클릭 ID | 도메인의 _epik 쿠키 또는 URL의 &amp;epik= 쿼리 매개 변수에 저장된 고유 식별자입니다. |

>[!IMPORTANT]
>
>데이터를 로 보내기 전 [!DNL Pinterest] API 엔드포인트이며, 확장은 해시하고 이메일, 전화번호, 이름, 성, 성별, 생년월일, 도시, 주, 우편번호, 국가 및 외부 ID 필드의 값을 정규화합니다. SHA256 문자열이 이미 있는 경우 확장 프로그램은 이러한 필드의 값을 해시하지 않습니다.

### [!UICONTROL 사용자 정의 데이터]

규칙에 대해 다음 사용자 지정 데이터를 입력할 수 있습니다.

| 필드 이름 | 설명 |
| --- | --- |
| 통화 | ISO-4217 통화 코드. 제공되지 않으면, [!DNL Pinterest] 은 계정 생성 중에 설정된 광고주의 통화로 기본 설정됩니다. |
| 값 | 총 이벤트 값. 요청에서 문자열로 수락됩니다. 두 자릿수로 구문 분석됩니다. |
| 검색 문자열 | 사용자 전환 이벤트와 관련된 검색 문자열입니다. |
| 주문 ID | 주문 ID. 전송 중 `order_id` 도움이 됨 [!DNL Pinterest] 필요한 경우 이벤트 중복 제거 |
| 제품 수 | 이벤트의 총 제품 수입니다. 예를 들어 체크아웃 이벤트에서 구매한 총 항목 수입니다. |
| 컨텐츠 ID | 제품 ID 목록(배열). |
| 내용 | 가격 및 수량 등 제품에 대한 정보가 포함된 객체의 목록(배열)입니다. |

![다음 [!DNL Pinterest] [!UICONTROL 사용자 정의 데이터] 에서는 규칙 작업에 강조 표시되어 있습니다.](../../../images/extensions/server/pinterest/custom-data.png)

## 내에서 데이터 유효성 검사 [!DNL Pinterest]

이벤트 전달 규칙이 생성되고 실행되면 로 전송된 이벤트인지 확인합니다. [!DNL Pinterest] API는 의 예상대로 표시됩니다. [!DNL Pinterest] UI.

이벤트 컬렉션 및 [!DNL Experience Platform] 통합에 성공했습니다. 다음 내에서 이벤트가 표시됩니다. [!DNL Pinterest] UI.

![다음 [!DNL Pinterest] 이벤트 관리자](../../../images/extensions/server/pinterest/event-history.png)

드릴스루하여 다음을 볼 수 있습니다. [!DNL Pinterest] 이벤트 데이터 배포.

![다음 [!DNL Pinterest] 데이터 배포](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 다음 단계

이 안내서에서는 설치 및 구성 방법을 다룹니다. [!DNL Pinterest] ui의 이벤트 전달 확장. 자세한 내용은 공식 설명서를 참조하십시오.

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 전환 API 개요](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
