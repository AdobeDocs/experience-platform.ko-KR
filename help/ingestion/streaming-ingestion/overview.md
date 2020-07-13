---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 스트리밍 통합 개요
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# 스트리밍 통합 개요

Adobe Experience Platform에 대한 스트리밍 수집은 사용자에게 클라이언트 및 서버측 디바이스에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 제공합니다.

## 스트리밍 통합 기능

Adobe Experience Platform을 사용하면 각 개별 고객을 위한 실시간 고객 프로파일을 생성하여 연관성 있고 일관성 있는 경험을 제작할 수 있습니다. 스트리밍 통합 기능은 프로필 데이터를 Data Lake로 제공할 수 있도록 해주므로 가능한 지연 시간을 최소화하여 이러한 프로파일을 구축하는 데 중요한 역할을 합니다.

다음 비디오는 스트리밍 통합 이해를 지원하고 상기의 개념을 간략하게 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 스트림 프로필 레코드 및 ExperienceEvents

스트리밍 통합 기능을 사용하면 프로필 기록과 ExperienceEvents를 Platform으로 신속하게 스트리밍하여 실시간 개인화를 실현할 수 있습니다. 스트리밍 통합 API로 전송된 모든 데이터는 데이터 레이크에 자동으로 보관됩니다.

자세한 내용은 [스트리밍 연결 가이드](../tutorials/create-streaming-connection.md) 만들기를 참조하십시오.

### 데이터 세트로 스트리밍

데이터가 깨끗하다는 확신을 갖고 있다면 실시간 고객 프로필 및 ID 서비스에 대한 데이터 세트를 활성화할 수 있습니다.

프로필 및 ID 서비스에 대한 데이터 집합 활성화에 대한 자세한 내용은 데이터 집합 [구성 안내서를 참조하십시오](../../profile/tutorials/dataset-configuration.md).

## Platform에서 스트리밍 인제스트를 위한 예상 지연은 무엇입니까?

| 대상 | 예상 지연 |
| --------- | ---------------- |
| 실시간 고객 프로필 | &lt; 1분 |
| Data Lake | &lt; 60분 |

## Adobe Experience Platform 확장

Adobe Experience Platform 확장 기능을 사용하여 새 스트리밍 연결을 만들 수 있습니다. Experience Platform 익스텐션은 XDM(Experience Data Model) 형식의 비콘을 전송하여 Experience Platform에 실시간으로 수집하도록 하는 동작을 제공합니다. 자세한 내용은 [Experience Platform 익스텐션](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 설명서를 참조하십시오.