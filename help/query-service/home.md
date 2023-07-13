---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리
solution: Experience Platform
title: 쿼리 서비스 개요
description: 이 문서에서는 Experience Platform 내 쿼리 서비스의 역할에 대한 개요를 제공합니다.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# [!DNL Query Service] 개요

Adobe Experience Platform은 다양한 소스에서 데이터를 수집합니다. 마케터에게는 이 데이터를 이해하여 고객에 대한 통찰력을 얻는 것이 주요 과제입니다. Adobe Experience Platform [!DNL Query Service] 를 사용하면 표준 SQL을 사용하여에서 데이터를 쿼리할 수 있습니다 [!DNL Platform]. 사용 [!DNL Query Service], 의 모든 데이터 세트에 가입할 수 있습니다. [!DNL Data Lake] 및 보고, 머신 러닝 또는 수집에 사용할 새 데이터 세트로 쿼리 결과를 캡처합니다. [!DNL Real-Time Customer Profile]. 이 문서에서는 의 역할에 대한 개요를 제공합니다. [!DNL Query Service] 다음 범위 내 [!DNL Experience Platform].

[!DNL Query Service] 를 사용하면 브랜드가 온라인과 오프라인 고객 여정을 연결하고 옴니채널 속성을 이해할 수 있습니다. 다음 비디오는 경험 비즈니스에서 을 활용하는 방법을 보여 줍니다 [!DNL Query Service] 주요 사용 사례 및 방법 해결 [!DNL Query Service] 효과가 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 사용 [!DNL Query Service]

[!DNL Query Service] 는 SQL 쿼리를 만들어 데이터를 보다 효율적으로 분석할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 사용자 인터페이스를 사용하면 쿼리를 작성하여 실행하고, 이전에 실행한 쿼리를 보고, 조직 내에서 사용자가 저장한 쿼리에 액세스할 수 있습니다. 사용자 인터페이스는 더 넓은 데이터 세트에서 쿼리를 실행하기 전에 테스트하기 위한 샌드박스로 사용됩니다. 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 정보 [!DNL Platform] 에서 찾을 수 있음 [쿼리 서비스 사용자 인터페이스 안내서](ui/overview.md). RESTful API는 유사한 경험을 제공하므로 프로그래밍 방식으로 쿼리를 작성하여 실행하고, 향후 사용 및 반복을 위해 쿼리를 예약하며, 작성하려는 쿼리에 대한 템플릿을 만들 수 있습니다. 사용에 대한 추가 정보 [!DNL Query Service] API는에서 찾을 수 있습니다. [쿼리 서비스 개발자 안내서](api/getting-started.md).

## [!DNL Query Service] 및 [!DNL Experience Platform] 서비스

[!DNL Query Service] 가 상호 작용하여 여러 와 함께 사용할 수 있습니다 [!DNL Experience Platform] 서비스. 을 최대한 활용하기 위해 [!DNL Query Service's] 기능, 이러한 서비스와 상호 작용 방식을 숙지하는 것이 좋습니다 [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 기계 학습 및 인공 지능을 사용하여 내에 저장된 데이터에서 통찰력을 얻습니다. [!DNL Experience Platform]. [!DNL Data Science Workspace] 데이터 과학자는 고객 및 고객 활동에 대한 기록 및 시계열 데이터를 기반으로 레시피를 구축하여 개인이 이해하고 사용할 가능성이 높은 구매 성향 및 추천 오퍼와 같은 예측을 용이하게 할 수 있습니다. 다음 내에서 SQL을 사용할 수 있습니다. [!DNL Data Science Workspace] 를 통합함으로써 [!DNL Query Service] 대상 [!DNL JupyterLab]를 통해 Adobe Analytics 데이터를 탐색, 변환 및 분석할 수 있습니다. 다음을 읽으십시오. [!DNL Data Science Workspace] 개요 를 참조하십시오 [!DNL Data Science Workspace]및 [!DNL Query Service] 통합 안내서 를 참조하십시오. [!DNL Data Science Workspace] 과 상호 작용함 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 는 사용자가 고객을 유사한 트레이트를 공유하는 더 작은 그룹으로 나눌 수 있도록 해줍니다. 이러한 대상자는 다음에 대한 더 나은 분석을 제공하기 위해 평가될 수 있습니다. [!DNL Real-Time Customer Profile] 데이터. [!DNL Query Service] 내에서 이 대상 데이터에 대한 쿼리를 실행함으로써 이 분석을 제공하는 데 사용할 수 있습니다. [!DNL Data Lake]. 다음을 읽으십시오. [!DNL Segmentation Service] 세그먼테이션 및 [!DNL Profile Query Language] 대상 분석 방법에 대한 자세한 내용은 (PQL) 안내서를 참조하십시오.

## 사용 사례

[!DNL Query Service] 는 다양한 목적에 부합하는 데이터 처리에 대한 유연한 접근 방식을 제공합니다. 그 중에서도 마케터의 세그멘테이션의 부담을 덜고 실행 가능한 대상 및 의미 있는 비즈니스 통찰력을 생성하는 데 도움이 될 수 있습니다. 다음 사용 사례에서는 의 기능에 대한 보다 명확한 예를 제공합니다. [!DNL Query Service].

### Adobe Analytics 찾아보기 포기

이 [찾아보기 포기 예시 센터 Adobe 사용 [!DNL Analytics]](./use-cases/abandoned-browse.md) 실행 가능한 특정 대상을 만드는 데이터. [!DNL Query Service] 세분화를 위한 복잡한 논리를 수용하여 다운스트림에서 사용할 다양한 개인화된 속성을 계산하거나 대상자를 구성하는 방법을 크게 간소화합니다.

### Looker BI 대시보드

Adobe Experience Platform을 사용하면 행동, CRM 및 판매 시점 데이터를 포함하여 저장된 모든 데이터 세트를 수집, 저장, 구조 및 가져올 수 있습니다. 사용 [!DNL Experience Platform's Query Service], 이러한 데이터 세트에 대해 쿼리하고 비즈니스에 대한 특정 질문에 답한 다음 효과적인 통찰력을 생성하기 시작할 수 있습니다. 다음 비디오에서는 을 사용하여 BI(비즈니스 인텔리전스) 도구에서 대시보드를 작성하는 것의 가치를 보여 줍니다 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 다음 단계 및 추가 리소스

이 문서를 읽은 후에는 [!DNL Query Service] 및 의 광범위한 범위 내에서 작동하는 방식 [!DNL Experience Platform]. 내에서 다양한 끝점과 상호 작용하는 방법에 대한 자세한 내용은 [!DNL Query Service] API, 다음을 읽으십시오. [쿼리 서비스 개발자 안내서](api/getting-started.md). 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 정보 [!DNL Platform], 다음을 읽으십시오. [쿼리 서비스 사용자 인터페이스 안내서](ui/overview.md). 외부 클라이언트 연결에 대한 포괄적인 목록 [!DNL Query Service], 다음을 읽으십시오. [쿼리 서비스 클라이언트 개요](clients/overview.md).

쿼리 실행을 더 잘 준비하려면 다음 비디오를 시청하십시오. 이 비디오는 쿼리 편집기 인터페이스, PSQL 클라이언트, BI(비즈니스 인텔리전스) 솔루션 및 HTTP API에서 쿼리를 실행하기 위한 팁과 모범 사례를 공유합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
