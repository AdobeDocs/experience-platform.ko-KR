---
title: 회사
description: 구현된 태그 속성을 소유하는 IMS 조직에 대한 정보를 얻습니다.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

`_satellite.company` 개체는 태그 속성을 소유하는 IMS 조직 관련 정보를 표시합니다.

```ts
readonly _satellite.company: Company
```

## 사용 가능한 필드

이 개체를 호출할 때 사용할 수 있는 필드는 다음과 같습니다.

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| **`orgId`** | `string` | 태그 속성의 IMS 조직 ID. |
| **`dynamicCdnEnabled`** | `boolean` | 태그 속성이 Adobe의 동적 CDN 스위칭 기능을 사용하는지 여부를 결정합니다. `true`(으)로 설정하면 방문자가 위치에 따라 태그를 요청하는 CDN이 자동으로 전환됩니다. |
| **`cdnAllowList`** | `string[]` | 태그 속성을 로드할 수 있는 CDN입니다. |

`_satellite._container.company`에도 유사한 정보가 포함되어 있습니다. 자세한 내용은 [`_container`](container.md)을(를) 참조하십시오.
