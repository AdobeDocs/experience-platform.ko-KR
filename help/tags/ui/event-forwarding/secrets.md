---
title: 이벤트 전달 시 암호 구성
description: 이벤트 전달 속성에 사용되는 엔드포인트를 인증하도록 UI에서 보안을 구성하는 방법에 대해 알아봅니다.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 374c140a5db678adfa2e038b69478ad8c7f8dc95
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 2%

---

# 이벤트 전달 시 암호 구성

이벤트 전달 시 암호는 다른 시스템에 대한 인증 자격 증명을 나타내는 리소스이며, 이를 통해 데이터를 안전하게 교환할 수 있습니다. 비밀은 이벤트 전달 속성 내에서만 만들 수 있습니다.

현재 지원되는 비밀 유형은 다음과 같습니다.

| 암호 유형 | 설명 |
| --- | --- |
| [!UICONTROL Amazon OAuth 2] | [!DNL Amazon] 서비스를 사용하여 보안 인증을 사용하도록 설정합니다. 시스템은 토큰을 안전하게 저장하고 지정된 간격으로 갱신을 처리합니다. |
| [!UICONTROL Google OAuth 2] | [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview) 및 [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)에서 사용할 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 인증 사양을 지원하는 몇 가지 특성이 포함되어 있습니다. 시스템에서 필요한 정보를 요청한 다음 지정된 간격에 따라 이러한 토큰의 갱신을 처리합니다. |
| [!UICONTROL HTTP] | 사용자 이름과 암호에 대해 각각 두 개의 문자열 속성을 포함합니다. |
| [!UICONTROL [!DNL LinkedIn] OAuth 2] | 시스템에서 필요한 정보를 요청한 다음 지정된 간격에 따라 이러한 토큰의 갱신을 처리합니다. |
| [!UICONTROL OAuth 2] | [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 인증 사양에 대한 [클라이언트 자격 증명 부여 형식](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4)을(를) 지원하는 여러 특성이 포함되어 있습니다. 시스템에서 필요한 정보를 요청한 다음 지정된 간격에 따라 이러한 토큰의 갱신을 처리합니다. |
| [!UICONTROL OAuth 2 JWT] | [OAuth 2.0 권한 부여](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1)에 대한 JSON 웹 토큰(JWT) 프로필을 지원하는 몇 가지 특성이 포함되어 있습니다. 시스템에서 필요한 정보를 요청한 다음 지정된 간격에 따라 이러한 토큰의 갱신을 처리합니다. |
| [!UICONTROL 토큰] | 두 시스템에서 알려지고 이해하는 인증 토큰 값을 나타내는 단일 문자 문자열입니다. |

{style="table-layout:auto"}

이 안내서에서는 Experience Platform UI 또는 데이터 수집 UI에서 이벤트 전달([!UICONTROL Edge]) 속성에 대한 비밀을 구성하는 방법에 대한 높은 수준의 개요를 제공합니다.

>[!NOTE]
>
>비밀 구조의 JSON 예를 포함하여 Reactor API의 비밀을 관리하는 방법에 대한 자세한 지침은 [비밀 API 안내서](../../api/guides/secrets.md)를 참조하세요.

## 전제 조건

이 안내서에서는 데이터 요소와 이벤트 전달 규칙을 만드는 방법을 포함하여 UI에서 태그 및 이벤트 전달을 위한 리소스를 관리하는 방법을 이미 잘 알고 있다고 가정합니다. 소개가 필요한 경우 [리소스 관리](../managing-resources/overview.md)에 대한 안내서를 참조하십시오.

또한 라이브러리에 리소스를 추가하고 테스트를 위해 웹 사이트에 빌드를 설치하는 방법을 포함하여 태그 및 이벤트 전달을 위한 게시 플로우에 대해 잘 알고 있어야 합니다. 자세한 내용은 [게시 개요](../publishing/overview.md)를 참조하십시오.

## 시크릿 생성 {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="시크릿 환경"
>abstract="시크릿을 이벤트 전달에 사용하려면 기존 환경에 할당해야 합니다. 이벤트 전달 속성에 환경이 생성되지 않은 경우 계속하기 전에 환경을 구성해야 합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=ko" text="환경 개요"

암호를 만들려면 왼쪽 탐색에서 **[!UICONTROL 이벤트 전달]**&#x200B;을 선택한 다음 암호를 추가할 이벤트 전달 속성을 엽니다. 그런 다음 왼쪽 탐색에서 **[!UICONTROL 암호]**&#x200B;를 선택한 다음 **[!UICONTROL 새 암호 만들기]**&#x200B;를 선택합니다.

![새 암호 만들기](../../images/ui/event-forwarding/secrets/create-new-secret.png)

다음 화면에서는 비밀의 세부 사항을 구성할 수 있습니다. 시크릿을 이벤트 전달에 사용하려면 기존 환경에 할당해야 합니다. 이벤트 전달 속성에 대해 환경을 만들지 않은 경우 계속하기 전에 환경을 구성하는 방법에 대한 지침을 보려면 [환경](../publishing/environments.md)에 대한 안내서를 참조하십시오.

>[!NOTE]
>
>암호를 환경에 추가하기 전에 만들고 저장하려면 **[!UICONTROL 암호를 환경에 첨부]** 토글을 비활성화한 후 나머지 정보를 입력하십시오. 암호를 사용하려면 나중에 환경에 지정해야 합니다.
>
>![환경 비활성화](../../images/ui/event-forwarding/secrets/env-disabled.png)

**[!UICONTROL 대상 환경]**&#x200B;에서 드롭다운 메뉴를 사용하여 암호를 할당할 환경을 선택합니다. **[!UICONTROL 암호 이름]**&#x200B;에서 환경의 컨텍스트에서 암호 이름을 지정하십시오. 이 이름은 이벤트 전달 속성에 있는 모든 비밀에서 고유해야 합니다.

![환경 및 이름](../../images/ui/event-forwarding/secrets/env-and-name.png)

암호는 한 번에 하나의 환경에만 할당할 수 있지만 원할 경우 다른 환경의 여러 암호에 동일한 자격 증명을 할당할 수 있습니다. 목록에 다른 행을 추가하려면 **[!UICONTROL 환경 추가]**&#x200B;를 선택하십시오.

![환경 추가](../../images/ui/event-forwarding/secrets/add-env.png)

추가하는 각 환경에 대해 연결된 암호에 다른 고유한 이름을 제공해야 합니다. 사용 가능한 환경을 모두 소진하면 **[!UICONTROL 환경 추가]** 단추를 사용할 수 없습니다.

![환경을 추가할 수 없음](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

여기에서 암호를 만드는 단계는 만드는 암호 유형에 따라 다릅니다. 자세한 내용은 아래 하위 섹션을 참조하십시오.

* [[!UICONTROL 토큰]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)
* [[!UICONTROL [!DNL LinkedIn] OAuth 2]](#linkedin-oauth2)
* [[!UICONTROL [!DNL Amazon] OAuth 2]](#amazon-oauth2)

### [!UICONTROL 토큰] {#token}

토큰 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL Token]**&#x200B;을(를) 선택하십시오. 표시되는 **[!UICONTROL 토큰]** 필드에 인증 중인 시스템에서 인식하는 자격 증명 문자열을 제공하십시오. **[!UICONTROL 암호 만들기]**&#x200B;를 선택하여 암호를 저장합니다.

![토큰 암호](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

HTTP 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL 단순 HTTP]**&#x200B;을(를) 선택합니다. 아래 필드에 자격 증명의 사용자 이름과 암호를 입력한 다음 **[!UICONTROL 암호 만들기]**&#x200B;를 선택하여 암호를 저장하십시오.

>[!NOTE]
>
>저장되면 자격 증명이 [&quot;기본&quot; HTTP 인증 체계](https://www.rfc-editor.org/rfc/rfc7617.html)를 사용하여 인코딩됩니다.

![HTTP 암호](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

OAuth 2 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL OAuth 2]**&#x200B;을(를) 선택합니다. 아래 표시되는 필드에서 OAuth 통합을 위해 [[!UICONTROL 클라이언트 ID] 및 [!UICONTROL 클라이언트 암호]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)와 [[!UICONTROL 토큰 URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)을 제공합니다. UI의 [!UICONTROL 토큰 URL] 필드는 인증 서버 호스트와 토큰 경로 간의 연결입니다.

![OAuth 2 암호](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

**[!UICONTROL 자격 증명 옵션]**&#x200B;에서 키-값 쌍의 형태로 `scope` 및 `audience`과(와) 같은 다른 자격 증명 옵션을 제공할 수 있습니다. 키-값 쌍을 더 추가하려면 **[!UICONTROL 다른 키-값 쌍 추가]**&#x200B;를 선택하십시오.

![자격 증명 옵션](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

마지막으로 암호에 대해 **[!UICONTROL 새로 고침 오프셋]** 값을 구성할 수 있습니다. 시스템이 자동 새로 고침을 수행할 토큰 만료 전 시간(초)을 나타냅니다. 해당 시간(시간 및 분)은 필드 오른쪽에 표시되며 입력할 때 자동으로 업데이트됩니다.

![오프셋 새로 고침](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

예를 들어 새로 고침 오프셋이 `14400`(4시간)의 기본값으로 설정되고 액세스 토큰의 `expires_in` 값이 `86400`(24시간)이면 시스템은 20시간 후에 암호를 자동으로 새로 고칩니다.

>[!IMPORTANT]
>
>OAuth 암호는 새로 고침 사이에 최소 4시간이 필요하며 최소 8시간 동안에도 유효해야 합니다. 이 제한은 생성된 토큰에 문제가 발생할 경우 최소 4시간 동안 개입할 수 있도록 합니다.
>
>예를 들어, 오프셋이 `28800`(8시간)로 설정되고 액세스 토큰에 `expires_in`/`36000`(10시간)이 있는 경우 결과 차이가 4시간 미만이므로 교환이 실패합니다.

완료되면 **[!UICONTROL 암호 만들기]**&#x200B;를 선택하여 암호를 저장합니다.

![OAuth 2 오프셋 저장](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

OAuth 2 JWT 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL OAuth 2 JWT]**&#x200B;을(를) 선택합니다.

![OAuth 2 JWT 비밀이 [!UICONTROL Type] 드롭다운에서 강조 표시된 [!UICONTROL 비밀 만들기] 탭입니다.](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>현재 JWT 서명을 위해 지원되는 유일한 [!UICONTROL 알고리즘]은(는) RS256입니다.

아래 표시되는 필드에서 [!UICONTROL 발급자], [!UICONTROL 제목], [!UICONTROL 대상자], [!UICONTROL 사용자 지정 클레임], [!UICONTROL TTL]을 제공한 다음 드롭다운에서 [!UICONTROL 알고리즘]을 선택합니다. 그런 다음 OAuth 통합을 위해 [!UICONTROL 개인 키 ID]와 [[!UICONTROL 토큰 URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)을(를) 입력하십시오. [!UICONTROL 토큰 URL] 필드는 필수 필드가 아닙니다. 값이 제공되면 JWT는 액세스 토큰과 교환됩니다. 응답의 `expires_in` 특성 및 [!UICONTROL 새로 고침 오프셋] 값에 따라 암호가 새로 고쳐집니다. 값을 제공하지 않으면 가장자리로 밀린 비밀이 JWT입니다. [!UICONTROL TTL] 및 [!UICONTROL 오프셋 새로 고침] 값에 따라 JWT가 새로 고쳐집니다.

![선택한 입력 필드가 강조 표시된 [!UICONTROL 암호 만들기] 탭입니다.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

**[!UICONTROL 자격 증명 옵션]**&#x200B;에서 키-값 쌍의 형태로 `jwt_param`과(와) 같은 다른 자격 증명 옵션을 제공할 수 있습니다. 키-값 쌍을 더 추가하려면 **[!UICONTROL 다른 키-값 쌍 추가]**&#x200B;를 선택하십시오.

![[!UICONTROL 자격 증명 옵션] 필드를 강조 표시하는 [!UICONTROL 암호 만들기] 탭](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

마지막으로 암호에 대해 **[!UICONTROL 새로 고침 오프셋]** 값을 구성할 수 있습니다. 시스템이 자동 새로 고침을 수행할 토큰 만료 전 시간(초)을 나타냅니다. 해당 시간(시간 및 분)은 필드 오른쪽에 표시되며 입력할 때 자동으로 업데이트됩니다.

![[!UICONTROL 새로 고침 오프셋] 필드를 강조 표시하는 [!UICONTROL 암호 만들기] 탭입니다.](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

예를 들어 새로 고침 오프셋이 `1800`(30분)의 기본값으로 설정되고 액세스 토큰의 `expires_in` 값이 `3600`(1시간)이면 시스템은 1시간 후에 암호를 자동으로 새로 고칩니다.

>[!IMPORTANT]
>
>OAuth 2 JWT 암호는 새로 고침 사이에 최소 30분이 필요하며 최소 1시간 동안도 유효해야 합니다. 이 제한 사항은 생성된 토큰에 문제가 발생할 경우 개입할 수 있도록 최소 30분을 제공합니다.
>
>예를 들어, 오프셋이 `1800`(30분)으로 설정되고 액세스 토큰의 `expires_in`이(가) `2700`(45분)인 경우 결과 차이가 30분 미만이므로 교환이 실패합니다.

완료되면 **[!UICONTROL 암호 만들기]**&#x200B;를 선택하여 암호를 저장합니다.

![[!UICONTROL 암호 만들기] 탭 강조 표시 [!UICONTROL 암호 만들기]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Google OAuth 2 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL Google OAuth 2]**&#x200B;을(를) 선택합니다. **[!UICONTROL 범위]**&#x200B;에서 이 암호를 사용하여 액세스 권한을 부여할 Google API를 선택합니다. 현재 지원되는 제품은 다음과 같습니다.

* [Google 광고 API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

완료되면 **[!UICONTROL 암호 만들기]**&#x200B;를 선택합니다.

![Google OAuth 2 암호](../../images/ui/event-forwarding/secrets/google-oauth.png)

Google을 통해 암호를 수동으로 승인해야 함을 알리는 팝오버가 표시됩니다. 계속하려면 **[!UICONTROL 만들기 및 승인]**&#x200B;을 선택하세요.

![Google 권한 부여 팝오버](../../images/ui/event-forwarding/secrets/google-authorization.png)

Google 계정에 대한 자격 증명을 입력할 수 있는 대화 상자가 나타납니다. 화면의 지침에 따라 선택한 범위 아래의 데이터에 이벤트 전달 액세스 권한을 부여합니다. 인증 프로세스가 완료되면 비밀이 생성됩니다.

>[!IMPORTANT]
>
>조직에 Google Cloud 애플리케이션에 대한 재인증 정책이 설정되어 있는 경우 인증이 만료된 후(정책 구성에 따라 1~24시간) 생성된 비밀이 성공적으로 새로 고쳐지지 않습니다.
>
>이 문제를 해결하려면 Google Admin Console에 로그인하고 **[!DNL App access control]** 페이지로 이동하여 이벤트 전달 앱(Adobe Real-Time CDP 이벤트 전달)을 [!DNL Trusted]&#x200B;(으)로 표시합니다. 자세한 내용은 [Google Cloud 서비스의 세션 길이 설정](https://support.google.com/a/answer/9368756)에 대한 Google 설명서를 참조하십시오.

### [!UICONTROL [!DNL LinkedIn] OAuth 2] {#linkedin-oauth2}

[!DNL LinkedIn] OAuth 2 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL [!DNL LinkedIn]OAuth 2]**&#x200B;을(를) 선택합니다. **[!UICONTROL 암호 만들기]**&#x200B;를 선택합니다.

![[!UICONTROL Type] 필드가 강조 표시된 [!UICONTROL 암호 만들기] 탭.](../../images/ui/event-forwarding/secrets/linkedin-oauth.png)

[!DNL LinkedIn]을(를) 통해 암호를 수동으로 승인해야 함을 알리는 팝오버가 나타납니다. 계속하려면 **[!UICONTROL [!DNL LinkedIn]]**&#x200B;을(를) 사용하여 암호 만들기 및 권한 부여를 선택하십시오.

![LinkedIn 권한 부여 팝오버에서 &quot;LinkedIn으로 암호 만들기 및 승인&quot; 단추를 강조 표시합니다.](../../images/ui/event-forwarding/secrets/linkedin-authorization.png)

[!DNL LinkedIn] 자격 증명을 입력하라는 대화 상자가 나타납니다. 화면의 지침에 따라 데이터에 이벤트 전달 액세스 권한을 부여합니다.

인증 프로세스가 완료되면 새로 만든 암호를 볼 수 있는 **[!UICONTROL 암호]** 탭으로 돌아갑니다. 여기에서 암호의 상태와 만료일을 볼 수 있습니다.

![새로 만든 암호를 강조 표시하는 [!UICONTROL 암호] 탭](../../images/ui/event-forwarding/secrets/linkedin-new-secret.png)

#### [!UICONTROL [!DNL LinkedIn] OAuth 2] 암호 재인증

>중요 사항
>
>365일마다 [!DNL LinkedIn] 자격 증명을 사용하여 다시 승인해야 합니다. 기한 내에 재인증하지 않으면 암호가 새로 고쳐지지 않고 [!DNL LinkedIn] 전환 요청이 실패합니다.

재인증이 필요한 암호보다 3개월 먼저, 속성의 페이지를 탐색할 때 팝업이 표시됩니다. **[!UICONTROL 암호를 확인하려면 여기를 클릭하세요]**.

![비밀 재인증 팝업을 강조 표시하는 [!UICONTROL 속성 개요] 탭입니다.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization-popup.png)

[!UICONTROL 암호] 탭으로 리디렉션됩니다. 이 페이지에 나열된 비밀은 다시 승인해야 하는 비밀만 표시하도록 필터링됩니다. 다시 인증해야 하는 암호에 대해 **[!UICONTROL 인증 필요]**&#x200B;를 선택하십시오.

![[!UICONTROL 암호] 탭에서 [!DNL LinkedIn] 암호에 대해 [!UICONTROL 인증 필요]를 강조 표시합니다.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization.png)

[!DNL LinkedIn] 자격 증명을 입력하라는 대화 상자가 나타납니다. 화면의 지침에 따라 암호를 다시 인증합니다.

### [!UICONTROL [!DNL Amazon] OAuth 2] {#amazon-oauth2}

[!DNL Amazon] OAuth 2 암호를 만들려면 **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL [!DNL Amazon]OAuth 2]**&#x200B;을(를) 선택합니다. **[!UICONTROL 암호 만들기]**&#x200B;를 선택합니다.

![[!UICONTROL Type] 필드가 강조 표시된 [!UICONTROL 암호 만들기] 탭.](../../images/ui/event-forwarding/secrets/amazon-oauth.png)

[!DNL Amazon]을(를) 통해 암호를 수동으로 승인해야 함을 알리는 팝오버가 나타납니다. 계속하려면 **[!UICONTROL [!DNL Amazon]]**&#x200B;을(를) 사용하여 암호 만들기 및 권한 부여를 선택하십시오.

![Amazon 인증 팝오버에서 &quot;Amazon으로 암호 만들기 및 승인&quot; 단추를 강조 표시합니다.](../../images/ui/event-forwarding/secrets/amazon-authorization.png)

[!DNL Amazon] 자격 증명을 입력하라는 대화 상자가 나타납니다. 화면의 지침에 따라 데이터에 이벤트 전달 액세스 권한을 부여합니다.

인증 프로세스가 완료되면 새로 만든 암호를 볼 수 있는 **[!UICONTROL 암호]** 탭으로 돌아갑니다. 여기에서 암호의 상태와 만료일을 볼 수 있습니다.

![새로 만든 암호를 강조 표시하는 [!UICONTROL 암호] 탭](../../images/ui/event-forwarding/secrets/amazon-new-secret.png)

## 암호 편집

속성에 대한 암호를 만들면 **[!UICONTROL 암호]** 작업 영역에서 해당 암호를 찾을 수 있습니다. 기존 비밀의 세부 정보를 편집하려면 목록에서 해당 이름을 선택합니다.

![편집할 암호 선택](../../images/ui/event-forwarding/secrets/edit-secret.png)

다음 화면에서는 암호에 대한 이름 및 자격 증명을 변경할 수 있습니다.

![암호 편집](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>암호가 기존 환경과 연결된 경우 암호를 다른 환경에 재할당할 수 없습니다. 다른 환경에서 동일한 자격 증명을 사용하려면 대신 [새 암호를 만들어야](#create) 합니다. 이 화면에서 환경을 재할당하는 유일한 방법은 암호를 환경에 미리 할당하지 않았거나 암호가 첨부된 환경을 삭제한 경우입니다.

### 비밀 교환 다시 시도

편집 화면에서 비밀 교환을 다시 시도하거나 새로 고칠 수 있습니다. 이 프로세스는 편집되는 암호의 유형에 따라 달라집니다.

| 암호 유형 | 프로토콜 다시 시도 |
| --- | --- |
| [!UICONTROL 토큰] | 암호 교환을 다시 시도하려면 **[!UICONTROL 교환 암호]**&#x200B;를 선택하십시오. 이 컨트롤은 암호에 연결된 환경이 있을 때만 사용할 수 있습니다. |
| [!UICONTROL HTTP] | 암호에 연결된 환경이 없는 경우 **[!UICONTROL 암호 교환]**&#x200B;을 선택하여 base64로 자격 증명을 교환하세요. 환경이 연결되어 있으면 **[!UICONTROL Exchange 및 암호 배포]**&#x200B;를 선택하여 base64로 Exchange를 수행하고 암호를 배포합니다. |
| [!UICONTROL OAuth 2] | 자격 증명을 교환하고 인증 공급자로부터 액세스 토큰을 반환하려면 **[!UICONTROL 토큰 생성]**&#x200B;을 선택하십시오. |

## 암호 삭제

**[!UICONTROL 암호]** 작업 영역에서 기존 암호를 삭제하려면 **[!UICONTROL 삭제]**&#x200B;를 선택하기 전에 이름 옆에 있는 확인란을 선택하십시오.

![암호 삭제](../../images/ui/event-forwarding/secrets/delete.png)

## 이벤트 전달에 암호 사용

이벤트 전달에서 암호를 사용하려면 먼저 암호 자체를 참조하는 [데이터 요소](../managing-resources/data-elements.md)를 만들어야 합니다. 데이터 요소를 저장한 후 이벤트 전달 [규칙](../managing-resources/rules.md)에 데이터 요소를 포함하고 해당 규칙을 [라이브러리](../publishing/libraries.md)에 추가하여 [빌드](../publishing/builds.md)로서 Adobe 서버에 배포할 수 있습니다.

데이터 요소를 만들 때 **[!UICONTROL 코어]** 확장을 선택한 다음 데이터 요소 유형으로 **[!UICONTROL 암호]**&#x200B;를 선택합니다. 오른쪽 패널은 데이터 요소에 최대 세 개의 비밀([!UICONTROL 개발], [!UICONTROL 스테이징] 및 [!UICONTROL 프로덕션]에 대해 각각 하나씩)을 할당하도록 드롭다운 컨트롤을 업데이트하고 제공합니다.

![데이터 요소](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>개발, 스테이징 및 프로덕션 환경에 첨부된 비밀만 해당 드롭다운에 대해 표시됩니다.

단일 데이터 요소에 여러 암호를 할당하고 규칙을 포함하면 포함된 라이브러리가 [게시 흐름](../publishing/publishing-flow.md)에 있는 위치에 따라 데이터 요소의 값이 변경될 수 있습니다.

![여러 암호가 있는 데이터 요소](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>데이터 요소를 만들 때 개발 환경을 할당해야 합니다. 스테이징 및 프로덕션 환경에 대한 비밀이 필요하지 않지만, 해당 환경으로 전환하려는 빌드는 해당 환경에 대해 비밀 유형 데이터 요소에 비밀이 선택되어 있지 않으면 실패합니다.

## 다음 단계

이 안내서에서는 UI에서 비밀을 관리하는 방법을 다룹니다. Reactor API를 사용하여 암호와 상호 작용하는 방법에 대한 자세한 내용은 [암호 끝점 안내서](../../api/endpoints/secrets.md)를 참조하십시오.
