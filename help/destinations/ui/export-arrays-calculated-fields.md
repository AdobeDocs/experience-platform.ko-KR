---
title: (Beta) 계산된 필드를 사용하여 플랫 스키마 파일에서 배열 내보내기
type: Tutorial
description: 계산된 필드를 사용하여 플랫 스키마 파일의 배열을 Real-Time CDP에서 클라우드 스토리지 대상으로 내보내는 방법에 대해 알아봅니다.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 5%

---

# (Beta) 계산된 필드를 사용하여 플랫 스키마 파일에서 배열 내보내기 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) 배열 내보내기 지원"
>abstract="**계산된 필드 추가** 제어를 사용하여 정수, 문자열 또는 부울 값의 간단한 배열을 Experience Platform에서 원하는 클라우드 스토리지 대상으로 내보냅니다. 일부 제한 사항이 적용됩니다. 광범위한 예제와 지원 기능에 대한 설명서를 확인하시기 바랍니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=ko#examples" text="예시"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=ko#known-limitations" text="알려진 제한 사항"

>[!AVAILABILITY]
>
>* 계산된 필드를 통해 배열을 내보내는 기능은 현재 Beta에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

플랫 스키마 파일의 Real-Time CDP에서 [클라우드 저장소 대상](/help/destinations/catalog/cloud-storage/overview.md)(으)로 계산된 필드를 통해 배열을 내보내는 방법에 대해 알아봅니다. 이 기능을 통해 활성화되는 사용 사례를 이해하려면 이 문서 를 참조하십시오.

계산된 필드에 대한 광범위한 정보(이것이 무엇이며 왜 중요한지)를 얻을 수 있습니다. 데이터 준비의 계산된 필드에 대한 소개와 사용 가능한 모든 함수에 대한 자세한 내용은 아래 링크된 페이지를 참조하십시오.

* [UI 안내서 및 개요](/help/data-prep/ui/mapping.md#calculated-fields)
* [데이터 준비 기능](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Platform의 배열 및 기타 개체 유형 {#arrays-strings-other-objects}

Experience Platform에서 [XDM 스키마](/help/xdm/home.md)를 사용하여 다른 필드 유형을 관리할 수 있습니다. 이전에는 Experience Platform에서 벗어난 문자열과 같은 간단한 키-값 쌍 유형 필드를 원하는 대상으로 내보낼 수 있었습니다. 이전에 내보내기에 지원되는 이러한 필드의 예는 `personalEmail.address`:`johndoe@acme.org`입니다.

Experience Platform의 다른 필드 유형에는 배열 필드가 포함됩니다. [Experience Platform UI에서 배열 필드 관리](/help/xdm/ui/fields/array.md)에 대해 자세히 알아보십시오. 이전에 지원되는 필드 형식 외에도 이제 `organizations:[marketing, sales, engineering]`과(와) 같은 배열 개체를 내보낼 수 있습니다. 다양한 함수를 사용하여 배열 요소에 액세스하고 배열 요소를 문자열에 조인하는 방법 등에 대한 자세한 내용은 아래 [광범위한 예](#examples)를 참조하십시오.

## 알려진 제한 사항 {#known-limitations}

이 기능의 베타 릴리스에 대해 다음과 같은 알려진 제한 사항을 참고하십시오.

* 계층 구조 스키마가 있는 JSON 또는 Parquet 파일로 내보내기는 현재 지원되지 않습니다. 배열을 플랫 스키마 CSV, JSON 및 Parquet 파일로만 내보낼 수 있습니다.
* 현재 *단순 배열(또는 기본 값 배열)만 클라우드 저장소 대상으로 내보낼 수 있습니다*. 즉, 문자열, int 또는 부울 값을 포함하는 배열 개체를 내보낼 수 있습니다. 맵이나 맵 또는 개체 배열은 내보낼 수 없습니다. 계산된 필드 모달 창에는 내보낼 수 있는 배열만 표시됩니다.

## 전제 조건 {#prerequisites}

원하는 클라우드 저장소 대상에 [연결](/help/destinations/ui/connect-destination.md)하고, 클라우드 저장소 대상에 대한 [활성화 단계](/help/destinations/ui/activate-batch-profile-destinations.md)를 진행하고 [매핑](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 단계로 이동하십시오.

## 계산된 필드를 내보내는 방법 {#how-to-export-calculated-fields}

클라우드 저장소 대상에 대한 활성화 워크플로의 매핑 단계에서 **[!UICONTROL (Beta) 계산된 필드 추가]**&#x200B;를 선택합니다.

![일괄 활성화 워크플로의 매핑 단계에서 강조 표시된 계산된 필드를 추가합니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

이렇게 하면 Experience Platform 외부에서 속성을 내보내는 데 사용할 수 있는 속성을 선택할 수 있는 모달 창이 열립니다.

>[!IMPORTANT]
>
>XDM 스키마의 일부 필드만 **[!UICONTROL 필드]** 보기에서 사용할 수 있습니다. 문자열 값과 문자열, int 및 부울 값의 배열을 볼 수 있습니다. 예를 들어 `segmentMembership` 배열에는 다른 배열 값이 포함되어 있으므로 표시되지 않습니다.

![아직 함수가 선택되지 않은 계산된 필드 기능의 모달 창.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

예를 들어 아래 표시된 대로 `loyaltyID` 필드에서 `join` 함수를 사용하여 충성도 ID 배열을 CSV 파일에서 밑줄이 연결된 문자열로 내보냅니다. [이 예제와 다른 예제에 대한 자세한 내용은 아래에서 ](#join-function-export-arrays)을(를) 참조하십시오.

![조인 함수가 선택된 계산된 필드 기능의 모달 창](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

계산된 필드를 유지하고 매핑 단계로 돌아가려면 **[!UICONTROL 저장]**&#x200B;을(를) 선택하십시오.

![조인 함수를 선택하고 Save 컨트롤이 강조 표시된 계산된 필드 기능의 모달 창](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

워크플로우의 매핑 단계로 돌아가서 내보낸 파일의 이 필드에 사용할 열 머리글 값으로 **[!UICONTROL 대상 필드]**&#x200B;을(를) 채웁니다.

대상 필드가 강조 표시된 매핑 단계 ![1}](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![대상 필드 선택](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

준비가 되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 활성화 워크플로의 다음 단계로 진행합니다.

대상 필드가 강조 표시되고 대상 값이 채워진 ![매핑 단계.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 지원되는 함수 {#supported-functions}

파일 기반 대상으로 데이터를 활성화할 때 문서화된 모든 [데이터 준비 기능](/help/data-prep/functions.md)이 지원됩니다.

그러나 현재 다음 기능에 대해서는 계산된 필드의 베타 릴리스와 대상에 대한 어레이 지원에서만 광범위한 사용 사례 설명 및 샘플 출력 정보가 제공됩니다.

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

위에 나열된 함수 중 일부는 아래 섹션의 예제 및 추가 정보를 참조하십시오. 나열된 나머지 함수는 데이터 준비 섹션의 [일반 함수 설명서](/help/data-prep/functions.md)를 참조하십시오.

### 배열을 내보내는 `join` 함수 {#join-function-export-arrays}

`join` 함수를 사용하여 `_` 또는 `|`과 같은 원하는 구분 기호를 사용하여 배열의 요소를 문자열로 연결합니다.

예를 들어 `join('_',loyalty.loyaltyID)` 구문을 사용하여 매핑 스크린샷에 표시된 대로 아래의 다음 XDM 필드를 결합할 수 있습니다.

* `"organizations": ["Marketing","Sales,"Finance"]` 배열
* `person.name.firstName` 문자열
* `person.name.lastName` 문자열
* `personalEmail.address` 문자열

![조인 함수를 포함하는 매핑 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

이 경우 출력 파일은 다음과 같습니다. 배열의 세 요소가 `_` 문자를 사용하여 단일 문자열로 연결되는 방식을 확인합니다.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
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

`add_to_array` 함수를 사용하여 내보낸 배열에 요소를 추가합니다. 이 함수를 위에서 설명한 `join` 함수와 결합할 수 있습니다.

위에서 `organizations` 배열 개체를 계속 사용하면 `source: join('_', add_to_array(organizations,"2023"))`과(와) 같은 함수를 작성하여 개인이 2023년에 멤버로 속한 조직을 반환할 수 있습니다.

![add_to_array 함수를 포함하는 매핑 예](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

이 경우 출력 파일은 다음과 같습니다. 배열의 세 요소가 `_` 문자를 사용하여 단일 문자열로 연결되고 문자열 끝에 2023도 추가되는 방식을 확인합니다.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

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

### 해시 함수 {#hashing-functions}

배열이나 배열에서 요소를 내보내는 특정 함수 외에도 해시 함수를 사용하여 내보낸 파일의 속성을 해시할 수 있습니다. 예를 들어 속성에 개인 식별 가능한 정보가 있는 경우 내보낼 때 이러한 필드를 해시할 수 있습니다.

`md5(personalEmail.address)`과 같은 문자열 값을 직접 해시할 수 있습니다. 원할 경우 배열의 요소가 문자열이라고 가정하여 배열 필드의 개별 요소를 해시할 수도 있습니다. 예: `md5(purchaseTime[0])`

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