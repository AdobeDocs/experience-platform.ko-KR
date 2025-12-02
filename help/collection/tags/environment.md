---
title: 환경에만 해당되는 결과를 반환합니다
description: 태그 속성이 현재 사용하는 빌드 환경입니다.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

`_satellite.environment` 개체는 태그 속성이 현재 사용 중인 빌드 환경을 나타냅니다.

```js
readonly _satellite.environment: Environment
```

## 사용 가능한 필드

다음 필드는 이 개체를 호출할 때 사용할 수 있습니다.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| 이름 | 유형 | 설명 |
|---|---|---|
| **`id`** | `string` | 환경에 대한 고유 식별자. 태그 UI에서 **[!UICONTROL Install]** 아래의 [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) 아이콘을 선택하여 환경 ID를 찾을 수 있습니다. |
| **`stage`** | `development \| staging \| production` | 환경 유형. |
