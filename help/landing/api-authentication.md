---
solution: Experience Platform
title: Experience Platform API 인증 및 액세스
type: Tutorial
description: 이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다.
role: Developer
feature: API
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 850a4ae82fda22a761a28ac9059d7dea57c9662a
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 2%

---


# Experience Platform API 인증 및 액세스

이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다. 이 자습서가 끝나면 모든 Platform API 호출에서 헤더로 필요한 다음 자격 증명을 생성하거나 수집하게 됩니다.

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>위의 세 가지 자격 증명 외에도 많은 Platform API에는 헤더로 제공할 수 있는 올바른 `{SANDBOX_NAME}`이(가) 필요합니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를, 조직에서 사용할 수 있는 샌드박스를 나열하는 방법은 [샌드박스 관리 끝점](/help/sandboxes/api/sandboxes.md#list) 설명서를 참조하십시오.

애플리케이션 및 사용자의 보안을 유지하려면 OAuth와 같은 표준을 사용하여 Experience Platform API에 대한 모든 요청을 인증 및 승인해야 합니다.

이 자습서에서는 아래 순서도에 설명된 대로 Platform API 호출을 인증하는 데 필요한 자격 증명을 수집하는 방법을 다룹니다. 초기 1회 설정에서 필요한 자격 증명 대부분을 수집할 수 있습니다. 그러나 액세스 토큰은 24시간마다 새로 고쳐야 합니다.

![일회성 초기 설정 및 후속 각 세션에 대한 인증 흐름 요구 사항입니다.](./images/api-authentication/authentication-flowchart.png)

## 전제 조건 {#prerequisites}

Experience Platform API를 성공적으로 호출하려면 다음 조건을 충족해야 합니다.

* Adobe Experience Platform에 액세스할 수 있는 조직입니다.
* 귀하를 제품 프로필의 개발자 및 사용자로 추가할 수 있는 Admin Console 관리자.
* API를 통해 Experience Platform의 여러 부분에서 읽기 또는 쓰기 작업을 수행하는 데 필요한 속성 기반 액세스 제어를 부여할 수 있는 Experience Platform 시스템 관리자.

또한 이 자습서를 완료하려면 Adobe ID이 있어야 합니다. Adobe ID이 없는 경우 다음 단계를 사용하여 만들 수 있습니다.

1. [Adobe Developer Console](https://console.adobe.io)(으)로 이동합니다.
2. **[!UICONTROL 새 계정 만들기]**&#x200B;를 선택합니다.
3. 등록 프로세스를 완료합니다.

## Experience Platform을 위한 개발자 및 사용자 액세스 권한 획득 {#gain-developer-user-access}

Adobe Developer Console에서 통합을 만들기 전에 계정에 Adobe Admin Console의 Experience Platform 제품 프로필에 대한 개발자 및 사용자 권한이 있어야 합니다.

### 개발자 액세스 권한 얻기 {#gain-developer-access}

조직의 Admin Console 관리자에게 문의하여 개발자로 Experience Platform 제품 프로필에 추가하십시오. [제품 프로필에 대한 개발자 액세스를 관리](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)하는 방법에 대한 특정 지침은 Admin Console 설명서를 참조하세요.

개발자로 할당되면 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)에서 통합 만들기를 시작할 수 있습니다. 이러한 통합은 외부 앱 및 서비스에서 Adobe API로의 파이프라인입니다.

### 사용자 액세스 권한 얻기 {#gain-user-access}

Admin Console 관리자가 귀하를 동일한 제품 프로필에 사용자로 추가해야 합니다. 사용자 액세스를 사용하면 UI에서 사용자가 수행하는 API 작업의 결과를 볼 수 있습니다.

자세한 내용은 [Admin Console에서 사용자 그룹 관리](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html)에 대한 안내서를 참조하십시오.

## API 키(클라이언트 ID) 및 조직 ID 생성 {#generate-credentials}

>[!NOTE]
>
>[Privacy Service API 안내서](../privacy-service/api/getting-started.md)에서 이 문서를 팔로우하는 경우 이제 해당 안내서로 돌아가서 [!DNL Privacy Service]에 고유한 액세스 자격 증명을 생성할 수 있습니다.

Admin Console을 통해 개발자 및 사용자가 플랫폼에 액세스할 수 있게 되면 다음 단계는 Adobe Developer Console에서 `{ORG_ID}` 및 `{API_KEY}` 자격 증명을 생성하는 것입니다. 이러한 자격 증명은 한 번만 생성하면 되며 향후 Platform API 호출에서 재사용할 수 있습니다.

>[!TIP]
>
>Developer Console으로 이동하는 대신 API 참조 설명서 페이지에서 직접 Platform API로 작업하는 데 필요한 모든 인증 자격 증명을 가져올 수 있습니다. 기능에 대해 [자세히 알아보십시오](#get-credentials-functionality).

### 프로젝트에 Experience Platform 추가 {#add-platform-to-project}

[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)(으)로 이동하여 Adobe ID으로 로그인합니다. 그런 다음 Adobe Developer Console 설명서에서 [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)에 대한 자습서에 설명된 단계를 수행합니다.

새 프로젝트를 만든 후에는 **[!UICONTROL 프로젝트 개요]** 화면에서 **[!UICONTROL API 추가]**&#x200B;를 선택합니다.

>[!TIP]
>
>여러 조직에 대해 프로비저닝된 경우 인터페이스의 오른쪽 상단에 있는 조직 선택기를 사용하여 필요한 조직에 있는지 확인합니다.

API 추가 옵션이 강조 표시된 ![Developer Console 화면.](./images/api-authentication/add-api.png)

**[!UICONTROL API 추가]** 화면이 나타납니다. **[!UICONTROL 다음]**&#x200B;을(를) 선택하기 전에 **[!UICONTROL Adobe Experience Platform]**&#x200B;의 제품 아이콘을 선택한 다음 **[!UICONTROL Experience Platform API]**&#x200B;을(를) 선택하십시오.

![API 추가 화면에서 Experience Platform API를 선택합니다.](./images/api-authentication/platform-api.png)

>[!TIP]
>
>**[!UICONTROL 문서 보기]** 옵션을 선택하여 별도의 브라우저 창에서 전체 [Experience Platform API 참조 설명서](https://developer.adobe.com/experience-platform-apis/)(으)로 이동합니다.

### [!UICONTROL OAuth 서버 간] 인증 유형 선택 {#select-oauth-server-to-server}

그런 다음 **[!UICONTROL OAuth 서버 간]** 인증 유형을 선택하여 액세스 토큰을 생성하고 Experience Platform API에 액세스합니다. **[!UICONTROL 다음]**&#x200B;을(를) 선택하기 전에 **[!UICONTROL 자격 증명 이름]** 텍스트 필드에 의미 있는 이름을 지정하십시오.

>[!IMPORTANT]
>
>**[!UICONTROL OAuth 서버 간]** 메서드는 앞으로 지원되는 유일한 토큰 생성 메서드입니다. 이전에 지원된 **[!UICONTROL 서비스 계정(JWT)]** 메서드는 더 이상 사용되지 않으며 새 통합에 대해 선택할 수 없습니다. JWT 인증 방법을 사용하는 기존 통합은 2025년 6월 30일까지 계속 작동하지만, Adobe은 해당 날짜 이전에 기존 통합을 새 [!UICONTROL OAuth 서버 간] 방법으로 마이그레이션할 것을 강력히 권장합니다. [!BADGE 사용되지 않음] 섹션에서 자세한 정보를 확인하세요.{type=negative}[JSON 웹 토큰(JWT) 생성](#jwt).

![Experience Platform API에 대한 OAuth 서버 간 인증 방법을 선택하십시오.](./images/api-authentication/oauth-authentication-method.png)

### 통합할 제품 프로필 선택 {#select-product-profiles}

**[!UICONTROL API 구성]** 화면에서 액세스 권한을 얻으려는 추가 제품 프로필과 함께 **[!UICONTROL AEP-Default-All-Users]**&#x200B;를 선택합니다.

>[!IMPORTANT]
>
Platform의 특정 기능에 액세스하려면 필요한 속성 기반 액세스 제어 권한을 부여하는 시스템 관리자도 필요합니다. [필요한 특성 기반 액세스 제어 권한 얻기](#get-abac-permissions) 섹션에서 자세히 알아보세요.

![통합할 제품 프로필을 선택하십시오.](./images/api-authentication/select-product-profiles.png)

준비가 되면 **[!UICONTROL 구성된 API 저장]**&#x200B;을(를) 선택하십시오.

위에서 설명한 Experience Platform API와의 통합 설정 단계에 대한 연습은 아래 비디오 튜토리얼에서도 사용할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### 자격 증명 수집 {#gather-credentials}

API가 프로젝트에 추가되면 프로젝트에 대한 **[!UICONTROL OAuth 서버 간]** 페이지에 Experience Platform API 호출에 필요한 다음 자격 증명이 표시됩니다.

![개발자 콘솔에서 API를 추가한 후의 통합 정보](./images/api-authentication/api-integration-information.png)

* `{API_KEY}`([!UICONTROL 클라이언트 ID])
* `{ORG_ID}`([!UICONTROL 조직 ID])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## 액세스 토큰 생성 {#generate-access-token}

다음 단계는 Platform API 호출에 사용할 `{ACCESS_TOKEN}` 자격 증명을 생성하는 것입니다. `{API_KEY}` 및 `{ORG_ID}`의 값과 달리 Platform API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다. 아래와 같이 액세스 토큰을 생성하는 **[!UICONTROL 액세스 토큰 생성]**&#x200B;을 선택하십시오.

![액세스 토큰을 생성하는 방법 표시](././images/api-authentication/generate-access-token.png)

>[!TIP]
>
Postman 환경 및 컬렉션을 사용하여 액세스 토큰을 생성할 수도 있습니다. 자세한 내용은 [Postman을 사용하여 API 호출 인증 및 테스트](#use-postman)에 대한 섹션을 참조하십시오.

## API 참조 설명서에서 직접 인증 자격 증명을 만들고 검색합니다. {#get-credentials-functionality}

2024년 11월 Experience Platform 릴리스부터 [!UICONTROL Developer Console](으)로 이동할 필요 없이 API 참조 페이지에서 직접 Experience Platform API를 사용하기 위한 자격 증명을 가져올 수 있습니다. [흐름 서비스 API - 대상 페이지](https://developer.adobe.com/experience-platform-apis/references/destinations/)에서 아래 예제를 보십시오.

![API 참조 페이지 상단에 강조 표시된 자격 증명 가져오기 기능입니다.](././images/api-authentication/get-credentials-highlighted.png)

Platform API를 호출하기 위한 자격 증명을 가져오려면 Experience Platform API 참조 페이지로 이동한 다음 페이지 맨 위에서 **[!UICONTROL 로그인]**&#x200B;을 선택합니다. **[!UICONTROL 개인 계정]** 또는 **[!UICONTROL 회사 또는 학교 계정]**&#x200B;으로 로그인하세요.

로그인 후 **[!UICONTROL 새 자격 증명 만들기]**&#x200B;를 선택하여 Platform API에 액세스할 수 있는 새 자격 증명 집합을 만듭니다.

![Platform API에 액세스하기 위해 새 자격 증명을 만듭니다.](././images/api-authentication/create-credentials.gif)

그런 다음 드롭다운 선택기를 사용하여 자격 증명 창을 열고, 액세스 토큰을 생성하고, API 키 및 조직 ID를 가져옵니다. Platform API 작업을 시작하려면 API 참조 페이지의 [**[!UICONTROL 시도]**](/help/release-notes/2024/may-2024.md#interactive-api-documentation) 블록에 자격 증명을 복사하세요.

![드롭다운 선택기를 사용하여 자격 증명을 보고 액세스 토큰을 생성합니다.](././images/api-authentication/view-copy-credentials.gif)

>[!TIP]
>
페이지 상단 자격 증명 블록은 Experience Platform API 참조 설명서에서 다른 엔드포인트 페이지 사이를 이동할 때 계속 표시됩니다.

## [!BADGE 사용되지 않음]{type=negative} JSON 웹 토큰(JWT) 생성 {#jwt}

>[!WARNING]
>
액세스 토큰을 생성하기 위한 JWT 메서드가 더 이상 사용되지 않습니다. 모든 새 통합은 [OAuth 서버 간 인증 방법](#select-oauth-server-to-server)을 사용하여 만들어야 합니다. 또한 Adobe을 사용하려면 통합이 계속 작동하도록 2025년 6월 30일까지 기존 통합을 OAuth 메서드로 마이그레이션해야 합니다. 다음 중요한 설명서를 참조하십시오.
> 
* [JWT에서 OAuth로의 응용 프로그램 마이그레이션 안내서](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
* [OAuth를 사용하는 새 응용 프로그램과 이전 응용 프로그램에 대한 구현 안내서](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
* [OAuth 서버 간 자격 증명 메서드를 사용할 때의 이점](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ 더 이상 사용되지 않는 정보 보기

다음 단계는 계정 자격 증명을 기반으로 JSON 웹 토큰(JWT)을 생성하는 것입니다. 이 값은 Platform API 호출에 사용할 `{ACCESS_TOKEN}` 자격 증명을 생성하는 데 사용되며 24시간마다 다시 생성해야 합니다.

>[!IMPORTANT]
>
이 자습서의 목적을 위해 아래 단계에서는 Developer Console 내에서 JWT를 생성하는 방법을 간략히 설명합니다. 하지만 이 생성 방법은 테스트 및 평가 목적으로만 사용해야 합니다.
>
일반 사용을 위해 JWT를 자동으로 생성해야 합니다. 프로그래밍 방식으로 JWT를 생성하는 방법에 대한 자세한 내용은 Adobe Developer의 [서비스 계정 인증 안내서](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/)를 참조하십시오.

왼쪽 탐색에서 **[!UICONTROL 서비스 계정(JWT)]**&#x200B;을 선택한 다음 **[!UICONTROL JWT 생성]**&#x200B;을 선택합니다.

![](././images/api-authentication/generate-jwt.png)

**[!UICONTROL 사용자 지정 JWT 생성]**&#x200B;에 제공된 텍스트 상자에 Platform API를 서비스 계정에 추가할 때 이전에 생성한 개인 키의 내용을 붙여 넣습니다. 그런 다음 **[!UICONTROL 토큰 생성]**&#x200B;을 선택하십시오.

![](././images/api-authentication/paste-key.png)

페이지는 액세스 토큰을 생성할 수 있는 샘플 cURL 명령과 함께 생성된 JWT를 표시하도록 업데이트됩니다. 이 자습서에서는 토큰을 클립보드에 복사하려면 **[!UICONTROL 생성된 JWT]** 옆에 있는 **[!UICONTROL 복사]**&#x200B;를 선택하십시오.

![](././images/api-authentication/copy-jwt.png)

**액세스 토큰 생성**

JWT를 생성했으면 API 호출에서 사용하여 `{ACCESS_TOKEN}`을(를) 생성할 수 있습니다. `{API_KEY}` 및 `{ORG_ID}`의 값과 달리 Platform API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

**요청**

다음 요청은 페이로드에 제공된 자격 증명을 기반으로 새 `{ACCESS_TOKEN}`을(를) 생성합니다. 이 끝점은 양식 데이터만 페이로드로 허용하므로 `multipart/form-data`의 `Content-Type` 헤더를 지정해야 합니다.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 속성 | 설명 |
| --- | --- |
| `{API_KEY}` | [이전 단계](#api-ims-secret)에서 검색한 `{API_KEY}`([!UICONTROL 클라이언트 ID]). |
| `{SECRET}` | [이전 단계](#api-ims-secret)에서 검색한 클라이언트 암호입니다. |
| `{JWT}` | [이전 단계](#jwt)에서 생성한 JWT. |

>[!NOTE]
>
동일한 API 키, 클라이언트 암호 및 JWT를 사용하여 각 세션에 대한 새 액세스 토큰을 생성할 수 있습니다. 이를 통해 애플리케이션에서 액세스 토큰 생성을 자동화할 수 있습니다.

**응답**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| 속성 | 설명 |
| --- | --- |
| `token_type` | 유형 of 토큰이 반환되고 있습니다. 액세스 토큰의 경우 이 값은 항상 `bearer`입니다. |
| `access_token` | 생성된 `{ACCESS_TOKEN}`. 접두사가 `Bearer`인 이 값은 모든 Platform API 호출에 `Authentication` 헤더로 필요합니다. |
| `expires_in` | 액세스 토큰이 만료될 때까지 남은 시간(밀리초)입니다. 이 값이 0에 도달하면 새 액세스 토큰을 생성해야 Platform API를 계속 사용할 수 있습니다. |

+++

## 액세스 자격 증명 테스트 {#test-credentials}

액세스 토큰, API 키 및 조직 ID 의 세 가지 필수 자격 증명을 모두 수집하면 다음 API 호출을 시도할 수 있습니다. 이 호출은 조직에서 사용할 수 있는 모든 표준 [!DNL Experience Data Model](XDM) 클래스를 나열합니다. [Postman](#use-postman)에서 호출을 가져오고 실행합니다.

>[!BEGINSHADEBOX]

**요청**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
```

**응답**

응답이 아래 표시된 응답과 유사한 경우 자격 증명이 유효하며 작동합니다. 이 응답은 공백으로 잘렸습니다.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
위의 호출로 액세스 자격 증명을 테스트할 수 있지만, 올바른 속성 기반 액세스 제어 권한을 보유하지 않으면 여러 리소스에 액세스하거나 수정할 수 없습니다. 아래의 **필요한 특성 기반 액세스 제어 권한 가져오기** 섹션에서 자세히 알아보세요.

## 필요한 속성 기반 액세스 제어 권한 얻기 {#get-abac-permissions}

Experience Platform 내에서 여러 리소스에 액세스하거나 수정하려면 적절한 액세스 제어 권한이 있어야 합니다. 시스템 관리자는 사용자에게 [필요한 권한](/help/access-control/ui/permissions.md)을 부여할 수 있습니다. [역할에 대한 API 자격 증명 관리](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role)에 대한 섹션에서 자세한 정보를 확인하세요.

시스템 관리자가 API를 통해 Platform 리소스에 액세스하는 데 필요한 권한을 부여하는 방법에 대한 자세한 내용은 아래 비디오 튜토리얼에서도 확인할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## Postman을 사용하여 API 호출 인증 및 테스트 {#use-postman}

[Postman](https://www.postman.com/)은(는) 개발자가 RESTful API를 탐색하고 테스트할 수 있도록 하는 인기 있는 도구입니다. Experience Platform Postman 컬렉션 및 환경을 사용하여 Experience Platform API를 통한 작업 속도를 높일 수 있습니다. [Experience Platform에서 Postman 사용](/help/landing/postman.md) 및 컬렉션 및 환경 시작하기에 대해 자세히 알아보십시오.

Experience Platform 컬렉션 및 환경과 함께 Postman 사용에 대한 자세한 내용은 아래 비디오 튜토리얼에서도 확인할 수 있습니다.

**Experience Platform API에 사용할 Postman 환경을 다운로드하여 가져오기**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**Postman 컬렉션을 사용하여 액세스 토큰을 생성합니다**

[Identity Management 서비스 Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)을 다운로드하고 아래 비디오를 시청하여 액세스 토큰을 생성하는 방법을 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**Experience Platform API Postman 컬렉션을 다운로드하고 API와 상호 작용**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Platform APIs.
-->

## 시스템 관리자: 개발자 및 API 액세스 제어에 Experience Platform 권한 부여 {#grant-developer-and-api-access-control}

Adobe Developer Console에서 통합을 만들려면 먼저 계정에 Experience Platform 제품 프로필에 대한 개발자 및 사용자 권한이 있어야 합니다.

>[!NOTE]
>
시스템 관리자만 권한에서 API 자격 증명을 보고 관리할 수 있습니다.

### 제품 프로필에 개발자 추가 {#add-developers-to-product-profile}

[Admin Console](https://adminconsole.adobe.com/)(으)로 이동하여 Adobe ID으로 로그인합니다.

탐색 모음에서 **[!UICONTROL 제품]**&#x200B;을 선택한 다음 제품 목록에서 **[!UICONTROL Adobe Experience Platform]**&#x200B;을 선택합니다.

![Adobe Experience Platform 제품이 강조 표시된 Adobe Admin Console의 제품 페이지입니다.](././images/api-authentication/products.png)

**[!UICONTROL 제품 프로필]** 탭에서 **[!UICONTROL AEP-Default-All-Users]**&#x200B;를 선택합니다. 또는 검색 창을 사용하여 이름을 입력하여 제품 프로필을 검색합니다.

![검색 창 및 AEP-Default-All-Users 제품이 강조 표시된 제품 프로필 페이지입니다.](././images/api-authentication/select-product-profile.png)

**[!UICONTROL 개발자]** 탭을 선택한 다음 **[!UICONTROL 개발자 추가]**&#x200B;를 선택합니다.

![개발자 추가 옵션이 강조 표시된 개발자 탭이 표시됩니다.](././images/api-authentication/add-developer1.png)

**[!UICONTROL 개발자 추가]** 대화 상자가 나타납니다. 개발자의 **[!UICONTROL 전자 메일 또는 사용자 이름]**&#x200B;을(를) 입력하십시오. 유효한 [!UICONTROL 전자 메일 또는 사용자 이름]이(가) 개발자 세부 정보를 표시합니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![개발자 정보를 입력하고 저장 옵션이 강조 표시된 개발자 추가 대화 상자.](././images/api-authentication/add-developer-email.png)

개발자가 추가되었으며 **[!UICONTROL 개발자]** 탭에 나타납니다.

![새로 추가된 개발자가 강조 표시된 모든 추가된 개발자 목록을 표시하는 개발자 탭입니다.](././images/api-authentication/developer-added.png)

### 역할에 API 자격 증명 할당

>[!NOTE]
>
시스템 관리자만 Experience Platform UI의 역할에 API를 할당할 수 있습니다.

Experience Platform API를 사용하고 작업을 수행하려면 시스템 관리자가 역할에 지정된 권한 집합 외에 API 자격 증명을 추가해야 합니다. [역할에 대한 API 자격 증명 관리](../access-control/abac/ui/permissions.md#manage-api-credentials-for-a-role)에 대한 섹션에서 자세한 정보를 확인하세요.

제품 프로필에 개발자를 추가하고 API를 역할에 할당하기 위해 위에서 설명한 단계에 대한 연습은 아래 비디오 튜토리얼에서도 사용할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)

## 추가 리소스 {#additional-resources}

Experience Platform API를 시작하는 데 도움이 필요하면 아래 연결된 추가 리소스를 참조하십시오

* [Experience Platform API 인증 및 액세스](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=ko) 비디오 튜토리얼 페이지
* 액세스 토큰을 생성하기 위한 [Identity Management 서비스 Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
* [API Postman 컬렉션 Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## 다음 단계 {#next-steps}

이 문서를 읽고 Platform API에 대한 액세스 자격 증명을 수집하고 성공적으로 테스트했습니다. 이제 [설명서](../landing/documentation/overview.md) 전체에서 제공된 예제 API 호출과 함께 따라갈 수 있습니다.

이 자습서에서 수집한 인증 값 외에도 많은 Platform API를 사용하려면 헤더로 올바른 `{SANDBOX_NAME}`을(를) 제공해야 합니다. 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오.
