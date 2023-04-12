---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리
solution: Experience Platform
title: 쿼리 서비스 개요
description: 이 문서에서는 Experience Platform 내에서 Query Service 역할에 대한 개요를 제공합니다.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# [!DNL Query Service] 개요

Adobe Experience Platform은 다양한 소스에서 데이터를 수집합니다. 마케터가 해결해야 할 주요 과제는 고객에 대한 통찰력을 얻기 위해 이 데이터를 파악하는 것입니다. Adobe Experience Platform [!DNL Query Service] 표준 SQL을 사용하여 데이터를 쿼리할 수 있도록 함으로써 [!DNL Platform]. 사용 [!DNL Query Service]를 채울 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고, 머신 러닝 또는 수집 시 사용할 새로운 데이터 집합으로 캡처합니다. [!DNL Real-Time Customer Profile]. 이 문서에서는 [!DNL Query Service] within [!DNL Experience Platform].

[!DNL Query Service] 는 브랜드가 온라인-오프라인 고객 여정을 연결하고 옴니채널 속성을 이해할 수 있도록 합니다. 다음 비디오에서는 경험 비즈니스가 활용하는 방법을 보여줍니다 [!DNL Query Service] 주요 사용 사례 및 방법을 해결합니다. [!DNL Query Service] 작동합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 사용 [!DNL Query Service]

[!DNL Query Service] 은 데이터를 보다 효과적으로 분석하기 위해 SQL 쿼리를 만들 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다. 사용자 인터페이스를 사용하면 쿼리를 작성 및 실행하고, 이전에 실행된 쿼리를 보고, 조직 내 사용자가 저장한 쿼리에 액세스할 수 있습니다. 사용자 인터페이스는 더 넓은 데이터 세트에서 실행하기 전에 쿼리를 테스트하기 위해 샌드박스로 사용됩니다. 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 정보 [!DNL Platform] 은 [Query Service 사용자 인터페이스 안내서](ui/overview.md). RESTful API는 유사한 환경을 제공하여 쿼리를 프로그래밍 방식으로 작성 및 실행하고, 향후 사용 및 반복을 위한 쿼리를 예약하고, 작성하려는 쿼리에 대한 템플릿을 만들 수 있습니다. 사용에 대한 자세한 정보 [!DNL Query Service] API는 [Query Service 개발자 안내서](api/getting-started.md).

## [!DNL Query Service] 및 [!DNL Experience Platform] 서비스

[!DNL Query Service] 상호 작용하며 여러 과 함께 사용할 수 있습니다 [!DNL Experience Platform] 서비스. 최대한 활용하기 위해서 [!DNL Query Service's] 기능, 이러한 서비스와 상호 작용하는 방법을 잘 알고 있는 것이 좋습니다 [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 머신 러닝 및 인공 지능을 사용하여 내에 저장된 데이터를 통해 통찰력을 얻을 수 있습니다 [!DNL Experience Platform]. [!DNL Data Science Workspace] 데이터 과학자들이 고객 및 해당 활동에 대한 기록 및 시계열 데이터를 기반으로 레서피를 작성할 수 있도록 하여, 개인이 인식하거나 사용할 가능성이 높은 성향 및 권장 오퍼 구매와 같은 예측을 용이하게 할 수 있습니다. 내에서 SQL을 사용할 수 있습니다 [!DNL Data Science Workspace] 통합 [!DNL Query Service] 변환 [!DNL JupyterLab]: Adobe Analytics 데이터를 탐색, 변환 및 분석할 수 있습니다. 자세한 내용은 [!DNL Data Science Workspace] 개요 [!DNL Data Science Workspace], 및 [!DNL Query Service] 통합 방법에 대한 자세한 정보 [!DNL Data Science Workspace] 상호 작용 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 에서는 유사한 트레이트를 공유하는 작은 그룹으로 고객을 나눌 수 있습니다. 이러한 세그먼트를 나중에 평가하여 보다 나은 분석을 제공할 수 있습니다 [!DNL Real-Time Customer Profile] 데이터. [!DNL Query Service] 에서는 내에서 이 세그먼트 데이터에 대한 쿼리를 실행하여 이 분석을 제공하는 데 사용할 수 있습니다 [!DNL Data Lake]. 자세한 내용은 [!DNL Segmentation Service] 세그먼테이션에 대한 자세한 내용 및 [!DNL Profile Query Language] (PQL) 안내서 를 참조하십시오.

## 사용 사례

[!DNL Query Service] 는 다양한 용도로 사용되는 데이터 처리에 유연한 접근 방식을 제공합니다. 무엇보다도 Labs는 마케터의 세그멘테이션 부담을 덜어주고, 실행 가능한 대상과 의미 있는 비즈니스 통찰력을 생성하는 데 도움이 될 수 있습니다. 다음 사용 사례에서는 의 기능에 대한 보다 심층적인 예를 제공합니다 [!DNL Query Service].

### Adobe Analytics 찾아보기 포기

이 [찾아보기 포기 예는 Adobe 사용을 중심으로 [!DNL Analytics]](./use-cases/abandoned-browse.md) 데이터를 추가하여 실행 가능한 특정 대상을 만들 수 있습니다. [!DNL Query Service] 세그먼테이션에 대한 복잡한 로직을 사용하여 다운스트림을 사용할 수 있는 다양한 개인화된 특성을 계산하거나 세그먼트를 작성하는 방법을 크게 간소화합니다.

### 전환 BI 대시보드

Adobe Experience Platform을 사용하면 행동, CRM 및 판매 지점 데이터를 포함하여 저장된 모든 데이터 세트를 수집, 저장, 구조 및 가져올 수 있습니다. 사용 [!DNL Experience Platform's Query Service]를 사용하면 이러한 데이터 세트를 쿼리하고 비즈니스에 대한 특정 질문에 답한 다음 영향력 있는 통찰력을 생성할 수 있습니다. 다음 비디오에서는 을(를) 사용하여 비즈니스 인텔리전스(BI) 도구에서 대시보드를 만드는 가치를 보여줍니다. [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 다음 단계 및 추가 리소스

이 문서를 읽은 후에는 [!DNL Query Service] 그리고 더 큰 범위 내에서 작동 [!DNL Experience Platform]. 내의 다양한 종단점과 상호 작용하는 방법에 대한 자세한 정보 [!DNL Query Service] API입니다. [Query Service 개발자 안내서](api/getting-started.md). 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 내용 [!DNL Platform]을(를) 참조하십시오. [Query Service 사용자 인터페이스 안내서](ui/overview.md). 외부 클라이언트와 [!DNL Query Service]을(를) 참조하십시오. [Query Service 클라이언트 개요](clients/overview.md).

쿼리를 실행할 준비를 더 잘 하려면 다음 비디오를 시청하십시오. 이 비디오에서는 쿼리 편집기 인터페이스, PSQL 클라이언트, BI(비즈니스 인텔리전스) 솔루션 및 HTTP API에서 쿼리를 실행하기 위한 팁과 모범 사례를 공유합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
