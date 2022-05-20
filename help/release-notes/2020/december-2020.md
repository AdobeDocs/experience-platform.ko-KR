---
title: Adobe Experience Platform 릴리스 노트 - 2020년 12월
description: Adobe Experience Platform에 대한 2020년 12월 릴리스 노트입니다.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 12월 9일**

Adobe Experience Platform의 새로운 기능:

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스 간에 구성되므로, 데이터를 소스 커넥터에서 타겟 데이터 세트로, ID 및 프로필 서비스, 대상으로 이동하는 데 도움이 됩니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 흐름의 투명도 | 데이터 흐름에서 소스 및 대상을 모니터링할 수 있습니다. 자세한 내용은 [소스 모니터링에 대한 자습서](../../dataflows/ui/monitor-sources.md) 또는 [대상 모니터링 자습서](../../dataflows/ui/monitor-destinations.md). |

데이터 흐름에 대한 자세한 내용은 [데이터 흐름 개요](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace는 기계 학습 및 인공 지능을 사용하여 데이터를 통해 통찰력을 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace을 사용하면 Adobe 솔루션에서 컨텐츠 및 데이터 자산을 사용하여 예측을 할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| --- | ---|
| Adobe Experience Platform Intelligence 패키지 추가 | Adobe Experience Platform Intelligence 패키지 addon 은 다음과 같은 추가 주요 기능을 잠금 해제하는 Data Science Workspace 업그레이드입니다. <li> UI 기반의 모델 실험 및 평가</li><li> 예정된 교육 및 참조 작업을 통해 모델을 배포하고 운영할 수 있습니다.</li><li> GPU 컴퓨팅(Tensorflow Model)에서 심층 학습을 지원합니다.</li><li> 대규모 데이터 세트(10MM + 행)에 대해 교육 및 점수를 매기는 스파크 기반 분산 컴퓨팅.</li><li>기타</li> |

Adobe Experience Platform Intelligence 패키지에 대한 자세한 내용은 [데이터 과학 작업 공간 액세스 및 기능](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 소스에 대한 계정 및 연결 세부 정보 업데이트 | 이제 를 사용하여 기존 스트리밍 연결의 이름, 설명 및 자격 증명을 업데이트할 수 있습니다 [!DNL Flow Service] API 및 UI. 자세한 내용은 [api를 사용하여 연결 업데이트](../../sources/tutorials/api/update.md) 및 [ui를 사용하여 계정 세부 사항 편집](../../sources/tutorials/ui/monitor.md). |
| 데이터 흐름 삭제 | 이제 오류가 포함되거나 불필요하게 된 스트리밍 데이터 흐름을 [!DNL Flow Service] API 및 UI. 자세한 내용은 [API를 사용하여 데이터 흐름 삭제](../../sources/tutorials/api/delete-dataflows.md) 및 [UI를 사용하여 데이터 흐름 삭제](../../sources/tutorials/ui/delete.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
