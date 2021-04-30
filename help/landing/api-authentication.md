---
keywords: Experience Platform;홈;인기 항목;인증;액세스
solution: Experience Platform
title: Experience Platform API 인증 및 액세스
topic-legacy: tutorial
type: Tutorial
description: 이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 7%

---


# Experience Platform API 인증 및 액세스

이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다. 이 자습서가 끝나면 모든 플랫폼 API 호출에 필요한 다음 자격 증명을 생성하게 됩니다.

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

응용 프로그램 및 사용자의 보안을 유지하려면 OAuth 및 JWT(JSON 웹 토큰)와 같은 표준을 사용하여 Adobe I/O API에 대한 모든 요청을 인증하고 인증해야 합니다. JWT는 개인 액세스 토큰을 생성하기 위해 클라이언트별 정보와 함께 사용됩니다.

이 자습서에서는 다음 순서도에 설명된 대로 플랫폼 API 호출을 인증하기 위해 필요한 자격 증명을 수집하는 방법에 대해 설명합니다.

![](./images/api-authentication/authentication-flowchart.png)

## 전제 조건

Experience Platform API를 성공적으로 호출하려면 다음 항목이 있어야 합니다.

* Adobe Experience Platform에 액세스할 수 있는 IMS 조직
* 개발자 및 제품 프로필에 대한 사용자로 추가할 수 있는 Admin Console 관리자

이 튜토리얼을 완료하려면 Adobe ID도 있어야 합니다. Adobe ID이 없는 경우 다음 단계를 사용하여를 만들 수 있습니다.

1. [Adobe 개발자 콘솔](https://console.adobe.io)로 이동합니다.
2. **[!UICONTROL Create a new account]**&#x200B;를 선택합니다.
3. 등록 프로세스를 완료합니다.

## Experience Platform에 대한 개발자 및 사용자 액세스 권한 획득

Adobe 개발자 콘솔에서 통합을 생성하기 전에 계정에 Adobe Admin Console의 Experience Platform 제품 프로필에 대한 개발자 및 사용자 권한이 있어야 합니다.

### 개발자 액세스 권한 얻기

[[!DNL Admin Console]](https://adminconsole.adobe.com/)을(를) 사용하여 Experience Platform 제품 프로필에 개발자로 추가하려면 조직의 [!DNL Admin Console] 관리자에게 문의하십시오. 제품 프로필에 대한 [개발자 액세스 관리 방법에 대한 자세한 지침은 [!DNL Admin Console] 설명서를 참조하십시오](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

개발자로 지정되면 [Adobe 개발자 콘솔](https://www.adobe.com/go/devs_console_ui)에서 통합을 만들 수 있습니다. 이러한 통합은 외부 앱 및 서비스에서 Adobe API로 연결되는 파이프라인입니다.

### 사용자 액세스 권한 얻기

[!DNL Admin Console] 관리자도 사용자를 동일한 제품 프로필에 사용자로 추가해야 합니다. 자세한 내용은  [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html)의 사용자 그룹 관리에 대한 가이드를 참조하십시오.[

## API 키, IMS 조직 ID 및 클라이언트 암호 {#api-ims-secret} 생성

>[!NOTE]
>
>[Privacy Service 개발자 안내서](../privacy-service/api/getting-started.md)에서 이 문서를 팔로우하는 경우 이제 해당 안내서로 돌아가 [!DNL Privacy Service]에 고유한 액세스 자격 증명을 생성할 수 있습니다.

[!DNL Admin Console]을 통해 플랫폼에 대한 개발자 및 사용자 액세스 권한을 부여받은 후 다음 단계는 Adobe 개발자 콘솔에서 `{IMS_ORG}` 및 `{API_KEY}` 자격 증명을 생성하는 것입니다. 이러한 자격 증명은 한 번만 생성되어야 하며 향후 플랫폼 API 호출에서 다시 사용할 수 있습니다.

### 프로젝트에 Experience Platform 추가

[Adobe 개발자 콘솔](https://www.adobe.com/go/devs_console_ui)로 이동하여 Adobe ID으로 로그인합니다. 그런 다음 Adobe 개발자 콘솔 문서에서 [빈 프로젝트](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)를 만드는 자습서에 설명된 단계를 따릅니다.

새 프로젝트를 만들었으면 **[!UICONTROL Project Overview]** 화면에서 **[!UICONTROL Add API]**&#x200B;을 선택합니다.

![](./images/api-authentication/add-api.png)

**[!UICONTROL Add an API]** 화면이 나타납니다. Adobe Experience Platform의 제품 아이콘을 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택하기 전에 **[!UICONTROL Experience Platform API]**&#x200B;을 선택합니다.

![](./images/api-authentication/platform-api.png)

여기서 서비스 계정(JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md)(&quot;API 구성&quot; 단계에서 시작)을 사용하여 프로젝트에 API를 추가하는 [의 튜토리얼에 설명된 단계를 따라 프로세스를 완료합니다.

>[!IMPORTANT]
>
>위에 링크된 프로세스 도중 특정 단계에서 브라우저는 개인 키와 연관된 공개 인증서를 자동으로 다운로드합니다. 이 개인 키는 이 튜토리얼의 이후 단계에서 필요하므로 컴퓨터에 저장되어 있는 위치를 확인합니다.

### 자격 증명 수집

API가 프로젝트에 추가되면 프로젝트의 **[!UICONTROL Experience Platform API]** 페이지에는 Experience Platform API에 대한 모든 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}` ([!UICONTROL Client ID])
* `{IMS_ORG}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

위의 자격 증명 외에도 향후 단계를 위해 생성된 **[!UICONTROL Client Secret]**&#x200B;도 필요합니다. **[!UICONTROL Retrieve client secret]**&#x200B;을 선택하여 값을 표시한 다음 나중에 사용할 수 있도록 복사합니다.

![](././images/api-authentication/client-secret.png)

## JWT(JSON 웹 토큰) {#jwt} 생성

다음 단계는 계정 자격 증명을 기반으로 JWT(JSON 웹 토큰)를 생성하는 것입니다. 이 값은 플랫폼 API 호출에서 사용할 자격 증명을 생성하는 데 사용됩니다. 이 자격 증명은 24시간마다 다시 생성해야 합니다.`{ACCESS_TOKEN}`

왼쪽 탐색 메뉴에서 **[!UICONTROL Service Account (JWT)]**&#x200B;을 선택하고 **[!UICONTROL Generate JWT]**&#x200B;을 선택합니다.

![](././images/api-authentication/generate-jwt.png)

**[!UICONTROL Generate custom JWT]**&#x200B;에 제공된 텍스트 상자에 플랫폼 API를 서비스 계정에 추가할 때 이전에 생성한 개인 키의 내용을 붙여 넣습니다. 그런 다음 **[!UICONTROL Generate Token]**&#x200B;을 선택합니다.

![](././images/api-authentication/paste-key.png)

액세스 토큰을 생성할 수 있는 샘플 cURL 명령과 함께 생성된 JWT를 표시하도록 페이지가 업데이트됩니다. 이 자습서를 사용하려면 **[!UICONTROL Generated JWT]** 옆에 있는 **[!UICONTROL Copy]**&#x200B;을 선택하여 토큰을 클립보드로 복사합니다.

![](././images/api-authentication/copy-jwt.png)

## 액세스 토큰 생성

JWT를 생성했으면 API 호출에서 JWT를 사용하여 `{ACCESS_TOKEN}`을(를) 생성할 수 있습니다. 플랫폼 API를 계속 사용하려면 `{API_KEY}` 및 `{IMS_ORG}`의 값과 달리 24시간마다 새 토큰이 생성되어야 합니다.

**요청**

다음 요청은 페이로드에서 제공하는 자격 증명을 기반으로 새 `{ACCESS_TOKEN}`을 생성합니다. 이 끝점은 양식 데이터를 페이로드로만 수용하므로 `multipart/form-data`의 `Content-Type` 헤더를 제공해야 합니다.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 속성 | 설명 |
| --- | --- |
| `{API_KEY}` | [이전 단계](#api-ims-secret)에서 검색한 `{API_KEY}`([!UICONTROL Client ID]). |
| `{SECRET}` | [이전 단계](#api-ims-secret)에서 검색한 클라이언트 암호입니다. |
| `{JWT}` | [이전 단계](#jwt)에서 생성한 JWT입니다. |

>[!NOTE]
>
>동일한 API 키, 클라이언트 암호 및 JWT를 사용하여 각 세션에 대한 새 액세스 토큰을 생성할 수 있습니다. 애플리케이션에서 액세스 토큰 생성을 자동화할 수 있습니다.

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
| `token_type` | 반환되는 토큰의 유형입니다. 액세스 토큰의 경우 이 값은 항상 `bearer`입니다. |
| `access_token` | 생성된 `{ACCESS_TOKEN}`입니다. 이 값은 `Bearer`이라는 단어와 함께 접두사로 추가되며 모든 플랫폼 API 호출에 대한 `Authentication` 헤더로 필요합니다. |
| `expires_in` | 액세스 토큰이 만료될 때까지 남은 시간(밀리초)입니다. 이 값이 0에 도달하면 플랫폼 API를 계속 사용하려면 새 액세스 토큰을 생성해야 합니다. |

## 액세스 자격 증명 테스트

3개의 필수 자격 증명을 모두 수집했으면 다음 API 호출을 시도할 수 있습니다. 이 호출에는 조직에서 사용할 수 있는 모든 표준 [!DNL Experience Data Model](XDM) 클래스가 나열됩니다.

**요청**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

응답이 아래에 표시된 것과 유사한 경우 자격 증명이 유효하고 작동합니다. 이 응답은 공간에 대해 잘렸습니다.

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

## Postman을 사용하여 API 호출 인증 및 테스트

[Postmanis](https://www.postman.com/) 는 개발자가 RESTful API를 시험해 보고 테스트할 수 있는 널리 사용되는 도구입니다. 이 [중간 게시물](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)에서는 JWT 인증을 자동으로 수행하고 이를 사용하여 플랫폼 API를 사용하는 방법을 설명합니다.

## 다음 단계

이 문서를 읽으면 플랫폼 API에 대한 액세스 자격 증명을 수집하여 테스트했습니다. 이제 [documentation](../landing/documentation/overview.md)에서 제공되는 예제 API 호출과 함께 따를 수 있습니다.

이 튜토리얼에서 수집한 인증 값 외에도 많은 플랫폼 API에서 유효한 `{SANDBOX_NAME}`을 헤더로 제공해야 합니다. 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오.