---
title: MTLS API 안내서
description: mTLS 서비스 API를 사용하여 Adobe에서 발급한 공개 인증서를 안전하게 검색하고 확인하는 방법을 알아봅니다.
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# MTLS 서비스 API 개요

MTLS 서비스 API를 사용하여 조직의 애플리케이션에 대해 Adobe이 발급한 공개 인증서를 안전하게 검색할 수 있습니다. 이 API는 고객과 Adobe Experience Platform 간의 데이터 교환을 인증 및 암호화하여 추가 보안 계층을 제공합니다. 인증서의 신뢰성을 외부에서 검증함으로써 신뢰를 높이고 민감한 정보를 안전하게 보호할 수 있습니다.

## 공개 인증서

공개 인증서는 보안 통신에서 서버 또는 클라이언트의 ID를 인증하는 데 사용되는 디지털 문서입니다. mTLS 서비스 API와 관련하여 이러한 인증서는 Adobe Experience Platform과의 데이터 교환이 인증되고 암호화되도록 합니다. API를 통해 이러한 인증서를 검색하고 확인하는 것은 인증서의 진위를 확인하여 데이터 트랜잭션의 보안과 신뢰성을 향상시키고 민감한 정보를 보호합니다. 공개 인증서를 검색하는 방법을 알아보려면 [끝점 안내서](./public-certificate-endpoint.md)를 참조하여 호출 방법을 알아보십시오.

## 다음 단계

MTLS 서비스 API를 사용하여 호출을 시작하려면 [시작 안내서](./getting-started.md)에서 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 읽어 보십시오.
