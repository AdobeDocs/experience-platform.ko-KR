---
keywords: Experience Platform;홈;인기 항목;인증;액세스
solution: Experience Platform
title: Experience Platform API 인증 및 액세스
type: Tutorial
description: 이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: fa4786b081b46c8f3c0030282ae3900891fbd652
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---


# Experience Platform API 인증 및 액세스

이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다. 이 자습서를 마치면 모든 Platform API 호출에 필요한 다음 자격 증명이 생성됩니다.

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

애플리케이션 및 사용자의 보안을 유지하려면 OAuth 및 JSON 웹 토큰(JWT)과 같은 표준을 사용하여 Adobe I/O API에 대한 모든 요청을 인증하고 승인해야 합니다. JWT는 클라이언트별 정보와 함께 개인 액세스 토큰을 생성하는 데 사용됩니다.

이 자습서에서는 다음 순서도에 설명된 대로 Platform API 호출을 인증하는 데 필요한 자격 증명을 수집하는 방법을 다룹니다.

![](./images/api-authentication/authentication-flowchart.png)

## 사전 요구 사항

Experience Platform API를 성공적으로 호출하려면 다음 조건을 충족해야 합니다.

* Adobe Experience Platform에 액세스할 수 있는 조직입니다.
* 귀하를 제품 프로필의 개발자 및 사용자로 추가할 수 있는 Admin Console 관리자.

또한 이 자습서를 완료하려면 Adobe ID이 있어야 합니다. Adobe ID이 없는 경우 다음 단계를 사용하여 만들 수 있습니다.

1. 다음으로 이동 [Adobe Developer 콘솔](https://console.adobe.io).
2. 선택 **[!UICONTROL 새 계정 만들기]**.
3. 등록 프로세스를 완료합니다.

## Experience Platform을 위한 개발자 및 사용자 액세스 권한 획득

Adobe Developer Console에서 통합을 만들기 전에 계정에 Adobe Admin Console의 Experience Platform 제품 프로필에 대한 개발자 및 사용자 권한이 있어야 합니다.

### 개발자 액세스 권한 얻기

다음 연락처로 이동 [!DNL Admin Console] 를 사용하여 귀하를 Experience Platform 제품 프로필에 개발자로 추가할 조직의 관리자 [[!DNL Admin Console]](https://adminconsole.adobe.com/). 다음을 참조하십시오. [!DNL Admin Console] 다음 방법에 대한 특정 지침 설명서 [제품 프로필에 대한 개발자 액세스 관리](https://helpx.adobe.com/kr/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

개발자로 할당되면에서 통합 만들기를 시작할 수 있습니다. [Adobe Developer 콘솔](https://www.adobe.com/go/devs_console_ui). 이러한 통합은 외부 앱 및 서비스에서 Adobe API로의 파이프라인입니다.

### 사용자 액세스 권한 얻기

사용자 [!DNL Admin Console] 관리자가 귀하를 동일한 제품 프로필에 사용자로 추가해야 합니다. 다음 안내서를 참조하십시오 [에서 사용자 그룹 관리 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) 추가 정보.

## API 키, 조직 ID 및 클라이언트 암호 생성 {#api-ims-secret}

>[!NOTE]
>
>에서 이 문서를 팔로우하는 경우 [Privacy Service API 안내서](../privacy-service/api/getting-started.md), 이제 해당 안내서로 돌아가서 고유한 액세스 자격 증명을 생성할 수 있습니다 [!DNL Privacy Service].

을 통해 개발자 및 사용자에게 플랫폼에 대한 액세스 권한이 부여되면 [!DNL Admin Console], 다음 단계는 를 생성하는 것입니다. `{ORG_ID}` 및 `{API_KEY}` Adobe Developer 콘솔의 자격 증명입니다. 이러한 자격 증명은 한 번만 생성하면 되며 향후 Platform API 호출에서 재사용할 수 있습니다.

### 프로젝트에 Experience Platform 추가

다음으로 이동 [Adobe Developer 콘솔](https://www.adobe.com/go/devs_console_ui) Adobe ID으로 로그인합니다. 다음은에 대한 자습서에 설명된 단계를 따릅니다. [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) Adobe Developer 콘솔 설명서에서 확인할 수 있습니다.

새 프로젝트를 만들었으면 다음을 선택합니다. **[!UICONTROL API 추가]** 다음에 있음 **[!UICONTROL 프로젝트 개요]** 화면.

![](./images/api-authentication/add-api.png)

다음 **[!UICONTROL API 추가]** 화면이 나타납니다. Adobe Experience Platform에 대한 제품 아이콘을 선택한 다음 을 선택합니다. **[!UICONTROL EXPERIENCE PLATFORM API]** 선택하기 전 **[!UICONTROL 다음]**.

![](./images/api-authentication/platform-api.png)

다음에서 자습서에 설명된 단계를 따릅니다. [서비스 계정(JWT)을 사용하여 프로젝트에 API 추가](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (&quot;API 구성&quot; 단계부터) 프로세스를 완료합니다.

>[!IMPORTANT]
>
>위에 링크된 프로세스 중 특정 단계에서, 브라우저는 개인 키와 연관된 공개 인증서를 자동으로 다운로드합니다. 이 개인 키는 이 자습서의 이후 단계에서 필요하므로 사용자 컴퓨터에 저장된 위치에 주목하십시오.

### 자격 증명 수집

API가 프로젝트에 추가되면 **[!UICONTROL EXPERIENCE PLATFORM API]** 프로젝트 페이지에는 모든 Experience Platform API 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}` ([!UICONTROL 클라이언트 ID])
* `{ORG_ID}` ([!UICONTROL 조직 ID])

![](././images/api-authentication/api-key-ims-org.png)

위의 자격 증명 외에도 다음을 생성해야 합니다 **[!UICONTROL 클라이언트 암호]** 다음 단계로 넘어갑니다. 선택 **[!UICONTROL 클라이언트 암호 검색]** 을 클릭하여 값을 표시한 다음 복사하여 나중에 사용합니다.

![](././images/api-authentication/client-secret.png)

## JSON 웹 토큰(JWT) 생성 {#jwt}

다음 단계는 계정 자격 증명을 기반으로 JSON 웹 토큰(JWT)을 생성하는 것입니다. 이 값은 다음을 생성하는 데 사용됩니다. `{ACCESS_TOKEN}` platform API 호출에 사용하기 위한 자격 증명으로, 24시간마다 다시 생성해야 합니다.

>[!IMPORTANT]
>
>이 자습서의 목적을 위해 아래 단계에서는 Developer Console 내에서 JWT를 생성하는 방법을 간략하게 설명합니다. 하지만 이 생성 방법은 테스트 및 평가 목적으로만 사용해야 합니다.
>
>일반 사용을 위해 JWT를 자동으로 생성해야 합니다. 프로그래밍 방식으로 JWT를 생성하는 방법에 대한 자세한 내용은 [서비스 계정 인증 안내서](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) Adobe Developer에서

선택 **[!UICONTROL 서비스 계정(JWT)]** 왼쪽 탐색에서 을(를) 선택합니다. **[!UICONTROL JWT 생성]**.

![](././images/api-authentication/generate-jwt.png)

아래에 제공된 텍스트 상자 **[!UICONTROL 사용자 지정 JWT 생성]**&#x200B;에 Platform API를 서비스 계정에 추가할 때 이전에 생성한 개인 키의 컨텐츠를 붙여넣습니다. 그런 다음 을 선택합니다. **[!UICONTROL 토큰 생성]**.

![](././images/api-authentication/paste-key.png)

페이지는 액세스 토큰을 생성할 수 있는 샘플 cURL 명령과 함께 생성된 JWT를 표시하도록 업데이트됩니다. 이 자습서에서는 다음을 선택하십시오. **[!UICONTROL 복사]** 다음에 **[!UICONTROL 생성된 JWT]** 토큰을 클립보드에 복사합니다.

![](././images/api-authentication/copy-jwt.png)

## 액세스 토큰 생성

JWT를 생성했으면 API 호출에서 사용하여 다음을 생성할 수 있습니다. `{ACCESS_TOKEN}`. 의 값과 다르게 `{API_KEY}` 및 `{ORG_ID}`Platform API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

**요청**

다음 요청은 새 를 생성합니다 `{ACCESS_TOKEN}` 페이로드에 제공된 자격 증명을 기반으로 합니다. 이 끝점은 양식 데이터만 페이로드로 허용하므로 값을 지정해야 합니다. `Content-Type` 헤더 `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 속성 | 설명 |
| --- | --- |
| `{API_KEY}` | 다음 `{API_KEY}` ([!UICONTROL 클라이언트 ID])에서 검색한 값 [이전 단계](#api-ims-secret). |
| `{SECRET}` | 에서 검색한 클라이언트 암호 [이전 단계](#api-ims-secret). |
| `{JWT}` | 에서 생성한 JWT [이전 단계](#jwt). |

>[!NOTE]
>
>동일한 API 키, 클라이언트 암호 및 JWT를 사용하여 각 세션에 대한 새 액세스 토큰을 생성할 수 있습니다. 이를 통해 애플리케이션에서 액세스 토큰 생성을 자동화할 수 있습니다.

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
| `token_type` | 반환되는 토큰의 유형입니다. 액세스 토큰의 경우 이 값은 항상 입니다 `bearer`. |
| `access_token` | 생성됨 `{ACCESS_TOKEN}`. 이 값, 단어 접두사 `Bearer`은(는) (으)로 필요합니다. `Authentication` 모든 플랫폼 API 호출에 대한 헤더입니다. |
| `expires_in` | 액세스 토큰이 만료될 때까지 남은 시간(밀리초)입니다. 이 값이 0에 도달하면 새 액세스 토큰을 생성해야 Platform API를 계속 사용할 수 있습니다. |

## 액세스 자격 증명 테스트

세 개의 필수 자격 증명을 모두 수집했으면 다음 API 호출을 시도할 수 있습니다. 이 호출은 모든 표준을 나열합니다. [!DNL Experience Data Model] 조직에서 사용할 수 있는 (XDM) 클래스.

**요청**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

## Postman을 사용하여 API 호출 인증 및 테스트

[Postman](https://www.postman.com/) 는 개발자가 RESTful API를 탐색하고 테스트할 수 있도록 하는 인기 있는 도구입니다. 이 [중간 게시물](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Postman을 설정하여 JWT 인증을 자동으로 수행하고 이를 사용하여 Platform API를 사용하는 방법에 대해 설명합니다.

## Experience Platform 권한을 사용하여 개발자 및 API 액세스 제어

>[!NOTE]
>
>시스템 관리자만 권한에서 API 자격 증명을 보고 관리할 수 있습니다.

Adobe Developer Console에서 통합을 만들기 전에 계정에 Adobe Admin Console의 Experience Platform 제품 프로필에 대한 개발자 및 사용자 권한이 있어야 합니다.

### 제품 프로필에 개발자 추가

[[!DNL Admin Console]](https://adminconsole.adobe.com/)으로 이동한 뒤 Adobe ID로 로그인합니다.

선택 **[!UICONTROL 제품]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL Adobe Experience Platform]** 을 클릭합니다.

![Admin Console의 제품 목록](././images/api-authentication/products.png)

다음에서 **[!UICONTROL 제품 프로필]** 탭, 선택 **[!UICONTROL AEP-Default-All-Users]**. 또는 검색 창을 사용하여 이름을 입력하여 제품 프로필을 검색합니다.

![제품 프로필 검색](././images/api-authentication/select-product-profile.png)

다음 항목 선택 **[!UICONTROL 개발자]** 탭을 선택한 다음 를 선택합니다 **[!UICONTROL 개발자 추가]**.

![개발자 탭에서 개발자 추가](././images/api-authentication/add-developer1.png)

개발자 입력 **[!UICONTROL 이메일 또는 사용자 이름]**. 유효 [!UICONTROL 이메일 또는 사용자 이름] 개발자 세부 사항이 표시됩니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![이메일 또는 사용자 이름을 사용하여 개발자 추가](././images/api-authentication/add-developer-email.png)

개발자가 추가되고에 표시됩니다. [!UICONTROL 개발자] 탭.

![개발자 탭에 나열된 개발자](././images/api-authentication/developer-added.png)

### API 설정

개발자는 Adobe Developer 콘솔에서 프로젝트 내에 API를 추가하고 구성할 수 있습니다.

프로젝트를 선택한 다음 을 선택합니다. **[!UICONTROL API 추가]**.

![프로젝트에 API 추가](././images/api-authentication/add-api-project.png)

다음에서 **[!UICONTROL API 추가]** 대화 상자 선택 **[!UICONTROL Adobe Experience Platform]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL EXPERIENCE PLATFORM API]**.

![Experience Platform에 API 추가](././images/api-authentication/add-api-platform.png)

다음에서 **[!UICONTROL API 구성]** 화면, 선택 **[!UICONTROL AEP-Default-All-Users]**.

### 역할에 API 할당

시스템 관리자는 Experience Platform UI의 역할에 API를 할당할 수 있습니다.

선택 **[!UICONTROL 권한]** API를 추가할 역할입니다. 다음 항목 선택 **[!UICONTROL API 자격 증명]** 탭을 선택한 다음 를 선택합니다 **[!UICONTROL API 자격 증명 추가]**.

![선택한 역할의 API 자격 증명 탭](././images/api-authentication/api-credentials.png)

역할에 추가할 API를 선택한 다음 를 선택합니다 **[!UICONTROL 저장]**.

![선택할 수 있는 API 목록](././images/api-authentication/select-api.png)

(으)로 돌아갑니다. [!UICONTROL API 자격 증명] 새로 추가된 API가 나열된 탭입니다.

![새로 추가된 API가 있는 API 자격 증명 탭](././images/api-authentication/api-credentials-with-added-api.png)

## 다음 단계

이 문서를 읽고 Platform API에 대한 액세스 자격 증명을 수집하고 성공적으로 테스트했습니다. 이제 를 통해 제공되는 예제 API 호출과 함께 따를 수 있습니다. [설명서](../landing/documentation/overview.md).

이 자습서에서 수집한 인증 값 외에도 많은 Platform API에 유효한 값이 필요합니다 `{SANDBOX_NAME}` 헤더로 제공될 예정입니다. 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오.