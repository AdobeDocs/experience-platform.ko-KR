---
keywords: 프로필 대상 활성화;대상 활성화;데이터 활성화 이메일 마케팅 대상 활성화 클라우드 스토리지 대상 활성화
title: 대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화
type: Tutorial
seo-title: 대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화
description: 세그먼트를 배치 프로필 기반 대상으로 보내 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
seo-description: 세그먼트를 배치 프로필 기반 대상으로 보내 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
source-git-commit: b1d9b03af1d5266a03d0f16c6a9803a08f19b7bd
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---


# 대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화

## 개요 {#overview}

이 문서에서는 클라우드 스토리지 및 이메일 마케팅 대상과 같은 Adobe Experience Platform 배치 프로필 기반 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로우를 설명합니다.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 [이(가) 대상](./connect-destination.md)에 연결되어 있어야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상을 선택합니다 {#select-destination}

1. **[!UICONTROL 연결 > 대상]**&#x200B;으로 이동하고 **[!UICONTROL 찾아보기]** 탭을 선택합니다.

   ![대상 찾아보기 탭](../assets/ui/activate-batch-profile-destinations/browse-tab.png)

1. 아래 그림과 같이 세그먼트를 활성화할 대상에 해당하는 **[!UICONTROL 세그먼트 추가]** 단추를 선택하십시오.

   ![단추 활성화](../assets/ui/activate-batch-profile-destinations/activate-buttons-browse.png)

1. 다음 섹션으로 이동하여 [세그먼트 선택](#select-segments).

## 세그먼트 선택 {#select-segments}

세그먼트 이름의 왼쪽에 있는 확인란을 사용하여 대상으로 활성화할 세그먼트를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![세그먼트 선택](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## 세그먼트 내보내기 예약 {#scheduling}

[!DNL Adobe Experience Platform] 이메일 마케팅 및 클라우드 스토리지 대상에 대한 데이터를  [!DNL CSV] 파일 형태로 내보냅니다. **[!UICONTROL 예약]** 페이지에서 내보낼 각 세그먼트에 대한 일정과 파일 이름을 구성할 수 있습니다. 예약을 구성해야 하지만 파일 이름을 구성하는 것은 선택 사항입니다.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 에서는 내보내기 파일을 파일당 500만 개의 레코드(행)로 자동 분할합니다. 각 행은 하나의 프로필을 나타냅니다.
>
>파일 이름을 분할하면 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다. `filename.csv`, `filename_2.csv`, `filename_3.csv`.

대상으로 전송할 세그먼트에 해당하는 **[!UICONTROL 예약 만들기]** 단추를 선택합니다.

![예약 만들기 단추](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### 전체 파일 내보내기 {#export-full-files}

**[!UICONTROL 전체 파일 내보내기]**&#x200B;를 선택하여 선택한 세그먼트에 대한 모든 프로필 자격에 대한 전체 스냅숏이 포함된 파일의 내보내기를 트리거합니다.

![전체 파일 내보내기](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. **[!UICONTROL 빈도]** 선택기를 사용하여 내보내기 빈도를 선택합니다.

   * **[!UICONTROL 한 번]**: 1회 온디맨드 파일 내보내기를 예약합니다.
   * **[!UICONTROL 일별]**: 전체 파일 내보내기를 매일 한 번 예약하고 시작 날짜부터 종료 날짜까지 오전 12:00 UTC(오후 7:00 EST)에 표시합니다.

1. **[!UICONTROL 시간]** 선택기를 사용하여 내보내기가 발생할 때 [!DNL UTC] 형식으로 하루 중 시간을 선택합니다. 파일 **[!UICONTROL Daily]**&#x200B;을 내보내면 파일을 시작 날짜에서 선택한 종료 날짜까지 매일 내보냅니다.

   >[!IMPORTANT]
   >
   >내부 Experience Platform 프로세스가 구성되는 방식 때문에 첫 번째 증분 또는 전체 파일 내보내기에 모든 채우기 데이터가 포함되지 않을 수 있습니다. <br> <br> 전체 파일과 증분 파일 모두에 대해 가장 최신의 채우기 데이터를 전체적으로 내보내려면 다음 날 오후 12시 GMT 이후에 첫 번째 파일 내보내기 시간을 설정하는 것이 좋습니다. 이는 향후 릴리스에서 해결될 수 있는 제한 사항입니다.

1. **[!UICONTROL 날짜]** 선택기를 사용하여 내보내기가 발생할 날짜 또는 간격을 선택합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 선택하여 일정을 저장합니다.


### 증분 파일 내보내기 {#export-incremental-files}

**[!UICONTROL 증분 파일 내보내기]**&#x200B;를 선택하여 첫 번째 파일이 선택한 세그먼트에 대한 모든 프로필 자격에 대한 전체 스냅샷이고 그 다음 파일은 이전 내보내기 이후의 증분 프로필 자격인 내보내기를 트리거합니다.

>[!IMPORTANT]
>
>처음 내보낸 증분 파일에는 세그먼트를 사용할 수 있는 모든 프로필이 포함되어 있으며 채우기 역할을 합니다.

![증분 파일 내보내기](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. **[!UICONTROL 빈도]** 선택기를 사용하여 내보내기 빈도를 선택합니다.

   * **[!UICONTROL 일별]**: 증분 파일 내보내기를 매일 1회 시작 날짜부터 종료 날짜까지 오전 12:00 UTC(오후 7:00 EST)에 예약합니다.
   * **[!UICONTROL 시간별]**: 3,6,7 또는 12시간마다 증분 파일 내보내기 예약

2. **[!UICONTROL 시간]** 선택기를 사용하여 내보내기가 발생할 때 [!DNL UTC] 형식으로 하루 중 시간을 선택합니다.

   >[!IMPORTANT]
   >
   >내보낼 시간을 선택하는 옵션은 선택한 고객 수만 사용할 수 있습니다. <br> <br> 내부 Experience Platform 프로세스가 구성되는 방식 때문에 첫 번째 증분 또는 전체 파일 내보내기에 모든 채우기 데이터가 포함되지 않을 수 있습니다.  <br> <br> 전체 파일과 증분 파일 모두에 대해 가장 최신의 채우기 데이터를 전체적으로 내보내려면 다음 날 오후 12시 GMT 이후에 첫 번째 파일 내보내기 시간을 설정하는 것이 좋습니다. 이는 향후 릴리스에서 해결될 수 있는 제한 사항입니다.

3. **[!UICONTROL 날짜]** 선택기를 사용하여 내보내기가 발생할 날짜 또는 간격을 선택합니다.
4. **[!UICONTROL 만들기]**&#x200B;를 선택하여 일정을 저장합니다.

### 파일 이름 구성 {#file-names}

기본 파일 이름은 대상 이름, 세그먼트 ID, 날짜 및 시간 표시기로 구성됩니다. 예를 들어 내보낸 파일 이름을 편집하여 서로 다른 캠페인을 구분하거나 데이터 내보내기 시간을 파일에 추가할 수 있습니다.

연필 아이콘을 선택하여 모달 창을 열고 파일 이름을 편집합니다. 파일 이름은 255자로 제한됩니다.

![파일 이름 구성](../assets/ui/activate-batch-profile-destinations/configure-name.png)

파일 이름 편집기에서 파일 이름에 추가할 다른 구성 요소를 선택할 수 있습니다.

![파일 이름 옵션 편집](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

대상 이름 및 세그먼트 ID는 파일 이름에서 제거할 수 없습니다. 이 외에도 다음을 추가할 수 있습니다.

* **[!UICONTROL 세그먼트 이름]**: 세그먼트 이름을 파일 이름에 추가할 수 있습니다.
* **[!UICONTROL 날짜 및 시간]**: 파일이  `MMDDYYYY_HHMMSS` 생성되는 시간의 형식 또는 Unix 10자리 타임스탬프를 추가하는 중 선택합니다. 각 증분 내보내기로 생성된 동적 파일 이름을 파일에 포함하려면 다음 옵션 중 하나를 선택합니다.
* **[!UICONTROL 사용자 지정 텍스트]**: 파일 이름에 사용자 지정 텍스트를 추가합니다.

**[!UICONTROL 변경 내용 적용]**&#x200B;을 선택하여 선택 내용을 확인합니다.

>[!IMPORTANT]
> 
>**[!UICONTROL 날짜 및 시간]** 구성 요소를 선택하지 않으면 파일 이름이 고정되고 새로 내보낸 파일이 각 내보내기로 저장소 위치에 있는 이전 파일을 덮어씁니다. 저장소 위치에서 이메일 마케팅 플랫폼으로 반복 가져오기 작업을 실행할 때 권장되는 옵션입니다.

모든 세그먼트 구성을 마치면 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속하십시오.

## 프로필 속성 선택 {#select-attributes}

프로필 기반 대상의 경우 대상 대상으로 전송할 프로필 속성을 선택해야 합니다.


1. **[!UICONTROL 속성 선택]** 페이지에서 **[!UICONTROL 새 필드 추가]**&#x200B;를 선택합니다.

   ![새 매핑 추가](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. **[!UICONTROL 스키마 필드]** 항목 오른쪽에 있는 화살표를 선택합니다.

   ![소스 필드 선택](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. **[!UICONTROL 필드 선택]** 페이지에서 대상으로 전송할 XDM 속성을 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

   ![소스 필드 선택 페이지](../assets/ui/activate-batch-profile-destinations/target-field-page.png)


1. 매핑을 더 추가하려면 1~3단계를 반복합니다.


>[!NOTE]
>
> Adobe Experience Platform은 스키마에서 일반적으로 사용되는 4가지 권장 속성으로 선택 사항을 미리 채웁니다. `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

파일 내보내기는 `segmentMembership.status` 선택 여부에 따라 다음과 같은 방식으로 달라집니다.
* `segmentMembership.status` 필드를 선택하면 내보낸 파일에는 초기 전체 스냅샷의 **[!UICONTROL Active]** 멤버와 후속 증분 내보내기의 **[!UICONTROL Active]** 및 **[!UICONTROL Expired]** 멤버가 포함됩니다.
* `segmentMembership.status` 필드를 선택하지 않으면 내보낸 파일에는 초기 전체 스냅샷과 후속 증분 내보내기에 **[!UICONTROL Active]** 멤버만 포함됩니다.

![권장 속성](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### 필수 속성 {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="필수 속성 정보"
>abstract="내보낸 모든 프로필에 포함해야 하는 XDM 스키마 속성을 선택합니다. 필수 키가 없는 프로필은 대상으로 내보내지지 않습니다. 필수 키를 선택하지 않으면 속성과 관계없이 자격이 있는 모든 프로필이 내보내집니다."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="자세한 내용은 문서에서 알아보십시오"

필수 속성은 모든 프로필 레코드에 선택한 속성이 포함되도록 하는 사용자 활성화 확인란입니다. 예: 내보낸 모든 프로필에 이메일 주소가 &#x200B; 있습니다.

속성을 필수로 표시하여 [!DNL Platform] 특정 속성을 포함하는 프로필만 내보내도록 할 수 있습니다. 따라서 추가 필터링 양식으로 사용할 수 있습니다. 속성을 필수로 표시하는 것은 **필수가 아닙니다**.

필수 속성을 선택하지 않으면 해당 속성과 관계없이 모든 자격이 있는 프로필이 내보내집니다.

특성 중 하나는 스키마의 [고유 식별자](../../destinations/catalog/email-marketing/overview.md#identity)인 것이 좋습니다. 필수 속성에 대한 자세한 내용은 [이메일 마케팅 대상](../../destinations/catalog/email-marketing/overview.md#identity) 설명서에서 ID 섹션을 참조하십시오.

### 중복 제거 키 {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="중복 제거 키 기본 정보"
>abstract="중복 제거 키를 선택하여 내보내기 파일에서 동일한 프로필의 여러 레코드를 제거합니다. 중복 제거 키로 단일 네임스페이스 또는 최대 2개의 XDM 스키마 속성을 선택합니다. 중복 제거 키를 선택하지 않으면 내보내기 파일에서 중복된 프로필 항목이 발생할 수 있습니다."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="자세한 내용은 문서에서 알아보십시오"

중복 제거 키는 사용자가 프로필을 중복 제거하려는 ID를 결정하는 사용자 정의 기본 키입니다&#x200B;.

중복 제거 키를 사용하면 한 내보내기 파일에 동일한 프로필의 여러 레코드가 있을 수 없습니다.

[!DNL Platform]에서 중복 제거 키를 사용할 수 있는 방법에는 세 가지가 있습니다.

* 단일 ID 네임스페이스를 [!UICONTROL 중복 제거 키]로 사용
* [!DNL XDM] 프로필의 단일 프로필 속성을 [!UICONTROL 중복 제거 키]로 사용
* [!DNL XDM] 프로필의 두 프로필 속성의 조합을 복합 키로 사용

>[!IMPORTANT]
>
> 단일 ID 네임스페이스를 대상으로 내보낼 수 있으며, 네임스페이스가 자동으로 중복 제거 키로 설정됩니다. 여러 네임스페이스를 대상에 보낼 수 없습니다.
> 
> ID 네임스페이스와 프로필 속성의 조합을 중복 제거 키로 사용할 수 없습니다.

### 중복 제거 예 {#deduplication-example}

이 예에서는 선택한 중복 제거 키에 따라 중복 제거가 작동하는 방식을 보여줍니다.

다음 두 프로필을 고려해 보겠습니다.

**프로필 A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**프로필 B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### 중복 제거 사용 사례 1: 중복 제거 없음 {#deduplication-use-case-1}

중복 제거를 사용하지 않는 경우 내보내기 파일에 다음 항목이 포함됩니다.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | 존 | Doe |
| johndoe@example.com | 존 | D |


### 중복 제거 사용 사례 2: id 네임스페이스를 기반으로 데이터 중복 제거 {#deduplication-use-case-2}

중복 제거를 [!DNL Email] 네임스페이스로 가정하면 내보내기 파일에 다음 항목이 포함됩니다. 프로필 B는 세그먼트에 대한 자격이 있는 최신 프로필이므로 내보낼 수 있는 유일한 프로필입니다.

| 이메일* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | 존 | D |
| johndoe_2@example.com | johndoe@example.com | 존 | D |

### 중복 제거 사용 사례 3: 단일 프로필 속성을 기반으로 한 중복 제거 {#deduplication-use-case-3}

`personal Email` 속성으로 중복 제거를 가정하면 내보내기 파일에 다음 항목이 포함됩니다. 프로필 B는 세그먼트에 대한 자격이 있는 최신 프로필이므로 내보낼 수 있는 유일한 프로필입니다.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | 존 | D |


### 중복 제거 사용 사례 4: 두 개의 프로필 속성을 기반으로 한 중복 제거 {#deduplication-use-case-4}

복합 키 `personalEmail + lastName`에 의해 중복 제거된다고 가정하면 내보내기 파일에 다음 항목이 포함됩니다.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | 존 |
| johndoe@example.com | Doe | 존 |


Adobe은 모든 프로필 레코드가 고유하게 식별되도록 [!DNL CRM ID] 또는 이메일 주소와 같은 ID 네임스페이스를 중복 제거 키로 선택하는 것이 좋습니다.

>[!NOTE]
> 
>데이터 사용 레이블이 데이터 세트 전체 데이터 세트가 아닌 데이터 세트 내의 특정 필드에 적용된 경우 활성화 시 해당 필드 수준 레이블의 적용은 다음 조건에서 수행됩니다.
>
>* 필드는 세그먼트 정의에 사용됩니다.
>* 필드는 대상 대상에 대한 예상 속성으로 구성됩니다.

>
> 
예를 들어 필드 `person.name.firstName`에 대상의 마케팅 작업과 충돌하는 특정 데이터 사용 레이블이 있는 경우 검토 단계에서 데이터 사용 정책 위반이 표시됩니다. 자세한 내용은 [Adobe Experience Platform의 데이터 거버넌스](../../rtcdp/privacy/data-governance-overview.md#destinations)를 참조하십시오.

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택 요약이 표시됩니다. **[!UICONTROL 취소]**&#x200B;를 선택하여 플로우를 분류하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택 내용을 확인하고 데이터를 대상에 보내려면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

>[!IMPORTANT]
>
>이 단계에서 Adobe Experience Platform은 데이터 사용 정책 위반을 확인합니다. 아래는 정책이 위반되는 예입니다. 위반을 해결해야 세그먼트 활성화 워크플로우를 완료할 수 있습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 설명서 섹션의 [정책 적용](../../rtcdp/privacy/data-governance-overview.md#enforcement)을 참조하십시오.

![데이터 정책 위반](../assets/common/data-policy-violation.png)

정책 위반이 감지되지 않은 경우 **[!UICONTROL 완료]**&#x200B;를 선택하여 선택 내용을 확인하고 데이터를 대상에 보냅니다.

![검토](../assets/ui/activate-batch-profile-destinations/review.png)

## 세그먼트 활성화 확인 {#verify}


이메일 마케팅 대상 및 클라우드 스토리지 대상의 경우, Adobe Experience Platform은 제공한 저장소 위치에 탭으로 구분된 `.csv` 파일을 만듭니다. 매일 저장소 위치에 새 파일이 생성될 것으로 예상됩니다. 기본 파일 형식은 다음과 같습니다.
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

3일 연속으로 받은 파일은 다음과 같습니다.

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

스토리지 위치에 이러한 파일이 있으면 성공적인 활성화를 확인할 수 있습니다. 내보낸 파일의 구조를 이해하기 위해 [샘플 .csv 파일](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)을 다운로드할 수 있습니다. 이 샘플 파일에는 프로필 속성 `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` 및 `personalEmail.address`가 포함되어 있습니다.
