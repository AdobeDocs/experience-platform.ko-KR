---
description: Adobe Experience Platform 대상 SDK에서 지원되는 인증 구성을 사용하여 사용자를 인증하고 데이터를 대상 종단점으로 활성화합니다.
title: 인증 구성
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 인증 구성 {#credentials}

## 지원되는 인증 유형 {#supported-authentication-types}

Adobe Experience Platform 대상 SDK는 다음과 같은 몇 가지 인증 유형을 지원합니다.

* 베어러 인증
* 인증 코드가 있는 OAuth 2
* 암호 부여가 있는 AUth 2
* 클라이언트 자격 증명 부여가 있는 OAuth 2

를 통해 대상에 대한 인증 정보를 구성할 수 있습니다 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 엔드포인트. 자세한 내용은 [고객 인증 구성 섹션](./destination-configuration.md#customer-authentication-configurations) 대상 구성 문서 및 아래 섹션에서 각 인증 유형에 대한 구성에 대한 세부 사항을 설명합니다.

## 베어러 인증 {#bearer}

대상에 대한 bearer 유형 인증을 설정하려면 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## OAuth 2 인증 {#oauth2}

지원되는 다양한 OAuth 2 흐름과 사용자 지정 OAuth 2 지원을 설정하는 방법에 대해서는 대상 SDK 설명서 를 참조하십시오. [OAuth 2 인증](./oauth2-authentication.md).


## 를 사용해야 하는 경우 `/credentials` API 엔드포인트 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 *포함하지 않음* 를 사용해야 함 `/credentials` API 엔드포인트. 대신 를 통해 대상에 대한 인증 정보를 구성할 수 있습니다 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 엔드포인트.

다음 `/credentials` API 엔드포인트는 Adobe과 대상 간 글로벌 인증 시스템이 있는 경우 대상 개발자에게 제공됩니다 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다.

이 경우 `/credentials` API 엔드포인트. 또한 선택해야 합니다 `PLATFORM_AUTHENTICATION` 에서 [대상 구성](./destination-configuration.md#destination-delivery). 읽기 [자격 증명 API 끝점 작업](./credentials-configuration-api.md) 에서 수행할 수 있는 전체 작업 목록 `/credentials` 엔드포인트.
