---
keywords: Experience Platform;홈;인기 항목;데이터 수집;수집된 데이터;스트리밍;개요;스트리밍 수집;지연;스트리밍 지연
solution: Experience Platform
title: 스트리밍 수집 개요
topic-legacy: overview
description: Adobe Experience Platform을 위한 스트리밍 수집에서는 사용자에게 클라이언트 및 서버측 장치에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 제공합니다.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 3%

---

# 스트리밍 수집 개요

Adobe Experience Platform에 대한 스트리밍 수집은 사용자에게 클라이언트 및 서버측 장치에서 실시간으로 [!DNL Experience Platform]으로 데이터를 전송하는 방법을 제공합니다.

## 스트리밍 수집으로 무엇을 수행할 수 있습니까?

Adobe Experience Platform을 사용하면 개별 고객에 대해 [!DNL Real-time Customer Profile]을 생성하여 연관성 있고 일관된 경험을 제공할 수 있습니다. 스트리밍 수집은 [!DNL Profile] 데이터를 [!DNL Data Lake](으)로 제공할 수 있게 하여 이러한 프로필을 빌드하는 데 중요한 역할을 하며, 가능한 한 지연이 거의 없습니다.

다음 비디오는 스트리밍 수집 방법에 대한 이해를 지원하고 위의 개념을 간략하게 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 스트림 프로필 레코드 및 [!DNL ExperienceEvents]

스트리밍 수집 기능을 사용하여 사용자는 프로필 레코드를 스트리밍하고 [!DNL ExperienceEvents] 을 [!DNL Platform] (으)로 스트리밍하여 실시간 개인화를 유도할 수 있습니다. 스트리밍 수집 API로 전송된 모든 데이터는 [!DNL Data Lake]에서 자동으로 유지됩니다.

자세한 내용은 [스트리밍 연결 안내서](../tutorials/create-streaming-connection.md)를 읽어보십시오.

### 데이터 세트로 스트리밍

데이터가 깨끗하다고 확신하면 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에 대해 데이터 세트를 활성화할 수 있습니다.

[!DNL Profile] 및 [!DNL Identity Service]에 대한 데이터 집합 활성화에 대한 자세한 내용은 [데이터 집합 안내서](../../profile/tutorials/dataset-configuration.md)를 참조하십시오.

## [!DNL Platform]에서 스트리밍 수집의 예상 대기 시간은 어떻게 됩니까?

| 대상 | 예상 지연 |
| --------- | ---------------- |
| 실시간 고객 프로필 | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60분 |

## Adobe Experience Platform 확장

Adobe Experience Platform 확장을 사용하여 새 스트리밍 연결을 만들 수 있습니다. [!DNL Experience Platform] 확장은 [!DNL Experience Platform]에 실시간으로 수집하기 위해 [!DNL Experience Data Model](XDM)에 형식의 비콘을 전송하는 작업을 제공합니다. 자세한 내용은 [Experience Platform 확장](../../tags/extensions/web/sdk/overview.md) 설명서를 참조하십시오.
