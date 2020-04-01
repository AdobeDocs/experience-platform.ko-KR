---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 스트리밍 통합 개요
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8

---


# 스트리밍 통합 개요

Adobe Experience Platform용 스트리밍 통합 기능을 사용하면 클라이언트 및 서버측 디바이스에서 Experience Platform으로 데이터를 실시간으로 전송할 수 있습니다.

## 스트리밍 통합 기능

Adobe Experience Platform을 사용하면 각 개별 고객을 위한 실시간 고객 프로파일을 생성하여 연관성 있고 일관성 있는 경험을 제공할 수 있습니다. 스트리밍 통합 기능은 프로필 데이터를 Data Lake로 최대한 지연 없이 제공할 수 있도록 함으로써 이러한 프로필을 구축하는 데 중요한 역할을 합니다.

### 스트림 프로필 레코드 및 ExperienceEvents

스트리밍 통합 기능을 사용하면 프로필 기록과 ExperienceEvents를 플랫폼에 신속하게 스트리밍하여 실시간 개인화를 실현할 수 있습니다. 스트리밍 통합 API로 전송된 모든 데이터는 Data Lake에 자동으로 보관됩니다.

자세한 내용은 [스트리밍 연결 가이드](../tutorials/create-streaming-connection.md) 만들기를 참조하십시오.

### 데이터 세트로 스트리밍

데이터가 깨끗하다고 확신하면 실시간 고객 프로필 및 ID 서비스에 대한 데이터 세트를 활성화할 수 있습니다.

프로필 및 ID 서비스에 대한 데이터 집합 활성화에 대한 자세한 내용은 데이터 집합 [구성 안내서를](../../profile/tutorials/dataset-configuration.md)참조하십시오.

## Platform(플랫폼)에서 스트리밍 인제스트를 위한 예상 지연은 무엇입니까?

| 대상 | 예상 지연 |
| --------- | ---------------- |
| 실시간 고객 프로필 | &lt; 1분 |
| Data Lake | &lt; 60분 |

## Adobe Experience Platform 확장

Adobe Experience Platform 익스텐션을 사용하여 새로운 스트리밍 연결을 만들 수 있습니다. 경험 플랫폼 익스텐션은 경험 데이터 모델(XDM)에서 포맷된 비콘을 전송하여 경험 플랫폼에 실시간으로 통합합니다. 자세한 내용은 [Experience Platform](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) Extension 설명서를 참조하십시오.