---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Sensei 머신 러닝 API 개발자 가이드
topic: Developer guide
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---


# Sensei 머신 러닝 API 개발자 가이드

Sensei Machine Learning API는 데이터 과학자들이 알고리즘 온보딩, 실험, 서비스 배포에 이르기까지 머신 러닝 서비스를 구성하고 관리하는 메커니즘을 제공합니다.

이 개발자 가이드는 Sensei Machine Learning API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)사용을 시작하는 데 도움이 되는 단계를 제공하고 다양한 데이터 과학 작업 공간 리소스에서 CRUD 작업을 수행하는 API 호출을 시연합니다.

## 시작하기

API를 호출하기 위해 다음 요청 헤더에 액세스할 수 있으려면 [인증](../../tutorials/authentication.md) 자습서를 [!DNL Adobe Experience Platform] 완료해야 합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## 다음 단계

필요한 인증 자격 증명을 수집했으면 다음 끝점 그룹에 대한 샘플 API 호출을 위해 이 개발자 안내서의 다음 섹션으로 진행할 수 있습니다.

* [엔진](./engines.md)
* [실험](./experiments.md)
* [인사이트](./insights.md)
* [MLInestas(레서피)](./mlinstances.md)
* [MLSservices](./mlservices.md)
* [모델](./models.md)
* [부록](./appendix.md)