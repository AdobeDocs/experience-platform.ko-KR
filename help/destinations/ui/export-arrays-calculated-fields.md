---
title: 계산된 필드를 사용하여 배열을 문자열로 내보내기
type: Tutorial
description: 계산된 필드를 사용하여 배열을 Real-Time CDP에서 클라우드 스토리지 대상으로 문자열로 내보내는 방법을 알아봅니다.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 849d42e36921e60b6ac3a5e89336b954e64a35d7
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# 계산된 필드를 사용하여 배열을 문자열로 내보내기{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="어레이 내보내기 지원"
>abstract="<p>**계산된 필드 추가** 컨트롤을 사용하여 int, 문자열, 부울 및 개체 값의 배열을 Experience Platform에서 원하는 클라우드 저장소 대상으로 내보냅니다.</p><p> 배열은 `array_to_string` 함수를 사용하여 문자열로 내보내야 합니다. 이 설명서에서 다양한 예제 및 지원되는 함수를 확인하십시오.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="예시"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="알려진 제한 사항"

>[!AVAILABILITY]
>
>* 계산된 필드를 통해 배열을 내보내는 기능은 일반적으로 사용할 수 있습니다.

계산된 필드를 통해 배열을 Real-Time CDP에서 [클라우드 저장소 대상](/help/destinations/catalog/cloud-storage/overview.md)으로 문자열로 내보내는 방법에 대해 알아봅니다. 이 기능을 통해 활성화되는 사용 사례를 이해하려면 이 문서 를 참조하십시오.

계산된 필드에 대한 광범위한 정보(이것이 무엇이며 왜 중요한지)를 얻을 수 있습니다. 데이터 준비의 계산된 필드에 대한 소개와 사용 가능한 모든 함수에 대한 자세한 내용은 아래 링크된 페이지를 참조하십시오.

* [UI 안내서 및 개요](/help/data-prep/ui/mapping.md#calculated-fields)
* [데이터 준비 기능](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Platform의 배열 및 기타 개체 유형 {#arrays-strings-other-objects}

Experience Platform에서 [XDM 스키마](/help/xdm/home.md)를 사용하여 다른 필드 유형을 관리할 수 있습니다. 배열 내보내기에 대한 지원이 추가되기 전에 Experience Platform 문자열과 같은 간단한 키-값 쌍 유형 필드를 원하는 대상으로 내보낼 수 있습니다. 이전에 내보내기에 지원되는 이러한 필드의 예는 `personalEmail.address`:`johndoe@acme.org`입니다.

Experience Platform의 다른 필드 유형에는 배열 필드가 포함됩니다. [Experience Platform UI에서 배열 필드 관리](/help/xdm/ui/fields/array.md)에 대해 자세히 알아보십시오. 이전에 지원된 필드 형식 외에도 이제 `array_to_string` 함수를 사용하여 문자열로 연결된 아래 예제와 같은 배열 개체를 내보낼 수 있습니다.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

다양한 함수를 사용하여 배열 요소에 액세스하고, 배열을 변환 및 필터링하고, 배열 요소를 문자열로 결합하는 방법 등에 대한 자세한 내용은 아래 [광범위한 예제](#examples)를 참조하십시오.

## 알려진 제한 사항 {#known-limitations}

현재 이 기능에 적용되는 알려진 다음 제한 사항을 참고하십시오.

* 계층 구조 스키마 *을(를) 사용하여 JSON 또는 Parquet 파일*&#x200B;로 내보내기는 현재 지원되지 않습니다. `array_to_string` 함수를 사용하여 배열을 CSV, JSON 및 Parquet 파일 *만 문자열로* 내보낼 수 있습니다.

## 전제 조건 {#prerequisites}

원하는 클라우드 저장소 대상에 [연결](/help/destinations/ui/connect-destination.md)하고, 클라우드 저장소 대상에 대한 [활성화 단계](/help/destinations/ui/activate-batch-profile-destinations.md)를 진행하고 [매핑](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 단계로 이동하십시오.

## 계산된 필드를 내보내는 방법 {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="계층적 출력 스키마 활성화"
>abstract="배열과 같은 계층 구조를 내보내려면 켜십시오."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="비활성화된 계산된 필드 추가"
>abstract="대상에 연결할 때 플랫 구조를 내보내도록 선택했으므로 이 컨트롤이 비활성화됩니다."

클라우드 저장소 대상에 대한 활성화 워크플로의 매핑 단계에서 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택합니다.

![일괄 활성화 워크플로의 매핑 단계에서 강조 표시된 계산된 필드를 추가합니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Experience Platform 외부에서 속성을 내보낼 함수와 필드를 선택할 수 있는 모달 창이 열립니다.

![아직 함수가 선택되지 않은 계산된 필드 기능의 모달 창.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

예를 들어 아래 표시된 대로 `organizations` 필드에서 `array_to_string` 함수를 사용하여 조직 배열을 CSV 파일의 문자열로 내보냅니다. [이 예제와 다른 예제에 대한 자세한 내용은 아래에서 ](#array-to-string-function-export-arrays)을(를) 참조하십시오.

![배열-문자열 함수가 선택된 계산된 필드 기능의 모달 창입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

계산된 필드를 유지하고 매핑 단계로 돌아가려면 **[!UICONTROL 저장]**&#x200B;을(를) 선택하십시오.

![Array-to-string 함수가 선택되고 Save 컨트롤이 강조 표시된 계산된 필드 기능의 모달 창.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

워크플로우의 매핑 단계로 돌아가서 내보낸 파일의 이 필드에 사용할 열 머리글 값으로 **[!UICONTROL 대상 필드]**&#x200B;을(를) 채웁니다.

대상 필드가 강조 표시된 매핑 단계 ![1}](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![대상 필드 선택](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

준비가 되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 활성화 워크플로의 다음 단계로 진행합니다.

대상 필드가 강조 표시되고 대상 값이 채워진 ![매핑 단계.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 지원되는 함수 샘플을 사용하여 배열을 내보냅니다. {#supported-functions}

파일 기반 대상으로 데이터를 활성화할 때 문서화된 모든 [데이터 준비 기능](/help/data-prep/functions.md)이 지원됩니다.

어레이 내보내기 처리와 관련된 아래 기능은 예제와 함께 설명되어 있습니다.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## 배열을 내보내는 데 사용되는 함수의 예 {#examples}

위에 나열된 함수 중 일부는 아래 섹션의 예제 및 추가 정보를 참조하십시오. 나열된 나머지 함수는 데이터 준비 섹션의 [일반 함수 설명서](/help/data-prep/functions.md)를 참조하십시오.

### 배열을 내보내는 `array_to_string` 함수 {#array-to-string-function-export-arrays}

`array_to_string` 함수를 사용하여 `_` 또는 `|`과 같은 원하는 구분 기호를 사용하여 배열의 요소를 문자열로 연결합니다.

예를 들어 `array_to_string('_',organizations)` 구문을 사용하여 매핑 스크린샷에 표시된 대로 아래의 다음 XDM 필드를 결합할 수 있습니다.

* `organizations` 배열
* `person.name.firstName` 문자열
* `person.name.lastName` 문자열
* `personalEmail.address` 문자열

![array_to_string 함수를 포함하는 매핑 예](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

이 경우 출력 파일은 다음과 같습니다. 배열의 요소가 `_` 문자를 사용하여 단일 문자열로 연결되는 방식을 확인합니다.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### 필터링된 배열을 내보내는 `filterArray` 함수

`filterArray` 함수를 사용하여 내보낸 배열의 요소를 필터링합니다. 이 함수를 위에서 설명한 `array_to_string` 함수와 결합할 수 있습니다.

위에서 `organizations` 배열 개체를 계속 사용하면 `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`과(와) 같은 함수를 작성하여 2021년 또는 그 이상 최근 연도의 `founded` 값을 가진 조직을 반환할 수 있습니다.

![filterArray 함수의 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

이 경우 출력 파일은 다음과 같습니다. 기준을 충족하는 배열의 두 요소가 `_` 문자를 사용하여 단일 문자열로 연결되는 방식을 확인합니다.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### 변환된 배열을 내보내는 `transformArray` 함수

`transformArray` 함수를 사용하여 내보낸 배열의 요소를 변환합니다. 이 함수를 위에서 설명한 `array_to_string` 함수와 결합할 수 있습니다.

위에서 `organizations` 배열 개체를 계속 사용하면 `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`과(와) 같은 함수를 작성하여 모든 대문자로 변환된 조직의 이름을 반환할 수 있습니다.

![transformArray 함수의 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

이 경우 출력 파일은 다음과 같습니다. 배열의 세 요소가 `_` 문자를 사용하여 어떻게 변환되고 단일 문자열로 연결되는지 확인하십시오.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### 배열을 내보내는 `iif` 함수 {#iif-function-export-arrays}

특정 조건에서 배열의 요소를 내보내려면 `iif` 함수를 사용하십시오. 예를 들어 위에서 `organizations` 배열 개체를 계속 사용하면 `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`과(와) 같은 간단한 조건부 함수를 작성할 수 있습니다.

![iif 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

이 경우 출력 파일은 다음과 같습니다. 이 경우 배열의 첫 번째 요소는 마케팅이므로 개인은 마케팅 부서의 구성원입니다.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### 배열을 내보내는 `add_to_array` 함수 {#add-to-array-function-export-arrays}

`add_to_array` 함수를 사용하여 내보낸 배열에 요소를 추가합니다. 이 함수를 위에서 설명한 `array_to_string` 함수와 결합할 수 있습니다.

위에서 `organizations` 배열 개체를 계속 사용하면 `source: array_to_string('_', add_to_array(organizations,"2023"))`과(와) 같은 함수를 작성하여 개인이 2023년에 멤버로 속한 조직을 반환할 수 있습니다.

![add_to_array 함수를 포함하는 매핑 예](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

이 경우 출력 파일은 다음과 같습니다. 배열의 세 요소가 `_` 문자를 사용하여 단일 문자열로 연결되고 문자열 끝에 2023도 추가되는 방식을 확인합니다.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### 병합된 배열을 내보내는 `flattenArray` 함수

내보낸 다차원 배열을 병합하려면 `flattenArray` 함수를 사용하십시오. 이 함수를 위에서 설명한 `array_to_string` 함수와 결합할 수 있습니다.

위에서 `organizations` 배열 개체를 계속 사용하면 `array_to_string('_', flattenArray(organizations))`과(와) 같은 함수를 작성할 수 있습니다. `array_to_string` 함수는 기본적으로 입력 배열을 문자열로 병합합니다.

결과 출력은 위에서 설명한 `array_to_string` 함수와 동일합니다.

### 배열을 내보내는 `coalesce` 함수 {#coalesce-function-export-arrays}

`coalesce` 함수를 사용하여 배열의 null이 아닌 첫 번째 요소에 액세스하고 문자열로 내보냅니다.

예를 들어 `coalesce(subscriptions.hasPromotion)` 구문을 사용하여 아래 매핑 스크린샷에 표시된 대로 다음 XDM 필드를 결합하여 배열에서 `false`의 첫 번째 `true` 값을 반환할 수 있습니다.

* `"subscriptions.hasPromotion": [null, true, null, false, true]` 배열
* `person.name.firstName` 문자열
* `person.name.lastName` 문자열
* `personalEmail.address` 문자열

![병합 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

이 경우 출력 파일은 다음과 같습니다. 배열에서 null이 아닌 첫 번째 `true` 값을 파일에서 내보내는 방식을 확인합니다.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### 배열을 내보내는 `size_of` 함수 {#sizeof-function-export-arrays}

배열에 있는 요소의 수를 나타내려면 `size_of` 함수를 사용하십시오. 예를 들어, 타임스탬프가 여러 개인 `purchaseTime` 배열 개체가 있는 경우 `size_of` 함수를 사용하여 개인이 얼마나 많은 개별 구매를 했는지 나타낼 수 있습니다.

예를 들어 매핑 스크린샷에 표시된 대로 아래에 있는 다음 XDM 필드를 결합할 수 있습니다.

* 고객이 5개의 개별 구매 시간을 나타내는 `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` 배열
* `personalEmail.address` 문자열

![size_of 함수를 포함하는 매핑 예](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

이 경우 출력 파일은 다음과 같습니다. 두 번째 열은 고객이 별도로 구매한 횟수에 해당하는 배열의 요소 수를 어떻게 표시하는지 확인합니다.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 인덱스 기반 스토리지 액세스 {#index-based-array-access}

배열의 인덱스에 액세스하여 배열에서 단일 항목을 내보낼 수 있습니다. 예를 들어, `size_of` 함수에 대한 위의 예제와 유사하게 고객이 특정 제품을 처음 구매한 경우에만 액세스하고 내보내려고 하는 경우 `purchaseTime[0]`을(를) 사용하여 타임스탬프의 첫 번째 요소를 내보내고, `purchaseTime[1]`을(를) 사용하여 타임스탬프의 두 번째 요소를 내보내고, `purchaseTime[2]`을(를) 사용하여 타임스탬프의 세 번째 요소를 내보낼 수 있습니다.

![배열의 요소에 액세스하는 방법을 보여 주는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

이 경우 출력 파일은 아래와 같이 표시되며 고객이 처음 구매한 항목을 내보냅니다.

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### 배열을 내보내는 `first` 및 `last` 함수 {#first-and-last-functions-export-arrays}

`first` 및 `last` 함수를 사용하여 배열의 첫 번째 또는 마지막 요소를 내보냅니다. 예를 들어 이전 예제의 여러 타임스탬프가 있는 `purchaseTime` 배열 개체를 계속 사용하면 이러한 개체를 사용하여 한 사람이 만든 첫 번째 또는 마지막 구매 시간을 내보내는 함수에 사용할 수 있습니다.

![첫 번째 함수와 마지막 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

이 경우 출력 파일은 아래와 같이 표시되며 고객이 구매한 처음과 마지막 시간을 내보냅니다.

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->