---
title: Privacy Service API 시작하기
description: 설명서에서 Privacy Service API를 인증하는 방법과 예제 API 호출을 해석하는 방법을 알아봅니다.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Privacy Service API 시작하기

이 안내서에서는 Adobe Experience Platform Privacy Service API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.

## 전제 조건

이 안내서를 사용하려면 의 작업 이해를 필요로 합니다. [Privacy Service](../home.md) 및 을 통해 Adobe Experience Cloud 애플리케이션에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리하는 방법을 설명합니다.

API에 대한 액세스 자격 증명을 만들려면 조직 내의 관리자가 이전에 Adobe Admin Console 내에서 Privacy Service을 위해 제품 프로필을 설정했어야 합니다. API 통합에 할당하는 제품 프로필에 따라 Privacy Service 기능에 액세스할 때 통합이 갖는 권한이 결정됩니다. 다음 안내서를 참조하십시오 [Privacy Service 권한 관리](../permissions.md) 추가 정보.

## 필수 헤더에 대한 값 수집

Privacy Service API를 호출하려면 먼저 필수 헤더에 사용할 액세스 자격 증명을 수집해야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

이러한 값은 다음을 사용하여 생성됩니다 [Adobe Developer 콘솔](https://developer.adobe.com/console). 사용자 `{ORG_ID}` 및 `{API_KEY}` 한 번만 생성하면 되며 향후 API 호출에서 재사용할 수 있습니다. 하지만 `{ACCESS_TOKEN}` 은(는) 임시적이며 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

### 1회 설정

다음으로 이동 [Adobe Developer 콘솔](https://developer.adobe.com/console) Adobe ID으로 로그인합니다. 다음은에 대한 자습서에 설명된 단계를 따릅니다. [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) Developer Console 설명서에서 참조하십시오.

새 프로젝트를 만들었으면 다음을 선택합니다. **[!UICONTROL 프로젝트에 추가]** 및 선택 **[!UICONTROL API]** 드롭다운 메뉴를 통해 액세스합니다.

![에서 선택 중인 API 옵션 [!UICONTROL 프로젝트에 추가] developer Console의 프로젝트 세부 정보 페이지 드롭다운](../images/api/getting-started/add-api-button.png)

#### API 선택 및 키 쌍 생성 {#keypair}

다음 **[!UICONTROL API 추가]** 화면이 나타납니다. 선택 **[!UICONTROL Experience Cloud]** 사용 가능한 API 목록의 범위를 좁히려면 **[!UICONTROL PRIVACY SERVICE API]** 선택하기 전 **[!UICONTROL 다음]**.

![사용 가능한 API 목록에서 선택 중인 Privacy Service API 카드](../images/api/getting-started/add-privacy-service-api.png)

다음 **[!UICONTROL API 구성]** 화면이 나타납니다. 다음 옵션을 선택합니다. **[!UICONTROL 키 쌍 생성]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 키 쌍 생성]**.

![다음 [!UICONTROL 키 쌍 생성] 옵션이에서 선택 중 [!UICONTROL API 구성] 화면](../images/api/getting-started/generate-key-pair.png)

키 쌍이 자동으로 생성되고 개인 키와 공개 인증서가 포함된 ZIP 파일이 브라우저에 의해 다운로드됩니다(이후 단계에서 사용). 계속하려면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![UI에 표시된 키 쌍으로, 브라우저에서 값을 자동으로 다운로드합니다](../images/api/getting-started/key-pair-generated.png)

#### 제품 프로필을 통해 권한 할당 {#product-profiles}

마지막 구성 단계는 이 통합이 권한을 상속할 제품 프로필을 선택하는 것입니다. 프로필을 두 개 이상 선택하면 해당 권한 세트가 통합을 위해 결합됩니다.

>[!NOTE]
>
>제품 프로필과 이들이 제공하는 세분화된 권한은 Adobe Admin Console을 통해 관리자가 만들고 관리합니다. 다음 안내서를 참조하십시오 [Privacy Service 권한](../permissions.md) 추가 정보.

완료되면 다음을 선택합니다. **[!UICONTROL 구성된 API 저장]**.

![구성을 저장하기 전에 목록에서 단일 제품 프로필을 선택합니다.](../images/api/getting-started/select-product-profiles.png)

API가 프로젝트에 추가되면에 프로젝트 페이지가 다시 나타납니다. **Privacy Service API 개요** 페이지를 가리키도록 업데이트하는 중입니다. 여기에서 아래로 스크롤하여 **[!UICONTROL 서비스 계정(JWT)]** 섹션: Privacy Service API에 대한 모든 호출에 필요한 다음 액세스 자격 증명을 제공합니다.

* **[!UICONTROL 클라이언트 ID]**: 클라이언트 ID는 필수입니다 `{API_KEY}` 에 제공해야 합니다. `x-api-key` 머리글입니다.
* **[!UICONTROL 조직 ID]**: 조직 ID는 `{ORG_ID}` 에서 사용해야 하는 값 `x-gw-ims-org-id` 머리글입니다.

![API가 구성된 후 프로젝트 개요 페이지에 표시되는 클라이언트 ID 및 조직 ID 값](../images/api/getting-started/jwt-credentials.png)

### 각 세션에 대한 인증

수집해야 하는 최종 필수 자격 증명은 입니다. `{ACCESS_TOKEN}`: Authorization 헤더에 사용됩니다. 의 값과 다르게 `{API_KEY}` 및 `{ORG_ID}`API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

일반적으로 액세스 토큰을 생성하는 방법에는 두 가지가 있습니다.

* [수동으로 토큰 생성](#manual-token) 테스트 및 개발용.
* [토큰 생성 자동화](#auto-token) API 통합용

#### 수동으로 토큰 생성 {#manual-token}

새 항목을 수동으로 생성하려면 `{ACCESS_TOKEN}`로 이동하여 이전에 다운로드한 개인 키를 열고 컨텐츠를 옆에 있는 텍스트 상자에 붙여넣습니다 **[!UICONTROL 액세스 토큰 생성]** 선택하기 전 **[!UICONTROL 토큰 생성]**.

![이전에 생성된 액세스 토큰을 프로젝트의 개요 페이지에 [!UICONTROL 토큰 생성] 다음 시간 이후에 선택 중인 단추](../images/api/getting-started/paste-private-key.png)

새 액세스 토큰이 생성되고, 토큰을 클립보드에 복사하기 위한 버튼이 제공된다. 이 값은 필수 인증 헤더에 사용되며 형식으로 제공해야 합니다 `Bearer {ACCESS_TOKEN}`.

![UI에서 복사되는 생성된 액세스 토큰](../images/api/getting-started/generated-access-token.png)

#### 토큰 생성 자동화 {#auto-token}

JSON 웹 토큰(JWT)을 POST 요청을 통해 IMS(Identity Management Service) Adobe으로 전송하여 자동화된 프로세스에 대한 새 액세스 토큰을 생성할 수 있습니다. 의 Developer Console 문서를 참조하십시오. [JWT 인증](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 을 참조하십시오.

## 샘플 API 호출 읽기

각 엔드포인트 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) ( Platform API 시작 안내서).

## 다음 단계

사용할 헤더를 이해했으므로 이제 Privacy Service API를 호출할 준비가 되었습니다. 시작하려면 다음 끝점 안내서 중 하나를 선택하십시오.

* [개인 정보 작업](./privacy-jobs.md)
* [동의](./consent.md)
