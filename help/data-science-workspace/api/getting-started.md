---
keywords: Experience Platform;개발자 안내서;엔드포인트;Data Science Workspace;인기 주제;Data Science Workspace;Data Science
solution: Experience Platform
title: Sensei 머신 러닝 API 안내서
description: Sensei 머신 러닝 API를 통해 개발자는 다양한 데이터 과학 Workspace 리소스에 대한 CRUD 작업을 수행할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아봅니다.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 12%

---

# [!DNL Sensei Machine Learning] API 안내서

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

[!DNL Sensei Machine Learning] API는 데이터 과학자가 알고리즘 온보딩에서 실험 및 서비스 배포에 이르기까지 머신 러닝 서비스를 구성하고 관리할 수 있는 메커니즘을 제공합니다.

이 개발자 가이드는 [Sensei 머신 러닝 API](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) 사용을 시작하는 데 도움이 되는 단계를 제공하며 다양한 데이터 과학 Workspace 리소스에서 CRUD 작업을 수행하기 위한 API 호출을 보여 줍니다.

## 시작하기

[!DNL Adobe Experience Platform] API를 호출하기 위해 다음 요청 헤더에 액세스하려면 [인증](https://www.adobe.com/go/platform-api-authentication-en) 자습서를 완료해야 합니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* Content-Type: application/json

## 다음 단계

필요한 인증 자격 증명을 수집했으면 다음 끝점 그룹에 대한 샘플 API 호출에 대한 이 개발자 안내서의 후속 섹션으로 진행할 수 있습니다.

* [엔진](./engines.md)
* [실험](./experiments.md)
* [Insights](./insights.md)
* [MLInstances(레시피)](./mlinstances.md)
* [MLSservices](./mlservices.md)
* [모델](./models.md)
* [부록](./appendix.md)
