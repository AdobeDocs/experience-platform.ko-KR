---
title: 계산된 필드를 사용하여 클라우드 스토리지 대상으로 내보낸 데이터에 대한 변환을 수행합니다.
type: Tutorial
description: 계산된 필드 기능을 사용하여 클라우드 스토리지 대상으로 내보낸 데이터에 대한 변환을 수행하는 방법을 이해합니다
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: 14c672ef57e0b0247020075552c782ed18db8484
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 8%

---

# 계산된 필드를 사용하여 클라우드 스토리지 대상으로 내보낸 데이터에 대한 변환을 수행합니다. {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="계산된 필드 추가"
>abstract="<p>**계산된 필드 추가** 컨트롤을 사용하여 클라우드 스토리지 대상으로 내보낸 데이터에 다양한 데이터 변환을 수행합니다. 예를 들어 데이터에 해싱을 적용하고 배열을 문자열로 연결하는 등의 작업이 가능합니다."

<!--

disable additional URLs for a while

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html?lang=ko#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html?lang=ko#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>클라우드 저장소 대상으로 내보낸 데이터에 대한 변환을 수행하는 기능은 일반적으로 [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md) 대상과 [Destination SDK](/help/destinations/destination-sdk/overview.md)을(를) 통해 작성된 사용자 지정 파트너 작성 클라우드 저장소 대상에서도 사용할 수 있습니다.

클라우드 스토리지 대상으로 내보낸 데이터에 대해 다양한 변환을 수행하려면 내보내기 워크플로우의 매핑 단계에서 계산된 필드 기능을 사용해야 합니다. 계산된 필드에 대한 자세한 내용은 아래 링크된 페이지를 참조하십시오. 이러한 페이지에는 데이터 준비의 계산된 필드에 대한 소개와 사용 가능한 모든 함수에 대한 추가 정보가 포함되어 있습니다.

* [UI 안내서 및 개요](/help/data-prep/ui/mapping.md#calculated-fields)
* [데이터 준비 기능](/help/data-prep/functions.md)

## 전제 조건 {#prerequisites}

데이터 변환에 계산된 필드를 사용하려면 다음을 수행하십시오.

1. 원하는 클라우드 저장소 대상에 [연결](/help/destinations/ui/connect-destination.md)합니다. 원하는 클라우드 대상에 연결할 때 **[!UICONTROL 배열, 맵, 개체 내보내기]** [옵션 해제](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle)를 전환하십시오.
2. 클라우드 저장소 대상에 대한 [활성화 단계](/help/destinations/ui/activate-batch-profile-destinations.md)를 진행하고 [매핑](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 단계로 이동하십시오.

## 계산된 필드로 작업하는 방법 {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="계층적 출력 스키마 활성화"
>abstract="배열, 맵 및 오브젝트를 JSON 또는 Parquet 파일로 내보낼 수 있도록 설정을 켜짐으로 토글합니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="계산된 필드 추가 비활성화됨"
>abstract="이 대상 연결을 설정할 때 **배열, 맵, 오브젝트 내보내기**&#x200B;를 *켜짐*&#x200B;으로 토글했기 때문에 이 제어가 비활성화됩니다. 계산된 필드와 내부에서 사용할 수 있는 함수를 사용하려면 **배열, 맵, 오브젝트 내보내기**&#x200B;를 *꺼짐*&#x200B;으로 토글하여 새 대상 연결을 설정합니다."

클라우드 저장소 대상에 대한 활성화 워크플로의 매핑 단계에서 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택합니다.

>[!TIP]
>
>**[!UICONTROL 배열, 맵 및 개체 내보내기]** 컨트롤이 해제되어 있는 대상 연결에 대해 **[!UICONTROL 계산된 필드 추가]** 컨트롤을 사용할 수 없습니다. [자세히 보기](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![일괄 활성화 워크플로의 매핑 단계에서 강조 표시된 계산된 필드를 추가합니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

이렇게 하면 함수와 필드를 선택하여 Experience Platform에서 속성을 내보낼 수 있는 모달 창이 열립니다.

![아직 함수가 선택되지 않은 계산된 필드 기능의 모달 창.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

예를 들어 아래 표시된 대로 `organizations` 필드에서 `array_to_string` 함수를 사용하여 조직 배열을 CSV 파일의 문자열로 내보냅니다. [이 예제와 다른 예제에 대한 자세한 내용은 아래에서 ](#array-to-string-function-export-arrays)을(를) 참조하십시오.

![배열-문자열 함수가 선택된 계산된 필드 기능의 모달 창입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

계산된 필드를 유지하고 매핑 단계로 돌아가려면 **[!UICONTROL 저장]**&#x200B;을(를) 선택하십시오.

![Array-to-string 함수가 선택되고 Save 컨트롤이 강조 표시된 계산된 필드 기능의 모달 창.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

워크플로우의 매핑 단계로 돌아가서 내보낸 파일의 이 필드에 사용할 열 머리글 값으로 **[!UICONTROL 대상 필드]**&#x200B;을(를) 채웁니다.

대상 필드가 강조 표시된 매핑 단계 ![1&rbrace;](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![대상 필드 선택](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

준비가 되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 활성화 워크플로의 다음 단계로 진행합니다.

대상 필드가 강조 표시되고 대상 값이 채워진 ![매핑 단계.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 데이터 변환을 수행하기 위해 지원되는 샘플 함수 {#supported-functions}

파일 기반 대상으로 데이터를 활성화할 때 문서화된 모든 [데이터 준비 기능](/help/data-prep/functions.md)이 지원됩니다.

배열의 내보내기 처리 또는 필드에 해싱 적용과 관련된 아래 함수가 예제와 함께 설명되어 있습니다.

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

## 데이터 변환을 수행하는 데 사용되는 함수 예제 {#examples}

위에 나열된 함수 중 일부는 아래 섹션의 예제 및 추가 정보를 참조하십시오. 나열된 나머지 함수는 데이터 준비 섹션의 [일반 함수 설명서](/help/data-prep/functions.md)를 참조하십시오.

### 배열을 내보내는 `array_to_string` 함수 {#array-to-string-function-export-arrays}

`array_to_string` 함수를 사용하여 `_` 또는 `|`과 같은 원하는 구분 기호를 사용하여 배열의 요소를 문자열로 연결합니다. 이 함수는 Experience Platform의 배열 요소를 CSV 파일로 내보내려는 경우에 유용합니다.

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

### 필터링된 배열을 내보내는 `filterArray` 함수 {#filter-array}

`filterArray` 함수를 사용하여 내보낸 배열의 요소를 필터링합니다. 이 함수를 위에서 설명한 `array_to_string` 함수와 결합할 수 있습니다.

위에서 `organizations` 배열 개체를 계속 사용하면 `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`과(와) 같은 함수를 작성할 수 있습니다. 그러면 2021년 또는 그 이상 최근 연도의 `founded` 값이 있는 조직이 반환됩니다.

![filterArray 함수의 예입니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

이 경우 출력 파일은 다음과 같습니다. 기준을 충족하는 배열의 두 요소가 `_` 문자를 사용하여 단일 문자열로 연결되는 방식을 확인합니다.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### 변환된 배열을 내보내는 `transformArray` 함수 {#transform-array}

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

### 병합된 배열을 내보내는 `flattenArray` 함수 {#flatten-array}

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

>[!IMPORTANT]
>
>이 페이지에 설명된 다른 함수와 달리 배열의 개별 요소를 내보내려면 *UI에서&#x200B;**[!UICONTROL 계산된 필드]**&#x200B;컨트롤을 사용할 필요가 없습니다*.

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

사용 가능한 다른 함수는 배열이나 배열에서 요소를 내보내는 데 한정됩니다. 해시 함수를 사용하여 내보낸 파일의 속성을 해시할 수 있습니다. 예를 들어 속성에 개인 식별 가능한 정보가 있는 경우 내보낼 때 이러한 필드를 해시할 수 있습니다.

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
