---
title: Reactor API 인증 및 액세스
description: 필요한 액세스 자격 증명을 생성하는 단계를 포함하여 Reactor API를 시작하는 방법에 대해 알아봅니다.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 31e52dce23c558aaba822fe27d2e58ed6a7ce18d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 3%

---

# Reactor API 인증 및 액세스

[Reactor API](https://developer.adobe.com/experience-platform-apis/references/reactor/)을(를) 사용하여 Tags 확장을 만들고 관리하려면 각 요청에 다음 인증 헤더가 포함되어야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`
* `Accept: application/vnd.api+json;revision=1`
* `Content-Type: application/vnd.api+json`

이 안내서에서는 Reactor API를 호출할 수 있도록 Adobe Developer Console을 사용하여 이러한 각 헤더에 대한 값을 수집하는 방법을 다룹니다.

## Adobe Experience Platform에 대한 개발자 액세스 권한 얻기 {#gain-developer-access}

Reactor API에 대한 인증 값을 생성하려면 먼저 개발자에게 Experience Platform에 대한 액세스 권한이 있어야 합니다. 개발자 액세스 권한을 얻으려면 [Experience Platform 인증 자습서](/help/landing/api-authentication.md)의 시작 단계를 따르십시오. [사용자 액세스 권한 획득](/help/landing/api-authentication.md#gain-user-access) 단계를 완료했으면 이 자습서로 돌아가서 Reactor API와 관련된 자격 증명을 생성합니다.

## 액세스 자격 증명 생성 {#generate-access-credentials}

Adobe Developer Console을 사용하여 다음 세 가지 액세스 자격 증명을 생성해야 합니다.

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

조직의 ID(`{ORG_ID}`) 및 API 키(`{API_KEY}`)는 처음 생성된 후 향후 API 호출에서 다시 사용할 수 있습니다. 그러나 액세스 토큰(`{ACCESS_TOKEN}`)은 임시이므로 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

### 1회 설정 {#one-time-setup}

[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)&#x200B;(으)로 이동하여 Adobe ID으로 로그인합니다. 그런 다음 Developer Console 설명서에서 [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)에 대한 자습서에 설명된 단계를 수행합니다.

프로젝트를 만든 후에는 **프로젝트 개요** 화면에서 **API 추가**&#x200B;를 선택합니다.

![](../images/api/getting-started/add-api-button.png)

**API 추가** 화면이 나타납니다. **다음**&#x200B;을(를) 선택하기 전에 사용 가능한 API 목록에서 **Experience Platform Launch API**&#x200B;을(를) 선택하십시오.

![](../images/api/getting-started/add-launch-api.png)

그런 다음 인증 유형을 선택하여 액세스 토큰을 생성하고 Experience Platform API에 액세스합니다.

>[!IMPORTANT]
>
>**[!UICONTROL OAuth Server-to-Server]** 메서드를 선택하십시오. 이 메서드는 앞으로 지원되는 유일한 메서드입니다. **[!UICONTROL 서비스 계정(JWT)]** 메서드가 더 이상 사용되지 않습니다. JWT 인증 방법을 사용하는 통합은 2025년 1월 1일까지 계속 작동하지만, Adobe에서는 해당 날짜 이전에 기존 통합을 새로운 OAuth 서버 간 방법으로 마이그레이션할 것을 강력히 권장합니다. Experience Platform API 인증 자습서에서 [!BADGE 사용되지 않음]{type=negative} [JSON 웹 토큰(JWT) 생성](/help/landing/api-authentication.md#jwt) 섹션에 대한 자세한 내용을 확인하십시오.

계속하려면 **다음**&#x200B;을 선택합니다.

![OAuth 서버 간 인증 방법을 선택하십시오.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

다음 화면에서는 API 통합과 연결할 제품 프로필을 하나 이상 선택하라는 메시지가 표시됩니다.

>[!NOTE]
>
>제품 프로필은 Adobe Admin Console을 통해 조직에서 관리하며 세분화된 기능에 대한 특정 권한 세트를 포함합니다. 제품 프로필 및 해당 권한은 조직 내에서 관리자 권한이 있는 사용자만 관리할 수 있습니다. API에 대해 선택할 제품 프로필을 모를 경우 관리자에게 문의하십시오.

목록에서 원하는 제품 프로필을 선택한 다음 **구성된 API 저장**&#x200B;을 선택하여 API 등록을 완료합니다.

![](../images/api/getting-started/select-product-profile.png)

### 자격 증명 수집 {#gather-credentials}

API가 프로젝트에 추가되면 프로젝트에 대한 **[!UICONTROL Experience Platform API]** 페이지에 Experience Platform API에 대한 모든 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}`([!UICONTROL 클라이언트 ID])
* `{ORG_ID}`([!UICONTROL 조직 ID])

![Developer Console에서 API를 추가한 후의 통합 정보.](/help/tags/images/api/getting-started/api-integration-information.png)

### 액세스 토큰 생성 {#generate-access-token}

다음 단계는 Experience Platform API 호출에 사용할 `{ACCESS_TOKEN}` 자격 증명을 생성하는 것입니다. `{API_KEY}` 및 `{ORG_ID}`의 값과 달리 Experience Platform API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

>[!TIP]
>
>이러한 토큰은 24시간 후에 만료됩니다. 응용 프로그램에 이 통합을 사용하는 경우 응용 프로그램 내에서 전달자 토큰을 프로그래밍 방식으로 가져오는 것이 좋습니다.

사용 사례에 따라 액세스 토큰을 생성하는 두 가지 옵션이 있습니다.

* [토큰 수동 생성](#manual)
* [토큰 생성 자동화](#auto-token)

#### 액세스 토큰 수동으로 생성 {#manual}

새 `{ACCESS_TOKEN}`을(를) 수동으로 생성하려면 아래 표시된 대로 **[!UICONTROL 자격 증명]** > **[!UICONTROL OAuth 서버 간]**&#x200B;으로 이동한 다음 **[!UICONTROL 액세스 토큰 생성]**&#x200B;을 선택하십시오.

![Developer Console UI에서 및 액세스 토큰을 생성하는 방법에 대한 화면 기록입니다.](/help/tags/images/api/getting-started/generate-access-token.gif)

새 액세스 토큰이 생성되고, 토큰을 클립보드에 복사하기 위한 버튼이 제공된다. 이 값은 필요한 인증 헤더에 사용되며 `Bearer {ACCESS_TOKEN}` 형식으로 제공해야 합니다.

#### 토큰 생성 자동화 {#auto-token}

Postman 환경 및 컬렉션을 사용하여 액세스 토큰을 생성할 수도 있습니다. 자세한 내용은 Experience Platform API 인증 안내서에서 [Postman을 사용하여 API 호출 인증 및 테스트](/help/landing/api-authentication.md#use-postman)에 대한 섹션을 참조하십시오.

## API 자격 증명 테스트 {#test-api-credentials}

이 자습서의 단계에 따라 `{ORG_ID}`, `{API_KEY}` 및 `{ACCESS_TOKEN}`에 대해 유효한 값을 가져야 합니다. 이제 Reactor API에 대한 간단한 cURL 요청에서 이러한 값을 사용하여 이러한 값을 테스트할 수 있습니다.

먼저 [모든 회사를 나열](./endpoints/companies.md#list)하기 위한 API 호출을 시도합니다.

>[!NOTE]
>
>조직에 회사가 없을 수 있으며, 이 경우 응답은 HTTP 상태 404(찾을 수 없음)가 됩니다. 403(사용할 수 없음) 오류가 발생하지 않는 한 액세스 자격 증명이 유효하며 작동합니다.

액세스 자격 증명이 작동하는지 확인한 후 다른 API 참조 설명서를 계속 탐색하여 API의 다양한 기능을 알아보십시오.

## 샘플 API 호출 읽기 {#read-sample-api-calls}

각 엔드포인트 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform API 시작 안내서의 [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api)에 대한 섹션을 참조하십시오.

## 다음 단계 {#next-steps}

사용할 헤더를 이해했으므로 이제 Reactor API를 호출할 준비가 되었습니다. 시작하려면 다음 끝점 안내서 중 하나를 선택하십시오.

* [Reactor API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Reactor API 안내서 개요](/help/tags/api/overview.md)
