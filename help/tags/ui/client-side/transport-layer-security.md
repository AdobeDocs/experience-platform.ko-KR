---
title: TLS(전송 계층 보안) 정보
description: TLS 버전 및 암호에 대한 정보
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 236c5a11f40490fc7ee536358fb146027fe64545
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 15%

---

# TLS(전송 계층 보안) 정보

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참조는 [용어 업데이트](../../term-updates.md) 문서를 참조하십시오.

TLS(전송 계층 보안)는 인터넷을 통해 응용 프로그램 간에 전송되는 데이터에 대한 종단 간 보안을 제공하는 암호화 프로토콜입니다. TLS에 대한 자세한 내용은 [TLS 기본 사항](https://www.internetsociety.org/deploy360/tls/basics/) 설명서를 참조하십시오.

Adobe Experience Platform의 태그는 웹 사이트에서 스크립트를 동적으로 로드하도록 설계된 태그 관리 시스템입니다. TLS는 스크립트가 로드될 때 Adobe 호스트 `assets.adobedtm.com`과(와) 웹 사이트 간의 통신을 보호합니다.

여러 TLS 버전을 사용할 수 있으며 여러 다른 암호를 지원합니다. 일부 버전 및 암호가 다른 버전보다 작거나 더 안전한 것으로 간주되는 것과 동일한 것은 아닙니다.

## 지원되는 TLS 버전 및 암호

Adobe 호스트 옵션은 현재 다음 TLS 버전 및 암호를 지원합니다.

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### 자체 호스팅

라이브러리를 [자체 호스팅](../publishing/hosts/self-hosting-libraries.md)하는 경우 지원되는 TLS 버전은 자체 호스팅 서비스에 의해 결정됩니다.
