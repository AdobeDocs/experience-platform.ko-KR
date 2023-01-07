---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;프로필 사용;프로필 사용
title: 실시간 고객 프로필에 데이터 추가
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 에 데이터 추가 [!DNL Real-Time Customer Profile]

이 자습서에서는 데이터를 [!DNL Real-Time Customer Profile].

## 스키마 활성화 [!DNL Real-Time Customer Profile]

수집되는 데이터 [!DNL Experience Platform] 사용 [!DNL Real-Time Customer Profile] 반드시 [!DNL Experience Data Model] 에 활성화된 (XDM) 스키마 [!DNL Profile]. 프로필에 대해 스키마를 활성화하려면 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스 이름을 지정합니다.

에서 사용할 스키마를 활성화할 수 있습니다 [!DNL Real-Time Customer Profile] 사용 [!DNL Schema Registry] API 또는 [!DNL Schema Editor] 사용자 인터페이스. 시작하려면 다음의 자습서를 따르십시오. [api를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 UI를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-ui.md).

## 일괄 처리를 사용하여 데이터 추가

업로드된 모든 데이터 [!DNL Platform] 일괄 처리를 사용하여 개별 데이터 세트에 업로드됩니다. 이 데이터를 사용하려면 먼저 [!DNL Real-Time Customer Profile]로 지정하는 경우 해당 데이터 세트를 명시적으로 구성해야 합니다. 전체 지침은 [프로필 및 ID 서비스에 대한 데이터 세트 구성](dataset-configuration.md).

데이터 세트가 구성되면 데이터 집합에 데이터 수집을 시작할 수 있습니다. 자세한 내용은 [배치 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md) 를 참조하십시오.

## 스트리밍 수집 기능을 사용하여 데이터 추가

와 호환되는 모든 스트림 수집 데이터 [!DNL Profile]-enabled XDM 스키마는 자동으로 [!DNL Real-Time Customer Profile]. 레코드에 둘 이상의 ID가 제공되거나 시계열 데이터가 사용되는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 자세한 내용은 [스트리밍 수집 개발자 안내서](../../ingestion/tutorials/streaming-record-data.md) 추가 정보

## 업로드가 성공했는지 확인합니다

처음으로 데이터를 새 데이터 세트에 업로드하거나 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로, 데이터가 올바르게 업로드되었는지 여부를 신중하게 확인하는 것이 좋습니다.

사용 [!DNL Real-Time Customer Profile] API에 액세스하여 데이터 세트에 로드될 때 배치 데이터를 검색할 수 있습니다. 예상한 엔티티를 검색할 수 없는 경우 데이터 세트에 대해 를 사용할 수 없습니다 [!DNL Profile]. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 사용자의 기대를 지원하는지 확인합니다.

를 사용하여 엔티티에 액세스하는 방법에 대한 자세한 지침은 [!DNL Real-Time Customer Profile] API는 [엔티티 끝점 안내서](../api/entities.md)이라고도 하는 &quot;[!DNL Profile Access] API&quot;.

## 프로필 저장소 데이터 업데이트

간혹 조직의 프로필 저장소에서 데이터를 업데이트해야 할 수 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리를 통해 수행할 수 있으며, 후속 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 속성 업데이트를 위한 데이터 세트를 구성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [프로필 및 업데이트에 대한 데이터 세트 활성화](../../catalog/datasets/enable-upsert.md).
