---
title: Zendesk 이벤트 전달 확장
description: Adobe Experience Platform용 Zendesk 이벤트 전달 확장.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 4%

---

# [!DNL Zendesk] 이벤트 API 확장 개요

[Zendesk](https://www.zendesk.com)은(는) 고객 서비스 솔루션 및 판매 도구입니다. Zendesk [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장은 [[!DNL Zendesk Events API]](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)을(를) 활용하여 추가 처리를 위해 Adobe Experience Platform Edge Network에서 Zendesk로 이벤트를 전송합니다. 확장을 사용하여 다운스트림 분석 및 작업에 사용할 고객 프로필 상호 작용을 수집할 수 있습니다.

이 문서에서는 UI에서 확장을 설치하고 구성하는 방법을 다룹니다.

## 전제 조건

이 확장을 사용하려면 Zendesk 계정이 있어야 합니다. [Zendesk 웹 사이트](https://www.zendesk.com/register/)에서 Zendesk 계정을 등록할 수 있습니다.

또한 Zendesk 구성을 위해 다음 세부 정보를 수집해야 합니다.

| 키 유형 | 설명 | 예 |
| --- | --- | --- |
| 하위 도메인 | 등록 프로세스 중에 계정별로 고유한 **하위 도메인**&#x200B;이(가) 만들어집니다. 자세한 내용은 [Zendesk 설명서](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/)를 참조하세요. | `xxxxx.zendesk.com`(여기서 `xxxxx`은(는) 계정을 만드는 동안 제공된 값입니다.) |
| API 토큰 | Zendesk는 Zendesk API와 통신하는 인증 메커니즘으로 전달자 토큰을 사용합니다. Zendesk 포털에 로그인한 후 API 토큰을 생성합니다. 자세한 내용은 [Zendesk 설명서](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token)를 참조하세요. | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

마지막으로 API 토큰에 대한 이벤트 전달 암호를 만들어야 합니다. 암호 유형을 **[!UICONTROL Token]**(으)로 설정하고 값을 Zendesk 구성에서 수집한 API 토큰으로 설정합니다. 암호 구성에 대한 자세한 내용은 [이벤트 전달의 암호](../../../ui/event-forwarding/secrets.md)에 대한 설명서를 참조하십시오.

## 확장 설치 {#install}

UI에 Zendesk 확장을 설치하려면 **이벤트 전달**(으)로 이동하여 확장을 추가할 속성을 선택하거나 대신 새 속성을 만드십시오.

원하는 속성을 선택하거나 만든 후에는 **확장** > **카탈로그**(으)로 이동합니다. &quot;[!DNL Zendesk]&quot;을(를) 검색한 다음 Zendesk Extension에서 **[!DNL Install]**&#x200B;을(를) 선택합니다.

![UI에서 Zendesk 확장에 대한 설치 단추](../../../images/extensions/server/zendesk/install.png)

## 확장 구성 {#configure}

>[!IMPORTANT]
>
>구현 요구 사항에 따라 확장을 구성하기 전에 스키마, 데이터 요소 및 데이터 세트를 만들어야 할 수 있습니다. 사용 사례에 대해 설정해야 하는 엔터티를 결정하려면 시작하기 전에 모든 구성 단계를 검토하십시오.

왼쪽 탐색에서 **확장**&#x200B;을 선택합니다. **설치됨**&#x200B;에서 Zendesk 확장의 **구성**&#x200B;을(를) 선택합니다.

![UI에서 Zendesk 확장에 대한 구성 단추를 선택하고 있습니다](../../../images/extensions/server/zendesk/configure.png)

**[!UICONTROL Zendesk 도메인]**&#x200B;에서 Zendesk 하위 도메인의 값을 입력하십시오. **[!UICONTROL Zendesk 토큰]**&#x200B;에서 API 토큰이 포함된 이전에 만든 암호를 선택하십시오.

![UI에 구성 옵션이 입력됨](../../../images/extensions/server/zendesk/input.png)

## 이벤트 전달 규칙 구성

새 이벤트 전달 규칙 [규칙](../../../ui/managing-resources/rules.md)을(를) 만들고 원하는 대로 조건을 구성하십시오. 규칙에 대한 작업을 선택할 때 [!UICONTROL Zendesk] 확장을 선택한 다음 [!UICONTROL 이벤트 만들기] 작업 유형을 선택합니다.

![규칙 정의](../../../images/extensions/server/zendesk/rule.png)

작업 구성을 설정할 때 Zendesk로 보낼 다양한 속성에 데이터 요소를 할당하라는 메시지가 표시됩니다.

![작업 구성 정의](../../../images/extensions/server/zendesk/action-configurations.png)

이러한 데이터 요소는 아래에서 참조되는 대로 매핑해야 합니다.

### `event` 키

`event`은(는) 사용자가 트리거한 이벤트를 나타내는 JSON 개체입니다. `event` 개체에서 캡처한 속성에 대한 자세한 내용은 이벤트의 [구조](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/)에 있는 Zendesk 문서를 참조하십시오.

데이터 요소에 매핑할 때 `event` 개체 내에서 다음 키를 참조할 수 있습니다.

| `event` 키 | 유형 | 플랫폼 경로 | 설명 | 필수 | 제한 |
| --- | --- | --- | --- | --- | --- |
| `source` | 문자열 | `arc.event.xdm._extconndev.event_source` | 이벤트를 전송한 애플리케이션. | 예 | `Zendesk`은(는) Zendesk 표준 이벤트의 보호된 소스 이름이므로 값으로 사용하지 마십시오. 이를 사용하려고 하면 오류가 발생합니다.<br>값 길이는 40자를 초과할 수 없습니다. |
| `type` | 문자열 | `arc.event.xdm._extconndev.event_type` | 이벤트 유형의 이름입니다. 이 필드를 사용하여 주어진 소스에 대해 서로 다른 종류의 이벤트를 표시할 수 있습니다. 예를 들어 사용자 로그인에 대한 이벤트 세트와 장바구니에 대한 이벤트 세트를 만들 수 있습니다. | 예 | 값 길이는 40자를 초과할 수 없습니다. |
| `description` | 문자열 | `arc.event.xdm._extconndev.description` | 이벤트에 대한 설명. | 아니요 | (N/A) |
| `created_at` | 문자열 | `arc.event.xdm.timestamp` | 이벤트가 생성된 시간을 반영하는 ISO-8601 타임스탬프. | 아니요 | (N/A) |
| `properties` | 오브젝트 | `arc.event.xdm._extconndev.EventProperties` | 이벤트에 대한 세부 정보가 포함된 사용자 지정 JSON 개체입니다. | 예 | (N/A) |

{style="table-layout:auto"}

>[!NOTE]
>
>이벤트 속성에 대한 자세한 지침은 [[!DNL Zendesk Events API] 설명서](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)를 참조하세요.

### `profile` 키

`profile`은(는) 이벤트를 트리거한 사용자를 나타내는 JSON 개체입니다. `profile` 개체에서 캡처한 속성에 대한 자세한 내용은 [프로필 구조](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)의 Zendesk 문서를 참조하십시오.

데이터 요소에 매핑할 때 `profile` 개체 내에서 다음 키를 참조할 수 있습니다.

| `profile` 키 | 유형 | 플랫폼 경로 | 설명 | 필수 | 제한 |
| --- | --- | --- | --- | --- | --- |
| `source` | 문자열 | `arc.event.xdm._extconndev.profile_source` | `Support`, `CompanyName` 또는 `Chat` 등 프로필과 연결된 제품 또는 서비스입니다. | 예 | (N/A) |
| `type` | 문자열 | `arc.event.xdm._extconndev.profile_type` | 프로필 유형의 이름입니다. 이 필드를 사용하여 주어진 소스에 대해 서로 다른 종류의 프로필을 만들 수 있습니다. 예를 들어 고객에 대한 회사 프로필 세트와 직원에 대한 회사 프로필 세트를 만들 수 있습니다. | 예 | 프로필 유형 길이는 40자를 초과할 수 없습니다. |
| `name` | 문자열 | `arc.event.xdm._extconndev.name` | 프로필의 사용자 이름 | 아니요 | (N/A) |
| `user_id` | 문자열 | `arc.event.xdm._extconndev.user_id` | Zendesk의 개인 사용자 ID입니다. | 아니요 | (N/A) |
| `identifiers` | 배열 | `arc.event.xdm._extconndev.identifiers` | 하나 이상의 식별자가 포함된 배열입니다. 각 식별자는 유형과 값으로 구성됩니다. | 예 | `identifiers` 배열에 대한 자세한 내용은 [Zendesk 설명서](https://developer.zendesk.com/api-reference/ticketing/users/profiles_api/profiles_api/#identifiers-array)를 참조하세요. 모든 필드와 값은 고유해야 합니다. |
| `attributes` | 오브젝트 | `arc.event.xdm._extconndev.attrbutes` | 사용자에 대한 사용자 정의 속성이 포함된 객체입니다. | 아니요 | 프로필 특성에 대한 자세한 내용은 [Zendesk 설명서](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/#attributes)를 참조하세요. |

{style="table-layout:auto"}

## Zendesk 내에서 데이터 유효성 검사 {#validate}

이벤트 컬렉션 및 Adobe Experience Platform 통합이 성공적으로 수행된 경우 Zendesk 콘솔 내의 이벤트가 아래와 같이 표시됩니다. 이는 성공적인 통합을 나타냅니다.

프로필:

![Zendesk 프로필 페이지](../../../images/extensions/server/zendesk/zendesk-profiles.png)

이벤트:

![Zendesk 이벤트 페이지](../../../images/extensions/server/zendesk/zendesk-events.png)

## 요청 제한 {#limits}

Zendesk [!DNL Events API]은(는) 계정 유형에 따라 분당 다음 수의 요청을 처리할 수 있습니다.

| [!DNL Account Type] | 분당 요청 수 |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

이러한 제한에 대한 자세한 내용은 [Zendesk 설명서](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.)를 참조하세요.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

확장을 사용하거나 구성하는 동안 Zendesk Events API에서 아래 오류가 반환될 수 있습니다.

| 오류 코드 | 설명 | 해결 방법 | 예 |
|---|---|---|---|
| 400 | **잘못된 프로필 길이:** 이 오류는 프로필 특성의 길이가 40자를 초과할 때 발생합니다. | 프로필 속성 데이터의 길이를 최대 40자로 제한합니다. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **경로를 찾을 수 없음:** 이 오류는 잘못된 도메인을 제공했을 때 발생합니다. | 올바른 도메인이 다음 형식으로 제공되는지 확인하십시오. `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **인증 잘못됨 또는 누락:** 토큰에 액세스할 때 이 오류가 발생하며, 토큰이 잘못되었거나, 누락되었거나, 만료되었습니다. | 액세스 토큰이 유효하고 만료되지 않았는지 확인하십시오. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **권한 부족:** 리소스에 액세스할 수 있는 충분한 권한이 제공되지 않으면 이 오류가 발생합니다. | 필요한 권한이 제공되었는지 확인합니다. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **요청이 너무 많음:** 이 오류는 끝점 개체 레코드 제한을 초과할 때 발생합니다. | 제한당 임계값에 대한 자세한 내용은 [요청 제한](#limits)의 위 섹션을 참조하십시오. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## 다음 단계

이 문서에서는 UI에서 Zendesk 이벤트 전달 확장 기능을 설치하고 구성하는 방법에 대해 설명합니다. Zendesk에서 이벤트 데이터를 수집하는 방법에 대한 자세한 내용은 공식 설명서를 참조하십시오.

* [이벤트 시작](https://developer.zendesk.com/documentation/ticketing/events/getting-started-with-events/)
* [Zendesk 이벤트 API](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/)
* [이벤트 API 정보](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)
* 이벤트의 [구조](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/)
* [Zendesk 프로필 API](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/#profile-object)
* [프로필 API 정보](https://developer.zendesk.com/documentation/ticketing/profiles/about-the-profiles-api/)
* [프로필 구조](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)
