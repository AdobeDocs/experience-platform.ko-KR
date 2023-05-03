---
keywords: Experience Platform;홈;인기 항목;데이터 위치;데이터 위치;데이터 관리;계보;계보;계보;데이터 유형;데이터 유형;데이터 유형;데이터 유형
solution: Experience Platform
title: 데이터 세트 개요
description: 이 설명서는 Experience Platform의 데이터 세트에 대한 높은 수준의 개요를 제공합니다.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 8%

---

# 데이터 세트 개요

Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 [!DNL Data Lake] 을 데이터 세트로 사용합니다. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.

이 문서에서는 [!DNL Experience Platform].

## 데이터 세트 만들기 및 추적 메타데이터

[!DNL Catalog Service] 는 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다 [!DNL Experience Platform]과 는 데이터 세트를 만들고 관리하는 데 사용됩니다. [!DNL Catalog] 는 각 데이터 세트에 대한 참조를 포함하는 메타데이터를 추적합니다 [!DNL Experience Data Model] (XDM) 데이터 세트가 준수하는 스키마(다음 섹션에 설명되어 있음) 및 해당 데이터 세트에 수집된 레코드 수입니다.

자세한 내용은 [카탈로그 서비스 개요](../home.md) 추가 정보.

## 데이터 집합 데이터에 대한 제한 적용

[!DNL Experience Data Model] (XDM)은 [!DNL Platform] 고객 경험 데이터를 구성합니다. 수집되는 모든 데이터 [!DNL Platform] 에서 지속하려면 미리 정의된 XDM 스키마를 준수해야 합니다 [!DNL Data Lake] 데이터 세트로 사용

모든 데이터 세트에는 저장할 수 있는 데이터의 형식과 구조를 제한하는 XDM 스키마 참조를 포함합니다. 데이터 집합의 XDM 스키마를 따르지 않는 데이터 집합에 데이터를 업로드하려고 하면 섭취 오류가 발생합니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 데이터를 데이터 세트에 수집

Adobe Experience Platform 데이터 수집은 [!DNL Platform] 는 다양한 소스의 데이터를 설정합니다. 수집 방법과 관계없이 성공적으로 수집된 모든 데이터는 배치 파일로 변환됩니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 그런 다음 이러한 배치 파일을 전용 데이터 세트에 추가되고 [!DNL Data Lake].

자세한 내용은 [데이터 수집 개요](../../ingestion/home.md) 추가 정보.

## 데이터 세트에 사용 레이블 적용

Adobe Experience Platform 데이터 거버넌스를 사용하면 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하도록 고객 데이터를 관리할 수 있습니다. 데이터 거버넌스 프레임워크를 사용하면 사용 레이블을 적용하여 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

>[!IMPORTANT]
>
>데이터 세트 수준에서 레이블을 적용하는 것은 데이터 거버넌스 사용 사례에만 지원됩니다. 데이터에 대한 액세스 정책을 만들려고 하는 경우 다음을 수행해야 합니다 [스키마에 레이블 적용](../../xdm/tutorials/labels.md) 데이터 세트가 기반으로 합니다. 다음 사항에 대한 개요를 참조하십시오. [속성 기반 액세스 제어](../../access-control/abac/overview.md) 추가 정보.

데이터 사용 레이블은 전체 데이터 세트 또는 개별 데이터 세트 필드에 적용할 수 있습니다. 데이터 세트 수준에 추가된 레이블은 해당 데이터 세트 내의 모든 필드에 의해 상속됩니다.

자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md) 를 참조하십시오. 의 사용 레이블 사용 방법에 대한 절차 [!DNL Platform]에서 다음 안내서를 참조하십시오.

* [UI에서 레이블 관리](../../data-governance/labels/user-guide.md)
* [API에서 데이터 세트 레이블 관리](../../data-governance/labels/dataset-api.md)

## 다운스트림의 데이터 세트 [!DNL Platform] 서비스

수집된 데이터를 저장하는 데 데이터 세트를 사용하면 해당 데이터 세트를 다운스트림에서 사용합니다 [!DNL Platform] 머신 러닝을 통해 고객 프로필을 업데이트하고 통찰력을 얻을 수 있는 서비스

다음은 다양한 작업에 데이터 세트를 사용하는 다운스트림 서비스 목록입니다. 자세한 내용은 각 서비스의 설명서를 참조하십시오.

* [[!DNL Data Access API]](../../data-access/home.md): 데이터 세트 내에 저장된 파일의 컨텐츠에 액세스하고 다운로드할 수 있습니다.
* [Adobe Experience Platform Identity 서비스](../../identity-service/home.md): 장치 및 시스템 간에 ID를 브리징하여 XDM 스키마에서 정의한 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 활용 [!DNL Identity Service] 데이터 세트에서 실시간으로 세부 고객 프로필을 만들 수 있습니다. [!DNL Real-Time Customer Profile] 에서 데이터 가져오기 [!DNL Data Lake] 에서는 고객 프로필을 별도의 데이터 저장소에서 유지합니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md): 세그먼트를 작성하고 페이지의 [!DNL Real-Time Customer Profile] 데이터. 그런 다음 이러한 대상을 내의 고유한 데이터 세트로 내보낼 수 있습니다 [!DNL Data Lake].
* [Adobe Experience Platform 데이터 과학 작업 공간](../../data-science-workspace/home.md): 머신 러닝 및 인공 지능을 사용하여 대규모 데이터 세트에서 통찰력을 얻을 수 있습니다.
* [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md): 표준 SQL을 사용하여 데이터를 쿼리할 수 있습니다. [!DNL Experience Platform], 내에서 데이터 세트 가입 [!DNL Data Lake] 쿼리 결과를 보고에 사용할 새로운 데이터 세트로 캡처하고 [!DNL Data Science Workspace], 또는 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform 대상 서비스](../../destinations/home.md): 다음을 수행할 수 있습니다. [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md) 보고 또는 데이터 과학 활동을 위해 원하는 클라우드 스토리지 또는 이메일 마케팅 대상에 추가합니다.

## 다음 단계

이 문서를 다 읽으면에서 데이터 세트의 핵심 사용에 대해 알게 되었습니다 [!DNL Experience Platform]뿐만 아니라 [!DNL Platform] 데이터 세트를 활용하는 서비스. 에서 데이터 세트를 사용하는 여러 방법에 대한 자세한 내용 [!DNL Platform]를 검색하는 경우, 이 개요 전체에서 연결된 서비스 설명서를 검토하십시오.

내에서 데이터 세트와 상호 작용하는 방법에 대한 절차 [!DNL Experience Platform] UI를 참조하고 [데이터 세트 사용 안내서](user-guide.md).
