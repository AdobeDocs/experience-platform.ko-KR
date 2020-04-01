---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Audience Manager 매핑 필드
topic: overview
translation-type: tm+mt
source-git-commit: 985c450a174712fa4b4185d5a6527962e697b5ba

---


# Audience Manager 매핑 필드

아래 표에는 Adobe Audience Manager 데이터의 필드(실시간, 온보드 및 프로필 데이터)와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.

각 XDM [필드에 대한 자세한 내용은 XDM 필드 사전을](../../../xdm/schema/field-dictionary.md) 참조하십시오.

## 실시간 데이터

유형:실시간 데이터

| 실시간 데이터 필드 | XDM 필드 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *endUserIds에 있고 첫 번째 값만 있는 네임스페이스에만 해당합니다.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *endUserIds에 있는 네임스페이스와 첫 번째 값만.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType→유형</li><li>제조업체</li><li>marketingName→모델</li><li>modelNumber→모델</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country→countryCode</li><li>d_state→stateProvince</li><li>d_city→city</li><li>d_postal_→postalCode</li><li>d_lat→latitude</li><li>d_경도</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent→userAgent</li><li>h_accept-language→acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name→os 이름 </li><li>d_os_version→os_version</li></ul> |
| `Signals` | ExperienceEvent.signatures |

## 인바운드 데이터 **(더 이상 사용되지 않음)**

유형:ExperienceEvent

| 인바운드 필드 | XDM 필드 |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] 인바운드 필드는 향후 릴리스에서 더 이상 사용되지 않게 예정되어 있습니다.

## 프로필 데이터

유형:프로필 XDM

| 프로필 필드 | XDM 필드 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
