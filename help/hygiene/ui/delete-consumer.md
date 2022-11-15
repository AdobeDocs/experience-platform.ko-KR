---
title: 소비자 레코드 삭제
description: Adobe Experience Platform UI에서 소비자 레코드를 삭제하는 방법을 알아봅니다.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 7679de9d30c00873b279c5315aa652870d8c34fd
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# 소비자 레코드 삭제

다음 [[!UICONTROL 데이터 위생] 작업 영역](./overview.md) Adobe Experience Platform UI에서 ID 서비스 및 실시간 고객 프로필에 참여하는 소비자 레코드를 삭제할 수 있습니다.

>[!IMPORTANT]
>
>소비자 삭제 요청은 구매한 조직에만 사용할 수 있습니다 **Adobe 의료 보호**.
>
>
>소비자 삭제는 데이터 정리, 익명 데이터 제거 또는 데이터 최소화에 사용됩니다. 그렇습니다 **not** GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정에 관련된 데이터 주체 권한 요청(준수)에 사용됩니다. 모든 규정 준수 사용 사례의 경우 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 을 가리키도록 업데이트하는 것이 좋습니다.

## 전제 조건

소비자 레코드를 삭제하려면 Experience Platform에서 ID 필드가 작동하는 방식을 제대로 이해해야 합니다. 특히, 삭제할 데이터 세트(또는 데이터 세트)에 따라 레코드를 삭제할 소비자의 기본 ID 값을 알고 있어야 합니다.

Platform의 ID에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Adobe Experience Platform Identity 서비스](../../identity-service/home.md): 장치 및 시스템 간에 ID를 브리징하여 XDM 스키마에서 정의한 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
   * [ID 네임스페이스](../../identity-service/namespaces.md): ID 네임스페이스는 한 개인을 연결할 수 있는 다양한 유형의 ID 정보를 정의하며 각 ID 필드에 필요한 구성 요소입니다.
* [실시간 고객 프로필](../../profile/home.md): 소비자 ID 그래프를 활용하여 거의 실시간으로 업데이트되는 여러 소스의 집계 데이터를 기반으로 통합된 소비자 프로필을 제공합니다.
* [XDM(경험 데이터 모델)](../../xdm/home.md): 스키마를 사용하여 Platform 데이터에 대한 표준 정의 및 구조를 제공합니다. 모든 Platform 데이터 세트는 특정 XDM 스키마를 따르며 스키마는 ID인 필드를 정의합니다.
   * [ID 필드](../../xdm/ui/fields/identity.md): ID 필드가 XDM 스키마에서 정의되는 방법을 알아봅니다.

## 새 요청 만들기

프로세스를 시작하려면 다음을 선택합니다 **[!UICONTROL 요청 만들기]** 작업 공간의 기본 페이지에서 을 참조하십시오.

![이미지를 보여주는 이미지 [!UICONTROL 요청 만들기] 선택한 단추](../images/ui/delete-consumer/create-request-button.png)

요청 만들기 대화 상자가 나타납니다. 기본적으로 **[!UICONTROL 소비자]** 옵션 아래에 선택되어 있습니다 **[!UICONTROL 요청된 작업]** 섹션을 참조하십시오. 이 옵션을 선택된 상태로 두십시오.

![만들기 대화 상자에서 선택한 소비자 옵션을 보여주는 이미지](../images/ui/delete-consumer/consumer-action.png)

## 데이터 세트 선택

아래에 **[!UICONTROL 소비자 세부 사항]** 섹션에서 다음 단계는 단일 데이터 세트에서 소비자 데이터를 삭제할지 또는 모든 데이터 세트에서 삭제할지 여부를 결정하는 것입니다.

만약 **[!UICONTROL 데이터 세트 선택]**&#x200B;데이터베이스 아이콘( )을 선택합니다.![데이터베이스 아이콘 이미지](../images/ui/delete-consumer/database-icon.png))이면 목록에서 원하는 데이터 세트를 선택할 수 있는 대화 상자가 나타납니다.

![데이터 집합 선택 대화 상자를 보여주는 이미지](../images/ui/delete-consumer/select-dataset.png)

모든 데이터 세트에서 소비자 데이터를 삭제하려면 **[!UICONTROL 모든 데이터 세트]**.

![이미지를 보여주는 이미지 [!UICONTROL 모든 데이터 세트] 선택](../images/ui/delete-consumer/all-datasets.png)

>[!NOTE]
>
>선택 **[!UICONTROL 모든 데이터 세트]** 선택 사항으로 인해 삭제 작업이 오래 걸릴 수 있으며 정확한 레코드 삭제가 수행되지 않을 수 있습니다.

## 소비자 ID 제공 {#provide-consumer-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="기본 ID"
>abstract="기본 ID는 Experience Platform에서 소비자의 프로필에 레코드를 연결하는 속성입니다. 데이터 세트에 대한 기본 ID 필드는 데이터 세트가 기반으로 하는 스키마에 의해 정의됩니다. 이 열에서 소비자의 기본 ID에 대한 유형(또는 네임스페이스)을 제공해야 합니다(예: ) `email` 이메일 주소 및 `ecid` Experience Cloud ID용. 자세한 내용은 데이터 위생 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="ID 값"
>abstract="이 열에서 소비자의 기본 ID에 대한 값을 제공해야 합니다. 이 값은 왼쪽 열에 제공된 ID 유형과 일치해야 합니다. 기본 ID 유형이 `email`: 값은 소비자의 이메일 주소여야 합니다. 자세한 내용은 데이터 위생 UI 안내서를 참조하십시오."

소비자 데이터를 삭제할 때 시스템에서 삭제할 레코드를 결정할 수 있도록 ID 정보를 제공해야 합니다. Platform의 모든 데이터 세트에 대해 레코드는 **기본 ID** 데이터 집합 스키마에 의해 정의된 필드입니다.

Platform의 모든 ID 필드와 마찬가지로 기본 ID는 다음 두 가지 항목으로 구성됩니다. a **유형** (경우에 따라 id 네임스페이스라고도 함) 및 **value**. ID 유형은 필드가 소비자를 식별하는 방법에 대한 컨텍스트(예: 이메일 주소)를 제공하며 값은 해당 유형에 대한 소비자의 특정 ID를 나타냅니다(예: `jdoe@example.com` 대상 `email` id 유형).  ID로 사용되는 일반적인 필드에는 계정 정보, 장치 ID 및 쿠키 ID가 포함됩니다.

>[!TIP]
>
>특정 데이터 세트에 대한 기본 ID를 모를 경우 Platform UI에서 찾을 수 있습니다. 에서 **[!UICONTROL 데이터 세트]** 작업 영역의 목록에서 해당 데이터 세트를 선택합니다. 데이터 세트에 대한 세부 사항 페이지에서 오른쪽 레일에 있는 데이터 세트의 스키마 이름 위로 마우스 커서를 이동합니다. 기본 ID가 스키마 이름 및 설명과 함께 표시됩니다.
>
>![UI에 강조 표시된 데이터 세트의 기본 ID를 보여주는 이미지](../images/ui/delete-consumer/dataset-primary-identity.png)

데이터 세트에 기본 ID가 하나만 있을 수 있으므로 단일 데이터 세트에서 소비자 레코드를 삭제하는 경우, 제공하는 모든 ID의 유형이 같아야 합니다. 모든 데이터 세트에서 삭제하는 경우 서로 다른 데이터 세트에 서로 다른 기본 ID가 있을 수 있으므로 여러 ID 유형을 포함할 수 있습니다.

소비자 레코드를 삭제할 때 소비자 ID를 제공하는 두 가지 옵션이 있습니다.

* [JSON 파일 업로드](#upload-json)
* [ID 값을 수동으로 입력](#manual-identity)

### JSON 파일 업로드 {#upload-json}

JSON 파일을 업로드하려면 파일을 제공 영역으로 끌어다 놓거나 을 선택할 수 있습니다 **[!UICONTROL 파일 선택]** 로컬 디렉토리에서 을(를) 찾아 선택합니다.

![UI에서 JSON을 업로드하는 방법을 보여주는 이미지](../images/ui/delete-consumer/upload-json.png)

JSON 파일은 개체 배열로 포맷해야 하며 각 개체는 소비자 ID를 나타냅니다.

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
| `namespaceCode` | ID 유형입니다. |
| `value` | 유형으로 나타내는 소비자의 ID입니다. |

파일이 업로드되면 계속 [요청 제출](#submit).

### 수동으로 ID 입력 {#manual-identity}

ID를 수동으로 입력하려면 **[!UICONTROL ID 추가]**.

![이미지를 보여주는 이미지 [!UICONTROL ID 추가] 선택한 단추](../images/ui/delete-consumer/add-identity.png)

한 번에 하나씩 소비자 ID를 입력할 수 있는 컨트롤이 나타납니다. 아래 **[!UICONTROL 기본 ID]**&#x200B;드롭다운 메뉴를 사용하여 id 유형을 선택합니다. 아래 **[!UICONTROL ID 값]**&#x200B;는 소비자에 대한 기본 id 값을 제공합니다.

![수동으로 추가한 ID 필드를 보여주는 이미지](../images/ui/delete-consumer/identity-added.png)

ID를 더 추가하려면 더하기 아이콘(![더하기 아이콘 이미지](../images/ui/delete-consumer/plus-icon.png)) 내의 아무 곳에나 삽입할 수 있습니다. **[!UICONTROL ID 추가]**.

![요청에 ID를 더 추가하는 방법을 보여주는 이미지](../images/ui/delete-consumer/more-identities.png)

## 요청 제출(#submit)

요청에 ID를 추가했으면 아래의 **[!UICONTROL 요청 설정]**&#x200B;을(를) 선택하기 전에 요청에 대한 이름과 선택적 설명을 제공합니다 **[!UICONTROL 제출]**.

![이미지를 보여주는 이미지 [!UICONTROL 제출] 선택한 단추](../images/ui/delete-consumer/submit.png)

삭제할 데이터의 ID 목록을 확인하는 메시지가 표시됩니다. 선택 **[!UICONTROL 제출]** 을 클릭하여 선택 항목을 확인합니다.

![확인 대화 상자를 보여주는 이미지](../images/ui/delete-consumer/confirm-request.png)

요청이 제출되면 작업 순서가 만들어지고 다음에 나타납니다 [!UICONTROL 소비자] 의 탭 [!UICONTROL 데이터 위생] 작업 공간. 여기에서 요청을 처리할 때 작업 주문의 상태를 모니터링할 수 있습니다.

>[!NOTE]
>
>의 개요 섹션을 참조하십시오. [타임라인 및 투명도](../home.md#consumer-delete-transparency) 소비자 삭제를 실행한 후 처리하는 방법에 대한 자세한 내용은 다음을 참조하십시오.

## 다음 단계

이 문서에서는 Experience Platform UI에서 소비자 레코드를 삭제하는 방법에 대해 다룹니다. UI에서 기타 데이터 위생 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 위생 UI 개요](./overview.md).

데이터 위생 API를 사용하여 소비자 레코드를 삭제하는 방법에 대해 알아보려면 [work order endpoint 안내서](../api/workorder.md).
