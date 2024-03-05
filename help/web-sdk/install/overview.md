---
title: Web SDK 설치 개요
description: Experience Platform Web SDK를 설치하는 방법을 알아봅니다.
keywords: web sdk 설치;web sdk 설치;internet explorer;promise;npm 패키지
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Web SDK 설치 개요

Adobe Experience Platform Web SDK를 사용하는 세 가지 지원되는 방법은 다음과 같습니다.

1. **[Web SDK 태그 확장](extension.md)**: Adobe은 이 메서드를 사용할 것을 권장합니다. 사이트에 태그 로더를 설치한 다음 Adobe Experience Platform 데이터 수집 UI를 사용하여 구현을 구성합니다.
1. **[웹 SDK JavaScript 라이브러리](library.md)**: CDN에서 호스팅하는 라이브러리 파일을 참조하거나 자체 인프라를 사용하여 라이브러리 파일을 호스팅합니다. 사이트의 코드 내에서 라이브러리를 호출합니다.
1. **[NPM](npm.md)**: NPM 패키지 관리자 를 사용하여 사이트에 Web SDK를 설치합니다.

## 전제 조건

웹 SDK를 사용하거나 설치하기 전에 다음 요구 사항을 충족해야 합니다.

* Adobe Experience Platform의 아키텍처를 먼저 구성해야 합니다. 이러한 설정에는 필요한 스키마, ID 및 데이터스트림이 포함됩니다.
* 적절한 도구에 액세스하려면 적절한 권한이 구성되어 있어야 합니다. 예를 들어 조직에서 태그 확장을 사용하려는 경우 데이터 수집 UI에 액세스할 수 있는 올바른 권한이 있어야 합니다. 다음을 참조하십시오 [데이터 수집 권한 관리](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html) 추가 정보.
* 자사 도메인(CNAME)을 사용하는 것이 좋습니다. Adobe Analytics용 CNAME이 이미 있는 경우 해당 CNAME을 사용할 수 있습니다. Adobe 개발의 테스트는 CNAME 없이 작동하지만 프로덕션에 게시하기 전에 테스트하는 것이 좋습니다. 다음을 참조하십시오 [자사 디바이스 ID](../identity/first-party-device-ids.md) 추가 정보.
