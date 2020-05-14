---
title: 지원 동의
seo-title: Adobe Experience Platform 웹 SDK 동의 기본 설정 지원
description: Experience Platform 웹 SDK를 사용하여 동의 기본 설정을 지원하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 동의 기본 설정을 지원하는 방법 살펴보기
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# 지원 동의

사용자의 개인 정보를 존중하기 위해 SDK가 특정 목적을 위해 사용자별 데이터를 사용하도록 허용하기 전에 사용자의 동의를 요청할 수 있습니다. 현재, SDK는 사용자가 모든 목적의 사용을 옵트인하거나 옵트아웃할 수 있도록 허용하지만, 향후에 Adobe는 특정 목적을 보다 세부적으로 제어하기를 바랍니다.

사용자가 모든 목적으로 액세스하는 경우 SDK는 다음 작업을 수행할 수 있습니다.

* Adobe의 서버로 데이터를 전송합니다.
* 쿠키 또는 웹 저장소 항목을 읽고 씁니다(사용자의 옵트인 환경 설정을 유지하는 경우는 제외).

사용자가 모든 목적을 벗어나는 경우 SDK는 이러한 작업을 수행하지 않습니다.

## 동의 구성

기본적으로 사용자는 모든 목적으로 선택되어 있습니다. 사용자가 로그인할 때까지 SDK가 위의 작업을 수행하지 않도록 하려면 다음과 같이 SDK 구성 `"defaultConsent": { "general": "pending" }` 동안 전달합니다.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

일반 용도에 대한 기본 동의가 보류 중으로 설정된 경우 사용자 옵트인 환경 설정(예: 명령)에 의존하는 모든 명령을 실행하려고 하면 SDK 내에서 명령이 대기됩니다. `event` 이러한 명령은 사용자의 옵트인 환경 설정을 SDK에 전달해야만 처리됩니다.

이 경우 사용자에게 사용자 인터페이스 내 특정 위치에서 옵트인하도록 요청할 수 있습니다. 사용자의 기본 설정이 수집되면 SDK에 이러한 기본 설정을 알립니다.

## 동의 기본 사항 통신

사용자가 옵션을 선택한 경우 다음 `setConsent` `general` `in` 과 같이 옵션을 설정하여 명령을 실행합니다.

```javascript
alloy("setConsent", {
  "general": "in"
});
```

사용자가 이제 옵트인되었으므로 SDK는 이전에 큐에 있는 모든 명령을 실행합니다. 옵트인된 사용자에 따라 달라지는 향후 명령은 큐에 _들어가지_ 않고 즉시 실행됩니다.

사용자가 옵트아웃을 선택한 경우 다음과 같이 옵션을 설정하여 `setConsent` 명령을 `general``out` 실행합니다.

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>사용자가 옵트아웃한 후에는 SDK에서 사용자에게 동의 설정을 허용하지 않습니다 `in`.

사용자가 옵트아웃을 선택했기 때문에 이전에 큐에 있는 명령에서 반환된 약속이 거부됩니다. 사용자가 선택한 이후에 명령하면 비슷하게 거부된 약속이 반환됩니다. 오류 처리 또는 억제에 대한 자세한 내용은 명령 [실행을 참조하십시오](executing-commands.md).

>[!NOTE]
>
>현재 SDK는 `general` 목적만 지원합니다. Adobe는 서로 다른 Adobe 기능 및 제품 오퍼에 해당하는 보다 강력한 목적 또는 카테고리를 구축할 계획이지만, 현재 구현은 옵트인에 대한 전체 또는 무제한으로 접근할 수 있습니다.  이는 Adobe Experience Platform 웹 SDK에만 적용되며 다른 Adobe JavaScript 라이브러리는 해당되지 않습니다.

## 지속적인 동의 환경 설정

명령을 사용하여 SDK에 대한 사용자 환경 설정을 통신하면 SDK는 사용자 환경 설정을 쿠키로 유지합니다. `setConsent` 다음에 사용자가 브라우저에서 웹 사이트를 로드할 때 SDK는 이러한 지속적인 기본 설정을 검색하고 사용합니다. 사용자 환경 설정에서 변경 사항을 알리는 것 외에는 `setConsent` 명령을 다시 실행할 필요가 없습니다. 이 작업은 언제든지 수행할 수 있습니다.