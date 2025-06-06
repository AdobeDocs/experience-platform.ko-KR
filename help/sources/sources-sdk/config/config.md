---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프서비스 소스의 구성 옵션(일괄 SDK)
description: 이 문서에서는 셀프서비스 소스(일괄 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 셀프서비스 소스의 구성 옵션(일괄 SDK)

이 문서에서는 셀프서비스 소스(일괄 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.

## 연결 사양

연결 사양은 소스의 커넥터 속성을 반환합니다. 여기에는 기본 및 소스 연결 생성과 관련된 인증 사양과 특정 소스에 지정된 고정 연결 사양 ID가 포함됩니다. 연결 사양은 테넌트와 조직에 관계 없습니다. 일반적인 연결 사양에는 특정 소스에 대한 기본 정보와 세 개의 고유한 섹션(`authSpec`, `sourceSpec` 및 `exploreSpec`)이 포함됩니다.

| 사양 | 설명 |
| --- | --- |
| `authSpec` | `authSpec` 배열에는 원본을 Experience Platform에 연결하는 데 필요한 인증 매개 변수에 대한 정보가 포함되어 있습니다. 지정된 모든 소스는 서로 다른 여러 유형의 인증을 지원할 수 있습니다. |
| `sourceSpec` | `sourceSpec` 배열에는 UI에 소스를 제공하는 데 필요한 특성 정보, 설명서 링크, 페이지 매김, 헤더, 본문 및 예약에 대한 매개 변수 등 소스와 관련된 일반 정보가 포함되어 있습니다. 또한 `sourceSpec`은(는) 기본 연결에서 원본 연결을 만드는 데 필요한 매개 변수의 스키마를 설명하며 원본 연결을 만드는 데 필요합니다. |
| `exploreSpec` | `exploreSpec` 배열은 소스에 포함된 개체를 탐색하고 검사하는 데 필요한 매개 변수를 정의합니다. `exploreSpec`은(는) 개체를 탐색하고 검사할 때 반환되는 응답 형식도 정의합니다. |

{style="table-layout:auto"}

## 연결 사양 값 채우기

연결 사양은 인증 사양, 소스 사양 및 탐색 사양의 세 부분으로 나눌 수 있습니다.

연결 사양의 각 부분 값을 채우는 방법에 대한 지침은 다음 문서를 참조하십시오.

* [인증 사양 구성](./authspec.md)
* [소스 사양 구성](./sourcespec.md)
* [탐색 사양 구성](./explorespec.md)
