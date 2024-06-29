---
title: ID 그래프 연결 규칙 구성 안내서
description: ID 그래프 연결 규칙 구성을 사용하여 데이터를 구현할 때 따라야 할 권장 단계에 대해 알아봅니다.
badge: Beta
source-git-commit: d8a36650b2cd3ec9683763f536ea5c2c2e27455c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 5%

---

# ID 그래프 연결 규칙 구성 안내서

Adobe Experience Platform ID 서비스를 사용하여 데이터를 구현할 때 참조할 수 있는 단계별 안내서는 이 문서를 참조하십시오.

단계별 개요:

1. [필요한 ID 네임스페이스 만들기](#namespace)
2. [그래프 시뮬레이션 도구를 사용하여 ID 최적화 알고리즘을 숙지하십시오](#graph-simulation)
3. [ID 설정 도구를 사용하여 고유한 네임스페이스를 지정하고 네임스페이스에 대한 우선 순위 등급을 구성합니다](#identity-settings)
4. [XDM(경험 데이터 모델) 스키마 만들기](#schema)
5. [데이터 세트 만들기](#dataset)
6. [데이터를 Experience Platform으로 수집](#ingest)

## 사전 구현 사전 요구 사항

시작하기 전에 먼저 시스템의 인증된 이벤트에 항상 개인 식별자가 포함되어 있는지 확인해야 합니다.

<!-- ## Set permissions {#set-permissions}

The first step in the implementation process for Identity Service is to ensure that your Experience Platform account is added to a role that is provisioned with the necessary permissions. Your administrator can configure permissions for your account by navigating to the Permissions UI in Adobe Experience Cloud. From there, your account must be added to a role with the following permissions:

* manage-identity-settings
* view-identity-dashboard
* view-identity-simulation

For more information on permissions, read the [permissions guide](../../access-control/abac/ui/permissions.md). -->

## ID 네임스페이스 만들기 {#namespace}

데이터에 필요한 경우 먼저 조직에 적합한 네임스페이스를 만들어야 합니다. 사용자 지정 네임스페이스를 만드는 방법에 대한 단계는 의 안내서를 참조하십시오 [ui에서 사용자 정의 네임스페이스 만들기](../features/namespaces.md#create-custom-namespaces).

## 그래프 시뮬레이션 도구 사용 {#graph-simulation}

다음으로 이동 [그래프 시뮬레이션 도구](./graph-simulation.md) ID 서비스 UI 작업 공간. 그래프 시뮬레이션 도구를 사용하여 다양한 고유한 네임스페이스 및 네임스페이스 우선 순위 구성으로 구축된 ID 그래프를 시뮬레이션할 수 있습니다.

다양한 구성을 만들어 그래프 시뮬레이션 도구를 사용하여 ID 최적화 알고리즘 및 특정 구성이 그래프의 동작 방식에 어떻게 영향을 줄 수 있는지 배우고 더 잘 이해할 수 있습니다.

## ID 설정 구성 {#identity-settings}

그래프의 동작 방식에 대해 잘 알고 있는 경우 [id 설정 도구](./identity-settings-ui.md) ID 서비스 UI 작업 공간.

ID 설정 도구를 사용하여 고유한 네임스페이스를 지정하고 우선 순위별로 네임스페이스를 구성합니다. 설정 적용이 끝나면 새 설정이 ID 서비스에 반영되기까지 최소 6시간이 걸리기 때문에 데이터 수집을 진행하려면 최소 6시간 이상 기다려야 합니다.

## XDM 스키마 만들기 {#schema}

고유한 네임스페이스 및 네임스페이스 우선 순위가 설정되면 이제 데이터를 수집하기 위해 필요한 설정으로 진행할 수 있습니다. 먼저 XDM 스키마를 만들어야 합니다. 데이터에 따라 XDM 개인 프로필과 XDM ExperienceEvent 모두에 대한 스키마를 만들어야 할 수 있습니다.

실시간 고객 프로필로 데이터를 수집하려면 스키마에 기본 ID로 지정된 필드가 하나 이상 포함되어 있는지 확인해야 합니다. 기본 ID를 설정하여 프로필 수집에 주어진 스키마를 활성화할 수 있습니다.

스키마를 만드는 방법에 대한 지침은 의 안내서를 참조하십시오 [ui에서 XDM 스키마 만들기](../../xdm/tutorials/create-schema-ui.md).

## 데이터 세트 만들기 {#dataset}

그런 다음 데이터 세트를 만들어 수집할 데이터의 구조를 제공합니다. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트는 스키마와 함께 작동하며 데이터를 실시간 고객 프로필로 수집하려면 프로필 수집에 대해 데이터 세트를 활성화해야 합니다. 프로필에 대해 데이터 세트를 활성화하려면 프로필 수집에 대해 활성화된 스키마를 참조해야 합니다.

데이터 세트를 만드는 방법에 대한 지침은 [데이터 세트 UI 안내서](../../catalog/datasets/user-guide.md).

## 데이터 수집 {#ingest}

이 시점에는 다음 항목이 있어야 합니다.

* ID 서비스 기능에 액세스하는 데 필요한 권한입니다.
* 데이터를 위한 네임스페이스.
* 네임스페이스에 대해 지정된 고유한 네임스페이스와 구성된 우선 순위
* 하나 이상의 XDM 스키마. (데이터와 특정 사용 사례에 따라 프로필과 경험 이벤트 스키마를 모두 만들어야 할 수 있습니다.)
* 스키마를 기반으로 하는 데이터 세트입니다.

위에 나열된 모든 항목이 있으면 데이터 수집을 시작하여 Experience Platform을 수행할 수 있습니다. 여러 가지 다양한 방법을 통해 데이터 수집을 수행할 수 있습니다. 다음 서비스를 사용하여 데이터를 Experience Platform 상태로 만들 수 있습니다.

* [일괄 처리 및 스트리밍 수집](../../ingestion/home.md)
* [Experience Platform의 데이터 수집](../../collection/home.md)
* [Experience Platform 소스](../../sources/home.md)

>[!TIP]
>
>데이터가 수집되면 XDM 원시 데이터 페이로드는 변경되지 않습니다. UI에 기본 ID 구성이 계속 표시될 수 있습니다. 그러나 이러한 구성은 ID 설정에 의해 재정의됩니다.

피드백의 경우 **[!UICONTROL Beta 피드백]** 옵션을 선택할 수 있습니다.