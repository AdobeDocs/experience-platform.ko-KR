---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트(2020년 6월 10일)
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b6cfdf56c20065bdc3e8a9fedf6007ddd74eaeaa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 6월 10일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 과학 작업 공간](#dsw)
- [소스](#sources)

## 데이터 과학 작업 공간 {#dsw}

Data Science Workspace는 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 도출합니다. Adobe Experience Platform에 통합된 데이터 과학 작업 공간을 사용하면 Adobe 솔루션 전체에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 있습니다.

Data Science Workspace는 실시간 머신 러닝을 통해 향상된 경험과 예측을 가능하게 하는 새로운 방식을 모색하고 있습니다. 실시간 기계 학습은 API 종단점을 통해 실시간 점수 지정/활성화를 위해 맞춤형 또는 가져온 사전 교육 시스템 학습 모델을 업계 표준 상호 운용 가능한 모델 포맷으로 작성, 테스트 및 배포할 수 있는 기능을 제공합니다.

실시간 기계 학습은 알파 버전이며 현재 개발 중입니다.

| 기능 | 설명 |
|--- | ---|
| JupiterLab Launcher 실시간 ML 스타터 | JupiterLab Launcher에는 실시간 머신 러닝(Alpha)을 위한 Python 노트북 시작 도구가 포함되어 있습니다. |

실시간 기계 학습 알파에 대한 자세한 내용은 [실시간 기계 학습 개요를 참조하십시오](../../data-science-workspace/real-time-machine-learning/home.md).

## 소스 {#sources}

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 인제스트할 수 있으며, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

경험 플랫폼은 다양한 데이터 제공업체의 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 클라우드 스토리지 시스템에 대한 추가 API 및 UI 지원 | Apache HDFS용 새 소스 커넥터 |
| 데이터베이스에 대한 추가 API 및 UI 지원 | Couchbase용 새 소스 커넥터 |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).
