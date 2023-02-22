---
title: UI에서 XDM 필드 사용 안 함
description: Experience Platform 내에서 스키마 편집기를 사용하여 XDM(Experience Data Model) 필드를 사용하지 않는 방법을 알아봅니다.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# UI에서 XDM 필드 사용 안 함

XDM(Experience Data Model)은 데이터를 처리한 후 스키마 필드를 사용하지 않음으로써 비즈니스 요구 사항이 변경되므로 데이터 모델을 관리할 수 있는 유연성을 제공합니다. 원하지 않는 필드는 UI 보기에서 제거하고 다운스트림 UI에서 숨기기 위해 더 이상 사용되지 않을 수 있습니다. 스키마 편집기의 확인란을 통해 더 이상 사용되지 않는 필드를 표시할 수 있으며 필요한 경우 해당 필드를 더 이상 사용하지 않을 수도 있습니다.

기본적으로 더 이상 사용되지 않는 필드가 UI에서 숨겨지므로 스키마 편집기에서 스키마를 간소화하고 세그먼트 빌더, 여정 디자이너 등과 같은 다운스트림 종속성에 원치 않는 필드가 추가되지 않습니다. 필드 사용 중단도 이전 버전과 호환됩니다. 더 이상 사용되지 않는 필드(예: 세그먼트 및 쿼리)를 사용하는 다른 시스템은 의도한 대로 계속 평가됩니다. 더 이상 사용되지 않는 필드를 기존 세그먼트에서 사용하는 경우 정상적으로 처리됩니다. 즉, 필드가 세그먼트 빌더 캔버스에 예상대로 표시되거나 더 이상 사용되지 않는 필드에서 사용할 수 있는 모든 데이터를 기반으로 평가됩니다. 기존 데이터 흐름에 부정적인 영향을 주지 않는 끊김 없는 변경 사항입니다.

>[!NOTE]
>
>데이터를 스키마에 수집하기 전에 불필요한 필드 그룹을 제거할 수 있습니다. 다음 문서를 참조하십시오. [스키마에서 필드 그룹을 제거하는 방법](../ui/resources/schemas.md#remove-fields) 추가 정보.

데이터를 스키마에 수집하면 변경 작업을 수행하지 않고 더 이상 스키마에서 필드를 제거할 수 없습니다. 이 경우 [스키마 편집기](./create-schema-ui.md) 또는 [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

이 문서에서는 Experience Platform 사용자 인터페이스에서 스키마 편집기를 사용하여 다양한 XDM 리소스에 대한 필드를 사용하지 않는 방법을 설명합니다. API를 사용하여 XDM 필드를 사용하지 않는 방법에 대한 단계는 [스키마 레지스트리 API를 사용하여 XDM 필드 사용 안 함](./field-deprecation-api.md).

## 필드 사용 안 함 {#deprecate}

사용자 지정 필드를 사용하지 않으려면 편집할 스키마의 스키마 편집기로 이동합니다. 사용 중단하려는 필드를 [!UICONTROL 구조] 캔버스의 섹션, 그 다음에 **[!UICONTROL 사용 안 함]** 에서 [!UICONTROL 필드 속성].

![필드가 선택되어 있고 사용 중단이 강조 표시된 스키마 편집기.](../images/tutorials/field-deprecation/deprecate-single-field.png)

선택 사항을 확인하고 필드가 통합 스키마의 UI 보기에서 제거되고 다운스트림 UI에서 숨겨짐을 알리는 대화 상자가 나타납니다. 작업을 완료하려면 **[!UICONTROL 확인]**.

![확인 이 강조 표시된 사용 중단 필드 대화 상자](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

이제 필드가 UI 보기에서 제거됩니다.

>[!NOTE]
>
>사용 중단되면, 세그먼테이션 대시보드, Customer Journey Analytics 및 Adobe Journey Optimizer과 같은 다운스트림 UI가 더 이상 사용되지 않는 필드를 워크플로우의 일부로 표시하지 않습니다. 그러나 다운스트림 UI에는 필요한 경우 더 이상 사용되지 않는 필드를 표시하고 더 이상 사용되지 않는 필드를 정상적으로 처리하는 옵션이 있습니다. 자세한 내용은 해당 설명서 를 참조하십시오. 더 이상 사용되지 않는 필드를 사용하는 쿼리 및 세그먼트는 예상대로 계속 실행됩니다.

## 사용되지 않는 필드 표시 {#show-deprecated}

이전에 더 이상 사용되지 않는 필드를 보려면 스키마 편집기에서 관련 스키마로 이동합니다. 을(를) 선택합니다 **[!UICONTROL 사용되지 않는 필드 표시]** 확인란 [!UICONTROL 조성물] 캔버스의 섹션.

이제 사용되지 않는 필드가 UI 보기에 표시됩니다. 선택 **[!UICONTROL 저장]** 설정을 확인합니다.

![필드를 선택한 스키마 편집기, 사용되지 않는 필드 표시 및 강조 표시된 저장](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## 필드 사용 안 함 {#undeprecate-fields}

더 이상 사용되지 않는 필드를 취소하려면 먼저 [사용되지 않는 필드 표시](#show-deprecated) 위에 설명된 대로, 편집기의 [!UICONTROL 구조] 섹션을 참조하십시오. 다음 을 선택합니다. **[!UICONTROL 불사용]** 에서 [!UICONTROL 필드 속성] 사이드바 뒤에 **[!UICONTROL 저장]**.

![더 이상 사용되지 않는 필드, 더 이상 사용되지 않음 및 저장 이 강조 표시된 스키마 편집기.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

다음 [!UICONTROL 필드 사용 안 함] 대화 상자가 나타납니다. 변경 사항을 확인하려면 **[!UICONTROL 확인]**.

![다음 [!UICONTROL 필드 사용 안 함] 확인(Confirm)이 강조 표시된 대화 상자](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

이제 필드가 UI 보기 및 다운스트림 UI에 표준으로 표시됩니다. 다시 말하지만, 이제 필드를 사용하지 않는 옵션이 있습니다.

## 다음 단계

이 문서에서는 스키마 편집기 UI를 사용하여 XDM 필드를 사용하지 않는 방법에 대해 설명합니다. 사용자 지정 리소스에 대한 필드 구성에 대한 자세한 내용은 [api에서 XDM 필드 정의](./custom-fields-api.md). 설명자 관리에 대한 자세한 내용은 [엔드포인트 가이드](../api/descriptors.md).
