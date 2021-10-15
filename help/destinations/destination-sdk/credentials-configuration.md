---
description: Adobe Experience Platform 대상 SDK에서 지원되는 인증 구성을 사용하여 사용자를 인증하고 데이터를 대상 종단점으로 활성화합니다.
title: 인증 구성
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 인증 구성 {#credentials}

## 지원되는 인증 유형 {#supported-authentication-types}

Adobe Experience Platform 대상 SDK는 다음과 같은 몇 가지 인증 유형을 지원합니다.

* 베어러 인증
* 인증 코드가 있는 OAuth 2
* 암호 부여가 있는 AUth 2
* 클라이언트 자격 증명 부여가 있는 OAuth 2

지원되는 다양한 OAuth 2 흐름 및 사용자 지정 OAuth 2 지원의 경우 [OAuth 2 인증](./oauth2-authentication.md)에서 대상 SDK 설명서를 참조하십시오.

`/destinations` 종단점의 `customerAuthenticationConfigurations` 매개 변수를 통해 대상에 대한 인증 정보를 구성할 수 있습니다. 대상 구성 문서에서 [고객 인증 구성 섹션](./destination-configuration.md#customer-authentication-configurations)을 참조하십시오.

## `/credentials` API 엔드포인트를 사용해야 하는 경우 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 *은 `/credentials` API 엔드포인트를 사용할 필요가 없습니다.* 대신 `/destinations` 종단점의 `customerAuthenticationConfigurations` 매개 변수를 통해 대상에 대한 인증 정보를 구성할 수 있습니다.

Adobe과 대상 간에 글로벌 인증 시스템이 있고 [!DNL Platform] 고객이 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없는 경우 `activation/authoring/credentials` API 엔드포인트를 사용하고 [대상 구성](./destination-configuration.md#destination-delivery)에서 `PLATFORM_AUTHENTICATION`을(를) 선택합니다. 이 경우 `/credentials` API 엔드포인트를 사용하여 자격 증명 개체를 만들어야 합니다. `/credentials` 종단점에서 수행할 수 있는 전체 작업 목록은 [자격 증명 API 종단점 작업](./credentials-configuration-api.md)을 참조하십시오.
