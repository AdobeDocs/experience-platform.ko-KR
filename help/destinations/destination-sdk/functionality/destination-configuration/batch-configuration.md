---
description: Destination SDK으로 빌드된 대상에 대한 파일 내보내기 설정을 구성하는 방법을 알아봅니다.
title: 배치 구성
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---


# 배치 구성 {#batch-configuration}

Destination SDK의 일괄 구성 옵션을 사용하여 내보낸 파일 이름을 사용자 지정하고 기본 설정에 따라 내보내기 일정을 구성할 수 있습니다.

Destination SDK을 통해 파일 기반 대상을 만들 때 기본 파일 이름 지정 및 내보내기 일정을 구성하거나, 사용자에게 Platform UI에서 이러한 설정을 구성하는 옵션을 제공할 수 있습니다. 예를 들어 다음과 같은 동작을 구성할 수 있습니다.

* 세그먼트 ID, 대상 ID 또는 사용자 지정 정보와 같은 특정 정보를 파일 이름에 포함합니다.
* 사용자가 Platform UI에서 파일 이름을 사용자 지정할 수 있습니다.
* 설정된 시간 간격으로 파일 내보내기를 구성합니다.
* 사용자가 Platform UI에서 볼 수 있는 파일 이름 지정 및 내보내기 예약 사용자 지정 옵션을 정의합니다.

배치 구성 설정은 파일 기반 대상에 대한 대상 구성의 일부입니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서를 참조하십시오. [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

를 통해 파일 이름 지정 및 내보내기 예약 설정을 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 배치 구성 옵션에 대해 설명하고 고객이 플랫폼 UI에서 보게 되는 내용을 보여줍니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 아니요 |
| 파일 기반(일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

여기서 설정한 값은 [세그먼트 내보내기 예약](../../../ui/activate-batch-profile-destinations.md#scheduling) 파일 기반 대상 활성화 워크플로우의 단계입니다.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `allowMandatoryFieldSelection` | 부울 | 을 로 설정합니다. `true` 고객이 필수 프로필 속성을 지정할 수 있도록 해줍니다. 기본값은 `false`입니다. 자세한 내용은 [필수 속성](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 추가 정보. |
| `allowDedupeKeyFieldSelection` | 부울 | 을 로 설정합니다. `true` 고객이 중복 제거 키를 지정할 수 있도록 허용 기본값은 `false`입니다.  자세한 내용은 [중복 제거 키](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) 추가 정보. |
| `defaultExportMode` | 열거형 | 기본 파일 내보내기 모드를 정의합니다. 지원되는 값:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 기본값은 `DAILY_FULL_EXPORT`입니다. 자세한 내용은 [배치 활성화 설명서](../../../ui/activate-batch-profile-destinations.md#scheduling) 파일 내보내기 예약에 대한 자세한 내용은 다음을 참조하십시오. |
| `allowedExportModes` | 목록 | 고객이 사용할 수 있는 파일 내보내기 모드를 정의합니다. 지원되는 값:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 목록 | 고객이 사용할 수 있는 파일 내보내기 빈도를 정의합니다. 지원되는 값:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 열거형 | 기본 파일 내보내기 빈도를 정의합니다.지원되는 값:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 기본값은 `DAILY`입니다. |
| `defaultStartTime` | 문자열 | 파일 내보내기의 기본 시작 시간을 정의합니다. 24시간 파일 형식을 사용합니다. 기본값은 &quot;00:00&quot;입니다. |
| `filenameConfig.allowedFilenameAppendOptions` | 문자열 | *필수 여부*. 사용자가 선택할 수 있는 사용 가능한 파일 이름 매크로 목록 내보낸 파일 이름에 추가되는 항목(세그먼트 ID, 조직 이름, 내보내기 날짜 및 시간 등)을 결정합니다. 설정 시 `defaultFilename`를 사용하여 매크로가 중복되지 않도록 합니다. <br><br>지원되는 값: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>매크로를 정의하는 순서에 관계없이 Experience Platform UI에서 항상 여기에 표시된 순서대로 표시됩니다. <br><br> If `defaultFilename` 비어 있는 경우 `allowedFilenameAppendOptions` 목록에 하나 이상의 매크로가 있어야 합니다. |
| `filenameConfig.defaultFilenameAppendOptions` | 문자열 | *필수 여부*. 사용자가 선택 취소할 수 있는 미리 선택된 기본 파일 이름 매크로입니다.<br><br> 이 목록의 매크로는 `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | 문자열 | *선택 사항입니다*. 내보낸 파일의 기본 파일 이름 매크로를 정의합니다. 사용자가 덮어쓸 수 없습니다. <br><br>에 의해 정의된 모든 매크로 `allowedFilenameAppendOptions` 다음에 추가됩니다. `defaultFilename` 매크로 <br><br>If `defaultFilename` 비어 있으면, 에서 매크로를 하나 이상 정의해야 합니다. `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## 파일 이름 구성 {#file-name-configuration}

파일 이름 구성 매크로를 사용하여 내보낸 파일 이름에 포함해야 하는 항목을 정의합니다. 아래 표의 매크로에서는 [파일 이름 구성](../../../ui/activate-batch-profile-destinations.md#file-names) 화면.

>[!TIP]
> 
>가장 좋은 방법으로서, 항상 를 포함해야 합니다 `SEGMENT_ID` 내보낸 파일 이름에 매크로가 있습니다. 세그먼트 ID는 고유하므로 파일 이름도 고유하게 구별할 수 있는 가장 좋은 방법입니다.

| 매크로 | UI 레이블 | 설명 | 예 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 대상] | UI의 대상 이름입니다. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 세그먼트 ID] | 고유한 플랫폼 생성 세그먼트 ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 세그먼트 이름] | 사용자 정의 세그먼트 이름 | VIP 가입자 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 대상 ID] | 대상 인스턴스의 플랫폼 생성 고유 ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 대상 이름] | 대상 인스턴스의 사용자 정의 이름입니다. | 2022년 내 광고 대상 |
| `ORGANIZATION_NAME` | [!UICONTROL 조직 이름] | Adobe Experience Platform에 있는 고객 조직의 이름입니다. | 내 조직 이름 |
| `SANDBOX_NAME` | [!UICONTROL 샌드박스 이름] | 고객이 사용하는 샌드박스의 이름입니다. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 날짜 및 시간] | `DATETIME` 및 `TIMESTAMP` 두 정의 모두 파일이 생성된 시점을 정의하지만 형식은 다릅니다. <br><br><ul><li>`DATETIME` 는 다음 형식을 사용합니다. YYYMMDD_HMMSS.</li><li>`TIMESTAMP` 는 10자리 Unix 형식을 사용합니다. </li></ul> `DATETIME` 및 `TIMESTAMP` 는 함께 사용할 수 없으며 동시에 사용할 수 없습니다. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 사용자 정의 텍스트] | 파일 이름에 포함할 사용자 정의 사용자 정의 텍스트입니다. 에서는 사용할 수 없습니다. `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 날짜 및 시간] | 파일이 생성된 시간의 10자리 타임스탬프(Unix 형식)입니다. | 1652131584 |

{style="table-layout:auto"}

### 파일 이름 구성 예

아래 구성 예는 API 호출에 사용된 구성과 UI에 표시된 옵션 간의 서신을 보여줍니다.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![미리 선택된 매크로가 있는 파일 이름 구성 화면을 보여주는 UI 이미지](../../assets/functionality/destination-configuration/file-name-configuration.png)

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 파일 기반 대상의 파일 이름 지정 및 내보내기 일정을 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증 구성](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [내역 프로필 자격](historical-profile-qualifications.md)