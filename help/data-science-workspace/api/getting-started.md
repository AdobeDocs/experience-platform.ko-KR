---
keywords: Experience Platform;개발자 안내서;엔드포인트;데이터 과학 작업 공간;인기 항목;데이터 과학 작업 공간;데이터 과학
solution: Experience Platform
title: Sensei 기계 학습 API 안내서
description: Sensei 기계 학습 API를 사용하여 개발자는 다양한 데이터 과학 작업 공간 리소스에 대해 CRUD 작업을 수행할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%

---

# [!DNL Sensei Machine Learning] API 안내서

다음 [!DNL Sensei Machine Learning] API는 데이터 과학자가 알고리즘 온보딩에서 실험 및 서비스 배포에 이르기까지 기계 학습 서비스를 구성하고 관리하는 메커니즘을 제공합니다.

이 개발자 가이드는 를 사용하는 데 도움이 되는 단계를 제공합니다. [Sensei 기계 학습 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)및 는 다양한 데이터 과학 작업 공간 리소스에서 CRUD 작업을 수행하기 위한 API 호출을 보여줍니다.

## 시작하기

을(를) 완료해야 합니다. [인증](https://www.adobe.com/go/platform-api-authentication-en) 를 호출하기 위해 다음 요청 헤더에 액세스할 수 있는 자습서 [!DNL Adobe Experience Platform] API:

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## 다음 단계

필요한 인증 자격 증명을 수집한 후, 다음 엔드포인트 그룹에 대한 샘플 API 호출에 대한 이 개발자 안내서의 후속 섹션을 진행할 수 있습니다.

* [엔진](./engines.md)
* [실험](./experiments.md)
* [Insights](./insights.md)
* [MLInstance(레서피)](./mlinstances.md)
* [MLSservices](./mlservices.md)
* [모델](./models.md)
* [부록](./appendix.md)
