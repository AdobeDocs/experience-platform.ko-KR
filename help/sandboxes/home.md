---
keywords: Experience Platform;홈;인기 항목;샌드박스;샌드박스;테스트;테스트
solution: Experience Platform
title: 샌드박스 개요
topic: 개요
description: 샌드박스는 Experience Platform의 단일 인스턴스 내에서 가상 파티션으로, 디지털 경험 애플리케이션의 개발 프로세스와 매끄럽게 통합됩니다.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# 샌드박스 개요

Adobe Experience Platform은 디지털 경험 애플리케이션을 글로벌 규모로 보완하도록 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 고려해야 합니다.

이러한 요구를 해결하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

이 문서에서는 Experience Platform의 샌드박스에 대한 고급 개요를 제공합니다.

## 샌드박스 이해

샌드박스는 Experience Platform의 단일 인스턴스 내에서 가상 파티션으로, 디지털 경험 애플리케이션의 개발 프로세스와 매끄럽게 통합됩니다. Experience Platform 인스턴스는 하나의 프로덕션 샌드박스와 여러 개의 비프로덕션 샌드박스를 지원합니다. 각 샌드박스는 고유한 플랫폼 리소스(스키마, 데이터 세트, 프로필 등)의 독립적인 라이브러리를 유지 관리합니다.  샌드박스 내에서 수행되는 모든 컨텐츠 및 작업은 해당 샌드박스에만 제한되며 다른 샌드박스에는 영향을 주지 않습니다.

비프로덕션 샌드박스를 사용하면 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고 실험을 실행하며 사용자 정의 구성을 만들 수 있습니다. 또한 비프로덕션 샌드박스에는 샌드박스에서 고객이 생성한 모든 리소스를 제거하는 재설정 기능이 있습니다. 비프로덕션 샌드박스는 프로덕션 샌드박스로 변환할 수 없습니다. 기본 Experience Platform 라이센스는 5개의 샌드박스(1개의 프로덕션 및 4개의 비프로덕션)를 부여합니다. 비프로덕션 샌드박스 10개 팩을 총 샌드박스 최대 75개까지 추가할 수 있습니다. 자세한 내용은 IMS 조직 관리자 또는 Adobe 판매 담당자에게 문의하십시오.

>[!NOTE]
>
>샌드박스가 처음 만들어지면 데이터가 포함되지 않습니다. 각 샌드박스는 자체 분리된 데이터 저장소를 유지 관리하기 때문에 데이터를 독립적으로 인제스트해야 합니다.

요약하면 샌드박스는 다음과 같은 이점을 제공합니다.

* **애플리케이션 라이프사이클 관리**:디지털 경험 애플리케이션을 개발하고 발전시키는 별도의 가상 환경을 만들 수 있습니다.
* **프로젝트 및 브랜드 관리**:여러 프로젝트를 동일한 IMS 조직 내에서 동시에 실행할 수 있으며 격리 및 액세스 제어 기능을 제공합니다. 향후 릴리스는 여러 지역에 배포할 수 있도록 지원합니다.
* **유연한 개발 에코시스템**:탐색, 지원 및 데모를 위해 원활하고 확장 가능하고 비용 효과적인 방법으로 샌드박스를 제공합니다.

## 샌드박스에 대한 액세스 제어

기본적으로 조직의 모든 사용자는 프로덕션 샌드박스에 액세스할 수 있습니다. 비프로덕션 샌드박스에 대한 액세스 권한은 시스템 관리자, 제품 관리자 또는 제품 프로필 관리자가 [Adobe Admin Console](https://adminconsole.adobe.com)을 통해 부여해야 합니다.

비프로덕션 샌드박스를 보거나, 만들거나, 업데이트하거나 삭제하려면 사용자에게도 샌드박스 관리 권한이 부여되어야 합니다.

샌드박스의 역할 및 권한 관리에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

## Experience Platform UI의 샌드박스

[Experience Platform 사용자 인터페이스](https://platform.adobe.com)에서 사용자는 화면의 왼쪽 상단에 있는 **샌드박스 전환기** 컨트롤을 사용하여 액세스할 수 있는 샌드박스 사이를 전환할 수 있습니다.  샌드박스 관리 권한이 있는 사용자는 왼쪽 탐색의 **[!UICONTROL Sandboxes]** 탭에 액세스할 수 있으며 여기에서 조직의 샌드박스를 보고 관리할 수 있습니다. UI에서 샌드박스를 사용하여 작업하는 방법에 대한 자세한 내용은 [샌드박스 사용자 안내서](ui/overview.md)를 참조하십시오.

## Experience Platform API의 샌드박스

Experience Platform API를 호출할 때 샌드박스 이름을 `x-sandbox-name` 헤더 아래에 제공해야 합니다. 예를 들어 프로덕션 샌드박스 내의 모든 데이터 세트를 보기 위해 [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)을 호출할 때 샌드박스의 이름(&quot;prod&quot;)은 API 요청에서 헤더로 제공됩니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

`x-sandbox-name`이(가) API 호출에 포함되지 않은 경우 시스템은 대신 기본 샌드박스를 사용합니다. 하지만 우수 사례는 기본 샌드박스를 사용하는 경우에도 항상 모든 API 호출에 이 헤더를 포함하는 것입니다. 이러한 이유로 Experience Platform에 대한 API 설명서에서 `x-sandbox-name`을 필수 헤더로 처리합니다.

### 샌드박스 API

샌드박스 API를 사용하면 RESTful API 작업을 사용하여 샌드박스를 관리할 수 있습니다. 올바른 형식의 요청 및 예제 응답을 포함하여 API를 사용하는 방법에 대한 자세한 내용은 [샌드박스 개발자 안내서](api/getting-started.md)를 참조하십시오.

## 다음 단계

이 문서를 읽음으로써 Experience Platform의 샌드박스에 대한 필수 개념을 도입했습니다. 샌드박스 관리 방법에 대한 자세한 내용은 UI에 대한 [사용자 안내서](ui/overview.md) 또는 API에 대한 [개발자 안내서](./api/getting-started.md)를 참조하십시오.

샌드박스는 개발 팀의 플랫폼 환경을 분리하는 중요한 도구로 사용되지만 Adobe Admin Console을 사용하여 보다 세분화된 액세스 제어를 관리할 수도 있습니다. 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.