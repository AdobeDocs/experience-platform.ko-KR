---
title: 지원 동의
seo-title: Adobe Experience Platform 웹 SDK 동의 지원 기본 설정
description: Experience Platform 웹 SDK를 사용하여 동의 환경 설정을 지원하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 동의 환경 설정을 지원하는 방법 살펴보기
keywords: consent;defaultConsent;default consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: f178da80d0902f76868986426600f3da426cf24d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---


# 지원 동의

사용자의 개인 정보를 존중하기 위해 SDK가 특정 목적을 위해 사용자별 데이터를 사용하도록 허용하기 전에 사용자의 동의를 요청할 수 있습니다. 현재, SDK는 사용자가 모든 목적을 선택하거나 거부할 수 있도록 허용하지만, 향후 Adobe은 특정 목적을 보다 세부적으로 제어하기를 희망하고 있습니다.

사용자가 모든 목적으로 액세스하는 경우 SDK는 다음 작업을 수행할 수 있습니다.

* Adobe 서버에서 데이터를 전송합니다.
* 쿠키 또는 웹 저장소 항목을 읽고 씁니다(사용자의 옵트인 환경 설정을 유지하는 경우는 제외).

사용자가 모든 목적을 벗어나는 경우 SDK는 이러한 작업을 수행하지 않습니다.

## 동의 구성

기본적으로 사용자는 모든 목적으로 선택되어 있습니다. 사용자가 로그인할 때까지 SDK가 위의 작업을 수행하지 않도록 하려면 다음과 같이 SDK 구성 `"defaultConsent": "pending"` 동안 전달합니다.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

일반 용도에 대한 기본 동의가 보류 중으로 설정된 경우 사용자 옵트인 환경 설정(예: 명령)에 의존하는 모든 명령을 실행하려고 하면 SDK 내에서 명령이 대기됩니다. `event` 이러한 명령은 사용자의 옵트인 환경 설정을 SDK에 전달해야만 처리됩니다.

이 경우 사용자에게 사용자 인터페이스 내 특정 위치에서 옵트인하도록 요청할 수 있습니다. 사용자의 기본 설정이 수집되면 SDK에 이러한 기본 설정을 알립니다.

## Adobe 표준을 통해 동의 기본 사항 전달

사용자가 옵션을 선택한 경우 다음과 같이 `setConsent` 옵션 `general` `in` 을 설정하여 명령을 실행합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

사용자가 이제 옵트인되었으므로 SDK는 이전에 큐에 있는 모든 명령을 실행합니다. 옵트인된 사용자에 따라 달라지는 향후 명령은 큐에 _들어가지_ 않고 즉시 실행됩니다.

사용자가 옵트아웃을 선택한 경우 다음과 같이 옵션을 설정하여 `setConsent` 명령을 `general``out` 실행합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>사용자가 옵트아웃한 후에는 SDK에서 사용자에게 동의 설정을 허용하지 않습니다 `in`.

사용자가 옵트아웃을 선택했기 때문에 이전에 큐에 있는 명령에서 반환된 약속이 거부됩니다. 사용자가 선택한 이후에 명령하면 비슷하게 거부된 약속이 반환됩니다. 오류 처리 또는 억제에 대한 자세한 내용은 명령 [실행을 참조하십시오](executing-commands.md).

>[!NOTE]
>
>현재 SDK는 `general` 목적만 지원합니다. 서로 다른 Adobe 기능 및 제품 오퍼에 해당하는 보다 강력한 목적 또는 카테고리를 구축할 계획이지만 현재 구현은 옵트인하기 위한 전체 또는 전혀 접근 방식이 아닙니다.  이는 Adobe Experience Platform에만 적용되며 다른 Adobe JavaScript 라이브러리는 [!DNL Web SDK] 해당되지 않습니다.

## IAB TCF Standard를 통한 동의 환경 설정 통신

SDK는 IAB(Interactive Advertising Bureau Europe) TCF(Transparency and Consent Framework) 표준을 통해 제공되는 사용자의 동의 환경 설정을 기록하는 것을 지원합니다. 동의문자열은 위와 같은 setConsent 명령을 통해 다음과 같이 설정할 수 있습니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

이러한 방식으로 동의가 설정되면, 실시간 고객 프로필은 동의 정보로 업데이트됩니다. 이를 수행하려면 프로필 XDM 스키마에는 프로필 개인 정보 [믹신이 포함되어야 합니다](https://github.com/adobe/xdm/blob/master/docs/reference/context/profile-privacy.schema.md). 이벤트를 전송할 때 이벤트 XDM 개체에 IAB 동의 정보를 수동으로 추가해야 합니다. SDK는 이벤트에 동의 정보를 자동으로 포함하지 않습니다. 이벤트에서 동의 정보를 보내려면 [경험 이벤트 개인 정보](https://github.com/adobe/xdm/blob/master/docs/reference/context/experienceevent-privacy.schema.md) 혼합을 경험 이벤트 스키마에 추가해야 합니다.

## 하나의 요청에 두 표준 전송

또한 SDK는 요청에서 두 개 이상의 동의 개체 전송을 지원합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 동의 기본 설정 지속성

명령을 사용하여 SDK에 대한 사용자 환경 설정을 통신하면 SDK는 사용자 환경 설정을 쿠키로 유지합니다. `setConsent` 다음에 사용자가 브라우저에서 웹 사이트를 로드할 때 SDK는 이러한 지속적인 환경 설정을 검색하고 사용하여 이벤트를 Adobe으로 보낼 수 있는지 여부를 결정합니다. 사용자 환경 설정에서 변경 사항을 알리는 것 외에는 `setConsent` 명령을 다시 실행할 필요가 없습니다. 이 작업은 언제든지 수행할 수 있습니다.

## 동의를 설정하는 동안 ID 동기화

기본 동의가 보류 중일 때, &quot;setConsent&quot;는 외부로 나가서 ID를 설정하는 첫 번째 요청일 수 있습니다. 이러한 이유로 첫 번째 요청에서 ID를 동기화하는 것이 중요할 수 있습니다. ID 맵을 &quot;sendEvent&quot; 명령과 마찬가지로 &quot;setConsent&quot; 명령에 추가할 수 있습니다. Experience Cloud [ID 검색을 참조하십시오.](./identity.md)

