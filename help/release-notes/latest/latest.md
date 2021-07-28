---
title: Adobe Experience Platform 릴리스 정보
description: 2021년 7월 28일 Experience Platform 릴리스 노트.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: dc01e03975fdda375b31f44edc8459fa32b5a61b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 10%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 7월 28일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 과학 작업 영역](#dsw)
- [XDM(경험 데이터 모델)](#xdm)
- [소스](#sources)

## 데이터 과학 작업 영역 {#dsw}

Data Science Workspace는 기계 학습 및 인공 지능을 사용하여 데이터를 통해 통찰력을 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace을 사용하면 Adobe 솔루션에서 컨텐츠 및 데이터 자산을 사용하여 예측을 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 라이브러리 및 OS 업데이트 | Data Science Workspace는 기능과 유용성을 개선하기 위해 중요한 라이브러리 및 OS 업데이트를 만들었습니다. 여기에는 JupiterLab 1.2.20, Python 3.7, Penders 1.2.4, Tensorflow 2.4, CUDA 11 및 CUNN 8 지원 등이 포함됩니다. JupiterLab 내에서 사용 가능한 라이브러리를 보는 방법에 대해 알아보려면 JupiterLab 노트북 개요 설명서의 [지원되는 라이브러리](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) 섹션을 참조하십시오. |

데이터 과학 작업 공간에 대한 일반적인 정보는 [데이터 과학 작업 공간 개요](../../data-science-workspace/home.md)를 참조하십시오.

## XDM(경험 데이터 모델) {#xdm}

XDM(Experience Data Model)은 디지털 경험의 성능을 향상하도록 설계된 오픈 소스 사양입니다. 모든 응용 프로그램이 Platform 서비스와 통신할 수 있도록 하는 스키마 형식의 데이터에 대한 공통 구조 및 정의를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 통신 산업 필터 | UI에서 스키마에 필드 그룹을 추가할 때 이제 통신 산업별로 필터링할 수 있습니다. 통신 사용 사례에 대한 권장 데이터 모델을 보려면 [통신 업계 엔티티 관계 다이어그램(ERD)](../../xdm/schema/industries/telecom.md)을 참조하십시오. |

플랫폼의 XDM에 대한 일반적인 정보는 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| GA로 이동하는 베타 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (베타) | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Salesforce Marketing Cloud]을 Experience Platform에 연결할 수 있습니다. 자세한 내용은 [[!DNL Salesforce Marketing Cloud] 커넥터 개요](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md)를 참조하십시오. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md)를 참조하십시오.
