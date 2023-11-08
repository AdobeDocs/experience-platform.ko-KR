---
keywords: Experience Platform;홈;인기 항목;데이터 위치;데이터 위치;데이터 관리;데이터 관리;계보;계보;데이터 유형;데이터 유형;데이터 유형;데이터 유형
solution: Experience Platform
title: 데이터 세트 개요
description: 이 설명서는 Experience Platform의 데이터 세트에 대한 높은 수준의 개요를 제공합니다.
user-guide-description: 이 안내서를 통해 Experience Platform 내 데이터 세트에 대한 높은 수준의 개요를 살펴보십시오. 여기에서 데이터 세트를 만들고, 데이터에 대한 제약 조건을 적용하고, 데이터 세트로 데이터를 수집하는 방법을 알아봅니다.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 7%

---

# 데이터 세트 개요

Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 [!DNL Data Lake] 데이터 세트로. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.

이 문서에서는 의 데이터 세트에 대한 높은 수준의 개요를 제공합니다 [!DNL Experience Platform].

## 데이터 세트 만들기 및 메타데이터 추적

[!DNL Catalog Service] 는 내의 데이터 위치 및 계보를 위한 기록 시스템입니다 [!DNL Experience Platform]및 를 사용하여 데이터 세트를 만들고 관리할 수 있습니다. [!DNL Catalog] 에 대한 참조를 포함하는 각 데이터 세트에 대한 메타데이터를 추적합니다. [!DNL Experience Data Model] (XDM) 데이터 세트가 준수하는 스키마(다음 섹션에 설명) 및 해당 데이터 세트에 수집된 레코드 수.

다음을 참조하십시오. [카탈로그 서비스 개요](../home.md) 추가 정보.

## 데이터 세트 데이터에 대한 제한 적용

[!DNL Experience Data Model] (XDM)은 표준화된 프레임워크이며 [!DNL Platform] 고객 경험 데이터를 구성합니다. 에 수집되는 모든 데이터 [!DNL Platform] 에서 지속하려면 사전 정의된 XDM 스키마를 준수해야 합니다. [!DNL Data Lake] 데이터 세트로

모든 데이터 세트에는 저장할 수 있는 데이터의 형식 및 구조를 제한하는 XDM 스키마에 대한 참조가 포함됩니다. 데이터 세트의 XDM 스키마를 준수하지 않는 데이터 세트에 데이터를 업로드하려고 하면 수집이 실패합니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 데이터 세트에 데이터 수집

Adobe Experience Platform 데이터 수집은 다음과 같은 여러 가지 방법을 나타냅니다. [!DNL Platform] 다양한 소스에서 데이터를 수집합니다. 수집 방법에 관계없이 성공적으로 수집된 모든 데이터는 배치 파일로 변환됩니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 그런 다음 이러한 배치 파일이 전용 데이터 세트에 추가되고 [!DNL Data Lake].

다음을 참조하십시오. [데이터 수집 개요](../../ingestion/home.md) 추가 정보.

## 스키마에서 데이터 세트에 적용된 레이블

Adobe Experience Platform 데이터 거버넌스를 사용하면 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하도록 고객 데이터를 관리할 수 있습니다. 데이터 거버넌스 프레임워크를 사용하면 사용 레이블을 적용하여 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다. 레이블은 개별 스키마, 해당 스키마 내의 필드 및 전체 개별 데이터 세트에 적용할 수 있습니다. 레이블이 스키마에 직접 적용되면 해당 레이블은 해당 스키마를 기반으로 하는 모든 기존 및 향후 데이터 세트에 전파됩니다.

>[!IMPORTANT]
>
>더 이상 데이터 세트 수준의 필드에 레이블을 적용할 수 없습니다. 이 워크플로우는 더 이상 사용되지 않으며, 대신 스키마 수준에서 레이블을 적용합니다. 데이터 세트 개체 수준에서 이전에 적용된 모든 레이블은 2024년 5월 31일까지 Platform UI를 통해 계속 지원됩니다. 모든 스키마에서 레이블이 일관되도록 하려면 데이터 세트 수준의 필드에 이전에 첨부된 모든 레이블을 향후 연도에 따라 스키마 수준으로 마이그레이션해야 합니다. 의 섹션을 참조하십시오. [이전에 적용된 레이블 마이그레이션](../../data-governance/e2e.md#migrate-labels) 을 수행하는 방법에 대한 지침을 확인하십시오.

다음을 참조하십시오. [데이터 거버넌스 개요](../../data-governance/home.md) 를 참조하십시오. 에서 사용 레이블을 사용하여 작업하는 방법에 대한 단계 [!DNL Platform], 다음 안내서를 참조하십시오.

* [UI에서 레이블 관리](../../data-governance/labels/user-guide.md)
* [API에서 데이터 세트 레이블 관리](../../data-governance/labels/dataset-api.md)

## 다운스트림의 데이터 세트 [!DNL Platform] 서비스

수집된 데이터를 저장하는 데 데이터 세트가 사용되면 해당 데이터 세트는 다운스트림에서 사용됩니다 [!DNL Platform] 고객 프로필을 업데이트하고, 머신 러닝 등을 통해 통찰력을 얻는 서비스.

다음은 다양한 작업에 데이터 세트를 사용하는 다운스트림 서비스 목록입니다. 자세한 내용은 각 서비스에 대한 설명서를 참조하십시오.

* [[!DNL Data Access API]](../../data-access/home.md): 데이터 세트 내에 저장된 파일의 내용에 액세스하고 다운로드할 수 있습니다.
* [Adobe Experience Platform ID 서비스](../../identity-service/home.md): 디바이스와 시스템 간에 ID를 브리징하여 일치하는 XDM 스키마에 의해 정의된 ID 필드를 기반으로 데이터 세트를 서로 연결합니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 활용 [!DNL Identity Service] 을(를) 사용하여 실시간으로 데이터 세트에서 세부 고객 프로필을 만들 수 있습니다. [!DNL Real-Time Customer Profile] 에서 데이터 가져오기 [!DNL Data Lake] 별도의 데이터 저장소에서 고객 프로필을 유지합니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md): 세그먼트를 작성하고 의 대상자를 생성할 수 있습니다. [!DNL Real-Time Customer Profile] 데이터. 그런 다음 이러한 대상을 내의 자체 데이터 세트로 내보낼 수 있습니다. [!DNL Data Lake].
* [Adobe Experience Platform 데이터 과학 작업 영역](../../data-science-workspace/home.md): 머신 러닝 및 인공 지능을 사용하여 대규모 데이터 세트에서 통찰력을 발견합니다.
* [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md): 표준 SQL을 사용하여에서 데이터를 쿼리할 수 있습니다 [!DNL Experience Platform], 내의 모든 데이터 세트 결합 [!DNL Data Lake] 보고에 사용할 새 데이터 세트로 쿼리 결과 캡처 [!DNL Data Science Workspace], 또는 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform 대상 서비스](../../destinations/home.md): 다음 작업을 수행할 수 있습니다. [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md) 보고 또는 데이터 과학 활동을 위해 원하는 클라우드 스토리지 또는 이메일 마케팅 대상으로 이동합니다.

## 다음 단계

이 문서를 읽으면 의 데이터 세트 핵심 사용에 대해 이해할 수 있습니다 [!DNL Experience Platform]및 기타 [!DNL Platform] 데이터 세트를 활용하는 서비스. 에서 데이터 세트를 사용하는 여러 가지 방법에 대한 자세한 내용은 [!DNL Platform], 이 개요 전체에 연결된 서비스 설명서를 검토하십시오.

에서 데이터 세트와 상호 작용하는 방법에 대한 절차 [!DNL Experience Platform] UI에서 다음을 참조하십시오. [데이터 세트 사용 안내서](user-guide.md).
