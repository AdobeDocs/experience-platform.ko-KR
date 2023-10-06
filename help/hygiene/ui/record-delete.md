---
title: 레코드 삭제
description: Adobe Experience Platform UI에서 레코드를 삭제하는 방법을 알아봅니다.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 7%

---

# [!BADGE 베타]{type=Informative} 레코드 삭제 {#record-delete}

사용 [[!UICONTROL 데이터 수명 주기] 작업 영역](./overview.md) 기본 ID를 기반으로 Adobe Experience Platform에서 레코드를 삭제할 수 있습니다. 이러한 레코드는 개별 소비자 또는 ID 그래프에 포함된 다른 엔티티에 연결할 수 있습니다.

>[!IMPORTANT]
> 
>레코드 삭제 기능은 현재 베타 버전이며 다음에서만 사용할 수 있습니다. **제한된 릴리스**. 모든 고객이 이용할 수 있는 것은 아닙니다. 레코드 삭제 요청은 제한된 릴리스의 조직에만 사용할 수 있습니다.
> 
> 
>레코드 삭제는 데이터 정리, 익명 데이터 제거 또는 데이터 최소화에 사용됩니다. 다음과 같습니다 **아님** GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정에 관한 데이터 주체 권한 요청(준수)에 사용됩니다. 모든 규정 준수 사용 사례에 대해 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 대신,

## 전제 조건 {#prerequisites}

레코드를 삭제하려면 Experience Platform 시 ID 필드가 작동하는 방식을 이해해야 합니다. 특히 삭제할 데이터 세트(또는 데이터 세트)에 따라 레코드를 삭제할 엔티티의 기본 ID 값을 알고 있어야 합니다.

Platform의 ID에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Adobe Experience Platform ID 서비스](../../identity-service/home.md): 디바이스와 시스템 간에 ID를 브리징하여 일치하는 XDM 스키마에 의해 정의된 ID 필드를 기반으로 데이터 세트를 서로 연결합니다.
* [ID 네임스페이스](../../identity-service/namespaces.md): ID 네임스페이스는 단일 사용자와 관련될 수 있는 다양한 유형의 ID 정보를 정의하며, 각 ID 필드에 필요한 구성 요소입니다.
* [실시간 고객 프로필](../../profile/home.md): ID 그래프를 사용하여 실시간으로 업데이트되는 여러 소스의 집계 데이터를 기반으로 통합 소비자 프로필을 제공합니다.
* [경험 데이터 모델(XDM)](../../xdm/home.md): 스키마를 사용하여 플랫폼 데이터에 대한 표준 정의 및 구조를 제공합니다. 모든 Platform 데이터 세트는 특정 XDM 스키마를 준수하며, 스키마는 ID인 필드를 정의합니다.
* [ID 필드](../../xdm/ui/fields/identity.md): XDM 스키마에서 ID 필드를 정의하는 방법을 알아봅니다.

## 요청 만들기 {#create-request}

프로세스를 시작하려면 다음을 선택합니다 **[!UICONTROL 데이터 수명 주기]** ( 플랫폼 UI의 왼쪽 탐색 ). 다음 [!UICONTROL 데이터 라이프사이클 요청] 작업 영역이 나타납니다. 그런 다음 을 선택합니다. **[!UICONTROL 요청 만들기]** 작업 공간의 기본 페이지에서 가져온 템플릿입니다.

![다음 [!UICONTROL 데이터 라이프사이클 요청] 작업 공간 [!UICONTROL 요청 만들기] 선택됨.](../images/ui/record-delete/create-request-button.png)

요청 생성 워크플로가 나타납니다. 기본적으로 **[!UICONTROL 레코드 삭제]** 아래에 옵션이 선택되어 있습니다. **[!UICONTROL 요청된 작업]** 섹션. 이 옵션을 선택된 상태로 두십시오.

>[!IMPORTANT]
> 
>효율성을 향상시키고 데이터 세트 운영 비용을 절감하기 위한 지속적인 변경의 일환으로, 델타 포맷으로 이동한 조직은 ID 서비스, 실시간 고객 프로필 및 데이터 레이크에서 데이터를 삭제할 수 있습니다. 이러한 유형의 사용자를 델타 마이그레이션이라고 합니다. 델타 마이그레이션된 조직의 사용자는 단일 데이터 세트 또는 모든 데이터 세트에서 레코드를 삭제할 수 있습니다. 델타 마이그레이션되지 않은 조직의 사용자는 아래 이미지에 표시된 대로 단일 또는 모든 데이터 세트에서 레코드를 삭제할 수 없습니다. 이 경우 다음을 계속 진행하십시오. [id 제공](#provide-identities) 안내서의 섹션입니다.

![을(를) 사용한 요청 생성 워크플로 [!UICONTROL 레코드 삭제] 옵션을 선택하고 강조 표시합니다.](../images/ui/record-delete/delete-record.png)

## 데이터 세트 선택 {#select-dataset}

다음 단계는 단일 데이터 세트에서 레코드를 삭제할지 또는 모든 데이터 세트에서 레코드를 삭제할지를 결정하는 것입니다. 이 옵션을 사용할 수 없는 경우 [id 제공](#provide-identities) 안내서의 섹션입니다.

아래 **[!UICONTROL 기록 세부 정보]** 섹션에서 라디오 단추를 사용하여 특정 데이터 세트와 모든 데이터 세트 중에서 선택합니다. 다음을 선택하는 경우 **[!UICONTROL 데이터 세트 선택]**&#x200B;를 계속 진행하여 데이터베이스 아이콘(![데이터베이스 아이콘](../images/ui/record-delete/database-icon.png)사용 가능한 데이터 세트 목록을 제공하는 대화 상자를 엽니다. 목록에서 원하는 데이터 세트를 선택한 다음 **[!UICONTROL 완료]**.

![다음 [!UICONTROL 데이터 세트 선택] 데이터 세트가 선택되어 있고 [!UICONTROL 완료] 강조 표시됨.](../images/ui/record-delete/select-dataset.png)

모든 데이터 세트에서 레코드를 삭제하려면 **[!UICONTROL 모든 데이터 세트]**.

![다음 [!UICONTROL 데이터 세트 선택] 대화 상자 [!UICONTROL 모든 데이터 세트] 옵션이 선택되었습니다.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>선택 **[!UICONTROL 모든 데이터 세트]** 옵션을 사용하면 삭제 작업이 더 오래 걸릴 수 있으며 정확한 레코드 삭제가 수행되지 않을 수 있습니다.

## ID 제공 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="기본 ID"
>abstract="기본 ID는 레코드를 Experience Platform의 소비자 프로필에 연결하는 속성입니다. 데이터 세트의 기본 ID 필드는 데이터 세트가 기반으로 하는 스키마에 의해 정의됩니다. 이 열에서는 이메일 주소의 경우 `email` 및 Experience Cloud ID의 경우 `ecid` 등 레코드의 기본 ID 유형(또는 네임스페이스)을 입력해야 합니다. 자세한 내용은 데이터 라이프사이클 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="ID 값"
>abstract="이 열에서는 왼쪽 열에 입력한 ID 유형에 해당되는 레코드의 기본 ID 값을 입력해야 합니다. 기본 ID 유형이 `email`인 경우 값은 레코드의 이메일 주소이어야 합니다. 자세한 내용은 데이터 라이프사이클 UI 안내서 를 참조하십시오."

레코드를 삭제할 때 시스템에서 삭제할 레코드를 결정할 수 있도록 ID 정보를 제공해야 합니다. 플랫폼의 모든 데이터 세트에 대해 레코드는 **기본 ID** 데이터 세트의 스키마로 정의되는 필드입니다.

플랫폼의 모든 ID 필드와 마찬가지로 기본 ID는 **유형** (경우에 따라 id 네임스페이스라고도 함) 및 **값**. ID 유형은 필드가 레코드(예: 이메일 주소)를 식별하는 방법에 대한 컨텍스트를 제공하고, 값은 해당 유형에 대한 레코드의 특정 ID를 나타냅니다(예: `jdoe@example.com` 대상: `email` id 유형). ID로 사용되는 일반적인 필드에는 계정 정보, 디바이스 ID 및 쿠키 ID가 포함됩니다.

>[!TIP]
>
>특정 데이터 세트에 대한 기본 ID를 모를 경우 Platform UI에서 찾을 수 있습니다. 다음에서 **[!UICONTROL 데이터 세트]** 작업 영역에서 목록에서 해당 데이터 세트를 선택합니다. 데이터 세트에 대한 세부 정보 페이지에서 오른쪽 레일의 데이터 세트 스키마 이름 위로 마우스를 가져갑니다. 기본 ID가 스키마 이름 및 설명과 함께 표시됩니다.
>
>![데이터 세트가 선택되고 데이터 세트 세부 정보 패널에서 스키마 대화 상자가 열린 데이터 세트 대시보드. 데이터 세트의 기본 ID가 강조 표시됩니다.](../images/ui/record-delete/dataset-primary-identity.png)

단일 데이터 세트에서 레코드를 삭제하는 경우, 데이터 세트에는 기본 ID가 하나만 있을 수 있으므로, 제공한 모든 ID의 유형은 동일해야 합니다. 모든 데이터 세트에서 삭제하는 경우, 서로 다른 데이터 세트에 서로 다른 기본 ID가 있을 수 있으므로 여러 ID 유형을 포함할 수 있습니다.

레코드를 삭제할 때 ID를 제공하는 두 가지 옵션이 있습니다.

* [JSON 파일 업로드](#upload-json)
* [ID 값을 수동으로 입력](#manual-identity)

### JSON 파일 업로드 {#upload-json}

JSON 파일을 업로드하려면 해당 파일을 제공된 영역으로 끌어다 놓거나 **[!UICONTROL 파일 선택]** 로컬 디렉토리에서 을 찾아 선택합니다.

![강조 표시된 JSON 파일을 업로드하기 위한 파일 선택 및 드래그 앤 드롭 인터페이스가 있는 요청 생성 워크플로우입니다.](../images/ui/record-delete/upload-json.png)

JSON 파일의 형식은 개체 배열로 지정해야 하며 각 개체는 ID를 나타냅니다.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| 속성 | 설명 |
| --- | --- |
| `namespaceCode` | ID 유형. |
| `value` | 유형으로 표시되는 ID 값입니다. |

파일이 업로드되면 다음 작업을 계속할 수 있습니다. [요청 제출](#submit).

### ID 수동 입력 {#manual-identity}

ID를 수동으로 입력하려면 다음을 선택합니다. **[!UICONTROL ID 추가]**.

![을(를) 사용한 요청 생성 워크플로 [!UICONTROL ID 추가] 강조 표시된 옵션입니다.](../images/ui/record-delete/add-identity.png)

ID를 한 번에 하나씩 입력할 수 있는 컨트롤이 나타납니다. 아래 **[!UICONTROL 기본 ID]**&#x200B;드롭다운 메뉴를 사용하여 id 유형을 선택합니다. 아래 **[!UICONTROL ID 값]**&#x200B;레코드에 대한 기본 id 값을 제공합니다.

![ID 필드가 있는 요청 생성 워크플로우가 수동으로 추가되었습니다.](../images/ui/record-delete/identity-added.png)

ID를 더 추가하려면 더하기 아이콘(![더하기 아이콘](../images/ui/record-delete/plus-icon.png)) 행 중 하나의 옆에 있거나 **[!UICONTROL ID 추가]**.

![더하기 아이콘 및 ID 추가 아이콘이 강조 표시된 요청 생성 워크플로.](../images/ui/record-delete/more-identities.png)

## 요청 제출 {#submit}

요청에 ID를 추가했으면 **[!UICONTROL 요청 설정]**&#x200B;를 선택하기 전에 요청의 이름과 선택적 설명을 입력합니다. **[!UICONTROL 제출]**.

>[!IMPORTANT]
> 
>매월 제출할 수 있는 총 고유 ID 레코드 삭제 횟수에는 제한이 있습니다. 이러한 제한은 라이선스 계약을 기반으로 합니다. Adobe Real-time Customer Data Platform 및 Adobe Journey Optimizer의 모든 에디션을 구입한 조직은 매월 최대 10만 건의 ID 레코드 삭제를 제출할 수 있습니다. 구입한 조직 **Adobe 헬스케어 실드** 또는 **Adobe 개인정보 보호 및 보안 실드** 매달 최대 60만 개의 id 레코드 삭제를 제출할 수 있습니다.<br>UI를 통한 단일 레코드 삭제 요청으로 한 번에 10,000개의 ID를 제출할 수 있습니다. 다음 [레코드를 삭제하는 API 메서드](https://experienceleague.adobe.com/docs/experience-platform/hygiene/api/workorder.html?lang=en#create) 를 통해 한 번에 100,000개의 ID를 제출할 수 있습니다.

![요청 설정 [!UICONTROL 이름] 및 [!UICONTROL 설명] 필드가 있는 [!UICONTROL 제출] 강조 표시됨.](../images/ui/record-delete/submit.png)

A [!UICONTROL 요청 확인] 삭제한 후에는 id를 복구할 수 없음을 나타내는 대화 상자가 나타납니다. 선택 **[!UICONTROL 제출]** 삭제할 데이터가 있는 id 목록을 확인합니다.

![다음 [!UICONTROL 요청 확인] 대화 상자.](../images/ui/record-delete/confirm-request.png)

요청이 제출되면 작업 주문이 만들어지고 [!UICONTROL 기록] 의 탭 [!UICONTROL 데이터 수명 주기] 작업 영역. 여기에서 요청을 처리할 때 작업 주문의 상태를 모니터링할 수 있습니다.

>[!NOTE]
>
>의 개요 섹션을 참조하십시오. [타임라인 및 투명도](../home.md#record-delete-transparency) 레코드 삭제가 실행되면 처리되는 방식에 대한 자세한 정보.

![다음 [!UICONTROL 기록] 의 탭 [!UICONTROL 데이터 수명 주기] 새 요청이 강조 표시된 작업 영역.](../images/ui/record-delete/request-log.png)

## 다음 단계

이 문서에서는 Experience Platform UI에서 레코드를 삭제하는 방법을 다룹니다. UI에서 다른 데이터 수명 주기 관리 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 라이프사이클 UI 개요](./overview.md).

데이터 위생 API를 사용하여 레코드를 삭제하는 방법에 대해 알아보려면 다음을 참조하십시오. [작업 주문 끝점 안내서](../api/workorder.md).
