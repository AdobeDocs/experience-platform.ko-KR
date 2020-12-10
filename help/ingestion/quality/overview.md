---
keywords: Experience Platform;home;popular topics;Data quality;quality;Quality;Supported validation;Validation;supported validation;
solution: Experience Platform
title: 데이터 수집 품질
topic: overview
description: 다음 문서에서는 Adobe Experience Platform에서 일괄 처리 및 스트리밍 인제스트를 위한 지원되는 검사 및 유효성 검사 동작에 대한 요약을 제공합니다.
translation-type: tm+mt
source-git-commit: cfdaf72b7f4bf190877006ccd4cc6a7fd014adc2
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 5%

---


# Adobe Experience Platform의 데이터 품질

Adobe Experience Platform은 일괄 처리 또는 스트리밍 통합(ingestion)을 통해 업로드된 모든 데이터의 완벽성, 정확성 및 일관성에 대해 잘 정의된 보안을 제공합니다. 다음 문서에서는 일괄 처리 및 스트리밍 인제스트를 위한 지원되는 검사 및 유효성 검사 동작에 대한 요약을 제공합니다 [!DNL Experience Platform].

## 지원되는 검사

|   | 일괄 처리 | 스트리밍 통합 |
| ------ | --------------- | ------------------- |
| 데이터 유형 확인 | 예 | 예 |
| 열거형 검사 | 예 | 예 |
| 범위 확인(최소, 최대) | 예 | 예 |
| 필수 필드 확인 | 예 | 예 |
| 패턴 검사 | 아니요 | 예 |
| 포맷 확인 | 아니요 | 예 |

## 지원되는 유효성 검사 동작

일괄 처리 및 스트리밍 통합 모두 검색 및 분석을 위해 잘못된 데이터를 이동하여 실패한 데이터가 다운되는 것을 방지합니다 [!DNL Data Lake]. 데이터 수집은 일괄 처리 및 스트리밍 인제스트를 위한 다음과 같은 유효성 검사를 제공합니다.

### 일괄 처리

일괄 처리를 위해 다음 유효성 검사가 수행됩니다.

| 유효성 검사 영역 | 설명 |
| --------------- | ----------- |
| 스키마 | 스키마가 비어 있지 **않고** 다음과 같이 결합 스키마에 대한 참조를 포함하는지 확인합니다. `"meta:immutableTags": ["union"]` |
| `identityField` | 모든 유효한 ID 설명자가 정의되어 있는지 확인합니다. |
| `createdUser` | 배치를 인제스트한 사용자가 배치를 인제스트할 수 있는지 확인합니다. |

### 스트리밍 통합

다음 유효성 검사가 스트리밍 습득 수행됩니다.

| 유효성 검사 영역 | 설명 |
| --------------- | ----------- |
| 스키마 | 스키마가 비어 있지 **않고** 다음과 같이 결합 스키마에 대한 참조를 포함하는지 확인합니다. `"meta:immutableTags": ["union"]` |
| `identityField` | 모든 유효한 ID 설명자가 정의되어 있는지 확인합니다. |
| JSON | JSON이 유효한지 확인합니다. |
| IMS 조직 | 나열된 IMS 조직이 유효한 조직인지 확인합니다. |
| 소스 이름 | 데이터 소스의 이름이 지정되었는지 확인합니다. |
| 데이터 집합 | 데이터 세트를 지정, 활성화 및 제거하지 않았는지 확인합니다. |
| Header | 헤더가 지정되고 유효한지 확인합니다. |

데이터를 모니터링하고 검증하는 방법에 대한 자세한 내용은 [!DNL Platform] 모니터링 데이터 흐름 설명서를 참조하십시오 [](./monitor-data-ingestion.md).
