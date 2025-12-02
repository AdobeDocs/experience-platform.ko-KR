---
title: 컨테이너(_C)
description: 단일 개체에서 전체 태그 컨테이너를 봅니다.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

`_satellite._container` 개체는 페이지에 로드된 태그 속성의 전체 구성 및 런타임 컨텍스트를 포함합니다. 규칙, 데이터 요소, 확장, 환경 등 모든 정보는 이 개체 내에서 사용할 수 있습니다. 주요 용도는 노출 또는 게시된 논리를 정확하게 볼 수 있도록 구현 디버깅을 지원하는 것입니다.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>이 개체는 디버깅 목적으로만 사용됩니다. 프로덕션 논리를 이 개체에 연결하지 않거나, 구현에서 이 개체를 참조하거나, 이 개체 내에서 값을 편집하지 마십시오. Adobe은 언제든지 이 개체 내의 속성 또는 이름을 변경할 수 있습니다.

## 사용 가능한 필드

다음 객체를 참조할 수 있습니다.

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

`_satellite._container.buildInfo` 개체에 [`_satellite.buildInfo`](buildinfo.md)의 복사본이 있습니다.

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

`_satellite._container.company` 개체에 [`_satellite.company`](company.md)의 복사본이 있습니다.

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

`_satellite._container.dataElements` 개체는 태그 속성 내의 모든 데이터 요소에 대한 참조를 제공합니다.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

각 데이터 요소에는 다음 속성이 포함됩니다.

| 이름 | 유형 | 설명 |
|---|---|---|
| **`modulePath`** | `string` | 해당 데이터 요소 유형의 논리를 결정하는 JavaScript 파일의 경로입니다. |
| **`settings`** | `Settings` | 데이터 요소의 설정입니다. 이 개체 내의 속성은 데이터 요소 유형에 따라 다릅니다. |

## `environment`

`_satellite._container.environment` 개체에 [`_satellite.environment`](environment.md)의 복사본이 있습니다.

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

`_satellite._container.extensions` 개체는 태그 속성에 게시된 모든 확장을 나열합니다.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

각 확장에는 다음 속성이 포함됩니다.

| 이름 | 유형 | 설명 |
|---|---|---|
| **`displayName`** | `string` | 확장에 대한 알기 쉬운 이름. |
| **`hostedLibFilesUrl`** | `string` | 확장이 있는 CDN의 위치입니다. |
| **`modules`** | `Modules` | 확장에서 사용하는 모든 이벤트, 작업, 조건 및 데이터 요소에 대한 JavaScript 논리입니다. 이 객체의 내용은 확장마다 다릅니다. |

## `property`

`_satellite._container.property` 개체는 태그 속성 자체에 대한 정보를 제공합니다.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| 이름 | 유형 | 설명 |
|---|---|---|
| **`id`** | `string` | 태그 속성에 대한 고유 식별자입니다. |
| **`name`** | `string` | 태그 속성에 대한 알기 쉬운 이름. |
| **`settings`** | `PropertySettings` | 이 속성에 대한 설정입니다. 아래 표를 참조하십시오. |

| 설정 이름 | 유형 | 설명 |
|---|---|---|
| **`domains`** | `string[]` | [태그 속성을 구성](/help/tags/ui/administration/companies-and-properties.md)할 때 설정된 속성에 대해 구성된 도메인입니다. |
| **`ruleComponentSequencingEnabled`** | `boolean` | 태그 속성을 구성할 때 **[!UICONTROL Run rule components in sequence]** 확인란을 사용할지 여부를 결정합니다. |
| **`undefinedVarsReturnEmpty`** | `boolean` | 태그 속성을 구성할 때 **[!UICONTROL Return an empty string for undefined data elements]** 확인란을 사용할지 여부를 결정합니다. |

## `_container.rules`

`rules` 개체 배열은 태그 속성 내의 모든 규칙에 대한 참조를 제공합니다.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

각 규칙에는 다음 필드가 포함되어 있습니다.

| 이름 | 유형 | 설명 |
|---|---|---|
| **`id`** | `string` | 규칙의 고유 식별자입니다. |
| **`name`** | `string` | 규칙에 대한 알기 쉬운 이름. |
| **`events`** | `Event[]` | 규칙을 트리거하도록 구성한 이벤트 배열입니다. |
| **`conditions`** | `Condition[]` | 규칙을 트리거하기 위해 구성한 조건 배열입니다. |
| **`actions`** | `Action[]` | 규칙이 트리거될 때 실행되도록 구성한 작업의 배열입니다. |
