---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 인증 및 액세스 Experience Platform API
topic: tutorial
translation-type: tm+mt
source-git-commit: 280456e68f54f49ce4a0134e226af89ad1f849a4
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---


# Experience Platform API 인증 및 액세스

이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 액세스할 수 있는 단계별 자습서를 제공합니다.

## 인증을 통해 API 호출

응용 프로그램 및 사용자의 보안을 유지하려면 Adobe I/O API에 대한 모든 요청은 OAuth 및 JWT(JSON Web Tokens) 등의 표준을 사용하여 인증 및 인증되어야 합니다. 그러면 JWT가 클라이언트별 정보와 함께 사용되어 개인 액세스 토큰을 생성합니다.

이 자습서에서는 다음 순서도에 설명된 액세스 토큰을 만드는 과정을 통해 인증 단계를 설명합니다.
![](images/authentication/authentication-flowchart.png)

## 전제 조건

Experience Platform API를 성공적으로 호출하려면 다음이 필요합니다.

* Adobe Experience Platform 액세스 권한이 있는 IMS 조직
* 등록된 Adobe ID 계정
* 개발자 **및 제품** 사용자 **** 로 귀하를 추가할 Admin Console 관리자

다음 섹션에서는 Adobe ID을 만들고 조직의 개발자 및 사용자가 되는 단계를 안내합니다.

### Adobe ID 만들기

Adobe ID이 없는 경우 다음 단계를 사용하여을 만들 수 있습니다.

1. Adobe [Developer Console로 이동](https://console.adobe.io)
2. 새 계정 **만들기를 클릭합니다.**
3. 등록 프로세스 완료

## 조직의 Experience Platform 개발자 및 사용자 되기

Adobe I/O에 대한 통합을 만들기 전에 계정에 IMS 조직의 제품에 대한 개발자 권한이 있어야 합니다. Admin Console의 개발자 계정에 대한 자세한 내용은 개발자 관리를 위한 [지원 문서](https://helpx.adobe.com/kr/enterprise/using/manage-developers.html) 에서 확인할 수 있습니다.

**개발자 이용**

조직의 Admin Console 관리자에게 연락하여 [Admin Console을 사용하여 조직의 제품 중 하나에 대한 개발자로 추가합니다](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

계속하려면 관리자가 귀하를 개발자로 할당해야 합니다.

![](images/authentication/add-developer.png)

개발자로 지정되면 [Adobe I/O에 대한 통합을 만들 수 있는 액세스 권한이 부여됩니다](https://www.adobe.com/go/devs_console_ui). 이러한 통합은 외부 앱 및 서비스에서 Adobe API로의 파이프라인입니다.

**사용자 액세스 권한 얻기**

Admin Console 관리자는 사용자로 제품에 사용자를 추가해야 합니다.

![](images/authentication/assign-users.png)

개발자를 추가하는 프로세스와 유사하게, 관리자가 계속하려면 하나 이상의 제품 프로필에 사용자를 할당해야 합니다.

![](images/authentication/assign-user-details.png)

## Adobe 개발자 콘솔에서 액세스 자격 증명 생성

>[!NOTE] 이제 [Privacy Service 개발자 가이드에서](../privacy-service/api/getting-started.md)이 문서를 팔로우하는 경우 해당 가이드로 돌아가 Privacy Service에 고유한 액세스 자격 증명을 생성할 수 있습니다.

Adobe 개발자 콘솔을 사용하여 다음 세 가지 액세스 자격 증명을 생성해야 합니다.

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

사용자 `{IMS_ORG}` `{API_KEY}` 는 한 번만 생성되어야 하며 향후 Platform API 호출에서 다시 사용할 수 있습니다. 그러나, 사용자 `{ACCESS_TOKEN}` 는 임시 작업이므로 24시간마다 다시 생성되어야 합니다.

이러한 단계는 아래에 자세히 설명되어 있습니다.

### 일회성 설정

Adobe [Developer Console에서](https://www.adobe.com/go/devs_console_ui) Adobe ID으로 로그인합니다. 그런 다음 Adobe 개발자 콘솔 문서에서 빈 프로젝트 [를 만드는 방법에 대한 자습서에 나와](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 있는 단계를 따릅니다.

새 프로젝트를 만들었으면 프로젝트 개요 **[!UICONTROL 화면에서 API]** _추가_ 를클릭합니다.

![](images/authentication/add-api-button.png)

API _추가_ 화면이 나타납니다. Adobe Experience Platform에 대한 제품 아이콘을 클릭한 다음 **[!UICONTROL Experience Platform API를]** 선택한 다음 다음을 **[!UICONTROL 클릭합니다]**.

![](images/authentication/add-platform-api.png)

Experience Platform을 프로젝트에 추가할 API로 선택한 경우 서비스 계정(JWT)을 사용하여 프로젝트에 API를 [추가하는 방법에 대한 튜토리얼에 설명된 단계를 따라(&quot;API 구성&quot; 단계에서 시작)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) 프로세스를 완료합니다.

API가 프로젝트에 추가되면 _프로젝트 개요_ 페이지에는 Experience Platform API에 대한 모든 호출에 필요한 다음 자격 증명이 표시됩니다.

* `{API_KEY}` (클라이언트 ID)
* `{IMS_ORG}` (조직 ID)

![](./images/authentication/api-key-ims-org.png)

### 각 세션에 대한 인증

수집해야 하는 최종 자격 증명이 귀하의 것입니다 `{ACCESS_TOKEN}`. 및 `{API_KEY}` 의 값과 `{IMS_ORG}`달리 Platform API를 계속 사용하려면 24시간마다 새로운 토큰을 생성해야 합니다.

새 `{ACCESS_TOKEN}`를 생성하려면 개발자 콘솔 자격 증명 안내서에서 JWT 토큰을 [생성하는](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) 단계를 따르십시오.

## 액세스 자격 증명 테스트

세 개의 필수 자격 증명을 모두 수집했으면 다음 API 호출을 시도할 수 있습니다. 이 호출은 스키마 레지스트리의 컨테이너 내에 모든 XDM(경험 데이터 모델) 클래스를 `global` 나열합니다.

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

[Postman](https://www.getpostman.com/) 은 RESTful API를 사용하여 작업하는 데 널리 사용되는 도구입니다. 이 [중간 게시물에서는](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) JWT 인증을 자동으로 수행하고 이를 사용하여 Adobe Experience Platform API를 사용하는 방법을 설명합니다.

## 다음 단계

이 문서를 읽으면 Platform API에 대한 액세스 자격 증명을 수집하여 테스트했습니다. 이제 문서 전체에서 제공되는 예제 API 호출을 [따를 수 있습니다](../landing/documentation/overview.md).

이 튜토리얼에서 수집한 인증 값 외에도 많은 Platform API가 헤더로 제공되어야 `{SANDBOX_NAME}` 합니다. 자세한 내용은 [샌드박스 개요를](../sandboxes/home.md) 참조하십시오.