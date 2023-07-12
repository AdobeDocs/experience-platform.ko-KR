---
solution: Experience Platform
title: XDM에 Adobe Target 이벤트 데이터 매핑
description: Adobe Target 이벤트 필드를 Adobe Experience Platform에서 사용할 XDM(Experience Data Model) 스키마에 매핑하는 방법에 대해 알아봅니다.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 대상 매핑 필드 매핑

다음 표에서는 XDM(경험 데이터 모델) 경험 이벤트 스키마의 필드와 매핑되어야 하는 Adobe Target의 해당 필드에 대해 간략하게 설명합니다. 일부 매핑에 대한 추가 참고도 제공됩니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| XDM ExperienceEvent 필드 | Target 요청 필드 | 참고 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 고유 요청 식별자 |
| **`dataSource`** | | 모든 클라이언트에 대해 &quot;1&quot;로 구성됩니다. |
| `dataSource._id` | 요청과 함께 전달할 수 없는 시스템 생성 값입니다. | 해당 데이터 소스의 고유 ID. 데이터 소스를 만든 개인 또는 시스템에서 제공됩니다. |
| `dataSource.code` | 요청과 함께 전달할 수 없는 시스템 생성 값입니다. | 전체 @id 바로 가기. 하나 이상의 코드 또는 @id을 사용할 수 있습니다. 경우에 따라 이 코드를 데이터 소스 통합 코드라고 합니다. |
| `dataSource.tags` | 요청과 함께 전달할 수 없는 시스템 생성 값입니다. | 태그는 특정 데이터 소스로 표시되는 별칭이 해당 별칭을 사용하는 애플리케이션에 의해 어떻게 해석되어야 하는지 나타내는 데 사용됩니다.<br><br>예:<br><ul><li>`isAVID`: Analytics 방문자 ID를 나타내는 데이터 소스.</li><li>`isCRSKey`: CRS의 키로 사용해야 하는 별칭을 나타내는 데이터 소스입니다.</li></ul>태그는 데이터 소스가 생성될 때 설정되지만, 지정된 데이터 소스를 참조할 때 파이프라인 메시지에도 포함됩니다. |
| **`timestamp`** | 이벤트 타임스탬프 |
| **`channel`** | `context.channel` | 보기 게재에서만 작동합니다. 옵션은 &quot;web&quot; 및 &quot;mobile&quot;이며, 기본값은 &quot;web&quot;입니다. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | ECID(Experience Cloud ID)는 MCID라고도 하며 네임스페이스에서 계속 사용됩니다. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 요청의 IP 주소를 기반으로 확인된 이동통신사 이름입니다. |
| `environment.ipV4` | `mboxRequest.ipAddress` (V4 형식인 경우) |
| `environment.ipV6` | `mboxRequest.ipAddress` (V6 형식인 경우) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 고객 정의 환경(예: 개발, qa 또는 프로덕션)에 대한 Target의 내부 매핑. |
| `experience.target.supplementalDataID` | Target 이벤트를 Analytics 이벤트와 연결하는 데 사용되는 식별자 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 방문자가 자격을 부여받은 활동 목록(배열) |
| `experience.target.activities[i].activityID` | 방문자가 자격을 부여받은 활동의 ID |
| `experience.target.activities[i].version` | 방문자가 자격을 부여받은 활동의 버전 |
| `experience.target.activities[i].activityEvents` | 사용자가 이 이벤트와 함께 히트한 활동 이벤트의 세부 정보를 포함합니다. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 의 다음 속성 중 하나 `deviceAtlas` (또는 NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (빈 문자열) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (빈 문자열) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 무작위 UUID(필수) |
| `placeContext.geo.city` | 요청의 IP 주소를 기반으로 확인된 도시 이름입니다. |
| `placeContext.geo.countryCode` | 요청의 IP 주소를 기반으로 해결된 국가 코드입니다. |
| `placeContext.geo.dmaId` | 요청의 IP 주소를 기반으로 해결된 지정 시장 지역 코드. |
| `placeContext.geo.postalCode` | 요청의 IP 주소를 기반으로 해결된 우편 번호입니다. |
| `placeContext.geo.stateProvince` | 요청의 IP 주소를 기반으로 해결된 시/도입니다. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | 요청에 주문 세부 사항이 있는 경우에만 설정합니다. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
