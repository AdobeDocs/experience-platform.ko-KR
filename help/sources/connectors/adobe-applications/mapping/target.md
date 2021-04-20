---
keywords: Experience Platform;홈;인기 항목;대상 매핑;대상 매핑;Target mapping;Marketing Cloud;Marketing Cloud;Adobe Analytics Server ManagerAnalytics를
solution: Experience Platform
title: Adobe Target 이벤트 데이터를 XDM에 매핑
topic-legacy: overview
description: Adobe Experience Platform에서 사용할 수 있도록 Adobe Target 이벤트 필드를 XDM(Experience Data Model) 스키마에 매핑하는 방법을 알아봅니다.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# 대상 매핑 필드 매핑

Adobe Experience Platform을 사용하면 Target 소스 커넥터를 통해 Adobe Target 데이터를 인제스트할 수 있습니다. 커넥터를 사용할 때 Target 필드의 모든 데이터는 XDM ExperienceEvent 클래스와 연결된 [XDM(Experience Data Model)](../../../../xdm/home.md) 필드에 매핑되어야 합니다.

다음 표에서는 경험 이벤트 스키마(*XDM ExperienceEvent 필드*)의 필드와 해당 Target 필드를 (*Target 요청 필드*)에 매핑해야 하는 필드에 대해 간략히 설명합니다. 일부 매핑에 대한 추가 메모도 제공됩니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| XDM ExperienceEvent 필드 | Target 요청 필드 | 참고 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 고유한 요청 식별자 |
| **`dataSource`** |  | 모든 클라이언트에 대해 &quot;1&quot;로 구성되었습니다. |
| `dataSource._id` | 요청과 함께 전달할 수 없는 시스템 생성 값. | 이 데이터 소스의 고유 ID. 이 값은 데이터 소스를 만든 개인 또는 시스템에서 제공합니다. |
| `dataSource.code` | 요청과 함께 전달할 수 없는 시스템 생성 값. | 전체@id으로 바로 가기 코드 또는 @id 중 하나 이상을 사용할 수 있습니다. 경우에 따라 이 코드를 데이터 소스 통합 코드라고 합니다. |
| `dataSource.tags` | 요청과 함께 전달할 수 없는 시스템 생성 값. | 태그는 주어진 데이터 소스에 표현되는 별칭이 이러한 별칭을 사용하는 응용 프로그램에서 해석되는 방식을 나타내기 위해 사용됩니다.<br><br>예<br><ul><li>`isAVID`:Analytics 방문자 ID를 나타내는 데이터 소스입니다.</li><li>`isCRSKey`:CRS에서 키로 사용해야 하는 별칭을 나타내는 데이터 소스입니다.</li></ul>태그는 데이터 소스가 생성될 때 설정되지만 지정된 데이터 소스를 참조할 때 파이프라인 메시지에도 포함됩니다. |
| **`timestamp`** | 이벤트 타임스탬프 |
| **`channel`** | `context.channel` | 보기 배달에만 작동합니다. 옵션은 &quot;웹&quot; 및 &quot;모바일&quot;이며 &quot;웹&quot;은 기본값입니다. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 요청의 IP 주소를 기반으로 모바일 통신사 이름이 확인되었습니다. |
| `environment.ipV4` | `mboxRequest.ipAddress` (V4 형식의 경우) |
| `environment.ipV6` | `mboxRequest.ipAddress` (V6 형식의 경우) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 고객이 정의한 환경(예: dev, qa 또는 prod)에 대한 Target의 내부 매핑. |
| `experience.target.supplementalDataID` | Analytics 이벤트로 Target 이벤트를 연결하는 데 사용되는 식별자 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 방문자가 자격이 있는 활동 목록(배열) |
| `experience.target.activities[i].activityID` | 방문자가 자격이 있는 주어진 활동의 ID |
| `experience.target.activities[i].version` | 방문자가 자격이 있는 특정 활동의 버전 |
| `experience.target.activities[i].activityEvents` | 사용자가 이 이벤트를 히트한 활동 이벤트에 대한 세부 사항을 포함합니다. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | `deviceAtlas`(또는 NULL)의 다음 속성 중 하나: <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (빈 문자열) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (빈 문자열) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 임의 UUID(필수) |
| `placeContext.geo.city` | 요청의 IP 주소를 기반으로 도시 이름이 확인되었습니다. |
| `placeContext.geo.countryCode` | 요청의 IP 주소를 기반으로 국가 코드가 해결되었습니다. |
| `placeContext.geo.dmaId` | 요청의 IP 주소를 기반으로 해결된 지정된 시장 지역 코드. |
| `placeContext.geo.postalCode` | 요청의 IP 주소를 기반으로 우편 번호가 확인되었습니다. |
| `placeContext.geo.stateProvince` | 시/도는 요청의 IP 주소를 기반으로 해결되었습니다. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 주문 세부 사항이 요청에 있는 경우에만 설정합니다. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style=&quot;table-layout:auto&quot;}
