---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로필에 데이터 추가
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# 실시간 고객 프로필에 데이터 추가

이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.

## 실시간 고객 프로필에 대한 스키마 활성화

실시간 고객 프로필에서 사용하기 위해 Experience Platform으로 인제스트되는 데이터는 프로필에 대해 활성화된 XDM(Experience Data Model) 스키마를 따라야 합니다. 프로파일에 대한 스키마를 활성화하려면 XDM 개별 프로필 또는 XDM ExperienceEvent 클래스를 구현해야 합니다.

스키마 레지스트리 API 또는 스키마 편집기 사용자 인터페이스를 사용하여 실시간 고객 프로필에서 사용할 스키마를 활성화할 수 있습니다. 시작하려면 API를 사용하여 스키마 [를](../../xdm/tutorials/create-schema-api.md) 만들거나 스키마 편집기 UI를 사용하여 스키마 [를 만드는 자습서에 따르십시오](../../xdm/tutorials/create-schema-ui.md).

## 일괄 처리를 사용하여 데이터 추가

일괄 처리를 사용하여 Platform에 업로드된 모든 데이터는 개별 데이터 세트에 업로드됩니다. 실시간 고객 프로필에서 이 데이터를 사용하려면 먼저 문제의 데이터 세트를 구체적으로 구성해야 합니다. 전체 지침은 프로필 및 ID 서비스에 대한 데이터 세트 [구성에 대한 자습서를 참조하십시오](dataset-configuration.md).

데이터 세트를 구성한 후에는 데이터 데이터 인제스트를 시작할 수 있습니다. 다양한 형식으로 파일을 업로드하는 방법에 대한 자세한 [단계는 일괄 처리 통합 개발자 안내서를](../../ingestion/batch-ingestion/api-overview.md) 참조하십시오.

## 스트리밍 통합 기능을 사용하여 데이터 추가

프로필 사용 XDM 스키마를 준수하는 모든 스트림 인제스트된 데이터는 실시간 고객 프로필에 해당 레코드를 자동으로 추가하거나 덮어씁니다. 레코드에 둘 이상의 ID를 제공하거나 시간 시리즈 데이터를 사용하는 경우 추가 구성 없이 해당 ID가 ID 그래프에 매핑됩니다. 자세한 내용은 [스트리밍 통합 개발자 가이드](../../ingestion/tutorials/streaming-record-data.md) 를 참조하십시오.

## 업로드가 성공했는지 확인

처음 또는 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로 데이터를 새 데이터 세트에 업로드할 때는 데이터가 올바르게 업로드되었는지 확인하기 위해 데이터를 신중하게 확인하는 것이 좋습니다.

실시간 고객 프로필 액세스 API를 사용하여 데이터 세트에 로드되는 대로 일괄 데이터를 검색할 수 있습니다. 원하는 엔터티를 검색할 수 없는 경우 데이터 세트에 프로필 기능이 활성화되지 않을 수 있습니다. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 기대를 충족하는지 확인하십시오.

실시간 고객 프로필 API를 사용하여 엔터티에 액세스하는 방법에 대한 자세한 지침은 &quot;프로필 액세스 API&quot;라고도 하는 [개체 끝점 안내서](../api/entities.md)를 참조하십시오.