---
keywords: Experience Platform;홈;인기 항목;데이터 수집;수집된 데이터;스트리밍;개요;스트리밍 수집;지연;스트리밍 지연;
solution: Experience Platform
title: 스트리밍 수집 개요
description: Adobe Experience Platform용 스트리밍 수집은 클라이언트 및 서버측 장치에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 사용자에게 제공합니다.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# 스트리밍 수집 개요

Adobe Experience Platform용 스트리밍 수집은 클라이언트 및 서버측 장치에서 로 데이터를 전송하는 방법을 사용자에게 제공합니다 [!DNL Experience Platform] 실시간으로.

## 스트리밍 수집으로 무엇을 할 수 있습니까?

Adobe Experience Platform을 사용하면 를 생성하여 조정되고 일관되며 관련 있는 경험을 추진할 수 있습니다. [!DNL Real-Time Customer Profile] 개별 고객. 스트리밍 수집은 다음을 제공할 수 있도록 함으로써 이러한 프로필을 빌드하는 데 중요한 역할을 합니다 [!DNL Profile] 로 데이터 보내기 [!DNL Data Lake] 가능한 한 짧은 지연 시간.

다음 비디오에서는 스트리밍 수집에 대한 이해를 돕기 위해 제작되었으며 위의 개념에 대해 간략히 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 프로필 레코드 스트리밍 및 [!DNL ExperienceEvents]

스트리밍 수집을 통해 사용자는 프로필 레코드 및 [!DNL ExperienceEvents] 끝 [!DNL Platform] 실시간 개인화를 추진하는 데 도움이 되는 시간(초)입니다. 스트리밍 수집 API로 전송된 모든 데이터는 [!DNL Data Lake].

다음을 읽으십시오. [스트리밍 연결 안내서 만들기](../tutorials/create-streaming-connection.md) 추가 정보.

### 데이터 세트로 스트리밍

데이터가 깨끗하다고 확신하면 다음에 대한 데이터 세트를 활성화할 수 있습니다 [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service].

데이터 세트 활성화에 대한 자세한 내용 [!DNL Profile] 및 [!DNL Identity Service], 다음을 읽으십시오. [데이터 세트 안내서 구성](../../profile/tutorials/dataset-configuration.md).

## 스트리밍 수집에 대한 예상 지연 시간은 얼마입니까? [!DNL Platform]?

| 대상 | 예상 지연 시간 |
| --------- | ---------------- |
| 실시간 고객 프로필 | 1분 미만 |
| 데이터 레이크 | &lt; 60분 |

## 스트리밍 수집에 대한 RPS(초당 요청) 지침

아래 표에는 스트리밍 수집을 위한 초당 요청 제한 사항에 대한 지침이 나와 있습니다.

| RPS 제한 | 참고 |
| --- | --- |
| 초당 요청 1000개 | 사용할 때 여러 메시지가 포함될 수 있습니다 `/collection/batch` 엔드포인트. |
| 10000에 개별 메시지 표시 | 를 사용할 때 메시지를 더 적은 실제 요청으로 그룹화할 수 있습니다. `/collection/batch` 엔드포인트. |

>[!IMPORTANT]
>
>강제 적용 한도는 다음과 같이 변경됩니다. **분당 60개 요청** 디버깅 목적에 맞게 동기 유효성 검사를 사용하는 경우

## Adobe Experience Platform 확장

Adobe Experience Platform 확장을 사용하여 새 스트리밍 연결을 만들 수 있습니다. 다음 [!DNL Experience Platform] 확장은 다음 형식의 비콘을 보내는 작업을 제공합니다. [!DNL Experience Data Model] (XDM) 실시간 수집 대상 [!DNL Experience Platform]. 다음 방문: [Experience Platform 확장](../../tags/extensions/client/web-sdk/overview.md) 설명서 를 참조하십시오.
