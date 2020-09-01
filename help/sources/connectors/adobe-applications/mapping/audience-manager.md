---
keywords: Experience Platform;home;popular topics;Audience Manager mapping;audience manager mapping
solution: Experience Platform
title: Audience Manager 매핑 필드
topic: overview
description: 아래 표에는 Adobe Audience Manager 데이터(실시간, 온보드 및 프로필 데이터)의 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Audience Manager 매핑 필드

아래 표에는 Adobe Audience Manager 데이터(실시간, 온보드 및 프로필 데이터)의 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.

각 XDM 필드에 대한 자세한 내용은 [XDM 필드 사전을](../../../../xdm/schema/field-dictionary.md) 참조하십시오.

## 실시간 데이터

유형:실시간 데이터

| 실시간 데이터 필드 | XDM 필드 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *endUserIds에 있는 네임스페이스에만 해당되며 첫 번째 값만 제공됩니다.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - endUserIds *에 있는 네임스페이스와 첫 번째 값만 사용할 수 있습니다.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType→유형</li><li>제조업체</li><li>marketingName→모델</li><li>modelNumber→모델</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country:countryCode</li><li>d_state→stateProvince</li><li>d_city→구/시</li><li>d_postal-postalCode</li><li>위도(_lat)도</li><li>d_위도</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent→userAgent</li><li>h_accept-language→acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name;os 이름 </li><li>d_os_version→os_version</li></ul> |

## 프로필 데이터

유형:프로필 XDM

| 프로필 필드 | XDM 필드 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
