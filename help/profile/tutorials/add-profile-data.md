---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;프로필 활성화;프로필 활성화
title: 실시간 고객 프로필에 데이터 추가
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계에 대해 설명합니다.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# [!DNL Real-Time Customer Profile]에 데이터 추가

이 튜토리얼에서는 [!DNL Real-Time Customer Profile]에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.

## [!DNL Real-Time Customer Profile]에 대한 스키마 활성화

[!DNL Real-Time Customer Profile]에서 사용하기 위해 [!DNL Experience Platform]에 수집되는 데이터는 [!DNL Profile]에 대해 활성화된 [!DNL Experience Data Model]&#x200B;(XDM) 스키마를 준수해야 합니다. 프로필에 대해 스키마를 활성화하려면 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스를 구현해야 합니다.

[!DNL Schema Registry] API 또는 [!DNL Schema Editor] 사용자 인터페이스를 사용하여 [!DNL Real-Time Customer Profile]에서 사용할 스키마를 활성화할 수 있습니다. 시작하려면 [API를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 UI를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-ui.md)에 대한 자습서를 따르십시오.

## 일괄 처리 수집을 사용하여 데이터 추가

일괄 처리 수집을 사용하여 [!DNL Experience Platform]에 업로드된 모든 데이터는 개별 데이터 세트에 업로드됩니다. [!DNL Real-Time Customer Profile]에서 이 데이터를 사용하려면 먼저 해당 데이터 세트를 구체적으로 구성해야 합니다. 자세한 지침은 [프로필 및 ID 서비스에 대한 데이터 집합 구성](dataset-configuration.md)에 대한 자습서를 참조하십시오.

데이터 세트가 구성되면 데이터 세트로의 데이터 수집을 시작할 수 있습니다. 다양한 형식의 파일을 업로드하는 방법에 대한 자세한 단계는 [일괄 처리 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md)를 참조하십시오.

## 스트리밍 수집을 사용한 데이터 추가

[!DNL Profile] 사용 XDM 스키마와 호환되는 스트림 수집 데이터는 [!DNL Real-Time Customer Profile]의 해당 레코드를 자동으로 추가하거나 덮어씁니다. 레코드에 둘 이상의 ID가 제공되거나 시계열 데이터가 사용되는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 자세한 내용은 [스트리밍 수집 개발자 안내서](../../ingestion/tutorials/streaming-record-data.md)를 참조하십시오.

## 업로드가 성공했는지 확인

데이터를 새 데이터 세트에 처음 업로드할 때, 또는 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로 데이터가 올바르게 업로드되었는지 주의 깊게 확인하는 것이 좋습니다.

[!DNL Real-Time Customer Profile] Access API를 사용하면 일괄 처리 데이터를 데이터 세트로 로드할 때 검색할 수 있습니다. 예상한 엔터티를 검색할 수 없는 경우 [!DNL Profile]에 대해 데이터 집합을 사용할 수 없습니다. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 기대를 지원하는지 확인합니다.

[!DNL Real-Time Customer Profile] API를 사용하여 엔터티에 액세스하는 방법에 대한 자세한 지침은 &quot;[!DNL Profile Access] API&quot;라고도 하는 [엔터티 끝점 안내서](../api/entities.md)를 참조하십시오.

## 프로필 저장소 데이터 업데이트

조직의 프로필 스토어에서 데이터를 업데이트해야 하는 경우가 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리 수집을 통해 수행할 수 있으며 업데이트 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 특성 업데이트에 대한 데이터 집합을 구성하는 방법에 대한 자세한 내용은 [프로필 및 업데이트에 대한 데이터 집합 활성화](../../catalog/datasets/enable-upsert.md)에 대한 자습서를 참조하십시오.
