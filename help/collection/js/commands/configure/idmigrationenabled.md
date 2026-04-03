---
title: idMigrationEnabled
description: 웹 SDK에서 AMCV 쿠키를 읽을 수 있도록 합니다.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled` 속성을 사용하면 웹 SDK에서 이전 Adobe Experience Cloud 구현에서 설정한 AMCV 쿠키를 읽을 수 있습니다. 조직에서 구현을 웹 SDK으로 업그레이드하는 경우 이 설정을 사용하면 현재 Adobe Experience Cloud ID 서비스로 더 원활하게 전환할 수 있습니다. 이 설정은 웹 SDK으로 업그레이드할 때 고유 방문자 수가 급격히 증가하지 않도록 매우 중요합니다.

조직에서 새로운 웹 SDK 구현을 실행하는 경우 이 설정을 활성화해도 데이터 수집이나 방문자 식별에는 영향을 주지 않습니다. 모든 구현에 대해 이 기능을 활성화한 상태로 두는 단점이 없습니다.

## ID 마이그레이션 작동 방식 {#how-it-works}

방문자 API는 ECID(Experience Cloud ID)를 `AMCV_<ORG_ID>` 쿠키에 저장합니다. `idMigrationEnabled`이(가) `true`(기본값)이면 웹 SDK은 AMCV 쿠키에서 ECID를 자동으로 읽고 첫 번째 Edge Network 요청에서 방문자의 ID로 사용합니다.

1. 방문자가 이제 방문자 API 대신 웹 SDK을 사용하는 페이지에 도달합니다.
1. 웹 SDK에서 기존 `kndctr_` ID 쿠키(자체 쿠키 형식)를 확인합니다. 검색된 쿠키가 없으면 `AMCV_` 쿠키를 찾습니다.
1. `AMCV_` 쿠키가 있는 경우 웹 SDK은 ECID를 추출하여 방문자의 ID를 초기화하는 데 사용합니다.
1. 웹 SDK은 동일한 ECID를 사용하여 새 `kndctr_` ID 쿠키를 설정합니다.
1. 이후 방문 시 웹 SDK은 `kndctr_` 쿠키를 직접 사용합니다. `AMCV_` 쿠키가 더 이상 필요하지 않습니다.

마이그레이션이 작동하려면 방문자 API가 사용한 것과 동일한 [`orgId`](/help/collection/js/commands/configure/orgid.md)(으)로 웹 SDK을 구성하고 AMCV 쿠키가 설정된 동일한 도메인(또는 동일한 상위 도메인의 하위 도메인)에 배포해야 합니다.

## 지원되는 마이그레이션 시나리오

ID 마이그레이션은 다음과 같은 전환 패턴을 지원합니다.

* **일부 페이지는 여전히 방문자 API를 사용하고 다른 페이지는 웹 SDK을 사용합니다**: SDK은 기존 AMCV 쿠키를 읽고 기존 ECID로 새 쿠키를 작성합니다. 또한 방문자 API를 계속 사용하는 페이지가 동일한 방문자를 계속 인식할 수 있도록 AMCV 쿠키를 기록합니다.
* **웹 SDK과 방문자 API가 모두 같은 페이지에 있습니다**: AMCV 쿠키가 설정되지 않은 경우 SDK은 페이지에서 방문자 API를 찾아 사용하여 ECID를 가져옵니다.
* **사이트가 웹 SDK으로 완전히 이동되었습니다.**: 기존 AMCV 기반 방문자가 쿠키를 전환하는 동안 연속성을 유지할 수 있도록 일정 기간 동안 마이그레이션을 사용하도록 설정할 수 있습니다.

>[!IMPORTANT]
>
>AMCV 쿠키가 이미 설정되어 있는지 확인한 경우가 아니면 방문자 API와 웹 SDK을 동일한 페이지에 동시에 로드하지 마십시오. 단일 페이지에서 두 라이브러리를 모두 실행하면 각 라이브러리가 ID를 독립적으로 관리하려고 시도하는 경합 조건이 발생할 수 있으며, 이로 인해 중복 또는 충돌할 수 있는 ECID가 발생할 수 있습니다.

## 마이그레이션 끄기 {#turn-off-migration}

전체 사이트가 웹 SDK에서 실행되고 해당 `AMCV_` 쿠키 없이 `kndctr_` 쿠키만 포함하는 방문자가 없으면 `idMigrationEnabled`을(를) `false`(으)로 설정하여 ID 마이그레이션을 안전하게 비활성화할 수 있습니다. 이는 사소한 성능 최적화이며 ID 로직의 표면적을 줄입니다.

지침으로, 마지막 페이지가 마이그레이션된 후 AMCV 쿠키의 최대 라이프타임이 경과될 때까지 기다리십시오. AMCV 쿠키에 2년의 만료일이 있는 경우 최종 페이지가 웹 SDK으로 잘린 후 2년을 기다리십시오. 실제로 대부분의 조직은 몇 달 후 더 빨리 마이그레이션을 비활성화하고 오랜 부재 후 처음으로 돌아오는 적은 수의 방문자로부터 무시할만한 수준의 인플레이션을 받아들입니다.

## Audience Manager 트레이트 업데이트

마이그레이션 중에 XDM 형식 데이터를 Audience Manager으로 전송하면 해당 데이터를 신호로 변환해야 합니다. XDM에서 제공하는 새 키를 반영하도록 트레이트를 업데이트해야 합니다. 이 프로세스는 [BAAAM 도구](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)를 사용하여 쉽게 수행할 수 있습니다.

## 타사 ID 마이그레이션 {#third-party-id}

방문자 API 구현에서 타사 ID(`demdex.net` 쿠키)를 사용한 경우 웹 SDK에서 이를 마이그레이션할 수도 있습니다. 웹 SDK 구성에서 [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)을(를) `true`(으)로 구성합니다. 웹 SDK은 기존 Demdex 쿠키를 읽고 AMCV 쿠키와 동일한 마이그레이션 패턴에 따라, 자사 Edge Network 요청에 서드파티 ID를 포함합니다.

## 유효성 검사 {#validation}

ID 마이그레이션이 올바르게 작동하는지 확인하려면 다음을 수행하십시오.

1. 기존 `AMCV_` 쿠키가 있는 브라우저에서 이전에 방문자 API를 사용한 페이지(현재 웹 SDK 사용)를 엽니다.
2. 개발자 도구에서 `kndctr_` ID 쿠키가 설정되어 있고 ECID가 `AMCV_` 쿠키의 ID와 일치하는지 확인하십시오.
3. 배포 후 동일한 기간 동안 마이그레이션 전후의 고유 방문자 수를 비교합니다. 고유 방문자가 크게 증가하면 마이그레이션이 ID를 전달하지 않는다는 것을 나타낼 수 있습니다.

>[!TIP]
>
>`getIdentity`을(를) 사용하여 비교를 위해 ECID를 프로그래밍 방식으로 검색합니다.
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## 구성 `idMigrationEnabled` {#configure}

`idMigrationEnabled` 명령을 실행할 때 `configure` 부울을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 기본적으로 `true`이(가) 됩니다. 방문자 API에서 설정한 AMCV 쿠키를 읽는 기능을 비활성화하려면 이 속성을 설정합니다. 대부분의 조직에서는 이 속성을 설정할 필요가 없습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## 웹 SDK 태그 확장을 사용하여 방문자 ID 마이그레이션 활성화

이러한 설정은 [ID 구성 설정](/help/tags/extensions/client/web-sdk/configure/identity.md)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
