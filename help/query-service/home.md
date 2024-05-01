---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리
solution: Experience Platform
title: 쿼리 서비스 개요
description: Experience Platform 내에서 쿼리 서비스의 역할에 대해 알아봅니다.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 쿼리 서비스 개요

Adobe Experience Platform은 다양한 소스에서 데이터를 수집합니다. 마케터의 주요 과제는 이 데이터를 이해하여 고객에 대한 통찰력을 얻는 것입니다. 플랫폼에서 데이터를 쿼리하려면 표준 SQL 및 Adobe Experience Platform 쿼리 서비스를 사용할 수 있습니다. 쿼리 서비스 를 사용하여 데이터 레이크의 데이터 세트에 참여하고 쿼리 결과를 보고, 머신 러닝 또는 수집에 사용할 새 데이터 세트로 캡처할 수 있습니다 [!DNL Real-Time Customer Profile]. 이 문서에서는 Experience Platform 내 쿼리 서비스의 역할에 대한 개요를 제공합니다.

쿼리 서비스를 사용하여 온라인과 오프라인 고객 여정을 연결하고 브랜드에 대한 옴니채널 속성을 이해할 수 있습니다. 다음 비디오는 experience business에서 쿼리 서비스를 사용하여 주요 사용 사례를 처리하는 방법과 쿼리 서비스 작동 방식을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 쿼리 서비스 사용 {#usage}

데이터를 분석하려면 쿼리 서비스 사용자 인터페이스 또는 RESTful API를 사용하여 SQL 쿼리를 만들고 실행합니다.
Query Service UI를 사용하면 쿼리를 작성, 실행 및 예약하고, 이전에 실행한 쿼리를 보고, 조직 내에서 사용자가 저장한 쿼리에 액세스할 수 있습니다. 쿼리 편집기를 사용하여 더 넓은 데이터 세트에서 쿼리를 실행하기 전에 테스트할 수도 있습니다. 다음을 참조하십시오. [쿼리 서비스 UI 안내서](ui/overview.md) UI 기능에 대한 개요입니다.

RESTful API도 유사한 경험을 제공합니다. 쿼리 서비스 API를 사용하여 쿼리를 프로그래밍 방식으로 작성 및 실행하고, 조정할 쿼리에 대한 템플릿을 작성 및 저장하거나, 자동 실행을 위해 쿼리를 예약할 수 있습니다. 다음을 참조하십시오. [쿼리 서비스 개발자 안내서](api/getting-started.md) 쿼리 서비스 API 사용에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

쿼리 서비스 기능을 빠르게 시작하려면 다음 문서를 읽는 것이 좋습니다.

- [쿼리 실행에 대한 일반 지침](./best-practices/writing-queries.md)
- [쿼리 서비스의 SQL 구문](./sql/syntax.md)
- [SQL을 사용하여 파생 데이터 세트 만들기](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## 쿼리 서비스 및 Experience Platform 서비스 {#experience-platform-services}

쿼리 서비스는 상호 작용하며 여러 Experience Platform 서비스와 함께 사용할 수 있습니다. Query Service의 기능을 최대한 활용하려면 이러한 서비스와 이 서비스가 Query Service와 상호 작용하는 방법에 익숙해져야 합니다. 다음 [Experience Platform 설명서 랜딩 페이지](https://experienceleague.adobe.com/docs/experience-platform.html) 는 플랫폼의 기능에 대한 요약 및 링크를 제공합니다.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] 는 머신 러닝 및 인공 지능을 사용하여 Experience Platform 내에 저장된 데이터에서 통찰력을 얻습니다. 데이터 과학자는 [!DNL Data Science Workspace] 고객 및 고객 활동에 대한 기록 및 시계열 데이터를 기반으로 레시피를 빌드합니다. 이러한 레시피는 개인이 인식하고 사용할 가능성이 높은 구매 성향 및 추천 오퍼와 같은 예측을 용이하게 합니다. 다음 내에서 SQL을 사용할 수 있습니다. [!DNL Data Science Workspace] 쿼리 서비스를 로 통합하여 [!DNL JupyterLab] Adobe Analytics 데이터를 탐색, 변환 및 분석하기 위해 읽기 [[!DNL Data Science Workspace] 개요](../data-science-workspace/home.md) 및 [Jupyter Notebook 연결 안내서](./clients/jupyter-notebook.md) 자세한 내용은 [!DNL Data Science Workspace] 가 쿼리 서비스와 상호 작용합니다.

### [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform 세분화 서비스를 사용하여 고객을 유사한 트레이트를 공유하는 더 작은 그룹으로 나눕니다. 그런 다음 이러한 대상을 평가하여 실시간 고객 프로필 데이터에 대한 더 나은 분석을 제공할 수 있습니다. 쿼리 서비스 를 사용하여 데이터 레이크 내에서 이 대상 데이터에 대한 쿼리를 실행하고 분석을 제공할 수 있습니다. 읽기 [세그먼테이션 서비스 개요](../segmentation/home.md) 및 [[!DNL Profile Query Language] (PQL) 안내서](../segmentation/pql/overview.md) 대상자를 분석하는 방법에 대한 자세한 내용은 을 참조하십시오.

## 사용 사례 {#use-cases}

쿼리 서비스 는 다양한 용도로 사용되는 데이터 처리에 대한 유연한 접근 방식을 제공합니다. 그 중에서도 마케터의 세그멘테이션 부담을 덜고 실행 가능한 대상 및 의미 있는 비즈니스 통찰력을 생성하는 데 도움이 될 수 있습니다. 다음 사용 사례에서는 쿼리 서비스의 기능에 대한 보다 심층적인 예를 제공합니다.

### Adobe Analytics 찾아보기 포기 {#abandon-browse}

이 [찾아보기 포기 예시 센터 Adobe 사용 [!DNL Analytics]](./use-cases/abandoned-browse.md) 실행 가능한 특정 대상을 만드는 데이터. Query Service는 세분화를 위한 복잡한 논리를 수용하여 다운스트림에서 사용할 다양한 개인화된 특성을 계산하거나 대상을 구성하는 방법을 크게 단순화합니다.

## 사용자 정의 대시보드를 사용하여 인사이트 생성 {#custom-dashboards}

Adobe Experience Platform을 사용하면 행동, CRM 및 판매 시점 데이터를 포함하여 저장된 모든 데이터 세트를 수집, 저장, 구조 및 가져올 수 있습니다. 사용 [!DNL Experience Platform's Query Service], 이러한 데이터 세트에 대해 쿼리하고 비즈니스에 대한 특정 질문에 답한 다음 효과적인 통찰력을 생성하기 시작할 수 있습니다. 맞춤형 위젯을 만들고, 추가하고, 편집하여 주요 지표를 시각화할 수 있는 사용자 정의 대시보드를 만들고 관리하는 방법을 알아봅니다 [사용자 정의 대시보드](../dashboards/user-defined-dashboards.md). 다음을 수행할 수 있습니다. [자체 Real-Time CDP 보고서 사용자 지정](../dashboards/data-models/cdp-insights-data-model-b2c.md) Real-time Customer Data Platform Insights 데이터 모델과 함께 SQL 쿼리를 사용하여 마케팅 및 KPI 활용 사례

## 다음 단계 및 추가 리소스

이 문서를 읽은 후에는 쿼리 서비스 와 쿼리 서비스가 더 큰 Experience Platform 범위 내에서 작동하는 방식에 대해 알아보게 됩니다. 쿼리 서비스 기능에 대해 계속 알아보려면 다음 문서를 읽는 것이 좋습니다.

- 다음 [쿼리 서비스 개발자 안내서](api/getting-started.md): 쿼리 서비스 API 내의 다양한 끝점과 상호 작용하는 방법에 대한 자세한 정보.
- 다음 [쿼리 서비스 사용자 인터페이스 안내서](ui/overview.md): 쿼리 편집기 및 UI 사용에 대한 자세한 내용.
- 다음 [쿼리 서비스 클라이언트 개요](clients/overview.md): 쿼리 서비스와 연결할 포괄적인 외부 클라이언트 목록입니다.

쿼리 실행을 더 잘 준비하려면 다음 비디오를 시청하십시오. 이 비디오는 쿼리 편집기 인터페이스, PSQL 클라이언트, BI(비즈니스 인텔리전스) 솔루션 및 HTTP API에서 쿼리를 실행하기 위한 팁과 모범 사례를 공유합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
