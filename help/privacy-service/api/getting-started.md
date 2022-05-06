---
title: Privacy Service API 시작하기
description: Privacy Service API를 인증하는 방법과 설명서에서 예제 API 호출을 해석하는 방법을 알아봅니다.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 1%

---

# Privacy Service API 시작

이 안내서에서는 Privacy Service API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.

## 전제 조건

이 안내서에서는 다음 기능을 이해하고 있어야 합니다.

* [Adobe Experience Platform Privacy Service](../home.md): Adobe Experience Cloud 애플리케이션에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다.

## 필수 헤더에 대한 값을 수집합니다

Privacy Service API를 호출하려면 먼저 필수 헤더에서 사용할 액세스 자격 증명을 수집해야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

이 작업에는 Adobe Admin Console에서 Adobe Experience Platform에 대한 개발자 권한을 가져온 다음 Adobe Developer 콘솔에서 자격 증명을 생성하는 작업이 포함됩니다.

### 개발자에게 Experience Platform 액세스 권한 얻기

개발자 액세스 권한을 얻으려면 [!DNL Platform]에서 의 시작 단계를 따릅니다. [Experience Platform 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). &quot;Adobe Developer 콘솔에서 액세스 자격 증명 생성&quot; 단계에 도달하면 이 자습서로 돌아가 Privacy Service과 관련된 자격 증명을 생성합니다.

### 액세스 자격 증명 생성

Adobe Developer 콘솔을 사용하여 다음 세 가지 액세스 자격 증명을 생성해야 합니다.

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

사용자 `{ORG_ID}` 및 `{API_KEY}` 한 번만 생성하면 되고 향후 API 호출에서 다시 사용할 수 있습니다. 그러나, `{ACCESS_TOKEN}` 는 일시적이며 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

#### 1회 설정

이동 [Adobe 개발자 콘솔](https://www.adobe.com/go/devs_console_ui) Adobe ID으로 로그인합니다. 다음으로, 다음의 자습서에 설명된 단계를 수행합니다 [빈 프로젝트 만들기](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 를 클릭하십시오.

새 프로젝트를 만든 후 **[!UICONTROL API 추가]** on **[!UICONTROL 프로젝트 개요]** 화면.

![](../images/api/getting-started/add-api-button.png)

다음 **[!UICONTROL API 추가]** 화면이 나타납니다. 선택 **[!UICONTROL Privacy Service API]** 선택하기 전에 사용 가능한 API 목록에서 **[!UICONTROL 다음]**.

![](../images/api/getting-started/add-privacy-service-api.png)

다음 **[!UICONTROL API 구성]** 화면이 나타납니다. 옵션을 선택하여 **[!UICONTROL 키 쌍 생성]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 키 쌍 생성]** 오른쪽 아래 모서리에 있습니다.

![](../images/api/getting-started/generate-key-pair.png)

키 쌍이 자동으로 생성되며 개인 키 및 공개 인증서가 포함된 ZIP 파일이 로컬 컴퓨터에 다운로드됩니다(이후 단계에서 사용). 선택 **[!UICONTROL 구성된 API 저장]** 구성을 완료합니다.

![](../images/api/getting-started/key-pair-generated.png)

프로젝트에 API가 추가되면 프로젝트 페이지가 다시 **Privacy Service API 개요** 페이지. 여기에서 아래로 스크롤하여 **[!UICONTROL 서비스 계정(JWT)]** 섹션, Privacy Service API에 대한 모든 호출에 필요한 다음 액세스 자격 증명을 제공합니다.

* **[!UICONTROL 클라이언트 ID]**: 클라이언트 ID는 필수입니다 `{API_KEY}` 의 경우 x-api-key 헤더에 제공해야 합니다.
* **[!UICONTROL 조직 ID]**: 조직 ID는 `{ORG_ID}` x-gw-ims-org-id 헤더에서 사용해야 하는 값입니다.

![](../images/api/getting-started/jwt-credentials.png)

#### 각 세션에 대한 인증

수집해야 하는 최종 필수 자격 증명은 `{ACCESS_TOKEN}`: Authorization 헤더에 사용됩니다. 에 대한 값과 달리 `{API_KEY}` 및 `{ORG_ID}`를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다 [!DNL Platform] API.

새 `{ACCESS_TOKEN}`앞에서 다운로드한 개인 키를 열고 옆에 있는 텍스트 상자에 내용을 붙여 넣습니다. **[!UICONTROL 액세스 토큰 생성]** 선택하기 전에 **[!UICONTROL 토큰 생성]**.

![](../images/api/getting-started/paste-private-key.png)

새 액세스 토큰이 생성되고 토큰을 클립보드에 복사하는 단추가 제공됩니다. 이 값은 필요한 인증 헤더에 사용되며 형식으로 제공해야 합니다 `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) 플랫폼 API에 대한 시작 안내서에서 를 참조하십시오.

## 다음 단계

이제 사용할 헤더를 이해하므로 Privacy Service API를 호출할 준비가 되었습니다. 시작할 엔드포인트 가이드 중 하나를 선택합니다.

* [개인 정보 작업](./privacy-jobs.md)
* [동의](./consent.md)
