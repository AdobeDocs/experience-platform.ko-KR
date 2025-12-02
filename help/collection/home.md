---
solution: Experience Platform
title: 데이터 수집 개요
description: Adobe Experience Platform으로 데이터를 전송하는 방법에 대해 알아봅니다.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# 데이터 수집 개요

Adobe Experience Platform은 다양한 소스에서 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network으로 전송할 수 있는 기술 제품군을 제공합니다. 그런 다음 해당 데이터를 보강하고 변환하여 Adobe 또는 Adobe이 아닌 대상으로 배포할 수 있습니다.

Adobe은 데이터 수집을 위한 전용 라이브러리로 다음 코드 언어를 지원합니다.

* **JavaScript**: 웹 사이트 및 웹 기반 응용 프로그램용
* **Kotlin**: Android 장치용
* **Swift**: iOS 장치용
* **Brightscript**: Roku 장치용
* **조동**: Android + iOS 응용 프로그램에서 조동을 사용하는 경우
* **React Native**: Android + React Native을 사용하는 iOS 애플리케이션용

Adobe Experience Platform 데이터 수집의 태그 UI에는 Web SDK 및 Mobile SDK 확장이 포함되어 있습니다.

위의 SDK 중 프로젝트의 요구 사항을 충족하는 SDK가 없는 경우 [Adobe Experience Platform Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)를 사용하여 데이터를 Adobe으로 직접 전송할 수 있습니다.

## 데이터 수집 프로세스

각 Adobe 제품에 대해 별도의 개별 라이브러리를 설치하고 구현하는 대신 위의 SDK 또는 태그 확장 중 하나를 구현하여 원하는 모든 데이터를 단일 페이로드로 집계할 수 있습니다. 해당 페이로드는 Adobe Experience Platform Edge Network의 [데이터스트림](/help/datastreams/overview.md)(으)로 전송됩니다.

![데이터 수집 다이어그램](assets/tags-sdks.png)

Adobe Experience Platform Edge Network은 엄청난 규모로 데이터를 수신하고 처리할 수 있는 빠르고 안정적인 글로벌 서버 네트워크입니다. 데이터스트림이 데이터를 수신하면 사용자가 구성한 각 솔루션에 해당 데이터를 배포합니다. 데이터는 각 개별 제품이 이해하는 형식으로 전달됩니다.

![Adobe 솔루션 다이어그램](assets/adobe-solutions.png)

[이벤트 전달](/help/tags/ui/event-forwarding/overview.md)을 사용하여 클라이언트측 구현 코드 없이 짧은 대기 시간으로 Adobe이 아닌 대상으로 데이터를 변환, 강화 및 전송할 수도 있습니다.

![이벤트 전달 다이어그램](assets/event-forwarding.png)
