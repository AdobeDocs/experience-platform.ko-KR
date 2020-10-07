---
keywords: Experience Platform;home;popular topics;Authenticate;access
solution: Experience Platform
title: 인증 및 액세스 Experience Platform API
topic: tutorial
type: Tutorial
description: '이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다. '
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 3%

---


# API 인증 및 [!DNL Experience Platform] 액세스

이 문서에서는 API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 [!DNL Experience Platform] 제공합니다.

## 인증을 통해 API 호출

애플리케이션과 사용자의 보안을 유지하려면 OAuth 및 JWT(JSON 웹 토큰) 등의 표준을 사용하여 Adobe I/O API에 대한 모든 요청을 인증하고 인증해야 합니다. 그러면 JWT가 클라이언트별 정보와 함께 사용되어 개인 액세스 토큰을 생성합니다.

이 자습서에서는 다음 순서도에 설명된 액세스 토큰을 만드는 과정을 통해 인증 단계를 설명합니다.
![](images/authentication/authentication-flowchart.png)

## 전제 조건

API를 성공적으로 호출하려면 [!DNL Experience Platform] 다음이 필요합니다.

* Adobe Experience Platform 액세스 권한이 있는 IMS 조직
* 등록된 Adobe ID 계정
* 개발자 **및 제품** 사용자 **** 로 귀하를 추가할 Admin Console 관리자

다음 섹션에서는 Adobe ID을 만들고 조직의 개발자 및 사용자가 되는 단계를 안내합니다.

### Adobe ID 만들기

Adobe ID이 없는 경우 다음 단계를 사용하여를 만들 수 있습니다.

1. Adobe 개발자 [콘솔로 이동](https://console.adobe.io)
2. 새 계정 **[!UICONTROL 만들기를 클릭합니다.]**
3. 등록 프로세스 완료

## 조직의 개발자 및 사용자 [!DNL Experience Platform] 가 되기

Adobe I/O에 대한 통합을 만들기 전에 계정에 IMS 조직의 제품에 대한 개발자 권한이 있어야 합니다. Admin Console의 개발자 계정에 대한 자세한 내용은 개발자 관리를 위한 [지원 문서](https://helpx.adobe.com/kr/enterprise/using/manage-developers.html) 에서 확인할 수 있습니다.

**개발자 이용**

조직 [!DNL Admin Console] 의 관리자에게 문의하여 [[!DNL Admin Console]을 사용하여 조직의 제품 중 하나에 대한 개발자로 사용자를 추가하십시오](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

계속하려면 관리자가 귀하를 개발자로 할당해야 합니다.

![](images/authentication/add-developer.png)

개발자로 지정되면 [Adobe I/O에 대한 통합을 만들 수 있는 액세스 권한이 부여됩니다](https://www.adobe.com/go/devs_console_ui). 이러한 통합은 외부 앱 및 서비스에서 Adobe API로 연결되는 파이프라인입니다.

**사용자 액세스 권한 얻기**

관리자는 [!DNL Admin Console] 사용자로 제품에 사용자를 추가해야 합니다.

![](images/authentication/assign-users.png)

개발자를 추가하는 프로세스와 유사하게, 관리자가 계속하려면 하나 이상의 제품 프로필에 사용자를 할당해야 합니다.

![](images/authentication/assign-user-details.png)

## Adobe 개발자 콘솔에서 액세스 자격 증명 생성

>[!NOTE]
>
>이제 [Privacy Service 개발자 가이드에서](../privacy-service/api/getting-started.md)이 문서를 팔로우하는 경우 해당 가이드로 돌아가 고유한 액세스 자격 증명을 생성할 수 [!DNL Privacy Service]있습니다.

Adobe 개발자 콘솔을 사용하여 다음 세 가지 액세스 자격 증명을 생성해야 합니다.

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

사용자 `{IMS_ORG}` 와 `{API_KEY}` 는 한 번만 생성되어야 하며 향후 [!DNL Platform] API 호출에서 다시 사용할 수 있습니다. 그러나, 사용자 `{ACCESS_TOKEN}` 는 임시 작업이므로 24시간마다 다시 생성되어야 합니다.

이러한 단계는 아래에 자세히 설명되어 있습니다.

### 일회성 설정

Adobe 개발자 [콘솔로](https://www.adobe.com/go/devs_console_ui) 이동하여 Adobe ID에 로그인합니다. 그런 다음 Adobe 개발자 콘솔 설명서에서 빈 프로젝트 [를 만드는](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 자습서에 나와 있는 단계를 따릅니다.

새 프로젝트를 만들었으면 프로젝트 개요 **[!UICONTROL 화면에서 API]** **추가** 를클릭합니다.

![](images/authentication/add-api-button.png)

API **추가** 화면이 나타납니다. Adobe Experience Platform의 제품 아이콘을 클릭한 다음 **[!UICONTROL Experience Platform API]** 를 선택한 다음 다음을 **[!UICONTROL 클릭합니다]**.

![](images/authentication/add-platform-api.png)

프로젝트에 추가할 API로 선택한 경우, 서비스 계정(JWT) [!DNL Experience Platform] (&quot;API 구성&quot; 단계에서 시작)을 사용하여 프로젝트에 API를 [](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) 추가하는 튜토리얼에 설명된 단계에 따라 프로세스를 완료합니다.

API가 프로젝트에 추가되면 **프로젝트 개요** 페이지에는 모든 API 호출에 필요한 다음 자격 증명이 [!DNL Experience Platform] 표시됩니다.

* `{API_KEY}` (클라이언트 ID)
* `{IMS_ORG}` (조직 ID)

![](./images/authentication/api-key-ims-org.png)

### 각 세션에 대한 인증

수집해야 하는 최종 자격 증명이 귀하의 것입니다 `{ACCESS_TOKEN}`. 및 `{API_KEY}` 의 값과 `{IMS_ORG}`달리, API를 계속 사용하려면 24시간마다 새로운 토큰을 생성해야 [!DNL Platform] 합니다.

새 `{ACCESS_TOKEN}`를 생성하려면 개발자 콘솔 자격 증명 안내서에서 JWT 토큰을 [생성하는](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) 단계를 따르십시오.

## 액세스 자격 증명 테스트

세 개의 필수 자격 증명을 모두 수집했으면 다음 API 호출을 시도할 수 있습니다. 이 호출은 스키마 레지스트리 컨테이너 내의 모든 [!DNL Experience Data Model] (XDM) 클래스를 `global` 나열합니다.

**API 형식**

```http
GET /global/classes
```

**요청**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

응답이 아래에 표시된 응답과 유사한 경우 자격 증명이 유효하고 작동합니다. 이 응답은 공간에 대해 잘렸습니다.

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

## JWT 인증 및 API 호출에 Postman 사용

[Postman](https://www.postman.com/) 은 RESTful API를 사용하여 작업하는 데 널리 사용되는 도구입니다. 이 [중간 게시물은](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) JWT 인증을 자동으로 수행하고 이를 사용하여 Adobe Experience Platform API를 사용하는 방법에 대해 설명합니다.

## 다음 단계

이 문서를 읽으면 API에 대한 액세스 자격 증명을 수집하여 성공적으로 테스트했습니다 [!DNL Platform] . 이제 문서 전체에서 제공되는 예제 API 호출을 [따를 수 있습니다](../landing/documentation/overview.md).

이 튜토리얼에서 수집한 인증 값 외에 많은 [!DNL Platform] API도 헤더로 유효한 API를 제공해야 `{SANDBOX_NAME}` 합니다. 자세한 내용은 [샌드박스 개요를](../sandboxes/home.md) 참조하십시오.