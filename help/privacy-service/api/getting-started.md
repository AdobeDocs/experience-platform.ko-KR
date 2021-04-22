---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: Privacy Service API 안내서
description: 개발자는 Privacy Service API를 사용하여 법적 개인 정보 보호 규정을 준수하여 Experience Cloud 애플리케이션에서 고객 개인 데이터를 액세스하거나 삭제할 수 있는 고객 요청을 작성하고 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Privacy Service] API 안내서

Adobe Experience Platform [!DNL Privacy Service]은 Adobe Experience Cloud 응용 프로그램에서 데이터 주체(고객)의 개인 데이터를 관리(액세스 및 삭제)할 수 있는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service] 또한 애플리케이션과 관련된 작업의 상태 및 결과에 액세스할 수 있는 중앙 감사 및 로깅 메커니즘을  [!DNL Experience Cloud] 제공합니다.

이 안내서에서는 [!DNL Privacy Service] API를 사용하는 방법에 대해 설명합니다. UI 사용 방법에 대한 자세한 내용은 [Privacy Service UI 개요](../ui/overview.md)를 참조하십시오. [!DNL Privacy Service] API에서 사용 가능한 모든 끝점의 전체 목록을 보려면 [API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)를 참조하십시오.

## 시작하기 {#getting-started}

이 안내서에서는 다음 [!DNL Experience Platform] 기능을 이해하는 작업이 필요합니다.

* [[!DNL Privacy Service]](../home.md):Adobe Experience Cloud 응용 프로그램에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리하고 삭제할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다.

다음 섹션에서는 Privacy Service API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md)를 읽는 방법에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

[!DNL Privacy Service] API를 호출하려면 먼저 필요한 헤더에 사용할 액세스 자격 증명을 수집해야 합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

이 작업에는 Adobe Admin Console에서 [!DNL Experience Platform]에 대한 개발자 권한을 취득한 다음 Adobe 개발자 콘솔에서 자격 증명을 생성하는 작업이 포함됩니다.

### 개발자가 [!DNL Experience Platform]에 액세스

개발자가 [!DNL Platform]에 액세스하려면 [Experience Platform 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)의 시작 단계를 따르십시오. &quot;Adobe 개발자 콘솔에서 액세스 자격 증명 생성&quot; 단계에 도달하면 이 자습서로 돌아가서 [!DNL Privacy Service]에 대한 자격 증명을 생성합니다.

### 액세스 자격 증명 생성

Adobe 개발자 콘솔을 사용하여 다음 3개의 액세스 자격 증명을 생성해야 합니다.

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

`{IMS_ORG}` 및 `{API_KEY}`은 한 번만 생성되어야 하며 향후 API 호출에서 다시 사용할 수 있습니다. 그러나 `{ACCESS_TOKEN}`은(는) 일시적이며 24시간마다 다시 생성해야 합니다.

이러한 값을 생성하는 단계는 아래에 자세히 설명되어 있습니다.

#### 일회성 설정

[Adobe 개발자 콘솔](https://www.adobe.com/go/devs_console_ui)로 이동하여 Adobe ID으로 로그인합니다. 그런 다음 Adobe 개발자 콘솔 문서에서 [빈 프로젝트](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)를 만드는 자습서에 설명된 단계를 따릅니다.

새 프로젝트를 만들었으면 **[!UICONTROL Project Overview]** 화면에서 **[!UICONTROL Add API]**&#x200B;을 선택합니다.

![](../images/api/getting-started/add-api-button.png)

**[!UICONTROL Add an API]** 화면이 나타납니다. **[!UICONTROL Next]**&#x200B;을 선택하기 전에 사용 가능한 API 목록에서 **[!UICONTROL Privacy Service API]**&#x200B;을 선택합니다.

![](../images/api/getting-started/add-privacy-service-api.png)

**[!UICONTROL Configure API]** 화면이 나타납니다. **[!UICONTROL Generate a key pair]** 옵션을 선택한 다음 오른쪽 아래 모서리에서 **[!UICONTROL Generate keypair]** 을 선택합니다.

![](../images/api/getting-started/generate-key-pair.png)

키 쌍이 자동으로 생성되고 개인 키 및 공개 인증서가 포함된 ZIP 파일이 로컬 컴퓨터에 다운로드됩니다(다음 단계에서 사용). **[!UICONTROL Save configured API]**&#x200B;을 선택하여 구성을 완료합니다.

![](../images/api/getting-started/key-pair-generated.png)

API가 프로젝트에 추가되면 프로젝트 페이지가 **Privacy Service API 개요** 페이지에 다시 나타납니다. 여기서 [!DNL Privacy Service] API에 대한 모든 호출에 필요한 다음 액세스 자격 증명을 제공하는 **[!UICONTROL Service Account (JWT)]** 섹션으로 스크롤합니다.

* **[!UICONTROL CLIENT ID]**:클라이언트 ID는 x-api-key 헤더 `{API_KEY}` 에 제공해야 하는 경우 필요합니다.
* **[!UICONTROL ORGANIZATION ID]**:조직 ID는  `{IMS_ORG}` x-gw-ims-org-id 헤더에서 사용해야 하는 값입니다.

![](../images/api/getting-started/jwt-credentials.png)

#### 각 세션의 인증

수집해야 하는 최종 필수 자격 증명은 인증 헤더에서 사용되는 `{ACCESS_TOKEN}`입니다. `{API_KEY}` 및 `{IMS_ORG}`에 대한 값과 달리 [!DNL Platform] API를 계속 사용하려면 24시간마다 새 토큰을 생성해야 합니다.

새 `{ACCESS_TOKEN}`을(를) 생성하려면 **[!UICONTROL Generate Token]**&#x200B;를 선택하기 전에 이전에 다운로드한 개인 키를 열고 **[!UICONTROL Generate access token]** 옆의 텍스트 상자에 내용을 붙여 넣습니다.

![](../images/api/getting-started/paste-private-key.png)

새 액세스 토큰이 생성되고 토큰을 클립보드에 복사할 단추가 제공됩니다. 이 값은 필요한 인증 헤더에 사용되며 `Bearer {ACCESS_TOKEN}` 형식으로 제공해야 합니다.

![](../images/api/getting-started/generated-access-token.png)

## 다음 단계

이제 사용할 헤더를 이해했으므로 [!DNL Privacy Service] API에 대한 호출을 시작할 준비가 되었습니다. [개인 정보 작업](privacy-jobs.md)의 문서는 [!DNL Privacy Service] API를 사용하여 수행할 수 있는 다양한 API 호출을 안내합니다. 각 예제 호출에는 일반 API 형식, 필수 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.
