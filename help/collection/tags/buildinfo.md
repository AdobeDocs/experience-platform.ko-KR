---
title: buildInfo
description: 사이트에 구현된 태그 빌드에 대한 정보를 얻습니다.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

`_satellite.buildInfo` 개체에는 구현된 태그 속성의 빌드에 대한 정보가 포함되어 있습니다. 이 개체는 자주 사용하는 빌드를 디버깅하여 최신 버전을 사용하고 있는지 확인할 때 가장 유용합니다.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## 사용 가능한 필드

다음 필드는 이 개체를 호출할 때 사용할 수 있습니다.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| **`minified`** | `boolean` | 라이브러리가 축소되었는지 여부를 나타냅니다. 프로덕션 빌드는 일반적으로 축소되지만(`true`), 개발 및 스테이징 빌드는 일반적으로 축소되지 않습니다(`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | JavaScript 파일을 빌드하고 게시한 날짜 및 시간입니다. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine)은(는) 태그 규칙을 처리하고 논리를 태그 확장에 위임하는 Adobe의 엔진입니다. 이 필드에는 태그 속성을 게시하는 데 사용되는 Turbine 빌드의 날짜와 시간이 포함됩니다. |
| **`turbineVersion`** | `string` | 태그 속성을 빌드하고 게시하는 데 사용되는 Turbine 버전입니다. |

`_satellite._container.buildInfo`에도 유사한 정보가 포함되어 있습니다. 자세한 내용은 [`_container`](container.md)을(를) 참조하십시오.
