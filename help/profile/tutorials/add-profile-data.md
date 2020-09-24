---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
title: 실시간 고객 프로필에 데이터 추가
topic: tutorial
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 데이터 추가 [!DNL Real-time Customer Profile]

이 자습서에서는 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다 [!DNL Real-time Customer Profile].

## 스키마 사용 [!DNL Real-time Customer Profile]

사용 [!DNL Experience Platform] 을 위해 수집되는 데이터는 에 활성화된 [!DNL Real-time Customer Profile] (XDM) 스키마를 [!DNL Experience Data Model] 준수해야 합니다 [!DNL Profile]. 프로필에 대해 스키마를 활성화하려면 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스를 구현해야 합니다.

API 또는 사용자 인터페이스 [!DNL Real-time Customer Profile] 를 사용하는 데 사용할 수 있는 스키마를 활성화할 수 [!DNL Schema Registry] [!DNL Schema Editor] 있습니다. 시작하려면 API를 사용하여 스키마 [를](../../xdm/tutorials/create-schema-api.md) 만들거나 스키마 편집기 UI를 사용하여 스키마 [를 만드는 자습서에 따르십시오](../../xdm/tutorials/create-schema-ui.md).

## 일괄 처리를 사용하여 데이터 추가

일괄 처리를 [!DNL Platform] 사용하여 업로드된 모든 데이터는 개별 데이터 세트에 업로드됩니다. 이 데이터를 사용하려면 먼저 해당 데이터 세트 [!DNL Real-time Customer Profile]를 구체적으로 구성해야 합니다. 전체 지침은 프로필 및 ID 서비스에 대한 데이터 세트 [구성에 대한 자습서를 참조하십시오](dataset-configuration.md).

데이터 세트를 구성한 후에는 데이터 데이터 인제스트를 시작할 수 있습니다. 다양한 형식으로 파일을 업로드하는 방법에 대한 자세한 [단계는 일괄 처리 통합 개발자 안내서를](../../ingestion/batch-ingestion/api-overview.md) 참조하십시오.

## 스트리밍 통합 기능을 사용하여 데이터 추가

XDM 스키마를 준수하는 모든 스트림 인제스트된 데이터는 [!DNL Profile]해당 레코드를 자동으로 추가하거나 덮어씁니다 [!DNL Real-time Customer Profile]. 레코드에 둘 이상의 ID를 제공하거나 시간 시리즈 데이터를 사용하는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 자세한 내용은 [스트리밍 통합 개발자 가이드](../../ingestion/tutorials/streaming-record-data.md) 를 참조하십시오.

## 업로드가 성공했는지 확인

처음 또는 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로 데이터를 새 데이터 세트에 업로드할 때는 데이터가 올바르게 업로드되었는지 확인하기 위해 데이터를 신중하게 확인하는 것이 좋습니다.

액세스 [!DNL Real-time Customer Profile] API를 사용하여 일괄 처리 데이터가 데이터 세트에 로드될 때 이를 검색할 수 있습니다. 원하는 엔터티를 검색할 수 없는 경우 데이터 세트에 대한 기능이 활성화되지 않을 수 있습니다 [!DNL Profile]. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 기대를 충족하는지 확인하십시오.

API를 사용하여 엔터티에 액세스하는 방법에 대한 자세한 지침은 &quot; [!DNL Real-time Customer Profile] API&quot;라고도 하는 [엔티티 끝점 안내서](../api/entities.md)를 참조하십시오[!DNL Profile Access] .