---
keywords: Experience Platform;홈;인기 항목;데이터 통합;인제스트된 데이터;스트리밍;개요;스트리밍 통합;지연;스트리밍 지연;;home;popular topics;ensouristed data;streaming;overview;streaming ingestion;laytency;streaming latency
solution: Experience Platform
title: 스트리밍 통합 개요
topic-legacy: overview
description: Adobe Experience Platform에 대한 스트리밍 수집은 사용자에게 클라이언트 및 서버측 디바이스에서 실시간으로 Experience Platform으로 데이터를 보내는 방법을 제공합니다.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# 스트리밍 통합 개요

Adobe Experience Platform에 대한 스트리밍 인제스트는 사용자에게 클라이언트 및 서버측 디바이스에서 실시간으로 데이터를 [!DNL Experience Platform]으로 전송하는 방법을 제공합니다.

## 스트리밍 섭취 관련 이점

Adobe Experience Platform을 사용하면 각 개별 고객에 대해 [!DNL Real-time Customer Profile]을(를) 생성하여 연관성이 높고 일관성을 유지할 수 있는 경험을 만들 수 있습니다. 스트리밍 수집은 가능한 지연 시간을 최소화하면서 [!DNL Profile] 데이터를 [!DNL Data Lake]에 제공할 수 있게 함으로써 이러한 프로파일을 구축하는 데 중요한 역할을 합니다.

다음 비디오는 스트리밍 통합 이해를 지원하고 상기의 개념을 개략적으로 설명하는 데 도움이 됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 스트림 프로필 레코드 및 [!DNL ExperienceEvents]

스트리밍 통합 기능을 통해 사용자는 프로필 기록과 [!DNL ExperienceEvents]을(를) [!DNL Platform](으)로 스트리밍하여 실시간으로 개인화할 수 있습니다. 스트리밍 통합 API로 전송된 모든 데이터는 자동으로 [!DNL Data Lake]에 보관됩니다.

자세한 내용은 [스트리밍 연결 안내서](../tutorials/create-streaming-connection.md)를 참조하십시오.

### 데이터 세트로 스트리밍

데이터가 깨끗하다고 확신하면 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에 대해 데이터 세트를 활성화할 수 있습니다.

[!DNL Profile] 및 [!DNL Identity Service]에 대한 데이터 집합 활성화에 대한 자세한 내용은 [데이터 집합 안내서](../../profile/tutorials/dataset-configuration.md)를 참조하십시오.

## [!DNL Platform]에서 스트리밍 인제스트에 대한 예상 지연은 무엇입니까?

| 대상 | 예상 지연 |
| --------- | ---------------- |
| 실시간 고객 프로필 | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60분 |

## Adobe Experience Platform 확장

Adobe Experience Platform 확장 기능을 사용하여 새 스트리밍 연결을 만들 수 있습니다. [!DNL Experience Platform] 익스텐션은 [!DNL Experience Data Model](XDM)에 서식이 지정된 비콘을 전송하여 실시간으로 [!DNL Experience Platform]에 수집할 수 있는 동작을 제공합니다. 자세한 내용은 [Experience Platform 확장](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 설명서를 참조하십시오.
