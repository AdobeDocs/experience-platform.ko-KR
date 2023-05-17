---
description: Destination SDK으로 빌드된 대상에 대해 설명서 링크, 대상 카드 카테고리, 대상 연결 유형 및 빈도와 같은 UI 속성을 구성하는 방법을 알아봅니다.
title: UI 속성
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# UI 속성

UI 속성은 대상 플랫폼 로고, 설명서 페이지에 대한 링크, 대상 설명 및 해당 카테고리 및 유형과 같은 Adobe이 Adobe Experience Platform 사용자 인터페이스에 대상 카드에 대해 표시해야 하는 시각적 요소를 정의합니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서나 다음 대상 구성 개요 페이지를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

When [대상 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md) Destination SDK, `uiAttributes` 섹션에서 대상 카드의 다음 시각적 속성을 정의합니다.

* 대상 설명서 페이지의 [대상 카탈로그](../../../catalog/overview.md).
* 대상 카탈로그 카드에 표시할 아이콘을 호스팅한 URL입니다.
* 대상이 Platform UI에 표시되는 카테고리입니다.
* 대상에 대한 데이터 내보내기 빈도입니다.
* Amazon S3, Azure Blob 등과 같은 대상 연결 유형입니다.

를 통해 UI 속성을 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 UI 속성에 대해 설명하고 고객이 Experience Platform UI에서 보게 될 내용을 보여줍니다.

![Experience Platform 인터페이스의 UI 속성을 보여주는 UI 스크린샷](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` 는 페이지의 [대상 카탈로그](../../../catalog/overview.md) 목적지에 대해 지정합니다. Adobe Experience Platform의 모든 제품화된 대상에는 해당 설명서 페이지가 있어야 합니다. [대상 설명서 페이지를 만드는 방법을 알아봅니다](../../docs-framework/documentation-instructions.md) 목적지에 대해 지정합니다. 이는 개인/사용자 지정 대상에 필요하지 않습니다.

다음 형식을 사용하십시오. `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, 위치 `YOURDESTINATION` 은 대상의 이름입니다. Moviestar라는 대상의 경우 `http://www.adobe.com/go/destinations-moviestar-en`.

사용자는 UI의 대상 카탈로그 페이지에서 설명서 링크를 보고 방문할 수 있습니다. 대상 카드를 찾은 다음 **[!UICONTROL 추가 작업]**, 그런 다음 **[!UICONTROL 설명서 보기]**&#x200B;를 클릭하십시오.

![설명서 링크 위치를 보여주는 UI 이미지입니다.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>이 링크는 Adobe이 대상을 라이브로 설정하고 설명서가 게시된 후에만 작동합니다.

### `category` {#category}

`category` 는 Adobe Experience Platform에서 대상에 지정된 카테고리를 참조하는 문자열 매개 변수입니다. 자세한 내용은 [대상 카테고리](../../../destination-types.md). 다음 값 중 하나를 사용합니다. `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

사용자는 아래 이미지와 같이 대상 카탈로그의 화면 왼쪽에 있는 대상 카테고리 목록을 볼 수 있습니다.

![대상 카테고리 위치를 보여주는 UI 이미지입니다.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` 는 대상에 따라 연결 유형을 참조하는 문자열 매개 변수입니다. 지원되는 값: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

사용자는 [찾아보기](../../../ui/destinations-workspace.md#browse) 대상 작업 공간의 탭.

![UI에서 연결 유형 위치를 보여주는 UI 이미지입니다.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` 는 대상에서 지원하는 데이터 내보내기 유형을 참조하는 문자열 매개 변수입니다. 을 로 설정합니다. `Streaming` API 기반 통합용 또는 `Batch` 파일을 대상으로 내보낼 때

사용자는 **[!UICONTROL 데이터 흐름 실행]** 각 대상 연결의 페이지입니다.

![UI에서 빈도 유형 위치를 보여주는 UI 이미지.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Destination SDK으로 만드는 대상을 제한된 수의 고객에게 사용할 수 있는 경우 대상 카탈로그의 대상 카드를 베타로 표시할 수 있습니다.

이렇게 하려면 `isBeta: "true"` 대상 구성의 UI 속성 섹션에 있는 매개 변수를 사용하여 대상 카드를 적절하게 표시할 수 있습니다.

![베타로 표시된 대상 카드를 보여주는 UI 이미지입니다.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상에 대해 구성할 수 있는 UI 특성과 사용자가 Platform UI에서 해당 속성을 볼 수 있는 위치를 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [배치 구성](batch-configuration.md)
* [내역 프로필 자격](historical-profile-qualifications.md)