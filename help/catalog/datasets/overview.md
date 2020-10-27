---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: 데이터 집합 개요
topic: datasets
description: 이 문서는 Experience Platform의 데이터 세트에 대한 개요 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 1c00456ee06c1fc09c8e4ce070c90255f51811e1
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 3%

---


# 데이터 집합 개요

Adobe Experience Platform에 성공적으로 수집되는 모든 데이터는 데이터 세트 내에 [!DNL Data Lake] 유지됩니다. 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구성체입니다. 데이터 세트에는 저장된 데이터의 다양한 측면을 설명하는 메타데이터도 포함되어 있습니다.

이 문서는 데이터 세트에 대한 개요 정보를 제공합니다 [!DNL Experience Platform].

## 데이터 집합 만들기 및 메타데이터 추적

[!DNL Catalog Service] 는 데이터 위치 및 계열에 대한 기록 시스템으로 데이터 세트 [!DNL Experience Platform]를 만들고 관리하는 데 사용됩니다. [!DNL Catalog] 데이터 세트에 따르는 [!DNL Experience Data Model] (XDM) 스키마에 대한 참조와 해당 데이터 세트에 수집되는 레코드 수를 포함하는 각 데이터 세트에 대한 메타데이터를 추적합니다.

자세한 내용은 [카탈로그 서비스 개요를](../home.md) 참조하십시오.

## 데이터 세트 데이터에 대한 제한 적용

[!DNL Experience Data Model] (XDM)은 고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크입니다. 인제스트된 모든 데이터는 사전 정의된 XDM 스키마를 [!DNL Platform] 준수해야 데이터 세트로 유지될 수 [!DNL Data Lake] 있습니다.

모든 데이터 집합은 저장할 수 있는 데이터의 형식 및 구조를 제한하는 XDM 스키마에 대한 참조를 포함합니다. 데이터 집합의 XDM 스키마를 따르지 않는 데이터 세트에 데이터를 업로드하려고 하면 데이터 수집이 실패합니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요를 참조하십시오](../../xdm/home.md).

## 데이터를 데이터 세트에 인제스트

Adobe Experience Platform 데이터 수집은 다양한 소스의 데이터를 [!DNL Platform] 인제스트하는 여러 방법을 나타냅니다. 인제스트 방법에 관계없이 성공적으로 인제스트한 모든 데이터는 일괄 처리 파일로 변환됩니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 그런 다음 이러한 일괄 처리 파일은 전용 데이터 세트에 추가되어 데이터 세트 내에 지속됩니다 [!DNL Data Lake].

자세한 내용은 [데이터 수집 개요를](../../ingestion/home.md) 참조하십시오.

## 데이터 세트에 사용 레이블 적용

Adobe Experience Platform [!DNL Data Governance] 를 사용하면 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하기 위해 고객 데이터를 관리할 수 있습니다. 이 [!DNL Data Governance] 프레임워크를 사용하면 사용 레이블을 적용하여 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

데이터 사용 레이블은 전체 데이터 세트 또는 개별 데이터 세트 필드에 적용할 수 있습니다. 데이터 집합 수준에서 추가된 레이블은 해당 데이터 집합 내의 모든 필드에 의해 상속됩니다.

서비스에 대한 자세한 내용은 [데이터 거버넌스](../../data-governance/home.md) 개요를 참조하십시오. 사용 레이블로 작업하는 방법에 대한 단계 [!DNL Platform]는 다음 가이드를 참조하십시오.

* [UI에서 레이블 관리](../../data-governance/labels/user-guide.md)
* [API에서 데이터 세트 레이블 관리](../../data-governance/labels/dataset-api.md)

## 다운스트림 [!DNL Platform] 서비스의 데이터 세트

데이터 세트를 사용하여 인제스트한 데이터를 저장한 다음 다운스트림 [!DNL Platform] 서비스에서 고객 프로파일을 업데이트하고 머신 러닝을 통해 인사이트를 얻는 등 데이터 세트를 사용합니다.

다음은 다양한 작업에 데이터 세트를 사용하는 다운스트림 서비스 목록입니다. 자세한 내용은 각 서비스의 설명서를 참조하십시오.

* [[!DNL Data Access API]](../../data-access/home.md):데이터 세트 내에 저장된 파일의 컨텐츠를 액세스하고 다운로드할 수 있습니다.
* [Adobe Experience Platform ID 서비스](../../identity-service/home.md):장치 및 시스템 간에 ID를 연결하고, XDM 스키마로 정의된 ID 필드를 기반으로 데이터 세트를 연결합니다.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):데이터 세트 [!DNL Identity Service] 에서 실시간으로 세부 고객 프로파일을 생성합니다. [!DNL Real-time Customer Profile] 데이터 저장소에서 데이터를 [!DNL Data Lake] 가져와 별도의 데이터 저장소에 고객 프로파일을 유지합니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md):세그먼트를 만들고 [!DNL Real-time Customer Profile] 데이터에서 대상을 생성할 수 있습니다. 그런 다음 이러한 대상을 해당 데이터 세트 내에 있는 데이터 세트로 내보낼 수 있습니다 [!DNL Data Lake].
* [Adobe Experience Platform 데이터 과학 작업 공간](../../data-science-workspace/home.md):머신 러닝과 인공 지능을 사용하여 대용량 데이터 세트에서 인사이트를 도출합니다.
* [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md):표준 SQL을 사용하여 데이터를 쿼리 [!DNL Experience Platform]로, 데이터 세트 내에 모든 데이터 세트를 [!DNL Data Lake] 연결하고 쿼리 결과를 보고, [!DNL Data Science Workspace]또는 [!DNL Real-time Customer Profile]보고서에 사용할 새로운 데이터 세트로 캡처할 수 있습니다.

## 다음 단계

이 문서를 읽음으로써 데이터 세트를 활용하는 다양한 서비스뿐만 아니라 데이터 세트 [!DNL Experience Platform]의 핵심 사용 [!DNL Platform] 방식을 도입하게 됩니다. 데이터 세트를 사용하는 여러 방법에 대한 자세한 내용 [!DNL Platform]은 이 개요 전체에서 링크된 서비스 설명서를 참조하십시오.

UI 내에서 데이터 세트와 상호 작용하는 방법에 대한 단계는 [!DNL Experience Platform] 데이터 세트 사용자 안내서를 참조하십시오 [](user-guide.md).