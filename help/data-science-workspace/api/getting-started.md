---
keywords: Experience Platform;개발자 가이드;끝점;데이터 과학 작업 공간;인기 있는 주제;데이터 과학 작업 공간;데이터 과학
solution: Experience Platform
title: Sensei 기계 학습 API 가이드
topic-legacy: Developer guide
description: 개발자는 Sensei 기계 학습 API를 사용하여 다양한 데이터 과학 작업 공간 리소스에 대해 CRUD 작업을 수행할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] API 안내서

[!DNL Sensei Machine Learning] API는 알고리즘 온보딩, 실험 및 서비스 배포에 이르기까지 데이터 과학자들이 기계 학습 서비스를 구성하고 관리하는 메커니즘을 제공합니다.

이 개발자 안내서에서는 [Sensei 기계 학습 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 사용을 시작하는 데 도움이 되는 단계를 제공하며 다양한 데이터 과학 작업 공간 리소스에서 CRUD 작업을 수행하는 API 호출을 보여 줍니다.

## 시작하기

[!DNL Adobe Experience Platform] API를 호출하기 위해 다음 요청 헤더에 액세스하려면 [인증](https://www.adobe.com/go/platform-api-authentication-en) 자습서를 완료해야 합니다.

* 인증:Bearer `{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name:`{SANDBOX_NAME}`

[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 다음 단계

필요한 인증 자격 증명을 수집했으면 다음 끝점 그룹에 대한 샘플 API 호출을 위해 이 개발자 안내서의 다음 섹션으로 진행할 수 있습니다.

* [엔진](./engines.md)
* [실험](./experiments.md)
* [인사이트](./insights.md)
* [MLInests(레서피)](./mlinstances.md)
* [MLSservices](./mlservices.md)
* [모델](./models.md)
* [부록](./appendix.md)
