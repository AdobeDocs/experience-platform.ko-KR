---
keywords: Experience Platform;홈;인기 항목;Audience Manager 매핑;audience manager 매핑
solution: Experience Platform
title: Adobe Audience Manager 소스 커넥터에 대한 매핑 필드
description: Adobe Audience Manager 데이터(실시간, 온보딩 및 프로필 데이터)를 Audience Manager 소스 커넥터의 해당 XDM(Experience Data Model) 필드에 매핑하는 방법을 알아봅니다.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 3%

---

# Audience Manager 필드 매핑

아래 표에는 Adobe Audience Manager 데이터(실시간, 온보딩된 및 프로필 데이터)의 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.

자세한 내용은 [XDM 필드 사전](../../../../xdm/schema/field-dictionary.md) 를 참조하십시오.

## 실시간 데이터

유형: 실시간 데이터

| 실시간 데이터 필드 | XDM 필드 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *endUserIds에 있는 네임스페이스에만 해당하고 첫 번째 값만 사용합니다.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *endUserIds에 있는 네임스페이스에만 해당하고 첫 번째 값만 사용합니다.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → 유형</li><li>제조업체 → 제조업체</li><li>marketingName → 모델</li><li>modelNumber → 모델</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateState</li><li>d_city → city</li><li>d_postal → postalCode</li><li>위도_lat →</li><li>d_longitude → 경도</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os 이름 </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 프로필 데이터

유형: 프로필 XDM

| 프로필 필드 | XDM 필드 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
