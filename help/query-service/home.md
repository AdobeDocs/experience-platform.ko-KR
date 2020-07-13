---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 쿼리 서비스
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# 쿼리 서비스 개요

Adobe Experience Platform 인제스트는 다양한 소스의 데이터를 가져옵니다. 마케터는 이러한 데이터를 활용하여 고객에 대한 통찰력을 얻는 것이 가장 큰 과제입니다. Adobe Experience Platform 쿼리 서비스는 표준 SQL을 사용하여 Platform에서 데이터를 쿼리할 수 있도록 함으로써 이러한 작업을 쉽게 해줍니다. 쿼리 서비스를 사용하면 Data Lake의 모든 데이터 세트에 참여하고 쿼리 결과를 보고, 머신 러닝 또는 실시간 고객 프로파일에 수집하기 위한 새로운 데이터 세트로 캡처할 수 있습니다. 이 문서에서는 Experience Platform 내의 쿼리 서비스 역할에 대한 개요를 제공합니다.

Query Service를 통해 브랜드 기업은 온라인-오프라인 고객 여정을 연계하고 옴니채널 기여도를 파악할 수 있습니다. 다음 비디오에서는 경험 비즈니스가 쿼리 서비스를 활용하여 주요 사용 사례와 쿼리 서비스 작동 방식을 해결하는 방법을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 쿼리 서비스 사용

쿼리 서비스는 데이터를 보다 효과적으로 분석하기 위해 SQL 쿼리를 만들 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 사용자 인터페이스를 사용하여 쿼리를 작성 및 실행하고, 이전에 실행한 쿼리를 보고, IMS 조직 내에서 사용자가 저장한 쿼리에 액세스할 수 있습니다. 사용자 인터페이스는 더 광범위한 데이터 세트에서 쿼리를 실행하기 전에 쿼리를 테스트하기 위한 샌드박스로 사용됩니다. Platform 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 내용은 [쿼리 서비스 사용자 인터페이스 안내서를 참조하십시오](ui/overview.md). RESTful API는 유사한 환경을 제공하므로 프로그래밍 방식으로 쿼리를 작성 및 실행하고 향후 사용 및 반복을 위해 쿼리를 예약하고 작성할 쿼리에 사용할 템플릿을 만들 수 있습니다. 쿼리 서비스 API 사용에 대한 자세한 내용은 [쿼리 서비스 개발자 안내서를 참조하십시오](api/getting-started.md).

## 쿼리 서비스 및 Experience Platform 서비스

쿼리 서비스는 상호 작용하며 여러 Experience Platform 서비스와 함께 사용할 수 있습니다. 쿼리 서비스의 기능을 최대한 활용하려면 이러한 서비스와 쿼리 서비스와 상호 작용하는 방법에 익숙해지는 것이 좋습니다.

### 데이터 과학 작업 공간

Adobe Experience Platform 데이터 과학 작업 공간은 머신 러닝과 인공 지능을 사용하여 Experience Platform 내에 저장된 데이터를 통해 통찰력을 얻고 있습니다. 데이터 과학 작업 공간을 사용하면 데이터 과학자는 고객과 고객의 활동에 대한 기록 및 시간 시리즈 데이터를 기반으로 레서피를 만들 수 있으므로 개인 취향이나 권장 제안을 보고 사용할 수 있습니다. Query Service를 JupiterLab에 통합하여 데이터 과학 작업 공간에서 SQL을 사용할 수 있으므로 Adobe Analytics 데이터를 탐색, 변환 및 분석할 수 있습니다. 데이터 과학 작업 공간과 쿼리 서비스 상호 작용하는 방법에 대한 자세한 내용은 데이터 과학 작업 공간 개요 및 쿼리 서비스 통합 안내서를 참조하십시오.

### 세그멘테이션 서비스

Adobe Experience Platform 세그멘테이션 서비스를 사용하면 고객이 유사한 트레이트를 공유하는 작은 그룹으로 나눌 수 있습니다. 이러한 세그먼트는 나중에 평가하여 실시간 고객 프로필 데이터에 대한 더 나은 분석을 제공할 수 있습니다. 쿼리 서비스는 데이터 레이크 내에서 이 세그먼트 데이터에 대한 쿼리를 실행하여 이 분석을 제공하는 데 사용할 수 있습니다. 세그먼트 분석 방법에 대한 자세한 내용은 세그멘테이션 서비스 개요 및 PQL(프로필 쿼리 언어) 안내서를 참조하십시오.

### BI 사용 사례 보기

Adobe Experience Platform을 통해 행동, CRM, POS 데이터 등 저장된 모든 데이터 세트를 인제스트, 저장, 구조 및 가져올 수 있습니다. 데이터 세트 [!DNL Experience Platform's Query Service]에 대해 쿼리하고 비즈니스에 대한 특정 질문에 답변한 다음 효과적인 통찰력을 생성할 수 있습니다. 다음 비디오에서는 을 사용하여 BI(Business Intelligence) 도구에서 대시보드를 만드는 가치를 보여 줍니다 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 다음 단계 및 추가 리소스

이 문서를 읽음으로써 쿼리 서비스에 대해 소개하고 더 큰 Experience Platform 범위 내에서 어떻게 작동하는지 알게 되었습니다. 쿼리 서비스 API 내의 다양한 끝점과 상호 작용에 대한 자세한 내용은 [쿼리 서비스 개발자 안내서를 참조하십시오](api/getting-started.md). Platform 내에서 대화형 서비스를 사용하는 방법에 대한 자세한 내용은 [쿼리 서비스 사용자 인터페이스 안내서를 참조하십시오](ui/overview.md). 외부 클라이언트를 쿼리 서비스와 연결하는 방법에 대한 포괄적인 목록은 [쿼리 서비스 클라이언트 개요를 참조하십시오](clients/overview.md).

쿼리를 실행할 수 있는 준비를 하려면 다음 비디오를 시청하십시오. 이 비디오는 쿼리 편집기 인터페이스, PSQL 클라이언트, 비즈니스 인텔리전스(BI) 솔루션 및 HTTP API에서 쿼리를 실행하기 위한 팁과 모범 사례를 공유합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
