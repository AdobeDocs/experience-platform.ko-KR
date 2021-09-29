---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;프로필 사용;프로필 사용
title: 실시간 고객 프로필에 데이터 추가
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile]에 데이터 추가

이 자습서에서는 [!DNL Real-time Customer Profile]에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.

## [!DNL Real-time Customer Profile]에 대한 스키마 활성화

[!DNL Real-time Customer Profile]에서 사용하기 위해 [!DNL Experience Platform]에 수집되는 데이터는 [!DNL Profile]에 대해 활성화된 [!DNL Experience Data Model] (XDM) 스키마를 준수해야 합니다. 프로필에 대해 스키마를 활성화하려면 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스를 구현해야 합니다.

[!DNL Schema Registry] API 또는 [!DNL Schema Editor] 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화할 수 있습니다. 시작하려면 [API](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 UI](../../xdm/tutorials/create-schema-ui.md)를 사용하여 스키마를 만들기 위한 자습서에 따르십시오.

## 일괄 처리를 사용하여 데이터 추가

일괄 처리를 사용하여 [!DNL Platform]에 업로드된 모든 데이터는 개별 데이터 세트에 업로드됩니다. 이 데이터를 [!DNL Real-time Customer Profile]에서 사용하려면 먼저 해당 데이터 세트를 명시적으로 구성해야 합니다. 전체 지침은 [프로필 및 ID 서비스에 대한 데이터 세트 구성](dataset-configuration.md)에서 자습서를 참조하십시오.

데이터 세트가 구성되면 데이터 집합에 데이터 수집을 시작할 수 있습니다. 다른 형식으로 파일을 업로드하는 방법에 대한 자세한 단계는 [배치 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md)를 참조하십시오.

## 스트리밍 수집 기능을 사용하여 데이터 추가

[!DNL Profile] 사용 XDM 스키마와 호환되는 스트림이 수집된 데이터는 자동으로 [!DNL Real-time Customer Profile]에 해당 레코드를 추가하거나 덮어씁니다. 레코드에 둘 이상의 ID가 제공되거나 시계열 데이터가 사용되는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 자세한 내용은 [스트리밍 수집 개발자 안내서](../../ingestion/tutorials/streaming-record-data.md)를 참조하십시오.

## 업로드가 성공했는지 확인합니다

처음으로 데이터를 새 데이터 세트에 업로드하거나 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로, 데이터가 올바르게 업로드되었는지 여부를 신중하게 확인하는 것이 좋습니다.

[!DNL Real-time Customer Profile] Access API를 사용하여 일괄 처리 데이터가 데이터 세트에 로드될 때 검색할 수 있습니다. 원하는 엔터티를 검색할 수 없는 경우 [!DNL Profile]에 대해 데이터 집합을 사용할 수 없습니다. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 사용자의 기대를 지원하는지 확인합니다.

[!DNL Real-time Customer Profile] API를 사용하여 엔터티에 액세스하는 방법에 대한 자세한 지침은 [엔티티 엔드포인트 가이드](../api/entities.md)(&quot;[!DNL Profile Access] API&quot;라고도 함)를 참조하십시오.

## 프로필 저장소 데이터 업데이트

간혹 조직의 프로필 저장소에서 데이터를 업데이트해야 할 수 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리 또는 스트리밍 처리를 통해 수행할 수 있으며, 업로드 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 특성 업데이트를 위한 데이터 집합을 구성하는 방법에 대한 자세한 내용은 [프로필 데이터 집합 활성화 및 업데이트](../../catalog/datasets/enable-upsert.md)에 대한 자습서를 참조하십시오.
