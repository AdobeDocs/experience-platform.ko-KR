---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Adobe Experience Platform 쿼리 서비스
topic: overview
description: 이 문서에서는 Experience Platform 내의 쿼리 서비스 역할에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---


# [!DNL Query Service]개요

Adobe Experience Platform은 다양한 소스에서 데이터를 수집합니다. 마케터는 이러한 데이터를 활용하여 고객에 대한 통찰력을 얻는 것이 가장 큰 과제입니다. Adobe Experience Platform [!DNL Query Service] 는 표준 SQL을 사용하여 데이터를 쿼리할 수 있도록 함으로써 이러한 작업을 쉽게 해줍니다 [!DNL Platform]. 를 [!DNL Query Service]사용하면 데이터 세트에 [!DNL Data Lake] 참여하고 쿼리 결과를 보고, 머신 러닝 또는 인제스트를 위한 새로운 데이터 세트로 캡처할 수 있습니다 [!DNL Real-time Customer Profile]. 이 문서에서는 내부 [!DNL Query Service] 역할의 개요를 제공합니다 [!DNL Experience Platform].

[!DNL Query Service] 를 사용하면 브랜드 기업이 온라인-오프라인 고객 여정을 연계하고 옴니채널 기여도를 파악할 수 있습니다. 다음 비디오에서는 경험 비즈니스가 주요 활용 사례 [!DNL Query Service] 와 작동 방식을 해결하는 데 활용할 수 있는 방법을 [!DNL Query Service] 보여줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Using [!DNL Query Service]

[!DNL Query Service] SQL 쿼리를 만들어 데이터를 보다 효과적으로 분석할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 사용자 인터페이스를 사용하여 쿼리를 작성 및 실행하고, 이전에 실행한 쿼리를 보고, IMS 조직 내에서 사용자가 저장한 쿼리에 액세스할 수 있습니다. 사용자 인터페이스는 더 광범위한 데이터 세트에서 쿼리를 실행하기 전에 쿼리를 테스트하기 위한 샌드박스로 사용됩니다. 대화형 서비스 사용 방법에 대한 자세한 내용은 [!DNL Platform] 쿼리 서비스 사용자 인터페이스 안내서를 참조하십시오 [](ui/overview.md). RESTful API는 유사한 환경을 제공하므로 프로그래밍 방식으로 쿼리를 작성 및 실행하고 향후 사용 및 반복을 위해 쿼리를 예약하고 작성할 쿼리에 사용할 템플릿을 만들 수 있습니다. API 사용에 대한 자세한 내용은 [!DNL Query Service] 쿼리 서비스 개발자 안내서를 참조하십시오 [](api/getting-started.md).

## [!DNL Query Service] 및 [!DNL Experience Platform] 서비스

[!DNL Query Service] 인터랙션하고 여러 [!DNL Experience Platform] 서비스와 함께 사용할 수 있습니다. 기능을 최대한 활용하려면 이러한 서비스와 서비스 이용 방법에 대해 잘 알고 있어야 합니다 [!DNL Query Service's] [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 는 기계 학습과 인공 지능을 사용하여 안에 저장된 데이터를 통해 통찰력을 얻고 [!DNL Experience Platform]있습니다. [!DNL Data Science Workspace] 데이터 과학자는 고객과 고객 활동에 대한 기록 및 시간 시리즈 데이터를 기반으로 레시피를 제작할 수 있으므로 개인별로 인식하거나 사용할 가능성이 높은 성향 및 권장 제안을 구입하는 것을 용이하게 합니다. Adobe Analytics 데이터를 탐색, 변형 및 분석할 수 있도록 통합 [!DNL Data Science Workspace] 을 통해 SQL [!DNL Query Service] [!DNL JupyterLab]에서 사용할 수 있습니다. 자세한 내용은 [!DNL Data Science Workspace] 개요 [!DNL Data Science Workspace]및 [!DNL Query Service] 통합 가이드를 [!DNL Data Science Workspace] 참조하십시오 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 는 고객이 비슷한 특성을 가진 작은 그룹으로 나뉘어 관계를 맺도록 한다. 이러한 세그먼트는 나중에 [!DNL Real-time Customer Profile] 데이터에 대한 더 나은 분석을 제공하기 위해 평가될 수 있습니다. [!DNL Query Service] 이 세그먼트 데이터에 대한 쿼리를 실행하여 이 분석을 제공하는 데 사용할 수 [!DNL Data Lake]있습니다. 세그먼트 [!DNL Segmentation Service] 분석에 대한 자세한 내용은 개요 및 [!DNL Profile Query Language] (PQL) 안내서를 참조하십시오.

### BI 사용 사례 보기

Adobe Experience Platform을 사용하면 행동, CRM, POS 데이터 등 저장된 모든 데이터 세트를 인제스트, 저장, 구조 및 가져올 수 있습니다. 데이터 세트 [!DNL Experience Platform's Query Service]에 대해 쿼리하고 비즈니스에 대한 특정 질문에 답변한 다음 효과적인 통찰력을 생성할 수 있습니다. 다음 비디오에서는 을 사용하여 BI(Business Intelligence) 도구에서 대시보드를 만드는 가치를 보여 줍니다 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 다음 단계 및 추가 리소스

이 문서를 읽음으로써, 당신은 많은 범위 내에서 그것이 어떻게 [!DNL Query Service] 작동하는지를 알게 되었다 [!DNL Experience Platform]. API 내의 다양한 끝점과 상호 작용에 대한 자세한 내용은 [!DNL Query Service] 쿼리 서비스 개발자 안내서를 참조하십시오 [](api/getting-started.md). 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 내용 [!DNL Platform]은 [쿼리 서비스 사용자 인터페이스 안내서를 참조하십시오](ui/overview.md). 외부 클라이언트와 연결 방법에 대한 전체 목록 [!DNL Query Service]은 [쿼리 서비스 클라이언트 개요를 참조하십시오](clients/overview.md).

쿼리를 실행할 수 있는 준비를 하려면 다음 비디오를 시청하십시오. 이 비디오는 쿼리 편집기 인터페이스, PSQL 클라이언트, 비즈니스 인텔리전스(BI) 솔루션 및 HTTP API에서 쿼리를 실행하기 위한 팁과 모범 사례를 공유합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
