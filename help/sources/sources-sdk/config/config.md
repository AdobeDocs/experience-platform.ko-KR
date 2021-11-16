---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 소스 SDK의 구성 옵션
topic-legacy: overview
description: 이 문서에서는 소스 SDK를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 1%

---

# 소스 SDK의 구성 옵션

>[!IMPORTANT]
>
>소스 SDK는 현재 베타 버전이며 조직에서 아직 액세스할 수 없습니다. 이 설명서에 설명된 기능은 변경될 수 있습니다.

이 문서에서는 소스 SDK를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.

## 연결 사양

연결 사양은 소스의 커넥터 속성을 반환합니다. 여기에는 기본 및 소스 연결 생성과 관련된 인증 사양과 특정 소스에 할당된 고정 연결 사양 ID가 포함됩니다. 연결 사양은 테넌트 및 IMS 조직에 관계 없습니다. 일반적인 연결 사양은 특정 소스에 대한 기본 정보와 세 개의 개별 섹션을 포함합니다. `authSpec`, `sourceSpec`, 및 `exploreSpec`.

| 사양 | 설명 |
| --- | --- |
| `authSpec` | 다음 `authSpec` 배열에 소스를 Platform에 연결하는 데 필요한 인증 매개 변수에 대한 정보가 포함되어 있습니다. 지정된 모든 소스는 다양한 유형의 인증을 지원할 수 있습니다. |
| `sourceSpec` | 다음 `sourceSpec` 배열에는 UI에서 소스를 제공하는 데 필요한 속성에 대한 정보, 설명서 링크, 페이지 매김, 헤더, 본문 및 예약과 관련된 매개 변수 등 소스와 관련된 일반 정보가 포함되어 있습니다. 또한, `sourceSpec` 기본 연결에서 소스 연결을 만드는 데 필요한 매개 변수의 스키마에 대해 설명하고 소스 연결을 만드는 데 필요합니다. |
| `exploreSpec` | 다음 `exploreSpec` 배열은 소스에 포함된 객체를 탐색하고 검사하는 데 필요한 매개변수를 정의합니다. 다음 `exploreSpec` 또한 객체를 탐색하고 검사할 때 반환되는 응답 형식을 정의합니다. |

{style=&quot;table-layout:auto&quot;}

## 연결 사양 값을 채웁니다

연결 사양은 세 개의 개별 부분으로 나눌 수 있습니다. 인증 사양, 소스 사양 및 탐색 사양입니다.

연결 사양의 각 부분의 값을 채우는 방법에 대한 지침은 다음 문서를 참조하십시오.

* [인증 사양 구성](./authspec.md)
* [소스 사양 구성](./sourcespec.md)
* [탐색 사양 구성](./explorespec.md)


