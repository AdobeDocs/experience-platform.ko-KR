---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;프로필 활성화;프로필 활성화
title: 실시간 고객 프로필에 데이터 추가
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계에 대해 설명합니다.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 데이터 추가 [!DNL Real-Time Customer Profile]

이 튜토리얼에서는에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다. [!DNL Real-Time Customer Profile].

## 다음에 대한 스키마 활성화: [!DNL Real-Time Customer Profile]

데이터 수집 대상 [!DNL Experience Platform] 사용: [!DNL Real-Time Customer Profile] 은(는) 다음을 준수해야 합니다. [!DNL Experience Data Model] 에 대해 활성화된 (XDM) 스키마 [!DNL Profile]. 프로필에 대해 스키마를 활성화하려면 다음 중 하나를 구현해야 합니다 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스.

에서 사용할 스키마를 활성화할 수 있습니다. [!DNL Real-Time Customer Profile] 사용 [!DNL Schema Registry] API 또는 [!DNL Schema Editor] 사용자 인터페이스. 시작하려면 다음 튜토리얼을 따르십시오 [api를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 UI를 사용하여 스키마 생성](../../xdm/tutorials/create-schema-ui.md).

## 일괄 처리 수집을 사용하여 데이터 추가

모든 데이터를에 업로드함 [!DNL Platform] 일괄 처리 수집 사용은 개별 데이터 세트에 업로드됩니다. 이 데이터를 사용할 수 있는 사람: [!DNL Real-Time Customer Profile]: 해당 데이터 세트를 구체적으로 구성해야 합니다. 전체 지침은 다음 튜토리얼 을 참조하십시오. [프로필 및 ID 서비스에 대한 데이터 세트 구성](dataset-configuration.md).

데이터 세트가 구성되면 데이터 세트로의 데이터 수집을 시작할 수 있습니다. 다음을 참조하십시오. [일괄 처리 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md) 다른 형식으로 파일을 업로드하는 방법에 대한 자세한 단계입니다.

## 스트리밍 수집을 사용한 데이터 추가

를 준수하는 스트림 수집된 모든 데이터 [!DNL Profile]-enabled XDM 스키마는에서 적절한 레코드를 자동으로 추가하거나 덮어씁니다. [!DNL Real-Time Customer Profile]. 레코드에 둘 이상의 ID가 제공되거나 시계열 데이터가 사용되는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 다음을 참조하십시오. [스트리밍 수집 개발자 안내서](../../ingestion/tutorials/streaming-record-data.md) 자세히 알아보십시오.

## 업로드가 성공했는지 확인

데이터를 새 데이터 세트에 처음 업로드할 때, 또는 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로 데이터가 올바르게 업로드되었는지 주의 깊게 확인하는 것이 좋습니다.

사용 [!DNL Real-Time Customer Profile] API에 액세스하여 데이터 세트에 로드될 때 배치 데이터를 검색할 수 있습니다. 예상한 엔티티를 검색할 수 없는 경우 데이터 세트가 활성화되지 않을 수 있습니다 [!DNL Profile]. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 기대를 지원하는지 확인합니다.

를 사용하여 엔티티에 액세스하는 방법에 대한 자세한 지침은 [!DNL Real-Time Customer Profile] API, 다음을 참조하십시오. [엔티티 끝점 안내서](../api/entities.md), &quot;라고도 함[!DNL Profile Access] API&quot;.

## 프로필 저장소 데이터 업데이트

조직의 프로필 스토어에서 데이터를 업데이트해야 하는 경우가 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리 수집을 통해 수행할 수 있으며 업데이트 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 속성 업데이트를 위한 데이터 세트를 구성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [프로필 및 업데이트에 대한 데이터 세트 활성화](../../catalog/datasets/enable-upsert.md).
