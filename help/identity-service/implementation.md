---
title: ID 서비스 구현 안내서
description: ID 서비스에서 ID 그래프를 작성하는 데 사용하기 전에 Adobe Experience Platform에 제공된 데이터를 처리하는 방법에 대해 알아봅니다.
source-git-commit: bdda234c44b63999d7582857975afa64fdb93605
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# ID 서비스 구현 안내서

이 문서에서는 특정 고객에 대한 ID 그래프를 작성하기 위해 ID 서비스에서 사용하기 전에 Adobe Experience Platform에 제공된 데이터가 처리되는 방법에 대한 정보를 제공합니다.

## ID 필드 결정

엔터프라이즈 데이터 수집 전략에 따라 ID로 레이블을 지정하는 데이터 필드에 따라 ID 맵에 포함되는 데이터가 결정됩니다. Experience Platform의 이점을 극대화하고 가능한 가장 포괄적인 고객 ID를 얻으려면 온라인과 오프라인 데이터를 모두 업로드해야 합니다.

* 온라인 데이터는 사용자 이름 및 이메일 주소와 같이 온라인 상태 및 동작을 설명하는 데이터입니다.

* 오프라인 데이터는 CRM 시스템의 ID와 같이, 온라인 존재와 직접 관련이 없는 데이터를 의미한다. 이러한 유형의 데이터는 ID를 보다 강력하게 만들고 개별 시스템 전반에서 데이터 결합을 지원합니다.

## 추가 ID 네임스페이스 만들기

Experience Platform은 다양한 표준 네임스페이스를 제공하지만 ID를 적절하게 분류하려면 추가 네임스페이스를 만들어야 할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [조직에 대한 사용자 정의 네임스페이스 만들기](./namespaces.md).

>[!NOTE]
>
>ID 네임스페이스는 ID의 한정자입니다. 따라서 네임스페이스가 만들어지면 삭제할 수 없습니다.

## XDM(Experience Data Model)에 ID 데이터 포함

Experience Platform이 고객 데이터를 구성하는 표준화된 프레임워크로서, XDM(Experience Data Model)을 통해 Experience Platform과 상호 작용하는 Experience Platform 및 기타 서비스에서 데이터를 공유하고 이해할 수 있습니다. 자세한 내용은 [XDM 시스템 개요](../xdm/home.md).

레코드와 시계열 스키마 모두 ID 데이터를 포함하는 수단을 제공합니다. 데이터가 수집될 때 공통 ID 데이터를 공유하는 것으로 확인되면 ID 그래프는 서로 다른 네임스페이스의 데이터 조각 간에 새로운 관계를 생성합니다.

## XDM 필드에 ID 레이블 지정

유형의 모든 필드 `string` 레코드 또는 시계열 XDM 클래스를 구현하는 스키마에서는 ID 필드로 레이블 지정할 수 있습니다. 따라서 해당 필드에 수집된 모든 데이터는 ID 데이터로 간주됩니다.

ID 필드를 사용하면 공통 PII 데이터를 공유하는 경우 ID를 연결할 수도 있습니다.
예를 들어 전화 번호 필드에 ID 필드로 레이블을 지정하면 Identity Service는 동일한 전화 번호를 사용하고 있는 것으로 확인된 다른 개인과의 관계를 자동으로 그래프로 표시합니다.

>[!NOTE]
>
>* 배열 및 맵 유형 필드는 지원되지 않으며 ID 필드로 표시하고 레이블 지정할 수 없습니다.
>* 결과 ID의 네임스페이스는 필드에 레이블이 지정될 때 제공됩니다.

## ID 서비스에 대한 데이터 세트 구성

스트리밍 수집 프로세스 중에 Identity Service는 레코드 및 시계열 데이터에서 ID 데이터를 자동으로 추출합니다. 그러나 데이터를 수집하려면 ID 서비스에 대해 활성화해야 합니다. 다음에 대한 자습서 읽기:  [api를 사용하여 실시간 고객 프로필 및 ID 서비스에 대한 데이터 세트 구성](../profile/tutorials/dataset-configuration.md) 추가 정보.

## ID 서비스로 데이터 수집

ID 서비스는 다음 중 하나를 통해 Experience Platform으로 전송된 XDM 호환 데이터를 사용합니다. [일괄 처리 수집](../ingestion/batch-ingestion/overview.md) 또는 [스트리밍 수집](../ingestion/streaming-ingestion/overview.md).

다음 비디오는 ID 서비스에 대한 이해를 돕기 위한 것입니다. 이 비디오는 데이터 필드에 ID로 레이블을 지정하고 ID 데이터를 수집한 다음 데이터가 Adobe Experience Platform ID 서비스 개인 그래프에 적용되었는지 확인하는 방법을 보여 줍니다.

>[!WARNING]
>
>다음 비디오에 표시된 Experience Platform UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 설명서 를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)