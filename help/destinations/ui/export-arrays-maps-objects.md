---
title: Real-Time CDP에서 배열, 맵 및 개체 내보내기
type: Tutorial
description: Real-Time CDP에서 클라우드 스토리지 대상으로 배열, 맵 및 개체를 내보내는 방법에 대해 알아봅니다.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: f7ff10dd6489842adb8de49b3f8634c20d77cc71
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 13%

---

# Real-Time CDP에서 배열, 맵 및 개체 내보내기 {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>배열 및 기타 복잡한 개체를 클라우드 저장소 대상으로 내보내는 기능은 일반적으로 [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md) 대상에 사용할 수 있습니다.
>
>또한 맵 유형 필드를 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) 대상으로 내보낼 수 있습니다.


Real-Time CDP에서 [클라우드 저장소 대상](/help/destinations/catalog/cloud-storage/overview.md)(으)로 배열, 맵 및 개체를 내보내는 방법에 대해 알아봅니다. 또한 맵 유형 필드를 [엔터프라이즈 대상](/help/destinations/destination-types.md#advanced-enterprise-destinations) 및 제한된 [에지 개인화 대상](/help/destinations/destination-types.md#edge-personalization-destinations)(으)로 내보낼 수 있습니다. 내보내기 워크플로우, 이 기능에서 활성화된 사용 사례 및 알려진 제한 사항을 이해하려면 이 문서 를 참조하십시오. 대상 유형별로 사용할 수 있는 기능을 이해하려면 아래 표를 참조하십시오.

| 대상 유형 | 배열, 맵 및 기타 사용자 지정 개체 내보내기 기능 |
|---|---|
| Adobe 작성 클라우드 스토리지 대상(Amazon S3, Azure Blob, Azure Data Lake Storage Gen2, 데이터 랜딩 영역, Google 클라우드 스토리지, SFTP) | 예. 대상 연결을 설정할 때 배열, 맵 및 개체의 내보내기 활성화 토글이 켜져 있습니다. |
| 파일 기반 이메일 마케팅 대상(Adobe Campaign, Oracle Eloqua, Oracle Responsys, Salesforce Marketing Cloud) | 아니요 |
| 기존 사용자 지정 파트너가 빌드한 클라우드 스토리지 대상(Destination SDK을 통해 빌드한 사용자 지정 파일 기반 대상) | 아니요 |
| 엔터프라이즈 대상(Amazon Kinesis, Azure Event Hubs, HTTP API) | 부분적으로요 활성화 워크플로의 매핑 단계에서 맵 유형 개체를 선택하고 내보낼 수 있습니다. |
| 스트리밍 대상(예: Facebook, Braze, Google Customer Match 등) | 아니요 |
| Edge 개인화 대상 | 아니요 |

{style="table-layout:auto"}

Experience Platform에서 배열, 맵 및 기타 개체 유형을 내보내는 방법에 대해 알고 싶은 경우 이 페이지를 방문하십시오.

## 맨 앞까지 내림표

이 섹션에서 기능에 대한 가장 중요한 정보를 얻고 아래에서 문서의 다른 섹션으로 이동하여 자세한 내용을 확인하십시오.

* 클라우드 저장소 대상의 경우 배열, 맵 및 개체를 내보내는 기능은 **배열, 맵, 개체 내보내기** 토글 선택에 따라 다릅니다. 자세한 내용은 [페이지의 아래쪽에서](#export-arrays-maps-objects-toggle)를 참조하세요.
* 배열, 맵 및 개체를 `JSON` 및 `Parquet` 파일의 클라우드 저장소 대상으로 내보낼 수 있습니다. Enterprise 및 Edge 개인화 대상의 경우 내보낸 데이터 형식은 `JSON`입니다. 사용자 및 잠재 고객은 지원되지만 계정 대상은 지원되지 않습니다.
* 파일 기반 클라우드 저장소 대상의 경우 배열, 맵 및 개체를 CSV 파일로 *할 수*&#x200B;있지만 계산된 필드 기능을 사용하고 `array_to_string` 함수를 사용하여 문자열로 연결하기만 하면 됩니다.

## Experience Platform의 배열 및 기타 개체 유형 {#arrays-strings-other-objects}

Experience Platform에서는 [XDM 스키마](/help/xdm/home.md)를 사용하여 다른 필드 유형을 관리할 수 있습니다. 배열 내보내기에 대한 지원이 추가되기 전에 Experience Platform의 문자열과 같은 간단한 키-값 쌍 유형 필드를 원하는 대상으로 내보낼 수 있습니다. 이전에 내보내기에 지원되는 이러한 필드의 예는 `personalEmail.address`:`johndoe@acme.org`입니다.

Experience Platform의 다른 필드 유형에는 배열 필드가 포함됩니다. [Experience Platform UI에서 배열 필드 관리](/help/xdm/ui/fields/array.md)에 대해 자세히 알아보십시오. 이제 아래 예와 같은 배열 개체를 내보낼 수 있습니다.

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

어레이 외에도 Experience Platform의 맵과 개체를 원하는 클라우드 스토리지 대상으로 내보낼 수도 있습니다. Experience Platform의 [맵](/help/xdm/ui/fields/map.md) 및 [개체](/help/xdm/ui/fields/object.md)에 대해 자세히 알아보십시오.

## 전제 조건 {#prerequisites}

원하는 클라우드 저장소 대상에 [연결](/help/destinations/ui/connect-destination.md)하고, 클라우드 저장소 대상에 대한 [활성화 단계](/help/destinations/ui/activate-batch-profile-destinations.md)를 진행하고 [매핑](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 단계로 이동하십시오. 원하는 클라우드 대상에 연결할 때 **[!UICONTROL 배열, 맵, 개체 내보내기]** 토글을 선택해야 합니다. 자세한 내용은 아래 섹션을 참조하십시오.

>[!NOTE]
>
>엔터프라이즈 및 에지 개인화 대상의 경우 **[!UICONTROL 배열, 맵, 개체 내보내기]** 토글을 선택하지 않아도 맵 유형 필드에 대한 내보내기 지원을 사용할 수 있습니다. 이러한 유형의 대상에 연결하는 경우 이 토글을 사용하거나 사용할 수 없습니다.

## 배열, 맵 및 오브젝트 토글 내보내기 {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="배열, 맵 및 오브젝트 내보내기"
>abstract="<p> 배열, 맵 및 오브젝트를 JSON 또는 Parquet 파일로 내보낼 수 있도록 설정을 <b>켜짐</b>으로 토글합니다. 매핑 단계의 소스 필드 보기에서 이들 오브젝트 유형을 선택할 수 있습니다. 토글을 켜면 매핑 단계에서 계산된 필드 옵션을 사용할 수 없습니다.</p><p>이 설정을 <b>꺼짐</b>으로 토글하여 계산된 필드 옵션을 사용하고 대상자를 활성화할 때 다양한 데이터 변환 기능을 적용할 수 있습니다. 단, 배열, 맵, 오브젝트를 JSON이나 Parquet 파일로 내보낼 수는 <i>없으며</i> 해당 목적에 대한 별도의 대상을 구성해야 합니다.</p>"

파일 기반 클라우드 저장소 대상에 연결할 때 **[!UICONTROL 배열 내보내기, 맵, 개체]** 토글을 설정하거나 해제할 수 있습니다.

![배열, 맵, 개체 내보내기는 팝오버를 강조 표시하고 켜기 또는 끄기 설정으로 전환됩니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

배열, 맵 및 오브젝트를 JSON 또는 Parquet 파일로 내보낼 수 있도록 설정을 **켜짐**&#x200B;으로 토글합니다. 대상을 클라우드 저장소 대상으로 활성화할 때 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)의 원본 필드 보기에서 이러한 개체 유형을 선택할 수 있습니다. 그러나 이 설정을에 두고, [계산된 필드] 옵션을 사용하여 활성화 시 데이터를 변환할 수 없습니다.

이 설정을 **꺼짐**&#x200B;으로 토글하여 계산된 필드 옵션을 사용하고 대상자를 활성화할 때 다양한 데이터 변환 기능을 적용할 수 있습니다. 그러나 배열, 맵 및 개체를 JSON 또는 Parquet 파일로 내보낼 수 없으며 이를 위해 별도의 대상을 구성해야 합니다.

## 배열, 맵, 개체 내보내기 *켜짐* 전환 {#export-arrays-maps-objects-toggle-on}

이 설정을 켜면 활성화 워크플로의 매핑 단계에서 소스 필드 선택기를 통해 전체 개체(예: `person.name`) 및 배열을 선택하여 내보낼 수 있습니다.

![활성화 워크플로의 매핑 단계에서 원본 필드 선택기를 통해 개체를 선택합니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

이 옵션을 선택하면 사용자 인터페이스에서 계산된 필드를 사용할 수 없게 되며 아래와 같이 **[!UICONTROL 계산된 필드 추가]** 컨트롤이 비활성화됩니다. 데이터 변환에 계산된 필드를 사용하려면 토글을 해제하여 대상 연결을 설정하십시오.

![계산된 필드 컨트롤이 비활성화되었습니다.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## 배열, 맵, 개체 내보내기 *끄기* {#export-arrays-maps-objects-toggle-off}

이 옵션을 *off*(으)로 설정하면 계산된 필드 옵션을 사용하고 대상을 활성화할 때 다양한 데이터 변환 함수를 적용할 수 있습니다. 그러나 배열, 맵 및 개체를 JSON 또는 Parquet 파일로 내보낼 수 없으며 이를 위해 별도의 대상을 구성해야 합니다.

계산된 필드 기능을 사용하여 배열, 맵 및 개체를 CSV 파일로 *할 수*&#x200B;있으며 `array_to_string` 함수를 사용하여 문자열로 연결합니다. 해당 함수 사용에 대해 [자세히 읽어보세요](#array-to-string-function-export-arrays).

[클라우드 저장소 대상으로 내보낸 데이터에 변환을 수행](/help/destinations/ui/data-transformations-calculated-fields.md)하기 위해 계산된 필드를 사용하여 작업하는 방법에 대해 자세히 알아보십시오.

## 내보낸 샘플 파일 {#sample-exported-files}

이 기능을 사용하면 데이터가 Experience Platform의 구조를 유지하는 Parquet 및 JSON 파일을 내보낼 수 있습니다. 내보낸 JSON 파일의 아래를 봅니다.

+++ 내보낸 JSON 파일을 보려면 을 선택합니다.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++