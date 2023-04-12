---
description: 이 페이지에서는 Adobe Experience Platform Destination SDK 인증 및 사용 시작 방법에 대해 설명합니다. 여기에는 Adobe I/O 인증 자격 증명, 샌드박스 이름 및 대상 작성 액세스 제어 권한을 가져오는 방법에 대한 지침이 포함되어 있습니다.
title: Destination SDK 시작
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 4%

---

# 시작하기

## 개요 {#overview}

이 페이지에서는 Adobe Experience Platform Destination SDK 인증 및 사용 시작 방법에 대해 설명합니다. 여기에는 Adobe I/O 인증 자격 증명, 샌드박스 이름 및 대상 작성 액세스 제어 권한을 가져오는 방법에 대한 지침이 포함되어 있습니다.

## 용어 {#terminology}

이 안내서에서는 조직 및 샌드박스와 같은 플랫폼별 개념을 사용합니다. 자세한 내용은 [Experience Platform 용어집](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) 를 참조하십시오.

## 필요한 인증 자격 증명 얻기 {#obtain-authentication-credentials}

Destination SDK 사용 [Adobe I/O](https://www.adobe.io/) 인증을 위한 게이트웨이입니다. Destination SDK 종단점에 API를 호출하려면 API 호출에서 특정 헤더를 제공해야 합니다. Adobe Exchange 팀과 협력하여 [Adobe Developer 콘솔](https://developer.adobe.com/console).

Destination SDK API 엔드포인트를 성공적으로 호출하려면 [Experience Platform 인증 자습서](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). 자습서를 &quot;&quot;에서 시작합니다.[API 키, 조직 ID 및 클라이언트 암호 생성](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot; 단계입니다. Adobe 교환 팀이 이전 단계를 처리합니다. 인증 자습서를 완료하면 아래와 같이 Destination SDK API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `x-api-key: {API_KEY}`를 클라이언트 ID라고도 합니다
* `x-gw-ims-org-id: {ORG_ID}`를 조직 ID라고도 합니다
* `Authorization: Bearer {ACCESS_TOKEN}` 질문에 답합니다. 액세스 토큰에는 만료 시간이 24시간이며, 밀리초 단위로 표시되므로 새로 고쳐야 합니다. 액세스 토큰을 새로 고치려면 인증 자습서에 설명된 단계를 반복합니다.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## 대상 소유권 및 샌드박스 {#destination-ownership}

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. Destination SDK 요청에는 작업이 발생하는 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

Adobe Exchange 팀에서는 Destination SDK API 엔드포인트 호출에 사용해야 하는 샌드박스 이름을 제공합니다.

## 역할 기반 액세스 제어(RBAC) {#rbac}

에 설명된 Destination SDK API 엔드포인트를 사용하려면 [참조 설명서](./configuration-options.md), 다음을 수행해야 합니다. **[!UICONTROL 대상 작성]** 액세스 제어 권한. Adobe Exchange 팀과 협력하여 이 권한을 할당받으십시오. [Adobe Admin Console](https://adminconsole.adobe.com/).

![대상 작성 권한](./assets/destination-authoring-permission.png)

자세한 내용은 다음 Experience Platform 액세스 제어 문서를 참조하십시오.

* [제품 프로필에 대한 권한 관리](/help/access-control/ui/permissions.md)
* [Experience Platform 사용 가능 권한](/help/access-control/home.md#permissions)
* [Adobe Admin Console 설명서](https://helpx.adobe.com/kr/enterprise/using/admin-console.html)

## 추가 고려 사항 {#additional-considerations}

* 대상 구성을 만들거나 편집하든 Adobe이 하든 대상 구성에 수행한 모든 변경 사항을 검토하고 승인해야 합니다. 검토를 수행한 후에만 변경 사항이 대상에 반영됩니다.
* 동일한 조직에 속하고 샌드박스에 액세스할 수 있는 사용자만 대상 구성을 편집할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서의 절차에 따라 Adobe I/O, 샌드박스 이름 및 대상 작성 액세스 제어 권한에 대한 인증 자격 증명을 받았습니다. 다음으로, Destination SDK을 사용하여 대상을 설정할 수 있습니다.

* 대상 유형에 따라 다음 구성 안내서를 읽어 보십시오.

   * [Destination SDK을 사용하여 스트리밍 대상 구성](./configure-destination-instructions.md)
   * [Destination SDK을 사용하여 파일 기반 대상 구성](./configure-file-based-destination-instructions.md)

* 모든 작업에 대해서는 [대상 작성 API 설명서](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* 를 사용하십시오 [대상 작성 API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) Destination SDK API 엔드포인트를 사용하여 대상을 구성하기 위해 Postman을 시작하려면 다음을 참조하십시오. [환경 및 컬렉션 가져오기 절차](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) 그리고 [Postman 환경 만들기를 위한 비디오 안내서](https://video.tv.adobe.com/v/28832).
