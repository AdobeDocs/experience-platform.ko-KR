---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 외부 대상 가져오기 및 사용
description: Adobe Experience Platform에서 외부 대상을 사용하는 방법에 대해 알아보려면 이 자습서를 따르십시오.
topic: 자습서
translation-type: tm+mt
source-git-commit: 400e4d9007212ed2693d031ae912a4f1cca97c57
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# 외부 대상 가져오기 및 사용

Adobe Experience Platform은 나중에 새 세그먼트 정의에 대한 구성 요소로 사용할 수 있는 외부 대상을 가져오는 기능을 지원합니다. 이 문서에서는 외부 대상을 가져오고 사용할 Experience Platform 설정을 위한 자습서를 제공합니다.

## 시작하기

- [세그멘테이션 서비스](../home.md):실시간 고객 프로필 데이터에서 대상 세그먼트를 만들 수 있습니다.
- [실시간 고객 프로필](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [경험 데이터 모델(XDM)](../../xdm/home.md):Platform(플랫폼)이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [데이터 세트](../../catalog/datasets/overview.md):Experience Platform의 데이터 지속성 저장 및 관리 구성
- [스트리밍 통합](../../ingestion/streaming-ingestion/overview.md):클라이언트 및 서버측 디바이스의 데이터를 실시간으로 Experience Platform 인제스트 및 저장하는 방법입니다.

## 외부 대상을 위한 ID 네임스페이스 만들기

외부 대상을 사용하기 위한 첫 번째 단계는 ID 네임스페이스를 만드는 것입니다. ID 네임스페이스를 통해 Platform은 세그먼트가 시작되는 위치를 연결할 수 있습니다.

ID 네임스페이스를 만들려면 [identity namespace guide](../../identity-service/namespaces.md#manage-namespaces)의 지침을 따릅니다. ID 네임스페이스를 만들 때 ID 네임스페이스에 소스 세부 정보를 추가하고 해당 [!UICONTROL Type]을(를) **[!UICONTROL Non-people identifier]**(으)로 표시합니다.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## 세그먼트 메타데이터의 스키마 만들기

ID 네임스페이스를 만든 후 만들 세그먼트에 대한 새 스키마를 만들어야 합니다.

스키마 구성을 시작하려면 먼저 왼쪽 탐색 막대에서 **[!UICONTROL Schemas]**&#x200B;을 선택하고 스키마 작업 영역의 오른쪽 위 모서리에 **[!UICONTROL Create schema]**&#x200B;을 선택합니다. 여기서 **[!UICONTROL Browse]**&#x200B;을 선택하여 사용 가능한 스키마 유형의 전체 선택을 확인합니다.

![](../images/tutorials/external-audiences/create-schema-browse.png)

사전 정의된 클래스인 세그먼트 정의를 만들기 때문에 **[!UICONTROL Use existing class]**&#x200B;을 선택합니다. 이제 **[!UICONTROL Segment definition]** 클래스 뒤에 **[!UICONTROL Assign class]**&#x200B;가 옵니다.

![](../images/tutorials/external-audiences/assign-class.png)

스키마가 생성되었으므로 세그먼트 ID를 포함할 필드를 지정해야 합니다. 이 필드는 기본 ID로 표시하고 이전에 만든 네임스페이스에 할당되어야 합니다.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

`_id` 필드를 기본 ID로 표시한 후 스키마의 제목을 선택하고 **[!UICONTROL Profile]** 토글을 표시합니다. [!DNL Real-time Customer Profile]에 대한 스키마를 활성화하려면 **[!UICONTROL Enable]**&#x200B;을 선택합니다.

![](../images/tutorials/external-audiences/schema-profile.png)

이제 이 스키마는 사용자가 만든 비개인 ID 네임스페이스에 기본 ID가 할당되어 프로필에 대해 활성화됩니다. 따라서 이 스키마를 사용하여 플랫폼에 가져온 세그먼트 메타데이터는 다른 사람 관련 프로필 데이터와 병합하지 않고 프로필로 인제스트됩니다.

## 스키마에 대한 데이터 집합 만들기

스키마를 구성한 후에는 세그먼트 메타데이터에 대한 데이터 세트를 만들어야 합니다.

데이터 세트를 만들려면 [데이터 집합 사용자 안내서](../../catalog/datasets/user-guide.md#create)의 지침을 따릅니다. 이전에 만든 스키마를 사용하여 **[!UICONTROL Create dataset from schema]** 옵션을 따를 수 있습니다.

![](../images/tutorials/external-audiences/select-schema.png)

데이터 세트를 만든 후 [데이터 집합 사용자 안내서](../../catalog/datasets/user-guide.md#enable-profile)의 지침에 따라 이 데이터 집합을 실시간 고객 프로필에 사용하도록 설정합니다.

![](../images/tutorials/external-audiences/dataset-profile.png)

## 대상 데이터 설정 및 가져오기

이제 데이터 세트를 활성화하면 UI를 통해 또는 Experience Platform API를 사용하여 데이터를 플랫폼에 보낼 수 있습니다. 이 데이터를 플랫폼에 인제스트하려면 스트리밍 연결을 만들어야 합니다.

스트리밍 연결을 만들려면 [API 자습서](../../sources/tutorials/api/create/streaming/http.md) 또는 [UI 자습서](../../sources/tutorials/ui/create/streaming/http.md)의 지침을 따를 수 있습니다.

스트리밍 연결을 만들면 데이터를 전송할 수 있는 고유한 스트리밍 끝점에 액세스할 수 있습니다. 이러한 끝점으로 데이터를 보내는 방법에 대한 자세한 내용은 스트리밍 레코드 데이터](../../ingestion/tutorials/streaming-record-data.md#ingest-data)에 대한 [자습서를 참조하십시오.

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 가져온 대상을 사용하여 세그먼트 작성

가져온 대상이 설정되면 세그먼테이션 프로세스의 일부로 사용할 수 있습니다. 외부 대상을 찾으려면 세그먼트 빌더로 이동하고 **[!UICONTROL Fields]** 섹션에서 **[!UICONTROL Audiences]** 탭을 선택합니다.

![](../images/tutorials/external-audiences/external-audiences.png)

## 다음 단계

세그먼트에 외부 대상을 사용할 수 있으므로 세그먼트 빌더를 사용하여 세그먼트를 만들 수 있습니다. 세그먼트를 만드는 방법에 대해 알아보려면 세그먼트 만들기](./create-a-segment.md)에 대한 [자습서를 참조하십시오.