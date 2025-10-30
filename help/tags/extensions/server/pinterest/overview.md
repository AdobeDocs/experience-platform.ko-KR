---
keywords: 이벤트 전달 확장;pinterest;pinterest 이벤트 전달 확장
title: Pinterest 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장을 사용하면 비즈니스 요구 사항에 맞게 이벤트를 Pinterest에 수집할 수 있습니다.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 3%

---

# [!DNL Pinterest] 이벤트 전달 확장 기능

[!DNL Pinterest]은(는) 레시피, 홈 장식, 스타일 영감 등의 아이디어를 찾는 시각적 검색 엔진입니다. [!DNL Pinterest]에 수십억 개의 고정 항목이 있으며, [!DNL Pinterest]에 다른 사용자와 공유할 수도 있습니다. 사용자 상호 작용 이벤트를 대조하고 [!DNL Pinterest Analytics]을(를) 활용하여 사용자 행동을 이해하고 타깃팅된 광고를 실행할 수 있습니다.

[[!DNL Pinterest] 전환](https://developers.pinterest.com/docs/conversions/conversion-management/) API [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하여 [!DNL Pinterest]에 보낼 수 있습니다. 이 문서에서는 확장의 사용 사례, 설치 방법 및 해당 기능을 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)에 통합하는 방법에 대해 설명합니다.

전환 액세스 토큰은 [!DNL Pinterest] API와 상호 작용할 때 [!DNL Pinterest]에서 사용하는 인증 방법입니다.

## 사용 사례

[!DNL Pinterest]의 Edge Network 데이터를 사용하여 Customer Analytics 기능을 이용하려면 이 확장을 사용해야 합니다.

예를 들어 조직의 마케팅 팀을 생각해 보십시오. 팀은 웹 사이트에서 사용자 인터랙션 이벤트 데이터를 캡처하고 이 이벤트 전달 확장을 사용하여 [!DNL Pinterest]에 로드합니다.

그런 다음 마케팅 및 분석 팀은 [!DNL Pinterest] 분석 기능을 활용하여 주요 사용자 상호 작용 및 동작을 이해함으로써 사용자를 더 잘 이해하고 타깃팅된 광고 캠페인을 타깃팅할 수 있습니다.

[!DNL Pinterest]과(와) 관련된 사용 사례에 대한 자세한 내용은 [[!DNL Pinterest] 사용 사례](https://business.pinterest.com/en/success-stories) 설명서를 참조하세요.

## [!DNL Pinterest]개 필수 구성 요소 {#prerequisites}

이 확장을 사용하려면 올바른 [!DNL Pinterest] [비즈니스 계정](https://help.pinterest.com/en/business/article/get-a-business-account)이 있어야 합니다. 아직 계정이 없는 경우 [[!DNL Pinterest] 등록 페이지](https://www.pinterest.com/business/create/)&#x200B;(으)로 이동하여 등록하고 계정을 만드십시오.

[!DNL Pinterest] 비즈니스 계정과 연결되어야 하는 [!DNL Pinterest] 개발자 계정도 필요합니다. 개발자 계정을 비즈니스 계정에 연결하려면 [[!DNL Pinterest ] 개발자 계정](https://developers.pinterest.com/account-setup/)을 참조하세요.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Pinterest]에 연결하려면 다음 입력이 필요합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 광고 계정 ID | [!DNL Pinterest] 광고 계정 ID입니다. 자세한 내용은 [[!DNL Pinterest] 설명서](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)를 참조하세요. | 123456789012 |
| 전환 액세스 토큰 | [!DNL Pinterest] 전환 액세스 토큰입니다. 지침은 [[!DNL Pinterest] 전환 API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) 문서를 참조하십시오. <br> **토큰이 만료되지 않으므로 한 번만 수행하면 됩니다.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## [!DNL Pinterest] 확장 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 대신 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL Extensions]**&#x200B;을(를) 선택합니다. **[!UICONTROL Install]** 탭의 [!DNL Pinterest] 확장에 대한 카드에서 **[!UICONTROL Catalog]**&#x200B;을(를) 선택합니다.

![이(가) 강조 표시된 [!DNL Pinterest] 확장을 표시하는 [!UICONTROL Install]카탈로그.](../../../images/extensions/server/pinterest/install.png)

### [!DNL Pinterest] 확장 구성

>[!IMPORTANT]
>
>구현 요구 사항에 따라 확장을 구성하기 전에 스키마, 데이터 요소 및 데이터 세트를 만들어야 할 수 있습니다. 사용 사례에 대해 설정해야 하는 엔터티를 결정하려면 시작하기 전에 모든 구성 단계를 검토하십시오.

왼쪽 탐색에서 **[!UICONTROL Extensions]**&#x200B;을(를) 선택합니다. **[!UICONTROL Configure]** 탭에서 [!DNL Pinterest] 확장에 대한 카드에서 [!UICONTROL Installed]을**를) 선택합니다.

![[!DNL Pinterest]이(가) 강조 표시된 [!UICONTROL Install] 탭에 [!UICONTROL Configure] 확장이 표시됨.](../../../images/extensions/server/pinterest/configure.png)

다음 화면에서는 [!UICONTROL Ads Account Id]구성 세부 정보[!UICONTROL Conversion Access Token] 섹션에서 이전에 수집한 [ 및 ](#configuration-details)을(를) 입력합니다. 완료되면 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

![[!DNL Pinterest] 및 [!UICONTROL Configure] 입력 필드를 강조 표시하는 [!UICONTROL Ads Account Id] [!UICONTROL Conversion Access Token] 화면입니다.](../../../images/extensions/server/pinterest/input.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 [!DNL Pinterest]에 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙을 만들 수 있습니다.

이벤트 전달 속성에 새 [규칙](../../../ui/managing-resources/rules.md)을(를) 만듭니다. **[!UICONTROL Actions]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL Pinterest]**(으)로 설정합니다. Edge Network 이벤트를 [!DNL Pinterest]에 보내려면 **[!UICONTROL Action Type]**&#x200B;을(를) **[!UICONTROL Send Event].**(으)로 설정하십시오.

![[!DNL Pinterest] [!UICONTROL Send Event] 규칙 만들기.](../../../images/extensions/server/pinterest/rule.png)

선택 후 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다. [!DNL Pinterest] 이벤트 속성을 이전에 만든 데이터 요소에 매핑해야 합니다.

### [!UICONTROL Event Data]

새 규칙을 만들려면 다음 이벤트 데이터가 필요합니다.

| 필드 이름 | 설명 | 예 |
| --- | --- | --- | 
| [!UICONTROL Event Name] | 사용자 이벤트의 유형입니다. 모든 이벤트 유형일 수 있지만 [!DNL Pinterest Analytics]을(를) 활용하려면 [[!DNL Pinterest] 이벤트 코드](https://help.pinterest.com/en/business/article/add-event-codes)를 사용하는 것이 좋습니다. | &amp;ast; 체크아웃 <br> &amp;ast; add_to_cart <br> &amp;ast; page_visit <br> &amp;ast; 등록 <br> &amp;ast; [사용자 정의 이벤트] |
| [!UICONTROL Action Source] | 전환 이벤트가 발생한 위치를 나타내는 소스. | &amp;ast; app_android <br> &amp;ast; app_ios <br> &amp;ast; 웹 <br> &amp;ast; offline |
| [!UICONTROL Event Time] | 이벤트 시간을 나타냅니다. 사용되는 기본 시간 형식은 UNIX이며 로컬 시간대에 따라 `<seconds>.<miliseconds>` 형식입니다. 자세한 내용은 [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create)를 참조하세요. | 1433188255.500은 epoch 후 또는 2015년 6월 1일 월요일 오후 7:50:55분 GMT에서 1433188255초 및 500밀리초를 나타냅니다. |
| [!UICONTROL Event ID] | 이 이벤트를 식별하고 전환 API 및 Pinterest 추적을 통해 수집된 이벤트 간에 중복 제거하는 데 사용할 수 있는 고유한 ID 문자열입니다. 이 기능이 없으면 이벤트 데이터가 두 번 계산되고 지표 인플레이션을 보고할 가능성이 높습니다. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | 이벤트의 사용자 지정 속성이 포함된 JSON 개체입니다. 원시 JSON을 제공하거나 간소화된 키-값 입력 세트를 사용하여 선택하십시오. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![규칙 작업에 강조 표시된 [!DNL Pinterest] [!UICONTROL Event Data]입니다.](../../../images/extensions/server/pinterest/event-data.png)

다음 이벤트 속성을 구성할 수 있습니다.

| 필드 이름 | 설명 |
| --- | --- |
| 이벤트 Source URL | 웹 전환 이벤트의 URL. |
| 애플리케이션 저장소 ID | 앱스토어 앱 ID입니다. |
| 애플리케이션 이름 | 애플리케이션 이름. |
| Application Version | 애플리케이션의 버전입니다. |
| 장치 브랜드 | 사용자가 사용 중인 장치의 브랜드입니다. |
| 장치 캐리어 | 해당 디바이스에 대한 사용자의 이동통신사입니다. |
| 장치 모델 | 사용자 디바이스의 모델입니다. |
| 장치 유형 | 사용자가 사용 중인 장치의 유형입니다. |
| OS 버전 | 장치의 운영 체제 버전입니다. |
| 사용자 언어 | 사용자의 언어를 나타내는 두 문자 ISO-639-1 언어 코드. |

### [!UICONTROL User Data]

에서 입력할 수 있는 다음 사용자 데이터는 필수 필드가 아닙니다.

| 필드 이름 | 설명 | 예 |
| --- | --- | --- | 
| [!UICONTROL Email] | 사용자 이메일 주소 또는 사용자 주소 이메일의 SHA256 해시입니다. | ebd543592...f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | 사용자의 &quot;Google Advertising ID&quot;(GAID) 또는 &quot;Apple의 광고주용 식별자&quot;(IDFA)의 Sha256 해시 | ebd543592...f2b7e1 |
| [!UICONTROL Client IP Address] | IPv4 또는 IPv6 형식일 수 있는 사용자의 IP 주소입니다. 일치에 사용됩니다. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | 사용자 웹 브라우저의 사용자 에이전트 문자열입니다. | Mozilla/5.0 (플랫폼; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | 다른 고객 정보가 포함된 JSON 개체입니다. 원시 JSON을 제공하거나 간소화된 키-값 입력 세트를 사용하여 선택하십시오. | { &quot;ph&quot;: &quot;122333445&quot; } |

![규칙 작업에 강조 표시된 [!DNL Pinterest] [!UICONTROL User Data]입니다.](../../../images/extensions/server/pinterest/user-data.png)

구성할 수 있는 고객 정보 속성은 다음과 같습니다.

| 필드 이름 | 설명 |
| --- | --- |
| 휴대폰 | 사용자 연락처 번호. 숫자만 허용되며 국가 코드, 지역 코드 및 번호로 입력해야 합니다. |
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
>데이터를 [!DNL Pinterest] API 끝점으로 보내기 전에 확장에서 해시하고 전자 메일, 전화 번호, 이름, 성, 성별, 생년월일, 도시, 주, 우편 번호, 국가 및 외부 ID 필드의 값을 정규화합니다. SHA256 문자열이 이미 있는 경우 확장 프로그램은 이러한 필드의 값을 해시하지 않습니다.

### [!UICONTROL Custom Data]

규칙에 대해 다음 사용자 지정 데이터를 입력할 수 있습니다.

| 필드 이름 | 설명 |
| --- | --- |
| 통화 | ISO-4217 통화 코드. 이 값이 제공되지 않으면 [!DNL Pinterest]은(는) 계정 생성 중에 설정된 광고주의 통화로 기본 설정됩니다. |
| 값 | 총 이벤트 값. 요청에서 문자열로 수락됩니다. 두 자릿수로 구문 분석됩니다. |
| 검색 문자열 | 사용자 전환 이벤트와 관련된 검색 문자열입니다. |
| 주문 ID | 주문 ID. `order_id`을(를) 보내면 필요한 경우 [!DNL Pinterest]에서 이벤트 중복 제거에 도움이 됩니다. |
| 제품 수 | 이벤트의 총 제품 수입니다. 예를 들어 체크아웃 이벤트에서 구매한 총 항목 수입니다. |
| 컨텐츠 ID | 제품 ID 목록(배열). |
| 내용 | 가격 및 수량 등 제품에 대한 정보가 포함된 객체의 목록(배열)입니다. |

![규칙 작업에 강조 표시된 [!DNL Pinterest] [!UICONTROL Custom Data]입니다.](../../../images/extensions/server/pinterest/custom-data.png)

## [!DNL Pinterest] 내의 데이터 유효성 검사

이벤트 전달 규칙이 만들어지고 실행되면 [!DNL Pinterest] API로 전송된 이벤트가 [!DNL Pinterest] UI에 예상대로 표시되는지 확인합니다.

이벤트 컬렉션 및 [!DNL Experience Platform] 통합이 성공하면 [!DNL Pinterest] UI 내에 이벤트가 표시됩니다.

![[!DNL Pinterest] 이벤트 관리자](../../../images/extensions/server/pinterest/event-history.png)

추가로 드릴스루하여 [!DNL Pinterest] 이벤트 데이터 배포를 볼 수 있습니다.

![[!DNL Pinterest] 데이터 배포](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 다음 단계

이 안내서에서는 UI에서 [!DNL Pinterest] 이벤트 전달 확장을 설치하고 구성하는 방법을 다룹니다. 자세한 내용은 공식 설명서를 참조하십시오.

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 전환 API 개요](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
