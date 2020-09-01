---
keywords: Experience Platform;home;popular topics;data ingestion;ingested data;streaming;overview;streaming ingestion;latency;streaming latency;
solution: Experience Platform
title: Adobe Experience Platform 스트리밍 통합 개요
topic: overview
description: Adobe Experience Platform에 대한 스트리밍 수집은 사용자에게 클라이언트 및 서버측 디바이스에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 제공합니다.
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---


# 스트리밍 통합 개요

Adobe Experience Platform에 대한 스트리밍 수집은 사용자에게 클라이언트 및 서버측 디바이스에서 실시간으로 데이터를 전송하는 방법 [!DNL Experience Platform] 을 제공합니다.

## 스트리밍 통합 기능

Adobe Experience Platform을 사용하면 개별 고객에 맞는 경험을 생성하여 연관성 있고 조화로운 경험을 제공할 [!DNL Real-time Customer Profile] 수 있습니다. 스트리밍 통합 기능은 지연 시간을 최소화하면서 [!DNL Profile] 데이터를 제공할 수 있도록 함으로써 이러한 프로파일을 구축하는 데 중요한 역할을 [!DNL Data Lake] 합니다.

다음 비디오는 스트리밍 통합 이해를 지원하고 상기의 개념을 간략하게 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 프로필 레코드 및 [!DNL ExperienceEvents]

스트리밍 통합 기능을 사용하면 프로필 기록을 몇 초 [!DNL ExperienceEvents] 로 스트리밍하여 실시간 개인화 [!DNL Platform] 를 촉진할 수 있습니다. 스트리밍 통합 API로 전송된 모든 데이터는 자동으로 에 보관됩니다 [!DNL Data Lake].

자세한 내용은 [스트리밍 연결 가이드](../tutorials/create-streaming-connection.md) 만들기를 참조하십시오.

### 데이터 세트로 스트리밍

데이터가 깨끗하다는 확신이 생기면 데이터 세트를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Identity Service].

데이터 집합 활성화 [!DNL Profile] 에 대한 자세한 내용 [!DNL Identity Service]은 데이터 집합 [구성 안내서를 참조하십시오](../../profile/tutorials/dataset-configuration.md).

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| 대상 | 예상 지연 |
| --------- | ---------------- |
| 실시간 고객 프로필 | &lt; 1분 |
| Data Lake | &lt; 60분 |

## Adobe Experience Platform 확장

Adobe Experience Platform 확장 기능을 사용하여 새로운 스트리밍 연결을 만들 수 있습니다. 익스텐션은 XDM(Beacon Formatter 형식 [!DNL Experience Platform] )을 전송하여 실시간 인제스트 작업을 [!DNL Experience Data Model] [!DNL Experience Platform]제공합니다. 자세한 내용은 [Experience Platform 익스텐션](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 설명서를 참조하십시오.