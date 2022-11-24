---
keywords: Experience Platform;홈;인기 항목;데이터 수집;수집된 데이터;스트리밍;개요;스트리밍 수집;지연;스트리밍 지연
solution: Experience Platform
title: 스트리밍 수집 개요
topic-legacy: overview
description: Adobe Experience Platform을 위한 스트리밍 수집에서는 사용자에게 클라이언트 및 서버측 장치에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 제공합니다.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---

# 스트리밍 수집 개요

Adobe Experience Platform을 위한 스트리밍 수집에서는 사용자에게 클라이언트 및 서버측 장치에서 다음으로 데이터를 보내는 방법을 제공합니다 [!DNL Experience Platform] 실시간으로

## 스트리밍 수집으로 무엇을 수행할 수 있습니까?

Adobe Experience Platform을 사용하면 통합 및 일관되고 적절한 경험을 생성하는 데 사용할 수 있습니다 [!DNL Real-time Customer Profile] 각 개별 고객에 대해 고려할 수 있습니다. 스트리밍 수집은 게재를 통해 이러한 프로필을 빌드하는 데 중요한 역할을 합니다 [!DNL Profile] 데이터를에 [!DNL Data Lake] 가능한 한 짧은 지연 시간.

다음 비디오는 스트리밍 수집 방법에 대한 이해를 지원하고 위의 개념을 간략하게 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 프로필 레코드 및 스트림 [!DNL ExperienceEvents]

스트리밍 수집으로 프로필 레코드를 스트리밍하고 [!DNL ExperienceEvents] to [!DNL Platform] 실시간 개인화를 구현하는 데 도움이 되는 시간(초)입니다. 스트리밍 수집 API로 전송된 모든 데이터는 [!DNL Data Lake].

자세한 내용은 [스트리밍 연결 안내서 만들기](../tutorials/create-streaming-connection.md) 추가 정보.

### 데이터 세트로 스트리밍

데이터가 깨끗하다고 확신하면 데이터 세트에 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service].

데이터 집합 활성화에 대한 자세한 정보 [!DNL Profile] 및 [!DNL Identity Service]을(를) 참조하십시오. [데이터 세트 구성 안내서](../../profile/tutorials/dataset-configuration.md).

## 스트리밍 수집 지연 시간은 얼마입니까 [!DNL Platform]?

| 대상 | 예상 지연 |
| --------- | ---------------- |
| 실시간 고객 프로필 | &lt; 1분 |
| Data Lake | &lt; 60분 |

## 스트리밍 통합에 대한 RPS(초당 요청) 지침

아래 표에는 스트리밍 수집에 대한 초당 요청 제한에 대한 지침이 표시됩니다.

| RPS 제한 | 참고 |
| --- | --- |
| 초당 1000개 요청 | 사용할 때 여러 메시지가 포함될 수 있습니다 `/collection/batch` 엔드포인트. |
| 초당 개별 메시지 10000 | 메시지는 `/collection/batch` 엔드포인트. |

>[!IMPORTANT]
>
>강제 제한 **분당 60개의 요청** 는 디버깅 목적으로 동기 유효성 검사를 사용할 때 사용됩니다.

## Adobe Experience Platform 확장

Adobe Experience Platform 확장을 사용하여 새 스트리밍 연결을 만들 수 있습니다. 다음 [!DNL Experience Platform] 확장은 [!DNL Experience Data Model] (XDM) 을 참조하십시오 [!DNL Experience Platform]. 다음 방문 [Experience Platform 확장](../../tags/extensions/client/sdk/overview.md) 설명서 를 참조하십시오.
