---
title: 웹 SDK 설치 개요
description: Experience Platform 웹 SDK을 설치하는 방법을 알아봅니다.
keywords: web sdk 설치;web sdk 설치;internet explorer;promise;npm 패키지
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 웹 SDK 설치 개요

Adobe Experience Platform Web SDK을 사용하는 방법에는 세 가지가 있습니다.

1. **[웹 SDK 태그 확장](/help/tags/extensions/client/web-sdk/overview.md)**: Adobe에서는 이 메서드를 사용하는 것이 좋습니다. 사이트에 태그 로더를 설치한 다음 Adobe Experience Platform 데이터 수집 UI를 사용하여 구현을 구성합니다.
1. **[Web SDK JavaScript 라이브러리](library.md)**: CDN에서 호스팅하는 라이브러리 파일을 참조하거나 자체 인프라를 사용하여 라이브러리 파일을 호스팅합니다. 사이트의 코드 내에서 라이브러리를 호출합니다.
1. **[NPM](npm.md)**: NPM 패키지 관리자를 사용하여 웹 SDK을 사이트에 설치합니다.

## 전제 조건

웹 SDK을 사용하거나 설치하기 전에 다음 요구 사항을 충족해야 합니다.

* Adobe Experience Platform의 아키텍처를 먼저 구성해야 합니다. 이러한 설정에는 필요한 스키마, ID 및 데이터스트림이 포함됩니다.
* 적절한 도구에 액세스하려면 적절한 권한이 구성되어 있어야 합니다. 예를 들어 조직에서 태그 확장을 사용하려는 경우 데이터 수집 UI에 액세스할 수 있는 올바른 권한이 있어야 합니다. 자세한 내용은 [데이터 수집 권한](../../permissions.md)을 참조하세요.
* 자사 도메인(CNAME)을 사용하는 것이 좋습니다. Adobe Analytics용 CNAME이 이미 있는 경우 해당 CNAME을 사용할 수 있습니다. 개발의 테스트는 CNAME 없이 작동하지만 Adobe은 프로덕션에 게시하기 전에 테스트를 하는 것을 권장합니다. 자세한 내용은 [자사 장치 ID](../../use-cases/identity/first-party-device-ids.md)를 참조하십시오.
