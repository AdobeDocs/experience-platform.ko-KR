---
title: Privacy Service API 시작하기
description: Privacy Service API를 인증하는 방법과 설명서에서 예제 API 호출을 해석하는 방법을 알아봅니다.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Privacy Service API 시작

이 안내서에서는 Adobe Experience Platform Privacy Service API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.

## 전제 조건

이 안내서에서는 다음 사항을 이해하고 있어야 합니다 [Privacy Service](../home.md) 또한 Adobe Experience Cloud 애플리케이션에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리하는 방법을 사용할 수 있습니다.

API에 대한 액세스 자격 증명을 만들기 위해 조직 내의 관리자가 이전에 Adobe Admin Console 내의 Privacy Service에 대한 제품 프로필을 설정했어야 합니다. API 통합에 지정하는 제품 프로필은 Privacy Service 기능에 액세스할 때 통합이 가지고 있는 권한을 결정합니다. 다음 안내서를 참조하십시오. [Privacy Service 권한 관리](../permissions.md) 추가 정보.

## 필수 헤더에 대한 값을 수집합니다

Privacy Service API를 호출하려면 먼저 필수 헤더에서 사용할 액세스 자격 증명을 수집해야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

이러한 값은 [Adobe Developer 콘솔](https://developer.adobe.com/console). 사용자 `{ORG_ID}` 및 `{API_KEY}` 한 번만 생성하면 되고 향후 API 호출에서 다시 사용할 수 있습니다. 그러나, `{ACCESS_TOKEN}` 는 일시적이며 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

### 1회 설정

이동 [Adobe Developer 콘솔](https://developer.adobe.com/console) Adobe ID으로 로그인합니다. 다음으로, 다음의 자습서에 설명된 단계를 수행합니다 [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 개발자 콘솔 설명서에서 를 참조하십시오.

새 프로젝트를 만든 후 **[!UICONTROL 프로젝트에 추가]** 및 **[!UICONTROL API]** 드롭다운 메뉴에서 을 클릭합니다.

![API 옵션은 [!UICONTROL 프로젝트에 추가] 개발자 콘솔의 프로젝트 세부 사항 페이지에서 드롭다운](../images/api/getting-started/add-api-button.png)

#### API를 선택하고 키 쌍을 생성합니다 {#keypair}

다음 **[!UICONTROL API 추가]** 화면이 나타납니다. 선택 **[!UICONTROL Experience Cloud]** 사용 가능한 API 목록 범위를 좁히려면 **[!UICONTROL Privacy Service API]** 선택하기 전에 **[!UICONTROL 다음]**.

![사용 가능한 API 목록에서 선택되는 Privacy Service API 카드](../images/api/getting-started/add-privacy-service-api.png)

다음 **[!UICONTROL API 구성]** 화면이 나타납니다. 옵션을 선택하여 **[!UICONTROL 키 쌍 생성]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 키 쌍 생성]**.

![다음 [!UICONTROL 키 쌍 생성] 선택 [!UICONTROL API 구성] screen](../images/api/getting-started/generate-key-pair.png)

키 쌍은 자동으로 생성되며 개인 키 및 공개 인증서가 포함된 ZIP 파일은 브라우저에 의해 다운로드됩니다(나중에 사용하기 위해). 선택 **[!UICONTROL 다음]** 계속하십시오.

![브라우저에 의해 값이 자동으로 다운로드되는 UI에 표시되는 생성된 키 쌍](../images/api/getting-started/key-pair-generated.png)

#### 제품 프로필을 통해 권한 할당 {#product-profiles}

최종 구성 단계는 이 통합이 해당 권한을 상속할 제품 프로필을 선택하는 것입니다. 두 개 이상의 프로필을 선택하면 해당 권한 세트가 통합을 위해 결합됩니다.

>[!NOTE]
>
>제품 프로필 및 세분화된 권한은 Adobe Admin Console을 통해 관리자가 만들고 관리합니다. 다음 안내서를 참조하십시오. [Privacy Service 권한](../permissions.md) 추가 정보.

완료되면 을 선택합니다 **[!UICONTROL 구성된 API 저장]**.

![구성을 저장하기 전에 목록에서 선택되는 단일 제품 프로필](../images/api/getting-started/select-product-profiles.png)

프로젝트에 API가 추가되면 프로젝트 페이지가 다시 **Privacy Service API 개요** 페이지. 여기에서 아래로 스크롤하여 **[!UICONTROL 서비스 계정(JWT)]** 섹션, Privacy Service API에 대한 모든 호출에 필요한 다음 액세스 자격 증명을 제공합니다.

* **[!UICONTROL 클라이언트 ID]**: 클라이언트 ID는 필수입니다 `{API_KEY}` 다음에으로 제공해야 합니다. `x-api-key` 헤더.
* **[!UICONTROL 조직 ID]**: 조직 ID는 `{ORG_ID}` 에 사용해야 하는 값 `x-gw-ims-org-id` 헤더.

![클라이언트 ID 및 조직 ID 값은 API가 구성된 후 프로젝트 개요 페이지에 표시됩니다](../images/api/getting-started/jwt-credentials.png)

### 각 세션에 대한 인증

수집해야 하는 최종 필수 자격 증명은 `{ACCESS_TOKEN}`: Authorization 헤더에 사용됩니다. 에 대한 값과 달리 `{API_KEY}` 및 `{ORG_ID}`를 지정하는 경우 API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

일반적으로 액세스 토큰을 생성하는 방법에는 두 가지가 있습니다.

* [수동으로 토큰 생성](#manual-token) 테스트 및 개발 용도로 사용됩니다.
* [토큰 생성 자동화](#auto-token) API 통합을 위한 것입니다.

#### 수동으로 토큰 생성 {#manual-token}

새 `{ACCESS_TOKEN}`앞에서 다운로드한 개인 키를 열고 옆에 있는 텍스트 상자에 내용을 붙여 넣습니다. **[!UICONTROL 액세스 토큰 생성]** 선택하기 전에 **[!UICONTROL 토큰 생성]**.

![프로젝트의 개요 페이지에 붙여넣을 이전에 생성한 액세스 토큰을 다음과 같이 사용하여 [!UICONTROL 토큰 생성] 단추 선택 후](../images/api/getting-started/paste-private-key.png)

새 액세스 토큰이 생성되고 토큰을 클립보드에 복사하는 단추가 제공됩니다. 이 값은 필요한 인증 헤더에 사용되며 형식으로 제공해야 합니다 `Bearer {ACCESS_TOKEN}`.

![UI에서 복사되는 생성된 액세스 토큰](../images/api/getting-started/generated-access-token.png)

#### 토큰 생성 자동화 {#auto-token}

IMS(Identity Management Service)에 대한 POST 요청을 통해 JSON 웹 토큰(JWT)을 전송하여 자동화된 프로세스에 대한 새 액세스 토큰을 생성할 수 있습니다. 다음에서 개발자 콘솔 문서를 참조하십시오. [JWT 인증](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 자세한 단계.

## 샘플 API 호출 읽기

각 엔드포인트 안내서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) 플랫폼 API에 대한 시작 안내서에서 를 참조하십시오.

## 다음 단계

이제 사용할 헤더를 이해하므로 Privacy Service API를 호출할 준비가 되었습니다. 시작할 엔드포인트 가이드 중 하나를 선택합니다.

* [개인 정보 작업](./privacy-jobs.md)
* [동의](./consent.md)
