---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;;home;popular topics;query service;query
solution: Experience Platform
title: 쿼리 서비스 개요
topic-legacy: overview
description: 이 문서에서는 Experience Platform 내 쿼리 서비스 역할에 대한 개요를 제공합니다.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# [!DNL Query Service] 개요

Adobe Experience Platform은 다양한 소스의 데이터를 인제스트합니다. 마케터는 이러한 데이터를 활용하여 고객에 대한 통찰력을 얻는 것이 가장 큰 과제입니다. Adobe Experience Platform [!DNL Query Service]은 표준 SQL을 사용하여 [!DNL Platform]의 데이터를 쿼리할 수 있도록 함으로써 이러한 기능을 용이하게 합니다. [!DNL Query Service]을 사용하여 [!DNL Data Lake]의 모든 데이터 세트에 참여하고 쿼리 결과를 보고, 머신 러닝 또는 [!DNL Real-time Customer Profile]에 수집하기 위한 새로운 데이터 세트로 캡처할 수 있습니다. 이 문서에서는 [!DNL Experience Platform] 내 [!DNL Query Service] 역할에 대한 개요를 제공합니다.

[!DNL Query Service] 를 사용하면 브랜드 기업이 온라인-오프라인 고객 여정을 연결하고 옴니채널 기여도를 파악할 수 있습니다. 다음 비디오에서는 경험 비즈니스가 [!DNL Query Service]을(를) 활용하여 주요 사용 사례 및 [!DNL Query Service]의 작동 방식을 해결하는 방법을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## [!DNL Query Service] 사용

[!DNL Query Service] SQL 쿼리를 만들어 데이터를 보다 효과적으로 분석할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 사용자 인터페이스를 사용하여 쿼리를 작성 및 실행하고, 이전에 실행한 쿼리를 보고, IMS 조직 내에서 사용자가 저장한 쿼리에 액세스할 수 있습니다. 사용자 인터페이스는 더 광범위한 데이터 세트에서 실행하기 전에 쿼리를 테스트하기 위한 샌드박스로 사용됩니다. [!DNL Platform] 내 대화형 서비스 사용에 대한 자세한 내용은 [쿼리 서비스 사용자 인터페이스 안내서](ui/overview.md)에서 확인할 수 있습니다. RESTful API는 유사한 환경을 제공하므로 프로그래밍 방식으로 쿼리를 작성 및 실행하고 향후 사용 및 반복에 대한 쿼리를 예약하고 작성할 쿼리에 대한 템플릿을 만들 수 있습니다. [!DNL Query Service] API 사용에 대한 자세한 내용은 [쿼리 서비스 개발자 안내서](api/getting-started.md)에서 참조할 수 있습니다.

## [!DNL Query Service] 및  [!DNL Experience Platform] 서비스

[!DNL Query Service] 상호 작용하며 여러 서비스와 함께 사용할 수  [!DNL Experience Platform] 있습니다. [!DNL Query Service's] 기능을 최대한 활용하려면 이러한 서비스와 [!DNL Query Service]와의 상호 작용을 잘 아는 것이 좋습니다.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 기계 학습과 인공 지능을 사용하여 [!DNL Experience Platform] 내에 저장된 데이터를 통해 통찰력을 얻습니다. [!DNL Data Science Workspace] 데이터 과학자는 고객과 고객의 활동에 대한 기록 및 시간 시리즈 데이터를 기반으로 레서피를 만들 수 있도록 하여 개인이 평가하고 사용할 가능성이 높은 고객 성향 및 권장 오퍼를 구매하는 등의 예측을 용이하게 합니다. [!DNL Query Service]을(를) [!DNL JupyterLab]에 통합하여 [!DNL Data Science Workspace] 내에 SQL을 사용할 수 있으므로 Adobe Analytics 데이터를 탐색, 변환 및 분석할 수 있습니다. [!DNL Data Science Workspace]에 대한 자세한 내용은 [!DNL Data Science Workspace] 개요 및 [!DNL Data Science Workspace]와 [!DNL Query Service]의 상호 작용 방법에 대한 자세한 내용은 [!DNL Query Service] 통합 안내서를 참조하십시오.

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service]을(를) 사용하여 비슷한 트레이트를 공유하는 작은 그룹으로 고객을 나눌 수 있습니다. 나중에 이러한 세그먼트를 평가하여 [!DNL Real-time Customer Profile] 데이터에 대한 더 나은 분석을 제공할 수 있습니다. [!DNL Query Service] 의 세그먼트 데이터에 대한 쿼리를 실행하여 이 분석을 제공하는 데 사용할 수  [!DNL Data Lake]있습니다. 세그먼테이션에 대한 자세한 내용은 [!DNL Segmentation Service] 개요 및 세그먼트 분석 방법에 대한 자세한 내용은 [!DNL Profile Query Language] (PQL) 안내서를 참조하십시오.

### BI 사용 사례 보기

Adobe Experience Platform을 사용하면 행동, CRM, POS 데이터 등 저장된 모든 데이터 세트를 인제스트, 저장, 구조 및 가져올 수 있습니다. [!DNL Experience Platform's Query Service]을 사용하면 이러한 데이터 세트에 대해 쿼리하고 비즈니스에 대한 특정 질문에 답변한 다음 효과적인 통찰력을 생성할 수 있습니다. 다음 비디오에서는 [!DNL Query Service]을(를) 사용하여 비즈니스 인텔리전스(BI) 도구에서 대시보드를 만드는 값을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 다음 단계 및 추가 리소스

이 문서를 읽음으로써 [!DNL Query Service]에 소개되었으며, 이 문서가 [!DNL Experience Platform]의 보다 큰 범위 내에서 어떻게 작동하는지 알게 되었습니다. [!DNL Query Service] API 내의 다양한 끝점과 상호 작용하는 방법에 대한 자세한 내용은 [쿼리 서비스 개발자 안내서](api/getting-started.md)를 참조하십시오. [!DNL Platform] 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 내용은 [쿼리 서비스 사용자 인터페이스 안내서](ui/overview.md)를 참조하십시오. 외부 클라이언트를 [!DNL Query Service]과(와) 연결하는 방법에 대한 포괄적인 목록은 [쿼리 서비스 클라이언트 개요](clients/overview.md)를 참조하십시오.

쿼리를 실행할 수 있도록 준비할 수 있도록 다음 비디오를 보십시오. 이 비디오는 쿼리 편집기 인터페이스, PSQL 클라이언트, 비즈니스 인텔리전스(BI) 솔루션 및 HTTP API에서 쿼리를 실행하기 위한 팁과 모범 사례를 공유합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
