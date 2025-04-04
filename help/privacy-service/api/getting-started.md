---
title: Privacy Service API 인증 및 액세스
description: 설명서에서 Privacy Service API를 인증하는 방법과 예제 API 호출을 해석하는 방법을 알아봅니다.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 5%

---

# Privacy Service API 인증 및 액세스

이 안내서에서는 Adobe Experience Platform Privacy Service API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.

## 전제 조건 {#prerequisites}

이 안내서를 사용하려면 [Privacy Service](../home.md)과(와) Adobe Experience Cloud 응용 프로그램에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리하는 방법에 대해 이해하고 있어야 합니다.

API에 대한 액세스 자격 증명을 만들려면 조직 내의 관리자가 이전에 Adobe Admin Console 내에서 Privacy Service에 대한 제품 프로필을 설정했어야 합니다. API 통합에 할당하는 제품 프로필에 따라 Privacy Service 기능에 액세스할 때 통합이 갖는 권한이 결정됩니다. 자세한 내용은 [Privacy Service 권한 관리](../permissions.md)에 대한 안내서를 참조하십시오.

## 필수 헤더에 대한 값 수집 {#gather-values-required-headers}

Privacy Service API를 호출하려면 먼저 필수 헤더에 사용할 액세스 자격 증명을 수집해야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

이러한 값은 [Adobe Developer Console](https://developer.adobe.com/console)을(를) 사용하여 생성됩니다. `{ORG_ID}` 및 `{API_KEY}`은(는) 한 번만 생성하면 되며 이후 API 호출에서 재사용할 수 있습니다. 그러나 `{ACCESS_TOKEN}`은(는) 임시이며 24시간마다 다시 생성되어야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

### 1회 설정 {#one-time-setup}

[Adobe Developer Console](https://developer.adobe.com/console)&#x200B;(으)로 이동하여 Adobe ID으로 로그인합니다. 그런 다음 Developer Console 설명서에서 [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)에 대한 자습서에 설명된 단계를 수행합니다.

새 프로젝트를 만든 후에는 **[!UICONTROL 프로젝트에 추가]**&#x200B;를 선택하고 드롭다운 메뉴에서 **[!UICONTROL API]**&#x200B;을(를) 선택하십시오.

![Developer Console의 프로젝트 세부 정보 페이지에 있는 [!UICONTROL 프로젝트에 추가] 드롭다운에서 API 옵션을 선택하고](../images/api/getting-started/add-api-button.png)

#### Privacy Service API 선택 {#select-privacy-service-api}

**[!UICONTROL API 추가]** 화면이 나타납니다. **[!UICONTROL 다음]**&#x200B;을(를) 선택하기 전에 **[!UICONTROL Experience Cloud]**&#x200B;을(를) 선택하여 사용 가능한 API 목록을 줄인 다음 **[!UICONTROL Privacy Service API]**&#x200B;에 대한 카드를 선택하십시오.

![사용 가능한 API 목록에서 Privacy Service API 카드를 선택하고 있습니다](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>**[!UICONTROL 문서 보기]** 옵션을 선택하여 별도의 브라우저 창에서 전체 [Privacy Service API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/privacy-service/)로 이동합니다.

그런 다음 인증 유형을 선택하여 액세스 토큰을 생성하고 Privacy Service API에 액세스합니다.

>[!IMPORTANT]
>
>**[!UICONTROL OAuth Server-to-Server]** 메서드를 선택하십시오. 이 메서드는 앞으로 지원되는 유일한 메서드입니다. **[!UICONTROL 서비스 계정(JWT)]** 메서드가 더 이상 사용되지 않습니다. JWT 인증 방법을 사용하는 통합은 2025년 1월 1일까지 계속 작동하지만, Adobe에서는 해당 날짜 이전에 기존 통합을 새로운 OAuth 서버 간 방법으로 마이그레이션할 것을 강력히 권장합니다. [!BADGE 사용되지 않음] 섹션에서 자세한 정보를 확인하세요.{type=negative}[JSON 웹 토큰(JWT) 생성](/help/landing/api-authentication.md#jwt).

![Oauth 서버 간 인증 방법을 선택하십시오.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### 제품 프로필을 통해 권한 할당 {#product-profiles}

마지막 구성 단계는 이 통합이 권한을 상속할 제품 프로필을 선택하는 것입니다. 프로필을 두 개 이상 선택하면 해당 권한 세트가 통합을 위해 결합됩니다.

>[!NOTE]
>
제품 프로필과 이들이 제공하는 세분화된 권한은 Adobe Admin Console을 통해 관리자가 만들고 관리합니다. 자세한 내용은 [Privacy Service 권한](../permissions.md)에 대한 안내서를 참조하십시오.

완료되면 **[!UICONTROL 구성된 API 저장]**&#x200B;을 선택합니다.

![구성을 저장하기 전에 목록에서 단일 제품 프로필을 선택하고 있습니다](../images/api/getting-started/select-product-profiles.png)

API가 프로젝트에 추가되면 프로젝트에 대한 **[!UICONTROL Privacy Service API]** 페이지에 Privacy Service API에 대한 모든 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}`([!UICONTROL 클라이언트 ID])
* `{ORG_ID}`([!UICONTROL 조직 ID])

![Developer Console에서 API를 추가한 후의 통합 정보.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### 각 세션에 대한 인증 {#authentication-each-session}

수집해야 하는 최종 필수 자격 증명은 인증 헤더에 사용되는 `{ACCESS_TOKEN}`입니다. `{API_KEY}` 및 `{ORG_ID}`의 값과 달리 API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

일반적으로 액세스 토큰을 생성하는 방법에는 두 가지가 있습니다.

* 테스트 및 개발을 위해 [토큰을 수동으로 생성](#manual-token).
* API 통합을 위해 [토큰 생성을 자동화합니다](#auto-token).

#### 수동으로 토큰 생성 {#manual-token}

새 `{ACCESS_TOKEN}`을(를) 수동으로 생성하려면 아래 표시된 대로 **[!UICONTROL 자격 증명]** > **[!UICONTROL OAuth 서버 간]**&#x200B;으로 이동한 다음 **[!UICONTROL 액세스 토큰 생성]**&#x200B;을 선택하십시오.

![Developer Console UI에서 액세스 토큰을 생성하는 방법에 대한 화면 기록입니다.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

새 액세스 토큰이 생성되고, 토큰을 클립보드에 복사하기 위한 버튼이 제공된다. 이 값은 필수 [!DNL Authorization] 헤더에 사용되며 `Bearer {ACCESS_TOKEN}` 형식으로 제공해야 합니다.

#### 토큰 생성 자동화 {#auto-token}

Postman 환경 및 컬렉션을 사용하여 액세스 토큰을 생성할 수도 있습니다. 자세한 내용은 Experience Platform API 인증 안내서에서 [Postman을 사용하여 API 호출 인증 및 테스트](/help/landing/api-authentication.md#use-postman)에 대한 섹션을 참조하십시오.

## 샘플 API 호출 읽기 {#read-sample-api-calls}

각 엔드포인트 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform API 시작 안내서의 [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api)에 대한 섹션을 참조하십시오.

## 다음 단계 {#next-steps}

사용할 헤더를 이해했으므로 이제 Privacy Service API를 호출할 준비가 되었습니다. 시작하려면 다음 끝점 안내서 중 하나를 선택하십시오.

* [개인정보 보호 작업](./privacy-jobs.md)
* [동의](./consent.md)
