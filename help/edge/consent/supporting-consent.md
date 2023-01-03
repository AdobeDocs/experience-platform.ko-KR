---
title: Adobe Experience Platform Web SDK를 사용하여 고객 동의 기본 설정 지원
description: Adobe Experience Platform Web SDK를 사용하여 동의 환경 설정을 지원하는 방법을 알아봅니다.
keywords: 동의;defaultConsent;기본 동의;setConsent;프로필 개인 정보 필드 그룹;경험 이벤트 개인 정보 필드 그룹;개인 정보 필드 그룹;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# 고객 동의 기본 설정 지원

SDK가 특정 용도로 사용자별 데이터를 사용할 수 있도록 허용하기 전에 사용자의 동의를 요청할 수 있습니다. 현재 SDK는 사용자가 모든 목적을 옵트인하거나 옵트아웃할 수만 있지만 향후에 Adobe은 특정 목적을 보다 세밀하게 제어할 수 있기를 바랍니다.

사용자가 모든 용도로 옵트인하면 SDK에서 다음 작업을 수행할 수 있습니다.

* Adobe의 서버로 및 서버에서 데이터를 보냅니다.
* 쿠키 또는 웹 저장소 항목을 읽고 씁니다.

사용자가 모든 목적을 벗어나는 경우 SDK는 이러한 작업을 수행하지 않습니다.

## 동의 구성

기본적으로 사용자는 모든 목적으로 옵트인됩니다. 사용자가 옵트인할 때까지 SDK가 위의 작업을 수행하지 않도록 하려면 를 전달합니다 `"defaultConsent": "pending"` 를 구성하는 동안:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

일반 목적에 대한 기본 동의가 보류 중으로 설정된 경우 사용자 옵트인 환경 설정에 종속된 명령(예: `sendEvent` 명령)를 사용하면 SDK 내에서 명령이 대기됩니다. 이러한 명령은 사용자의 옵트인 환경 설정을 SDK에 전달할 때까지 처리되지 않습니다.

>[!NOTE]
>
>명령은 메모리에서만 큐에 있습니다. 이 워크플로우는 페이지 로드 간에 저장되지 않습니다.

사용자의 옵트인 환경 설정이 설정되기 전에 발생한 이벤트를 수집하지 않으려면 를 전달할 수 있습니다 `"defaultConsent": "out"` SDK 구성 중. 사용자 옵트인 환경 설정에 종속되는 모든 명령을 실행하려고 하면 사용자의 옵트인 환경 설정을 SDK에 전달할 때까지 효과가 없습니다.

>[!NOTE]
>
>현재 SDK는 단일 목적 또는 모든 용도로 만 지원합니다. 다양한 Adobe 기능 및 제품 오퍼링에 해당하는 보다 강력한 목적 또는 카테고리 세트를 구축할 계획이지만 현재 구현은 옵트인에 대한 접근 방식입니다.  이는 Adobe Experience Platform에만 적용됩니다 [!DNL Web SDK] 및 다른 Adobe JavaScript 라이브러리는 아님.

이때 사용자에게 사용자 인터페이스 내에서 옵트인하도록 요청할 수 있습니다. 사용자의 환경 설정이 수집되면 이러한 환경 설정을 SDK에 전달합니다.

## Adobe Experience Platform 표준을 통해 동의 기본 설정 전달

SDK는 Adobe Experience Platform 동의 표준 버전 1.0 및 2.0을 지원합니다. 현재, 1.0 및 2.0 표준은 동의 기본 설정의 자동 적용만 지원합니다. 1.0 표준은 2.0 표준이 찬성하여 단계적으로 폐지되고 있다. 2.0 표준을 사용하면 수동으로 동의 기본 설정을 적용하는 데 사용할 수 있는 추가 동의 환경 설정을 추가할 수 있습니다.

### Adobe 표준 버전 2.0 사용

Adobe Experience Platform을 사용하는 경우 프로필 스키마에 개인 정보 스키마 필드 그룹을 포함해야 합니다. 자세한 내용은 [Adobe Experience Platform의 거버넌스, 개인 정보 및 보안](../../landing/governance-privacy-security/overview.md) Adobe 표준 버전 2.0에 대한 자세한 정보. 아래의 값 개체 내에 데이터를 추가할 수 있습니다 `consents` 필드 [!UICONTROL 동의 및 기본 설정] 프로필 필드 그룹 을 참조하십시오.

사용자가 옵트인하는 경우 `setConsent` collect preference가 `y` 아래와 같이 변경하는 것을 의미합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

시간 필드는 사용자가 마지막으로 동의 환경 설정을 업데이트한 시기를 지정해야 합니다. 사용자가 옵트아웃하도록 선택하는 경우 `setConsent` collect preference가 `n` 아래와 같이 변경하는 것을 의미합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Adobe 표준 버전 1.0 사용

사용자가 옵트인하는 경우 `setConsent` 명령을 사용하여 `general` 옵션 설정 `in` 아래와 같이 변경하는 것을 의미합니다.

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

사용자가 옵트아웃하도록 선택하는 경우 `setConsent` 명령을 사용하여 `general` 옵션 설정 `out` 아래와 같이 변경하는 것을 의미합니다.

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

## IAB TCF 표준을 통해 동의 환경 설정을 통신합니다

SDK는 IAB(Interactive Advertising Bureau Europe) TCF(Transparency and Consent Framework) 표준을 통해 제공된 사용자의 동의 환경 설정 기록을 지원합니다. 동의 문자열은 동일하게 설정할 수 있습니다 `setConsent` 아래와 같이 명령을 수행합니다.

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

이러한 방식으로 동의가 설정되면 실시간 고객 프로필이 동의 정보로 업데이트됩니다. 이를 수행하려면 프로필 XDM 스키마에 [프로필 개인 정보 스키마 필드 그룹](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). 이벤트를 보낼 때 IAB 동의 정보를 이벤트 XDM 개체에 수동으로 추가해야 합니다. SDK는 이벤트에 동의 정보를 자동으로 포함하지 않습니다. 이벤트에서 동의 정보를 보내려면 [경험 이벤트 개인 정보 필드 그룹](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) 경험 이벤트 스키마에 를 추가해야 합니다.

## 하나의 요청에서 여러 표준 전송

또한 SDK는 요청에서 두 개 이상의 동의 개체 전송을 지원합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 동의 기본 설정의 지속성

를 사용하여 사용자 환경 설정을 SDK에 전달한 후 `setConsent` 명령을 사용하면, SDK는 사용자의 환경 설정을 쿠키에 유지합니다. 다음에 사용자가 브라우저에서 웹 사이트를 로드할 때 SDK는 이러한 지속적인 환경 설정을 검색하고 사용하여 이벤트를 Adobe으로 보낼 수 있는지 여부를 결정합니다.

현재 환경 설정으로 동의 대화 상자를 표시할 수 있으려면 사용자 환경 설정을 독립적으로 저장해야 합니다. SDK에서 사용자 환경 설정을 검색할 방법이 없습니다. 사용자 환경 설정이 SDK와 계속 동기화되도록 하기 위해 `setConsent` 페이지를 로드할 때마다 명령을 실행합니다. SDK는 환경 설정이 변경된 경우에만 서버 호출을 수행합니다.

## 동의를 설정하는 동안 ID 동기화

기본 동의가 보류 중이거나 종료되면 `setConsent` 은 외부로 나가서 id를 설정하는 첫 번째 요청일 수 있습니다. 이러한 이유로 첫 번째 요청에서 ID를 동기화하는 것이 중요할 수 있습니다. ID 맵을 `setConsent` 명령하는 것 처럼 `sendEvent` 명령. 자세한 내용은 [Experience Cloud ID 검색](../identity/overview.md)
