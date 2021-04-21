---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;프로필 사용;프로필 사용;프로필 사용
title: 실시간 고객 프로필에 데이터 추가
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 설명합니다.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]에 데이터 추가

이 자습서에서는 [!DNL Real-time Customer Profile]에 데이터를 추가하는 데 필요한 단계를 설명합니다.

## [!DNL Real-time Customer Profile]에 대한 스키마 사용

[!DNL Real-time Customer Profile]에서 사용하기 위해 인제스트되는 데이터는 [!DNL Profile]에 대해 활성화된 [!DNL Experience Data Model](XDM) 스키마를 따라야 합니다. [!DNL Experience Platform] 프로파일에 대해 스키마를 활성화하려면 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스를 구현해야 합니다.

[!DNL Schema Registry] API 또는 [!DNL Schema Editor] 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화할 수 있습니다. 시작하려면 [API를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 UI](../../xdm/tutorials/create-schema-ui.md)를 사용하여 스키마 만들기에 대한 자습서를 따르십시오.

## 일괄 처리를 사용하여 데이터 추가

일괄 처리를 사용하여 [!DNL Platform]에 업로드된 모든 데이터는 개별 데이터 세트에 업로드됩니다. 이 데이터를 [!DNL Real-time Customer Profile]에서 사용하려면 먼저 문제의 데이터 세트를 구체적으로 구성해야 합니다. 전체 지침은 [프로필 및 ID 서비스](dataset-configuration.md)에 대한 데이터 세트 구성에 대한 자습서를 참조하십시오.

데이터 세트를 구성한 후에는 데이터 데이터 데이터 인제스트를 시작할 수 있습니다. 다른 형식으로 파일을 업로드하는 방법에 대한 자세한 내용은 [일괄 처리 통합 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md)를 참조하십시오.

## 스트리밍 통합 기능을 사용하여 데이터 추가

[!DNL Profile] 활성화된 XDM 스키마를 준수하는 모든 스트림 인제스트된 데이터는 자동으로 [!DNL Real-time Customer Profile]에 해당 레코드를 추가하거나 덮어씁니다. 레코드에 둘 이상의 ID를 제공하거나 시간 시리즈 데이터를 사용하는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 자세한 내용은 [스트리밍 통합 개발자 가이드](../../ingestion/tutorials/streaming-record-data.md)를 참조하십시오.

## 업로드가 성공했는지 확인

처음 또는 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로 데이터를 새 데이터 세트에 업로드할 때는 데이터가 올바르게 업로드되었는지 확인하기 위해 데이터를 주의 깊게 확인하는 것이 좋습니다.

[!DNL Real-time Customer Profile] 액세스 API를 사용하여 일괄 처리 데이터가 데이터 세트에 로드될 때 이를 가져올 수 있습니다. 원하는 엔티티를 검색할 수 없는 경우 데이터 세트에 [!DNL Profile]이(가) 활성화되지 않을 수 있습니다. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 예상치를 지원하는지 확인하십시오.

[!DNL Real-time Customer Profile] API를 사용하여 엔터티에 액세스하는 방법에 대한 자세한 지침은 &quot;[!DNL Profile Access] API&quot;라고도 하는 [개체 끝점 안내서](../api/entities.md)를 참조하십시오.
