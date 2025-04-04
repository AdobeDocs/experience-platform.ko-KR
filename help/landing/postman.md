---
keywords: Experience Platform;홈;인기 항목;Adobe Experience Platform;api 안내서;플랫폼 api 안내서;플랫폼 소개;개발자 안내서
solution: Experience Platform
title: Adobe Experience Platform의 Postman
description: 이 문서에는 Postman 환경 설정, Postman 컬렉션 가져오기 및 각 Experience Platform 서비스에 대해 사용 가능한 컬렉션 목록을 설명하는 단계가 포함되어 있습니다.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Adobe Experience Platform의 Postman

Postman은 사전 설정된 변수로 환경을 설정하고, API 컬렉션을 공유하고, CRUD 요청을 간소화하는 등 다양한 작업을 수행할 수 있는 API 개발을 위한 협업 플랫폼입니다. 대부분의 Experience Platform API 서비스에는 API 호출을 지원하는 데 사용할 수 있는 Postman 컬렉션이 있습니다.

## Experience Platform용 Postman 환경을 설정하는 방법

다음 비디오 안내서에서는 Postman 환경 만들기 및 설정에 대해 간략하게 설명합니다. Postman 환경에는 아래에 제공된 다양한 컬렉션에 대한 API를 호출하는 데 필요한 모든 필수 헤더가 포함되어 있습니다. 설정이 완료되면 값이 만료될 때마다(예: `ACCESS_TOKEN`) 환경의 현재 값을 업데이트할 수 있으며 이 새 값은 모든 컬렉션에서 사용됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman 컬렉션 {#collections}

사용 가능한 모든 Postman 컬렉션이 포함된 폴더는 [Experience Platform Postman 샘플 GitHub 저장소](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)를 방문하여 찾을 수 있습니다. 또는 Postman 컬렉션 링크는 Adobe I/O의 [API 참조 설명서](https://www.adobe.com/go/platform-api-reference-en)에 있는 각 개별 Swagger 파일에서 찾을 수 있습니다.

Postman 컬렉션을 다운로드하려면 GitHub 페이지에서 **[!DNL Raw]**&#x200B;을(를) 선택하여 원시 JSON 파일을 새 탭에 로드합니다. 그런 다음 마우스 오른쪽 단추를 클릭하고 **[!DNL Save as]**&#x200B;을(를) 선택하여 선택한 로컬 대상에 파일을 저장합니다.

![원시 JSON](./images/api-guide/raw-collection.PNG)

## Postman 컬렉션 가져오기 {#import}

[Postman 컬렉션](#collections)을 사용하려면 환경을 설정해야 합니다. 환경 설정을 완료했으면 오른쪽 상단에서 **[!DNL Manage Environments]** 선택기를 선택합니다.

![환경 선택기 관리](./images/api-guide/environment-selector.png)

팝오버가 나타나고 현재 모든 환경이 표시됩니다. 컬렉션을 가져오려면 **[!DNL import]** 을(를) 선택합니다.

![가져오기 단추](./images/api-guide/import-collection.png)

가져올 파일을 선택하라는 메시지가 표시됩니다. 가져오려는 Postman 컬렉션 파일을 선택합니다. 선택하면 컬렉션이 컬렉션 탭 아래의 왼쪽 레일에 채워집니다.

![채워진 컬렉션](./images/api-guide/imported-collection.png)

각 컬렉션에는 성공적인 CRUD 작업을 수행하는 데 필요할 수 있는 서로 다른 키-값 쌍이 있습니다. 필요한 값, 팁에 대해 알아보고 예제를 보려면 서비스의 [API 개발자 안내서](api-guide.md#api-guides)를 검토하십시오.

Postman UI 및 사용 가능한 기능에 대한 자세한 내용은 [Postman 설명서](https://learning.postman.com/docs/getting-started/navigating-postman/)를 참조하세요.

### 비프로덕션 사용을 위해 Postman을 사용하여 액세스 토큰 생성

>[!WARNING]
>
>IMS(Identity Management 서비스) Postman 컬렉션에서 설명한 대로 표시된 생성 메서드는 **비프로덕션 사용**&#x200B;에 적합합니다. 로컬 서명은 서드파티 호스트에서 JavaScript 라이브러리를 로드하고 원격 서명은 개인 키를 Adobe이 소유 및 운영하는 웹 서비스로 전송합니다. Adobe은 이 개인 키를 저장하지 않지만 프로덕션 키는 누구와도 공유하면 안 됩니다.

아래 비디오는 공개 GitHub 저장소에서 다운로드할 수 있는 [Identity Management 서비스(IMS) Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json)을 사용합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 다음 단계

이 문서에서는 Postman 환경, 컬렉션 및 컬렉션을 가져오는 방법을 소개합니다. 이제 Postman을 준비했으므로 [Experience Platform 시작 안내서](api-guide.md)를 방문하여 필요한 헤더, 예제 및 각 Experience Platform 서비스에 사용할 수 있는 [API 안내서](api-guide.md#api-guides) 목록에 대한 정보를 확인하십시오.
