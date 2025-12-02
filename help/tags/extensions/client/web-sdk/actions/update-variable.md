---
title: 변수 업데이트
description: 변수 데이터 요소의 내용을 수정합니다.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 변수 업데이트

**[!UICONTROL Update variable]** 작업을 사용하면 [변수 데이터 요소](../data-element-types.md#variable)의 일부 또는 증분 변경을 수행할 수 있습니다. 이 작업을 사용하여 나중에 [[!UICONTROL Send event]](send-event.md) 작업에서 참조할 수 있는 개체를 만들 수 있습니다. 데이터 요소를 채우고 XDM 개체 내의 속성에 할당하는 것은 대부분의 사용 사례에 적합합니다. 이 작업을 사용하면 규칙 조건에 따라 속성을 조건부로 다른 데이터 요소로 설정할 수 있습니다.

이 작업을 사용하기 전에 변수 데이터 요소를 이미 만들어야 합니다. 수정할 변수 데이터 요소를 선택하면 이 작업에 대해 원하는 필드를 설정할 수 있는 편집기가 나타납니다.

![작업 구성 인터페이스 내에서 변수 업데이트 작업의 스크린샷](../assets/update-variable.png)

편집기에 사용된 XDM 스키마는 변수 데이터 요소 내에서 선택한 스키마와 일치합니다. 객체를 확장하고 원하는 등록 정보를 선택하여 객체의 등록 정보를 하나 이상 설정할 수 있습니다. 예를 들어 아래 스크린샷에서는 `producedBy` 속성이 데이터 요소 `%Produced by data element%`(으)로 설정되어 있습니다.

업데이트된 속성을 표시하는 작업 구성 인터페이스의 ![스크린샷](../assets/update-variable-set-property.png)

XDM 개체 대신 데이터 개체를 사용하는 변수 데이터 요소를 선택하는 경우 사용 가능한 필드는 데이터 요소를 구성할 때 선택한 제품에 따라 다릅니다. 예를 들어, Adobe Analytics, 필드를 포함하는 데이터 개체를 만드는 경우 이 UI에서 변수 데이터 요소를 선택하면 Adobe Analytics에 맞게 작성할 수 있는 필드가 제공됩니다.

![데이터 개체를 기반으로 변수 데이터 요소를 표시하는 작업 구성 인터페이스의 스크린샷](../assets/variable-data-element-data.png)
