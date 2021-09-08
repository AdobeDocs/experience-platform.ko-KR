---
description: 이 페이지에서는 Adobe Experience Platform 대상 SDK를 인증하고 사용하는 방법을 설명합니다. 여기에는 Adobe I/O 인증 자격 증명, 샌드박스 이름 및 대상 작성 액세스 제어 권한을 가져오는 방법에 대한 지침이 포함되어 있습니다.
title: 대상 SDK 시작하기
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# 시작하기

## 개요 {#overview}

이 페이지에서는 Adobe Experience Platform 대상 SDK를 인증하고 사용하는 방법을 설명합니다. 여기에는 Adobe I/O 인증 자격 증명, 샌드박스 이름 및 대상 작성 액세스 제어 권한을 가져오는 방법에 대한 지침이 포함되어 있습니다.

## 용어 {#terminology}

이 안내서에서는 IMS 조직 및 샌드박스와 같은 플랫폼별 개념을 사용합니다. 이 용어와 다른 용어에 대한 정의는 [Experience Platform 용어집](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html)을 참조하십시오.

## 필요한 인증 자격 증명 얻기 {#obtain-authentication-credentials}

대상 SDK는 인증에 [Adobe I/O](https://www.adobe.io/) 게이트웨이를 사용합니다. 대상 SDK 종단점에 대한 API를 호출하려면 API 호출에 특정 헤더를 제공해야 합니다. Adobe Exchange 팀과 협력하여 [Adobe 개발자 콘솔](http://console.adobe.io/)에 대한 인증을 설정합니다.

대상 SDK API 엔드포인트를 성공적으로 호출하려면 [Experience Platform 인증 자습서](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html)을 따르십시오. &quot;[API 키, IMS 조직 ID 및 클라이언트 암호](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret) 생성 단계에서 자습서를 시작합니다. Adobe 교환 팀이 이전 단계를 처리합니다. 인증 자습서를 완료하면 아래와 같이 대상 SDK API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `x-api-key: {API_KEY}`를 클라이언트 ID라고도 합니다
* `x-gw-ims-org-id: {IMS_ORG}`를 조직 ID라고도 합니다
* `Authorization: Bearer {ACCESS_TOKEN}` 질문에 답합니다. 액세스 토큰에는 만료 시간이 24시간이며, 밀리초 단위로 표시되므로 새로 고쳐야 합니다. 액세스 토큰을 새로 고치려면 인증 자습서에 설명된 단계를 반복합니다.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## 대상 소유권 및 샌드박스 {#destination-ownership}

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. 대상 SDK에 대한 요청에는 작업이 발생하는 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

Adobe Exchange 팀에서는 대상 SDK API 엔드포인트 호출에 사용해야 하는 샌드박스 이름을 제공합니다.

## 역할 기반 액세스 제어(RBAC) {#rbac}

[참조 설명서](./configuration-options.md)에 설명된 대상 SDK API 엔드포인트를 사용하려면 **[!UICONTROL 대상 작성]** 액세스 제어 권한이 필요합니다. Adobe Exchange 팀과 협력하여 [Adobe Admin Console](https://adminconsole.adobe.com/)에서 이 권한을 할당받으십시오.

![대상 작성 권한](./assets/destination-authoring-permission.png)

자세한 내용은 다음 Experience Platform 액세스 제어 문서를 참조하십시오.

* [제품 프로필에 대한 권한 관리](/help/access-control/ui/permissions.md)
* [Experience Platform 사용 가능 권한](/help/access-control/home.md#permissions)
* [Adobe Admin Console 설명서](https://helpx.adobe.com/kr/enterprise/using/admin-console.html)

## 추가 고려 사항 {#additional-considerations}

* 대상 구성을 만들거나 편집하든 Adobe이 하든 대상 구성에 수행한 모든 변경 사항을 검토하고 승인해야 합니다. 검토를 수행한 후에만 변경 사항이 대상에 반영됩니다.
* 동일한 조직에 속하고 샌드박스에 액세스할 수 있는 사용자만 대상 구성을 편집할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서의 절차에 따라 Adobe I/O, 샌드박스 이름 및 대상 작성 액세스 제어 권한에 대한 인증 자격 증명을 받았습니다. 다음으로, 대상 SDK를 사용하여 대상을 설정할 수 있습니다. 다음 단계에 대해 [대상 SDK를 사용하여 대상을 구성하십시오.](./configure-destination-instructions.md)
