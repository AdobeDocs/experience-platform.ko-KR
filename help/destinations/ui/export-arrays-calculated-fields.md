---
title: (Beta) 계산된 필드를 사용하여 플랫 스키마 파일로 배열을 내보냅니다
type: Tutorial
description: 계산된 필드를 사용하여 플랫 스키마 파일의 배열을 Real-Time CDP에서 클라우드 스토리지 대상으로 내보내는 방법에 대해 알아봅니다.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: b6bdfef8b9ac5ef03ea726d668477b8629b70b6c
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 5%

---

# (Beta) 계산된 필드를 사용하여 플랫 스키마 파일로 배열을 내보냅니다 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) 배열 내보내기 지원"
>abstract="**계산된 필드 추가** 제어를 사용하여 정수, 문자열 또는 부울 값의 간단한 배열을 Experience Platform에서 원하는 클라우드 스토리지 대상으로 내보냅니다. 일부 제한 사항이 적용됩니다. 광범위한 예제와 지원 기능에 대한 설명서를 확인하시기 바랍니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="예시"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="알려진 제한 사항"

>[!AVAILABILITY]
>
>* 계산된 필드를 통해 배열을 내보내는 기능은 현재 Beta 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

플랫 스키마 파일에서 Real-Time CDP의 계산된 필드를 통해 배열을 내보내는 방법에 대해 알아봅니다. [클라우드 스토리지 대상](/help/destinations/catalog/cloud-storage/overview.md). 이 기능을 통해 활성화되는 사용 사례를 이해하려면 이 문서 를 참조하십시오.

계산된 필드에 대한 광범위한 정보(이것이 무엇이며 왜 중요한지)를 얻을 수 있습니다. 데이터 준비의 계산된 필드에 대한 소개와 사용 가능한 모든 함수에 대한 자세한 내용은 아래 링크된 페이지를 참조하십시오.

* [UI 안내서 및 개요](/help/data-prep/ui/mapping.md#calculated-fields)
* [데이터 준비 기능](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>위에 나열된 모든 함수가 지원되는 것은 아닙니다. *필드를 클라우드 스토리지 대상으로 내보낼 때* 계산된 필드 기능 사용. 다음을 참조하십시오. [지원되는 함수 섹션](#supported-functions) 자세한 내용은 아래를 참조하십시오.

## Platform의 배열 및 기타 개체 유형 {#arrays-strings-other-objects}

Experience Platform에서 다음을 사용할 수 있습니다 [XDM 스키마](/help/xdm/home.md) 다른 필드 유형을 관리합니다. 이전에는 Experience Platform에서 벗어난 문자열과 같은 간단한 키-값 쌍 유형 필드를 원하는 대상으로 내보낼 수 있었습니다. 이전에 내보내기에 대해 지원되는 이러한 필드의 예는 다음과 같습니다. `personalEmail.address`:`johndoe@acme.org`.

Experience Platform의 다른 필드 유형에는 배열 필드가 포함됩니다. 자세한 내용 [Experience Platform UI에서 배열 필드 관리](/help/xdm/ui/fields/array.md). 이전에 지원되는 필드 유형 외에도 이제 다음과 같은 배열 개체를 내보낼 수 있습니다. `organizations:[marketing, sales, engineering]`. 아래 추가 참조 [광범위한 예](#examples) 다양한 함수를 사용하여 배열의 요소에 액세스하고 배열 요소를 문자열로 결합하는 방법 등에 대해 알아봅니다.

## 알려진 제한 사항 {#known-limitations}

이 기능의 베타 릴리스에 대해 다음과 같은 알려진 제한 사항을 참고하십시오.

* 계층 구조 스키마가 있는 JSON 또는 Parquet 파일로 내보내기는 현재 지원되지 않습니다. 배열을 플랫 스키마 CSV, JSON 및 Parquet 파일로만 내보낼 수 있습니다.
* 현재, *단순 배열(또는 기본 값 배열)만 클라우드 스토리지 대상으로 내보낼 수 있습니다.*. 즉, 문자열, int 또는 부울 값을 포함하는 배열 개체를 내보낼 수 있습니다. 맵이나 맵 또는 개체 배열은 내보낼 수 없습니다. 계산된 필드 모달 창에는 내보낼 수 있는 배열만 표시됩니다.

## 전제 조건 {#prerequisites}

[연결](/help/destinations/ui/connect-destination.md) 원하는 클라우드 스토리지 대상으로 이동하여 [클라우드 스토리지 대상에 대한 활성화 단계](/help/destinations/ui/activate-batch-profile-destinations.md) 및 로 이동 [매핑](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 단계.

## 계산된 필드를 내보내는 방법 {#how-to-export-calculated-fields}

클라우드 스토리지 대상에 대한 활성화 워크플로의 매핑 단계에서 다음을 선택합니다. **[!UICONTROL (Beta) 계산된 필드 추가]**.

![일괄 활성화 워크플로의 매핑 단계에서 강조 표시된 계산된 필드를 추가합니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

이렇게 하면 Experience Platform 외부에서 속성을 내보내는 데 사용할 수 있는 속성을 선택할 수 있는 모달 창이 열립니다.

>[!IMPORTANT]
>
>XDM 스키마의 일부 필드만 **[!UICONTROL 필드]** 보기. 문자열 값과 문자열, int 및 부울 값의 배열을 볼 수 있습니다. 예를 들어 `segmentMembership` 배열에는 다른 배열 값이 포함되어 있으므로 표시되지 않습니다.

![아직 함수가 선택되지 않은 계산된 필드 기능의 모달 창.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

예를 들어 `join` 에 대한 함수 `loyaltyID` 충성도 ID 배열을 CSV 파일에서 밑줄이 연결된 문자열로 내보내는 아래 표시된 필드. 보기 [이 예제와 다른 예제에 대한 자세한 내용은 아래에서 확인하십시오](#join-function-export-arrays).

![조인 함수가 선택된 계산된 필드 기능의 모달 창입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

선택 **[!UICONTROL 저장]** 계산된 필드를 유지하고 매핑 단계로 돌아갑니다.

![조인 함수가 선택되고 Save 컨트롤이 강조 표시된 계산된 필드 기능의 모달 창입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

워크플로우의 매핑 단계로 돌아가서 **[!UICONTROL 대상 필드]** (내보낸 파일의 이 필드에 사용할 열 머리글 값 포함)

![대상 필드가 강조 표시된 매핑 단계입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![대상 필드 2 선택](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

준비가 되면 다음을 선택합니다. **[!UICONTROL 다음]** 활성화 워크플로의 다음 단계로 진행합니다.

![대상 필드가 강조 표시되고 대상 값이 채워진 매핑 단계입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 지원되는 함수 {#supported-functions}

계산된 필드의 베타 릴리스 및 대상에 대한 배열 지원에서는 다음 함수만 지원됩니다.

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## 배열을 내보내는 데 사용되는 함수의 예 {#examples}

위에 나열된 함수 중 일부는 아래 섹션의 예제 및 추가 정보를 참조하십시오. 나열된 나머지 함수는 [데이터 준비 섹션의 일반 함수 설명서](/help/data-prep/functions.md).

### `join` 배열을 내보내는 함수 {#join-function-export-arrays}

사용 `join` 원하는 구분 기호(예: )를 사용하여 배열의 요소를 문자열로 연결하는 함수 `_` 또는 `|`.

예를 들어 를 사용하여 매핑 스크린샷에 표시된 대로 아래 XDM 필드를 결합할 수 있습니다. `join('_',loyalty.loyaltyID)` 구문:

* `"organizations": ["Marketing","Sales,"Finance"]` 배열
* `person.name.firstName` 문자열
* `person.name.lastName` 문자열
* `personalEmail.address` 문자열

![조인 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

이 경우 출력 파일은 다음과 같습니다. 를 사용하여 배열의 세 요소가 단일 문자열로 연결되는 방식을 확인합니다. `_` 문자.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` 배열을 내보내는 함수 {#iif-function-export-arrays}

사용 `iif` 특정 조건에서 배열의 요소를 내보내는 함수입니다. 예를 들어 을 계속 `organizations` 위에서 배열 개체를 만들면 다음과 같은 간단한 조건부 함수를 작성할 수 있습니다 `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![iif 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

이 경우 출력 파일은 다음과 같습니다. 이 경우 배열의 첫 번째 요소는 마케팅이므로 개인은 마케팅 부서의 구성원입니다.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` 배열을 내보내는 함수 {#add-to-array-function-export-arrays}

사용 `add_to_array` 내보낸 배열에 요소를 추가하는 함수입니다. 이 함수를 와 결합할 수 있습니다 `join` 위에서 추가로 설명한 함수.

을(를) 계속하는 중 `organizations` 위에서 배열 개체를 만들면 다음과 같은 함수를 작성할 수 있습니다. `source: join('_', add_to_array(organizations,"2023"))`를 반환하여 2023년에 개인이 멤버인 조직을 반환합니다.

![add_to_array 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

이 경우 출력 파일은 다음과 같습니다. 를 사용하여 배열의 세 요소가 단일 문자열로 연결되는 방식을 확인합니다. `_` 문자열 끝에 문자 및 2023도 추가됩니다.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` 배열을 내보내는 함수 {#coalesce-function-export-arrays}

사용 `coalesce` 배열의 null이 아닌 첫 번째 요소에 액세스하고 문자열로 내보내는 함수입니다.

예를 들어 를 사용하여 매핑 스크린샷에 표시된 대로 아래 XDM 필드를 결합할 수 있습니다. `coalesce(subscriptions.hasPromotion)` 첫 번째 `true` / `false` 배열의 값:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` 배열
* `person.name.firstName` 문자열
* `person.name.lastName` 문자열
* `personalEmail.address` 문자열

![결합 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

이 경우 출력 파일은 다음과 같습니다. null이 아닌 첫 번째 `true` 배열의 값을 파일로 내보냅니다.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` 배열을 내보내는 함수 {#sizeof-function-export-arrays}

사용 `size_of` 배열에 있는 요소의 수를 나타내는 함수입니다. 예를 들어 `purchaseTime` 여러 타임스탬프가 있는 배열 개체를 사용하면 `size_of` 개인이 몇 개의 개별 구매를 했는지 나타내는 함수입니다.

예를 들어 매핑 스크린샷에 표시된 대로 아래에 있는 다음 XDM 필드를 결합할 수 있습니다.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` 고객이 5개의 개별 구매 시간을 나타내는 스토리지 시스템
* `personalEmail.address` 문자열

![size_of 함수를 포함하는 매핑 예.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

이 경우 출력 파일은 다음과 같습니다. 두 번째 열은 고객이 별도로 구매한 횟수에 해당하는 배열의 요소 수를 어떻게 표시하는지 확인합니다.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 인덱스 기반 스토리지 액세스 {#index-based-array-access}

배열의 인덱스에 액세스하여 배열에서 단일 항목을 내보낼 수 있습니다. 예를 들어 의 위 예와 비슷합니다. `size_of` 기능을 사용하면 고객이 특정 제품을 처음 구매한 경우에만 액세스하고 내보내기를 하려는 경우 다음을 사용할 수 있습니다 `purchaseTime[0]` 타임스탬프의 첫 번째 요소를 내보내려면 `purchaseTime[1]` 타임스탬프의 두 번째 요소를 내보내려면 `purchaseTime[2]` 을 눌러 타임스탬프의 세 번째 요소를 내보내는 등의 작업을 수행합니다.

![배열의 요소에 액세스하는 방법을 보여 주는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

이 경우 출력 파일은 아래와 같이 표시되며 고객이 처음 구매한 항목을 내보냅니다.

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` 및 `last` 배열을 내보내는 함수 {#first-and-last-functions-export-arrays}

사용 `first` 및 `last` 배열에서 첫 번째 또는 마지막 요소를 내보내는 함수입니다. 예를 들어 을 계속 `purchaseTime` 이전 예제의 여러 타임스탬프가 있는 배열 개체를 사용하면 함수를 사용하여 한 사람이 만든 첫 번째 또는 마지막 구매 시간을 내보낼 수 있습니다.

![첫 번째 및 마지막 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

이 경우 출력 파일은 아래와 같이 표시되며 고객이 구매한 처음과 마지막 시간을 내보냅니다.

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### 해시 함수 {#hashing-functions}

배열이나 배열에서 요소를 내보내는 특정 함수 외에도 해시 함수를 사용하여 내보낸 파일의 속성을 해시할 수 있습니다. 예를 들어 속성에 개인 식별 가능한 정보가 있는 경우 내보낼 때 이러한 필드를 해시할 수 있습니다.

예를 들어 문자열 값을 직접 해시할 수 있습니다 `md5(personalEmail.address)`. 원하는 경우 다음과 같이 배열의 요소가 문자열이라고 가정하여 배열 필드의 개별 요소를 해시할 수도 있습니다. `md5(purchaseTime[0])`

지원되는 해시 함수는 다음과 같습니다.

| 함수 | 샘플 표현식 |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}