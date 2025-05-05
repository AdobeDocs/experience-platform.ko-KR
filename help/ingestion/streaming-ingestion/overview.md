---
keywords: Experience Platform;홈;인기 항목;데이터 수집;수집된 데이터;스트리밍;개요;스트리밍 수집;지연;스트리밍 지연;
solution: Experience Platform
title: 스트리밍 수집 개요
description: Adobe Experience Platform용 스트리밍 수집은 클라이언트 및 서버측 장치에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 사용자에게 제공합니다.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# 스트리밍 수집 개요

Adobe Experience Platform용 스트리밍 수집은 클라이언트 및 서버측 장치에서 실시간으로 [!DNL Experience Platform]&#x200B;(으)로 데이터를 전송하는 방법을 제공합니다.

## 스트리밍 수집으로 무엇을 할 수 있습니까?

Adobe Experience Platform을 사용하면 각 개별 고객에 대해 [!DNL Real-Time Customer Profile]을(를) 생성하여 조정되고 일관되며 관련 있는 경험을 추진할 수 있습니다. 스트리밍 수집은 [!DNL Profile] 데이터를 가능한 한 적은 지연 시간으로 [!DNL Data Lake]에 전달할 수 있도록 함으로써 이러한 프로필을 빌드하는 데 중요한 역할을 합니다.

다음 비디오에서는 스트리밍 수집에 대한 이해를 돕기 위해 제작되었으며 위의 개념에 대해 간략히 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/31706?quality=12&learn=on&captions=kor)

### 프로필 레코드 및 [!DNL ExperienceEvents] 스트리밍

스트리밍 수집을 통해 사용자는 프로필 레코드와 [!DNL ExperienceEvents]을(를) [!DNL Experience Platform]에 초 단위로 스트리밍하여 실시간 개인화를 촉진할 수 있습니다. 스트리밍 수집 API로 전송된 모든 데이터는 자동으로 [!DNL Data Lake]에 유지됩니다.

자세한 내용은 [스트리밍 연결 가이드 만들기](../tutorials/create-streaming-connection.md)를 참조하십시오.

### 데이터 세트로 스트리밍

데이터가 깨끗하다고 확신하면 [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service]에 데이터 세트를 사용하도록 설정할 수 있습니다.

[!DNL Profile] 및 [!DNL Identity Service]에 대한 데이터 집합을 사용하는 방법에 대한 자세한 내용은 [데이터 집합 구성 가이드](../../profile/tutorials/dataset-configuration.md)를 참조하십시오.

## Experience Platform에서 스트리밍 수집의 예상 대기 시간은 어떻게 됩니까?

>[!IMPORTANT]
>
>스트리밍 수집을 위한 가드레일은 샌드박스 수준이 아닌 조직 수준에서 계산됩니다. 즉, 샌드박스당 데이터 사용량이 전체 조직에 해당하는 총 라이선스 사용 권한에 바인딩됩니다. 또한 개발 샌드박스의 데이터 사용은 총 프로필의 10%로 제한됩니다. 라이선스 사용 권한에 대한 자세한 내용은 [데이터 관리 모범 사례 가이드](../../landing/license-usage-and-guardrails/data-management-best-practices.md)를 참조하세요.

| 대상 | 예상 지연 시간 |
| --------- | ---------------- |
| 실시간 고객 프로필 | 95번째 백분위수에서 15분 미만 |
| 데이터 레이크 | 60분 미만 |

## 스트리밍 수집에 대한 RPS(초당 요청) 지침

아래 표에는 스트리밍 수집을 위한 초당 요청 제한 사항에 대한 지침이 나와 있습니다.

| RPS 제한 | 참고 |
| --- | --- |
| 초당 요청 1000개 | `/collection/batch` 끝점을 사용할 때 여러 메시지가 포함될 수 있습니다. |
| 10000에 개별 메시지 표시 | `/collection/` 끝점을 사용할 때 메시지를 더 적은 실제 요청으로 그룹화할 수 있습니다. |

>[!IMPORTANT]
>
>디버깅 목적대로 동기 유효성 검사를 사용할 때 적용된 제한은 **분당 요청 수**&#x200B;입니다.

## Adobe Experience Platform 확장

Adobe Experience Platform 확장을 사용하여 새 스트리밍 연결을 만들 수 있습니다. [!DNL Experience Platform] 확장은 실시간 수집을 위해 [!DNL Experience Data Model]&#x200B;(XDM) 형식의 비콘을 [!DNL Experience Platform]&#x200B;(으)로 보내는 작업을 제공합니다. 자세한 내용은 [Experience Platform 확장](../../tags/extensions/client/web-sdk/overview.md) 설명서를 참조하십시오.
