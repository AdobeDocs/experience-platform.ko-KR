---
keywords: Experience Platform;홈;인기 항목;Audience Manager 매핑;대상 관리자 매핑
solution: Experience Platform
title: Adobe Audience Manager 소스 커넥터의 매핑 필드
topic-legacy: overview
description: Adobe Audience Manager 데이터(실시간, 온보드 및 프로필 데이터)를 Audience Manager 소스 커넥터의 해당 XDM(Experience Data Model) 필드에 매핑하는 방법을 알아봅니다.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Audience Manager 필드 매핑

아래 표에는 Adobe Audience Manager 데이터의 필드(실시간, 온보드 및 프로필 데이터)와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.

각 XDM 필드에 대한 자세한 내용은 [XDM 필드 사전](../../../../xdm/schema/field-dictionary.md)을 참조하십시오.

## 실시간 데이터

유형:실시간 데이터

| 실시간 데이터 필드 | XDM 필드 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -  *endUserIds에 있는 네임스페이스에만 해당되며 첫 번째 값만 있습니다.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *endUserIds에 있는 네임스페이스와 첫 번째 값만 제공됩니다.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → 형식</li><li>제조업체 →</li><li>marketingName → 모델</li><li>modelNumber → 모델</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProminity</li><li>d_city → city</li><li>d_postal→ postalCode</li><li>위도→</li><li>d_경도 → 경도</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os 이름 </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 프로필 데이터

유형:프로필 XDM

| 프로필 필드 | XDM 필드 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
