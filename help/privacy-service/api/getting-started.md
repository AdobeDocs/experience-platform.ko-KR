---
title: Privacy Service API 인증 및 액세스
description: 설명서에서 Privacy Service API를 인증하는 방법과 예제 API 호출을 해석하는 방법을 알아봅니다.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 5%

---

# Privacy Service API 인증 및 액세스

이 안내서에서는 Adobe Experience Platform Privacy Service API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.

## 전제 조건 {#prerequisites}

이 안내서를 사용하려면 의 작업 이해를 필요로 합니다. [Privacy Service](../home.md) 및 을 통해 Adobe Experience Cloud 애플리케이션에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리하는 방법을 설명합니다.

API에 대한 액세스 자격 증명을 만들려면 조직 내의 관리자가 이전에 Adobe Admin Console 내에서 Privacy Service을 위해 제품 프로필을 설정했어야 합니다. API 통합에 할당하는 제품 프로필에 따라 Privacy Service 기능에 액세스할 때 통합이 갖는 권한이 결정됩니다. 다음 안내서를 참조하십시오 [Privacy Service 권한 관리](../permissions.md) 추가 정보.

## 필수 헤더에 대한 값 수집 {#gather-values-required-headers}

Privacy Service API를 호출하려면 먼저 필수 헤더에 사용할 액세스 자격 증명을 수집해야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

이러한 값은 다음을 사용하여 생성됩니다 [Adobe Developer 콘솔](https://developer.adobe.com/console). 사용자 `{ORG_ID}` 및 `{API_KEY}` 한 번만 생성하면 되며 향후 API 호출에서 재사용할 수 있습니다. 하지만 `{ACCESS_TOKEN}` 은(는) 임시적이며 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

### 1회 설정 {#one-time-setup}

다음으로 이동 [Adobe Developer 콘솔](https://developer.adobe.com/console) Adobe ID으로 로그인합니다. 다음은에 대한 자습서에 설명된 단계를 따릅니다. [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) Developer Console 설명서에서 참조하십시오.

새 프로젝트를 만들었으면 다음을 선택합니다. **[!UICONTROL 프로젝트에 추가]** 및 선택 **[!UICONTROL API]** 드롭다운 메뉴를 통해 액세스합니다.

![에서 선택 중인 API 옵션 [!UICONTROL 프로젝트에 추가] developer Console의 프로젝트 세부 정보 페이지 드롭다운](../images/api/getting-started/add-api-button.png)

#### Privacy Service API 선택 {#select-privacy-service-api}

다음 **[!UICONTROL API 추가]** 화면이 나타납니다. 선택 **[!UICONTROL Experience Cloud]** 사용 가능한 API 목록의 범위를 좁히려면 **[!UICONTROL PRIVACY SERVICE API]** 선택하기 전 **[!UICONTROL 다음]**.

![사용 가능한 API 목록에서 선택 중인 Privacy Service API 카드](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>다음 항목 선택 **[!UICONTROL 문서 보기]** 별도의 브라우저 창에서 완료로 이동하는 옵션 [Privacy Service API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

그런 다음 인증 유형을 선택하여 액세스 토큰을 생성하고 Privacy Service API에 액세스합니다.

>[!IMPORTANT]
>
>다음 항목 선택 **[!UICONTROL OAuth 서버 간]** 메서드, 즉 이 메서드만 향후 지원됩니다. 다음 **[!UICONTROL 서비스 계정(JWT)]** 메서드가 더 이상 사용되지 않습니다. JWT 인증 방법을 사용하는 통합은 2025년 1월 1일까지 계속 작동하지만, Adobe은 해당 날짜 이전에 기존 통합을 새 OAuth 서버 간 방법으로 마이그레이션할 것을 강력히 권장합니다. 섹션에서 추가 정보 가져오기 [!BADGE 더 이상 사용되지 않음]{type=negative}[JSON 웹 토큰(JWT) 생성](/help/landing/api-authentication.md#jwt).

![Oauth 서버 간 인증 방법을 선택합니다.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### 제품 프로필을 통해 권한 할당 {#product-profiles}

마지막 구성 단계는 이 통합이 권한을 상속할 제품 프로필을 선택하는 것입니다. 프로필을 두 개 이상 선택하면 해당 권한 세트가 통합을 위해 결합됩니다.

>[!NOTE]
>
제품 프로필과 이들이 제공하는 세분화된 권한은 Adobe Admin Console을 통해 관리자가 만들고 관리합니다. 다음 안내서를 참조하십시오 [Privacy Service 권한](../permissions.md) 추가 정보.

완료되면 다음을 선택합니다. **[!UICONTROL 구성된 API 저장]**.

![구성을 저장하기 전에 목록에서 단일 제품 프로필을 선택합니다.](../images/api/getting-started/select-product-profiles.png)

API가 프로젝트에 추가되면 **[!UICONTROL PRIVACY SERVICE API]** 프로젝트 페이지에는 모든 Privacy Service API 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}` ([!UICONTROL 클라이언트 ID])
* `{ORG_ID}` ([!UICONTROL 조직 ID])

![Developer Console에서 API 추가 후 통합 정보.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### 각 세션에 대한 인증 {#authentication-each-session}

수집해야 하는 최종 필수 자격 증명은 입니다. `{ACCESS_TOKEN}`: Authorization 헤더에 사용됩니다. 의 값과 다르게 `{API_KEY}` 및 `{ORG_ID}`API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

일반적으로 액세스 토큰을 생성하는 방법에는 두 가지가 있습니다.

* [수동으로 토큰 생성](#manual-token) 테스트 및 개발용.
* [토큰 생성 자동화](#auto-token) API 통합용

#### 수동으로 토큰 생성 {#manual-token}

새 항목을 수동으로 생성하려면 `{ACCESS_TOKEN}`, 다음으로 이동 **[!UICONTROL 자격 증명]** > **[!UICONTROL OAuth 서버 간]** 및 선택 **[!UICONTROL 액세스 토큰 생성]**&#x200B;아래에 표시된 대로 를 클릭합니다.

![Developer Console UI에서 액세스 토큰이 생성되는 방식에 대한 화면 기록입니다.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

새 액세스 토큰이 생성되고, 토큰을 클립보드에 복사하기 위한 버튼이 제공된다. 이 값은 필수 항목에 사용됩니다. [!DNL Authorization] 헤더 및 를 형식으로 제공해야 합니다. `Bearer {ACCESS_TOKEN}`.

#### 토큰 생성 자동화 {#auto-token}

Postman 환경 및 컬렉션을 사용하여 액세스 토큰을 생성할 수도 있습니다. 자세한 내용은 다음 섹션을 참조하십시오 [Postman을 사용하여 API 호출 인증 및 테스트](/help/landing/api-authentication.md#use-postman) Experience Platform API 인증 안내서에서 확인할 수 있습니다.

## 샘플 API 호출 읽기 {#read-sample-api-calls}

각 엔드포인트 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) ( Platform API 시작 안내서).

## 다음 단계 {#next-steps}

사용할 헤더를 이해했으므로 이제 Privacy Service API를 호출할 준비가 되었습니다. 시작하려면 다음 끝점 안내서 중 하나를 선택하십시오.

* [개인정보 보호 작업](./privacy-jobs.md)
* [동의](./consent.md)
