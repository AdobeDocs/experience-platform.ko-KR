---
title: Reactor API 인증 및 액세스
description: 필요한 액세스 자격 증명을 생성하는 단계를 포함하여 Reactor API를 시작하는 방법에 대해 알아봅니다.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 4%

---

# Reactor API 인증 및 액세스

를 사용하려면 [반응기 API](https://developer.adobe.com/experience-platform-apis/references/reactor/) 태그 확장을 만들고 관리하려면 각 요청에는 다음 인증 헤더가 포함되어야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

이 안내서에서는 Reactor API를 호출할 수 있도록 Adobe Developer 콘솔을 사용하여 이러한 각 헤더에 대한 값을 수집하는 방법을 다룹니다.

## Adobe Experience Platform에 대한 개발자 액세스 권한 얻기 {#gain-developer-access}

Reactor API에 대한 인증 값을 생성하려면 먼저 개발자에게 Experience Platform 액세스 권한이 있어야 합니다. 개발자 액세스 권한을 얻으려면 [Experience Platform 인증 자습서](/help/landing/api-authentication.md). 을(를) 완료하면 [사용자 액세스 권한 얻기](/help/landing/api-authentication.md#gain-user-access) 단계: 이 자습서로 돌아가서 Reactor API와 관련된 자격 증명을 생성합니다.

## 액세스 자격 증명 생성 {#generate-access-credentials}

Adobe Developer 콘솔을 사용하여 다음 세 가지 액세스 자격 증명을 생성해야 합니다.

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

조직의 ID(`{ORG_ID}`) 및 API 키(`{API_KEY}`)는 처음 생성된 후 향후 API 호출에서 재사용할 수 있습니다. 그러나 액세스 토큰(`{ACCESS_TOKEN}`)은 임시이며 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

### 1회 설정 {#one-time-setup}

다음으로 이동 [Adobe Developer 콘솔](https://www.adobe.com/go/devs_console_ui) Adobe ID으로 로그인합니다. 다음은에 대한 자습서에 설명된 단계를 따릅니다. [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) Developer Console 설명서에서 참조하십시오.

프로젝트를 생성했으면 을 선택합니다. **API 추가** 다음에 있음 **프로젝트 개요** 화면.

![](../images/api/getting-started/add-api-button.png)

다음 **API 추가** 화면이 나타납니다. 선택 **EXPERIENCE PLATFORM LAUNCH API** 을(를) 선택하기 전에 사용 가능한 API 목록에서 **다음**.

![](../images/api/getting-started/add-launch-api.png)

그런 다음 인증 유형을 선택하여 액세스 토큰을 생성하고 Experience Platform API에 액세스합니다.

>[!IMPORTANT]
>
>다음 항목 선택 **[!UICONTROL OAuth 서버 간]** 메서드, 즉 이 메서드만 향후 지원됩니다. 다음 **[!UICONTROL 서비스 계정(JWT)]** 메서드가 더 이상 사용되지 않습니다. JWT 인증 방법을 사용하는 통합은 2025년 1월 1일까지 계속 작동하지만, Adobe은 해당 날짜 이전에 기존 통합을 새 OAuth 서버 간 방법으로 마이그레이션할 것을 강력히 권장합니다. 섹션에서 추가 정보 가져오기 [!BADGE 더 이상 사용되지 않음]{type=negative}[JSON 웹 토큰(JWT) 생성](/help/landing/api-authentication.md#jwt) ( 플랫폼 API 인증 튜토리얼 ).

계속하려면 **다음**&#x200B;을 선택합니다.

![OAuth 서버 간 인증 방법을 선택합니다.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

다음 화면에서는 API 통합과 연결할 제품 프로필을 하나 이상 선택하라는 메시지가 표시됩니다.

>[!NOTE]
>
제품 프로필은 Adobe Admin Console을 통해 조직에서 관리하며 세분화된 기능에 대한 특정 권한 세트를 포함합니다. 제품 프로필 및 해당 권한은 조직 내에서 관리자 권한이 있는 사용자만 관리할 수 있습니다. API에 대해 선택할 제품 프로필을 모를 경우 관리자에게 문의하십시오.

목록에서 원하는 제품 프로필을 선택한 다음 를 선택합니다 **구성된 API 저장** 를 클릭하여 API 등록을 완료합니다.

![](../images/api/getting-started/select-product-profile.png)

### 자격 증명 수집 {#gather-credentials}

API가 프로젝트에 추가되면 **[!UICONTROL EXPERIENCE PLATFORM API]** 프로젝트 페이지에는 모든 Experience Platform API 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}` ([!UICONTROL 클라이언트 ID])
* `{ORG_ID}` ([!UICONTROL 조직 ID])

![Developer Console에서 API 추가 후 통합 정보.](/help/tags/images/api/getting-started/api-integration-information.png)

### 액세스 토큰 생성 {#generate-access-token}

다음 단계는 를 생성하는 것입니다. `{ACCESS_TOKEN}` platform API 호출에 사용할 자격 증명입니다. 의 값과 다르게 `{API_KEY}` 및 `{ORG_ID}`Platform API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

>[!TIP]
>
이러한 토큰은 24시간 후에 만료됩니다. 응용 프로그램에 이 통합을 사용하는 경우 응용 프로그램 내에서 전달자 토큰을 프로그래밍 방식으로 가져오는 것이 좋습니다.

사용 사례에 따라 액세스 토큰을 생성하는 두 가지 옵션이 있습니다.

* [토큰 수동 생성](#manual)
* [토큰 생성 자동화](#auto-token)

#### 액세스 토큰 수동으로 생성 {#manual}

새 항목을 수동으로 생성하려면 `{ACCESS_TOKEN}`, 다음으로 이동 **[!UICONTROL 자격 증명]** > **[!UICONTROL OAuth 서버 간]** 및 선택 **[!UICONTROL 액세스 토큰 생성]**&#x200B;아래에 표시된 대로 를 클릭합니다.

![및 액세스 토큰이 Developer Console UI에서 생성되는 방식에 대한 화면 기록입니다.](/help/tags/images/api/getting-started/generate-access-token.gif)

새 액세스 토큰이 생성되고, 토큰을 클립보드에 복사하기 위한 버튼이 제공된다. 이 값은 필수 인증 헤더에 사용되며 형식으로 제공해야 합니다 `Bearer {ACCESS_TOKEN}`.

#### 토큰 생성 자동화 {#auto-token}

Postman 환경 및 컬렉션을 사용하여 액세스 토큰을 생성할 수도 있습니다. 자세한 내용은 다음 섹션을 참조하십시오 [Postman을 사용하여 API 호출 인증 및 테스트](/help/landing/api-authentication.md#use-postman) Experience Platform API 인증 안내서에서 확인할 수 있습니다.

## API 자격 증명 테스트 {#test-api-credentials}

이 자습서의 단계에 따라 다음에 대한 유효한 값이 있어야 합니다. `{ORG_ID}`, `{API_KEY}`, 및 `{ACCESS_TOKEN}`. 이제 Reactor API에 대한 간단한 cURL 요청에서 이러한 값을 사용하여 이러한 값을 테스트할 수 있습니다.

에 대한 API 호출을 시도하여 시작합니다. [모든 회사 나열](./endpoints/companies.md#list).

>[!NOTE]
>
조직에 회사가 없을 수 있으며, 이 경우 응답은 HTTP 상태 404(찾을 수 없음)가 됩니다. 403(사용할 수 없음) 오류가 발생하지 않는 한 액세스 자격 증명이 유효하며 작동합니다.

액세스 자격 증명이 작동하는지 확인한 후 다른 API 참조 설명서를 계속 탐색하여 API의 다양한 기능을 알아보십시오.

## 샘플 API 호출 읽기 {#read-sample-api-calls}

각 엔드포인트 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) ( Platform API 시작 안내서).

## 다음 단계 {#next-steps}

사용할 헤더를 이해했으므로 이제 Reactor API를 호출할 준비가 되었습니다. 시작하려면 다음 끝점 안내서 중 하나를 선택하십시오.

* [Reactor API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Reactor API 안내서 개요](/help/tags/api/overview.md)
