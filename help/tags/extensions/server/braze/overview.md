---
keywords: 이벤트 전달 확장;브레이즈;브레이즈 이벤트 전달 확장
title: 브레이즈 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장은 브레이즈로 Edge Network 이벤트를 보냅니다.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---

# [!DNL Braze Track Events API] 이벤트 전달 확장 기능

[[!DNL Braze]](https://www.braze.com)은(는) 소비자와 브랜드 간의 고객 중심 상호 작용을 실시간으로 향상시키는 고객 참여 플랫폼입니다. [!DNL Braze]을(를) 사용하여 다음을 수행할 수 있습니다.

- 언어 선호도, 위치 선호도 등을 기반으로 타겟팅된 사용자에게 데이터(예: 마케팅 메시지)를 전달하여 전환율을 높이고 주요 비즈니스 목표를 지원합니다.
- 이메일, 푸시 알림, 인앱 메시지 등 다양한 채널에서 적시에 원하는 언어로 고객에게 개인화된 메시지를 보낼 수 있습니다.
- 마케팅 및 홍보 캠페인에 특정 사용자를 타깃팅하여 반복 고객 수를 늘립니다.
- 사용자 행동 및 패턴을 연구하여 사용자 지정된 메시지로 특정 대상을 타깃팅하면 매출이 늘어날 수 있습니다.

[!DNL Braze Track Events API] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하고 [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API를 사용하여 서버측 이벤트 형식으로 [!DNL Braze]에 보낼 수 있습니다.

이 문서에서는 확장의 사용 사례, 이벤트 전달 라이브러리에 설치하는 방법, 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)에서 해당 기능을 사용하는 방법에 대해 설명합니다.

## 사용 사례

[!DNL Braze]에 있는 Edge Network의 데이터를 사용하여 고객 분석 및 타깃팅 기능을 이용하려면 이 확장을 사용해야 합니다.

예를 들어, 다중 채널 상태(웹 사이트 및 모바일)를 가지고 있고 트랜잭션 또는 대화형 입력을 웹 사이트 및 모바일 플랫폼의 이벤트 데이터로 캡처하고 있는 소매 조직을 생각해 보십시오. 다양한 [tag](../../../home.md) 규칙을 사용하여 이 데이터는 실시간으로 Edge Network으로 전송됩니다. 여기에서 [!DNL Braze] 이벤트 전달 확장은 서버측에서 관련 이벤트를 [!DNL Braze]에 자동으로 전송합니다.

데이터가 전송되면 조직의 분석 팀은 [!DNL Braze's] 기능을 활용하여 데이터 세트를 처리하고 비즈니스 인사이트를 도출하여 그래프, 대시보드 또는 비즈니스 이해 당사자에게 알릴 수 있습니다. 플랫폼의 다양한 사용 사례에 대한 자세한 내용은 [[!DNL Braze] 고객](https://www.braze.com/customers) 페이지를 참조하십시오.

## [!DNL Braze]개의 필수 구성 요소 및 보호 기능 {#prerequisites}

해당 기술을 사용하려면 [!DNL Braze] 계정이 있어야 합니다. 계정이 없는 경우 [!DNL Braze]의 [시작 페이지](https://www.braze.com/get-started/)(으)로 이동하여 [!DNL Braze Sales]에 연결하고 계정 만들기 프로세스를 시작하십시오.

### API 보호 기능

확장은 [!DNL Braze]의 API 중 2개를 사용하며 그 한도는 아래에 요약되어 있습니다.

| API | 비율 제한 |
| --- | --- |
| [!DNL User Track] | 분당 50,000개의 요청. <br>자세한 내용은 [[!DNL User Track] API 설명서](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit)를 참조하세요. |
| [!DNL User Identify] | 분당 요청 20,000개. <br>자세한 내용은 [[!DNL User Identify] API 설명서](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit)를 참조하세요. |

>[!NOTE]
>
> API 제한에 대한 자세한 내용은 [[!DNL Braze] API 제한](https://www.braze.com/docs/api/api_limits/)에 대한 안내서를 참조하십시오.

### 청구 가능 데이터 포인트

추가 사용자 지정 특성을 [!DNL Braze]에 보내면 [!DNL Braze] 데이터 지점 사용량이 늘어날 수 있습니다. 추가 사용자 지정 특성을 보내기 전에 [!DNL Braze] 계정 관리자에게 문의하십시오. 자세한 내용은 [청구 가능한 데이터 포인트](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable)에 대한 [!DNL Braze] 설명서를 참조하십시오.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Edge Network을 [!DNL Braze]에 연결하려면 다음 입력이 필요합니다.

| 키 유형 | 설명 | 예 |
| --- | --- | --- |
| [!DNL Braze] 인스턴스 | [!DNL Braze] 계정과 연결된 REST 끝점입니다. 지침은 [인스턴스](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)의 [!DNL Braze] 설명서를 참조하세요. | `https://rest.iad-03.braze.com` |
| API 키 | [!DNL Braze] 계정과 연결된 [!DNL Braze] API 키. <br/>자세한 내용은 [REST API 키](https://www.braze.com/docs/api/basics/#rest-api-key)의 [!DNL Braze] 설명서를 참조하세요. | `YOUR-BRAZE-REST-API-KEY` |

### 보안 생성

새 [이벤트 전달 암호](../../../ui/event-forwarding/secrets.md)를 만들고 값을 [[!DNL Braze] API 키](#configuration-details)(으)로 설정합니다. 값을 안전하게 유지하면서 계정에 대한 연결을 인증하는 데 사용됩니다.

## [!DNL Braze] 확장 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 대신 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 [!DNL Braze] 확장의 카드에서 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![확장 [!DNL Braze]을(를) 설치합니다.](../../../images/extensions/server/braze/install-extension.png)

다음 화면에서는 이전에 [!DNL Braze]에서 수집한 다음 [구성 값](#configuration-details)을 입력합니다.

- **[!UICONTROL Breze Rest 끝점 URL]**: 제공된 입력에 [!DNL Braze] rest 끝점 URL의 값을 일반 텍스트로 입력할 수 있습니다.
- **[!UICONTROL API 키]**: [!DNL Braze] API 키가 포함된 이전에 만든 [비밀 데이터 요소](#create-a-secret)를 선택합니다.

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![확장 구성 페이지 [!DNL Braze]입니다.](../../../images/extensions/server/braze/configure-extension.png)

## [!DNL Send Event] 규칙 만들기 {#tracking-rule}

확장을 설치한 후 새 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)을(를) 만들고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 구성할 때 **[!UICONTROL 중단]** 확장을 선택한 다음 작업 유형으로 **[!UICONTROL 이벤트 보내기]**&#x200B;를 선택하십시오.

![이벤트 전달 규칙 작업 구성을 추가합니다.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 사용자 식별]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 외부 사용자 ID] | 길고 무작위적이며 잘 분산된 UUID 또는 GUID입니다. 사용자 ID의 이름을 지정하는 다른 방법을 선택하는 경우 길이도 길고 무작위적이며 잘 배포되어야 합니다. [제안 사용자 ID 명명 규칙](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)에 대해 자세히 알아보세요. |
| [!UICONTROL 사용자 ID 동기화] | 사용자 식별자를 브레이즈합니다. |
| [!UICONTROL 사용자 별칭] | 별칭은 대체 고유 사용자 식별자 역할을 합니다. 별칭을 사용하여 코어 사용자 ID가 아닌 다른 차원의 사용자를 식별합니다. <br><br> 사용자 별칭 개체는 식별자 자체에 대한 alias_name과 별칭 유형을 나타내는 alias_label의 두 부분으로 구성됩니다. 사용자는 레이블이 다른 여러 별칭을 가질 수 있지만, alias_label당 하나의 alias_name만 가질 수 있습니다. |

{style="table-layout:auto"}

>[!NOTE]
>
> 이벤트를 사용자에게 연결하려면 [!UICONTROL 외부 사용자 ID] 필드 또는 [!UICONTROL 사용자 식별자 동기화] 필드 또는 [!UICONTROL 사용자 별칭] 섹션을 입력해야 합니다.

**[!UICONTROL 이벤트 데이터]**

| 입력 | 설명 | 필수 여부 |
| --- | --- | --- |
| [!UICONTROL 이벤트 &#x200B; 이름] | 이벤트 이름. | 예 |
| [!UICONTROL 이벤트 시간] | ISO 8601 또는 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 형식의 문자열로 표시된 날짜-시간입니다. | 예 |
| [!UICONTROL 앱 식별자] | 앱 식별자 또는 <strong>app_id</strong>은(는) 활동을 앱 그룹의 특정 앱과 연결하는 매개 변수입니다. 상호 작용 중인 앱 그룹 내의 앱을 지정합니다. [API 식별자 유형](https://www.braze.com/docs/api/identifier_types/)에 대해 자세히 알아보세요. | |
| [!UICONTROL 이벤트 &#x200B; 속성] | 이벤트의 사용자 지정 속성이 포함된 JSON 개체입니다. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> **[!UICONTROL 이벤트 보내기 브레이크]** 작업을 수행하려면 **[!UICONTROL 이벤트 이름]** 및 **[!UICONTROL 이벤트 시간]**&#x200B;만 지정해야 하지만 사용자 지정 속성 필드에 가능한 많은 정보를 포함해야 합니다. [!DNL Braze] 이벤트 개체에 대한 자세한 내용은 [공식 설명서](https://www.braze.com/docs/api/objects_filters/event_object/)를 참조하세요.

**[!UICONTROL 사용자 특성]**

사용자 속성은 지정된 사용자 프로필에서 제공된 이름 및 값으로 속성을 만들거나 업데이트하는 필드가 포함된 JSON 개체일 수 있습니다. 지원되는 속성은 다음과 같습니다.

| 사용자 속성 | 설명 |
| --- | --- |
| [!UICONTROL 이름] | |
| [!UICONTROL 성] | |
| [!UICONTROL 전화] | |
| [!UICONTROL 이메일] | |
| [!UICONTROL 성별] | 다음 문자열 중 하나: &quot;M&quot;, &quot;F&quot;, &quot;O&quot;(기타), &quot;N&quot;(적용할 수 없음), &quot;P&quot;(말하지 않음). |
| [!UICONTROL 구/군/시] | |
| [!UICONTROL 국가] | [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 형식의 문자열로서 국가입니다. |
| [!UICONTROL 언어] | [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 형식의 문자열 언어입니다. |
| [!UICONTROL 생년월일] | &quot;YYYY-MM-DD&quot; 형식의 문자열(예: 1980-12-21). |
| [!UICONTROL 표준 시간대] | [IANA 시간대 데이터베이스](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)의 시간대 이름(예: &#39;America/New_York&#39; 또는 &#39;Eastern Time(미국 및 캐나다)&#39;). |
| [!UICONTROL Facebook] | ID(문자열), 좋아요(문자열 배열), num_friends(정수) 중 하나를 포함하는 해시. |
| [!UICONTROL Twitter] | ID(정수), screen_name(문자열, Twitter 핸들), followers_count(정수), friends_count(정수), states_count(정수) 중 하나를 포함하는 해시입니다. |

{style="table-layout:auto"}

## [!DNL Send Purchase Event] 규칙 만들기 {#purchase-rule}

확장을 설치한 후 새 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)을(를) 만들고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 구성할 때 **[!UICONTROL 중단]** 확장을 선택한 다음 작업 유형으로 **[!UICONTROL 구매 이벤트 보내기]**&#x200B;를 선택하십시오.

![고정 구매 작업 유형 이벤트 전달 규칙 작업 구성을 추가합니다.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 사용자 식별]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 외부 사용자 ID] | 길고 무작위적이며 잘 분산된 UUID 또는 GUID입니다. 사용자 ID의 이름을 지정하는 다른 방법을 선택하는 경우 길이도 길고 무작위적이며 잘 배포되어야 합니다. [제안 사용자 ID 명명 규칙](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)에 대해 자세히 알아보세요. |
| [!UICONTROL 사용자 ID 동기화] | 사용자 식별자를 브레이즈합니다. |
| [!UICONTROL 사용자 별칭] | 별칭은 대체 고유 사용자 식별자 역할을 합니다. 별칭을 사용하여 코어 사용자 ID가 아닌 다른 차원의 사용자를 식별합니다. <br><br> 사용자 별칭 개체는 식별자 자체에 대한 alias_name과 별칭 유형을 나타내는 alias_label의 두 부분으로 구성됩니다. 사용자는 레이블이 다른 여러 별칭을 가질 수 있지만, alias_label당 하나의 alias_name만 가질 수 있습니다. |

{style="table-layout:auto"}

>[!NOTE]
>
> 이벤트를 사용자에게 연결하려면 [!UICONTROL 외부 사용자 ID] 필드, [!UICONTROL 사용자 식별자 동기화] 필드 또는 [!UICONTROL 사용자 별칭] 섹션을 완료해야 합니다.

**[!UICONTROL 구매 데이터]**

| 입력 | 설명 | 필수 여부 |
| --- | --- | --- |
| [!UICONTROL 제품 ID{&#x200B;1}] | 구매용 식별자. (예: 제품 이름 또는 제품 범주) | 예 |
| [!UICONTROL 구매 시간] | ISO 8601 또는 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 형식의 문자열로 표시된 날짜-시간입니다. | 예 |
| [!UICONTROL &#x200B;통화] | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 알파벳 통화 코드 형식의 문자열로 통화. | 예 |
| [!UICONTROL 가격{&#x200B;1}] | 가격. | 예 |
| [!UICONTROL &#x200B;수량] | 제공하지 않은 경우 기본값은 1입니다. 최대값은 100보다 작아야 합니다. | |
| [!UICONTROL 앱 식별자] | 앱 식별자 또는 <strong>app_id</strong>은(는) 활동을 앱 그룹의 특정 앱과 연결하는 매개 변수입니다. 상호 작용 중인 앱 그룹 내의 앱을 지정합니다. [API 식별자 유형](https://www.braze.com/docs/api/identifier_types/)에 대해 자세히 알아보세요. | |
| [!UICONTROL 구매 &#x200B; 속성] | 구매의 사용자 지정 속성을 포함하는 JSON 개체입니다. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> **[!UICONTROL 이벤트 보내기 브레이크]** 작업을 수행하려면 **[!UICONTROL 이벤트 이름]** 및 **[!UICONTROL 이벤트 시간]**&#x200B;만 지정해야 하지만 사용자 지정 속성 필드에 가능한 많은 정보를 포함해야 합니다. [!DNL Braze] 이벤트 개체에 대한 자세한 내용은 [공식 설명서](https://www.braze.com/docs/api/objects_filters/event_object/)를 참조하세요.

**[!UICONTROL 사용자 특성]**

사용자 속성은 지정된 사용자 프로필에서 제공된 이름 및 값으로 속성을 만들거나 업데이트하는 필드가 포함된 JSON 개체일 수 있습니다. 지원되는 속성은 다음과 같습니다.

| 사용자 속성 | 설명 |
| --- | --- |
| [!UICONTROL 이름] | |
| [!UICONTROL 성] | |
| [!UICONTROL 전화] | |
| [!UICONTROL 이메일] | |
| [!UICONTROL 성별] | 다음 문자열 중 하나: &quot;M&quot;, &quot;F&quot;, &quot;O&quot;(기타), &quot;N&quot;(적용할 수 없음), &quot;P&quot;(말하지 않음). |
| [!UICONTROL 구/군/시] | |
| [!UICONTROL 국가] | [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 형식의 문자열로서 국가입니다. |
| [!UICONTROL 언어] | [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 형식의 문자열 언어입니다. |
| [!UICONTROL 생년월일] | &quot;YYYY-MM-DD&quot; 형식의 문자열(예: 1980-12-21). |
| [!UICONTROL 표준 시간대] | [IANA 시간대 데이터베이스](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)의 시간대 이름(예: &#39;America/New_York&#39; 또는 &#39;Eastern Time(미국 및 캐나다)&#39;). |
| [!UICONTROL Facebook] | ID(문자열), 좋아요(문자열 배열), num_friends(정수) 중 하나를 포함하는 해시. |
| [!UICONTROL Twitter] | ID(정수), screen_name(문자열, Twitter 핸들), followers_count(정수), friends_count(정수), states_count(정수) 중 하나를 포함하는 해시입니다. |

{style="table-layout:auto"}

## [!DNL Braze] 내의 데이터 유효성 검사 {#validate}

이벤트 컬렉션 및 [!DNL Adobe Experience Platform] 통합이 성공하면 [사용자 프로필을 보는 중](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/)에 [!DNL Braze] 콘솔 내에서 이벤트가 표시됩니다. 특히 [!DNL Braze]에 전송된 새 이벤트 데이터는 특정 사용자의 [개요 탭](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab)의 [!DNL Purchases] 섹션에 반영됩니다.

## 다음 단계

이 안내서에서는 이벤트 전달을 사용하여 전환 이벤트를 [!DNL Braze]에 보내는 방법에 대해 설명합니다. [!DNL Braze](으)로 전송된 이벤트 데이터의 다운스트림 응용 프로그램에 대한 자세한 내용은 [공식 설명서](https://www.braze.com/docs)를 참조하세요.

Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
