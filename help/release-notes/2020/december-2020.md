---
title: Adobe Experience Platform 릴리스 노트 2020년 12월
description: Adobe Experience Platform의 2020년 12월 릴리스 정보.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 11%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2020년 12월 9일**

Adobe Experience Platform의 새로운 기능:

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 여러 다른 서비스에 걸쳐 구성되어 데이터를 소스 커넥터에서 타겟 데이터 세트, ID 및 프로필 서비스, 대상으로 이동하는 데 도움이 됩니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 흐름에 대한 투명도 | 소스 및 대상에 대한 데이터 흐름을 모니터링할 수 있습니다. 자세한 내용은 모니터링 소스에 대한 [튜토리얼](../../dataflows/ui/monitor-sources.md) 또는 모니터링 대상에 대한 [튜토리얼](../../dataflows/ui/monitor-destinations.md)을 참조하십시오. |

데이터 흐름에 대한 자세한 내용은 [데이터 흐름 개요](../../dataflows/home.md)를 참조하세요.

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace은 머신 러닝 및 인공 지능을 사용하여 데이터에서 통찰력을 만듭니다. Adobe Experience Platform에 통합된 Data Science Workspace은 Adobe 솔루션 전반에서 컨텐츠 및 데이터 자산을 사용하여 예측을 수행할 수 있도록 합니다.

**주요 기능**

| 기능 | 설명 |
| --- | ---|
| Adobe Experience Platform Intelligence 패키지 추가 | Adobe Experience Platform Intelligence 패키지 추가 는 다음과 같은 추가 주요 기능을 잠금 해제하는 Data Science Workspace 업그레이드입니다. <li> UI 기반 모델 실험 및 평가.</li><li> 예약된 교육 및 예측 작업으로 모델을 배포 및 운영하는 기능.</li><li> Tensorflow 모델(GPU Compute)에서 딥 러닝을 지원합니다.</li><li> 대규모 데이터 세트(10MM + 행)에 대해 교육하고 평가하는 Spark 기반 분산 컴퓨팅.</li><li>기타</li> |

Adobe Experience Platform Intelligence 패키지 추가 정보에 대한 자세한 내용은 [데이터 과학 Workspace 액세스 및 기능](../../data-science-workspace/access-features-dsw.md)에 대한 설명서를 참조하십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform]에서는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 소스에 대한 계정 및 연결 세부 정보 업데이트 | 이제 [!DNL Flow Service] API 및 UI를 사용하여 기존 스트리밍 연결의 이름, 설명 및 자격 증명을 업데이트할 수 있습니다. 자세한 내용은 [API를 사용하여 연결 업데이트](../../sources/tutorials/api/update.md) 및 [UI를 사용하여 계정 세부 정보 편집](../../sources/tutorials/ui/monitor.md)에 대한 자습서를 참조하십시오. |
| 데이터 흐름 삭제 | 오류가 있거나 불필요하게 된 스트리밍 데이터 흐름은 이제 [!DNL Flow Service] API 및 UI를 사용하여 삭제할 수 있습니다. 자세한 내용은 [API를 사용하여 데이터 흐름 삭제](../../sources/tutorials/api/delete-dataflows.md) 및 [UI를 사용하여 데이터 흐름 삭제](../../sources/tutorials/ui/delete.md)에 대한 자습서를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
