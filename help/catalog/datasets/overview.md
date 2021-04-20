---
keywords: Experience Platform;홈;인기 항목;데이터 위치;데이터 관리;데이터 관리;계보;계보;계보;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;Home;popular topics;data location location;
solution: Experience Platform
title: 데이터 세트 개요
topic: datasets
description: 이 문서는 Experience Platform의 데이터 집합에 대한 수준 높은 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---


# 데이터 세트 개요

Adobe Experience Platform으로 성공적으로 인제스트된 모든 데이터는 [!DNL Data Lake] 내에 데이터 세트로 유지됩니다. 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장된 데이터의 다양한 측면을 설명하는 메타데이터도 포함되어 있습니다.

이 문서에서는 [!DNL Experience Platform]의 데이터 집합에 대한 수준 높은 개요를 제공합니다.

## 데이터 집합 만들기 및 메타데이터 추적

[!DNL Catalog Service] 는 데이터 위치 및 해당 계열에 대한 기록 시스템으로 데이터 세트 [!DNL Experience Platform]를 만들고 관리하는 데 사용됩니다. [!DNL Catalog] 데이터세트가 준거하는( [!DNL Experience Data Model] (XDM) 스키마 참조(다음 섹션에 설명)와 해당 데이터 세트에 수집되는 레코드 수를 포함하는 각 데이터 세트에 대한 메타데이터를 추적합니다.

자세한 내용은 [카탈로그 서비스 개요](../home.md)를 참조하십시오.

## 데이터 세트 데이터에 대한 제한 적용

[!DNL Experience Data Model] (XDM)은 고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다. [!DNL Platform]에 인제스트된 모든 데이터는 사전 정의된 XDM 스키마를 준수해야 [!DNL Data Lake]에 데이터 집합으로 유지할 수 있습니다.

모든 데이터 집합은 저장할 수 있는 데이터의 형식 및 구조를 제한하는 XDM 스키마에 대한 참조를 포함합니다. 데이터 집합의 XDM 스키마를 따르지 않는 데이터 집합에 데이터를 업로드하려고 하면 수집이 실패합니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 데이터를 데이터 세트로 인제스트

Adobe Experience Platform 데이터 수집은 다양한 소스의 데이터를 수집하는 여러 메서드를 나타냅니다. [!DNL Platform] 통합 방법에 상관없이 성공적으로 인제스트한 모든 데이터는 일괄 처리 파일로 변환됩니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 그런 다음 이러한 일괄 처리 파일은 전용 데이터 세트에 추가되고 [!DNL Data Lake] 내에 지속됩니다.

자세한 내용은 [데이터 통합 개요](../../ingestion/home.md)를 참조하십시오.

## 데이터 세트에 사용 레이블 적용

Adobe Experience Platform [!DNL Data Governance]을(를) 사용하면 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하기 위해 고객 데이터를 관리할 수 있습니다. [!DNL Data Governance] 프레임워크를 사용하면 사용 레이블을 적용하여 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

데이터 사용 레이블은 전체 데이터 세트 또는 개별 데이터 세트 필드에 적용할 수 있습니다. 데이터 집합 수준에서 추가된 레이블은 해당 데이터 집합 내의 모든 필드에 의해 상속됩니다.

서비스에 대한 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하십시오. [!DNL Platform]에서 사용 레이블 사용 방법에 대한 자세한 내용은 다음 가이드를 참조하십시오.

* [UI에서 레이블 관리](../../data-governance/labels/user-guide.md)
* [API에서 데이터 세트 레이블 관리](../../data-governance/labels/dataset-api.md)

## 다운스트림 [!DNL Platform] 서비스의 데이터 집합

데이터 세트를 사용하여 인제스트한 데이터를 저장했으면 해당 데이터 세트를 다운스트림 [!DNL Platform] 서비스에서 사용하여 고객 프로파일을 업데이트하고 머신 러닝을 통해 통찰력을 얻는 등 다양한 방식으로 사용할 수 있습니다.

다음은 다양한 작업에 데이터 세트를 사용하는 다운스트림 서비스 목록입니다. 자세한 내용은 각 서비스에 대한 설명서를 참조하십시오.

* [[!DNL Data Access API]](../../data-access/home.md):데이터 세트 내에 저장된 파일의 컨텐츠를 액세스하고 다운로드할 수 있습니다.
* [Adobe Experience Platform ID 서비스](../../identity-service/home.md):장치 및 시스템 간에 ID를 연결하며, 이들이 준수하는 XDM 스키마로 정의된 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):데이터 세트 [!DNL Identity Service] 에서 실시간으로 상세한 고객 프로파일을 만들 수 있습니다. [!DNL Real-time Customer Profile] 데이터를  [!DNL Data Lake] 가져와서 별도의 데이터 저장소에 있는 고객 프로파일을 유지합니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md):세그먼트를 작성하고 데이터로부터 대상을 생성할 수  [!DNL Real-time Customer Profile] 있습니다. 그런 다음 이러한 대상을 [!DNL Data Lake] 내의 자체 데이터 세트로 내보낼 수 있습니다.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md):머신 러닝과 인공 지능을 사용하여 대용량 데이터 세트에서 인사이트를 도출합니다.
* [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md):표준 SQL을 사용하여 데이터를 쿼리하고 데이터 세트 내 [!DNL Experience Platform]에서 데이터 세트를  [!DNL Data Lake] 결합하고 쿼리 결과를 보고,  [!DNL Data Science Workspace]또는  [!DNL Real-time Customer Profile]보고서에 사용할 새 데이터 집합으로 캡처할 수 있습니다.

## 다음 단계

이 문서를 읽음으로써 데이터 세트를 활용하는 다양한 [!DNL Platform] 서비스뿐만 아니라 [!DNL Experience Platform]의 데이터 집합의 핵심 사용 방법을 알게 되었습니다. 데이터 세트가 [!DNL Platform]에서 사용되는 여러 방법에 대한 자세한 내용은 이 개요 전체에서 연결된 서비스 설명서를 참조하십시오.

[!DNL Experience Platform] UI 내에서 데이터 집합과 상호 작용하는 방법에 대한 단계는 [데이터 집합 사용자 안내서](user-guide.md)를 참조하십시오.