---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜:2020년 12월 9일**

Adobe Experience Platform의 새로운 기능:

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

데이터 프롤링은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 프롤링은 다양한 서비스에서 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 이동하고 ID 및 프로필 서비스로 이동할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 흐름 투명도 | 소스 및 대상의 데이터 흐름을 모니터링할 수 있습니다. 자세한 내용은 소스 모니터링에 대한 [자습서](../../dataflows/ui/monitor-sources.md) 또는 대상 [에 대한 자습서를 참조하십시오](../../dataflows/ui/monitor-destinations.md). |

데이터 흐름에 대한 자세한 내용은 데이터 흐름 [개요를 참조하십시오](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

데이터 과학 작업 공간은 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 생성합니다. Adobe Experience Platform에 통합된 데이터 과학 작업 공간은 Adobe 솔루션에서 컨텐츠와 데이터 자산을 사용하여 예측할 수 있도록 도와줍니다.

**주요 기능**

| 기능 | 설명 |
| --- | ---|
| Adobe Experience Platform 인텔리전스 패키지 addon | Adobe Experience Platform 인텔리전스 패키지 addon은 다음과 같은 추가 주요 기능을 잠금 해제하는 데이터 과학 작업 공간 업그레이드입니다. <li> UI 기반의 모델 실험 및 평가</li><li> 예정된 트레이닝 및 검토 작업을 통해 모델을 배포 및 운영할 수 있습니다.</li><li> Tensorflow 모델(GPU Compute)의 심층 학습 지원</li><li> 대용량 데이터 세트(10MM + 행)를 트레이닝하고 점수를 매길 수 있는 Spark 기반의 분산 컴퓨팅</li><li>기타</li> |

Adobe Experience Platform 인텔리전스 패키지에 대한 자세한 내용은 [데이터 과학 작업 공간 액세스 및 기능에 대한 설명서를 참조하십시오](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 소스에 대한 계정 및 연결 세부 정보 업데이트 | 이제 API와 UI를 사용하여 기존 스트리밍 연결의 이름, 설명 및 자격 증명을 업데이트할 수 [!DNL Flow Service] 있습니다. 자세한 내용은 API를 사용하여 연결 [업데이트 및 UI를 사용하여 계정 세부 사항](../../sources/tutorials/api/update.md) [편집 관련 자습서를 참조하십시오](../../sources/tutorials/ui/monitor.md). |
| 데이터 흐름 삭제 | 이제 API 및 UI를 사용하여 오류가 있거나 불필요한 데이터 흐름을 [!DNL Flow Service] 삭제할 수 있습니다. 자세한 내용은 API를 사용하여 데이터 흐름 [삭제](../../sources/tutorials/api/delete-dataflows.md) 및 UI를 사용하여 데이터 흐름 [삭제에 대한 자습서를 참조하십시오](../../sources/tutorials/ui/delete.md). |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).

