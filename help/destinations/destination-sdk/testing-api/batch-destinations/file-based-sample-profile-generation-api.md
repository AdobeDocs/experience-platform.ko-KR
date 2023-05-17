---
description: 이 페이지에서는 Destination SDK의 /sample-profiles API 엔드포인트를 사용하여 소스 스키마를 기반으로 샘플 프로필을 생성하는 방법에 대해 설명합니다. 이러한 샘플 프로필을 사용하여 파일 기반 대상 구성을 테스트할 수 있습니다.
title: 소스 스키마를 기반으로 샘플 프로필 생성
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---


# 소스 스키마를 기반으로 샘플 프로필 생성

파일 기반 대상을 테스트하는 첫 번째 단계는 `/sample-profiles` 기존 소스 스키마를 기반으로 샘플 프로필을 생성하는 끝점입니다.

샘플 프로필은 프로필의 JSON 구조를 이해하는 데 도움이 될 수 있습니다. 또한 추가적인 대상 테스트를 위해 자체 프로필 데이터로 사용자 지정할 수 있는 기본값을 제공합니다.

## 시작하기 {#getting-started}

계속하기 전에 [시작 안내서](../../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 사전 요구 사항 {#prerequisites}

를 사용하기 전에 `/sample-profiles` endpoint, 다음 조건을 충족하는지 확인하십시오.

* Destination SDK을 통해 만든 기존 파일 기반 대상이 있으며 [대상 카탈로그](../../../ui/destinations-workspace.md).
* Experience Platform UI에서 대상에 대해 하나 이상의 활성화 흐름을 만들었습니다. 다음 `/sample-profiles` 종단점은 활성화 흐름에 정의한 소스 스키마를 기반으로 프로필을 만듭니다. 자세한 내용은 [활성화 자습서](../../../ui/activate-batch-profile-destinations.md) 활성화 흐름을 만드는 방법을 알아봅니다.
* API 요청을 성공적으로 수행하려면 테스트할 대상 인스턴스에 해당하는 대상 인스턴스 ID가 필요합니다. Platform UI에서 대상과의 연결을 검색할 때 URL에서 API 호출에 사용해야 하는 대상 인스턴스 ID를 가져옵니다.

   ![URL에서 대상 인스턴스 ID를 가져오는 방법을 보여주는 UI 이미지입니다.](../../assets/testing-api/get-destination-instance-id.png)

## 대상 테스트를 위한 샘플 프로필 생성 {#generate-sample-profiles}

에 GET 요청을 수행하여 소스 스키마를 기반으로 샘플 프로필을 생성할 수 있습니다 `/sample-profiles` 테스트할 대상의 대상 인스턴스 ID가 포함된 끝점입니다.

**API 형식**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `destinationInstanceId` | 샘플 프로필을 생성하는 대상 인스턴스의 ID입니다. 자세한 내용은 [전제 조건](#prerequisites) 섹션을 참조하십시오. |
| `count` | *선택 사항입니다*. 생성할 샘플 프로필 수입니다. 매개 변수는 다음 사이 값을 가져올 수 있습니다 `1 - 1000`. 이 속성이 정의되지 않은 경우 API는 단일 샘플 프로필을 생성합니다. |

**요청**

다음 요청은 대상 인스턴스에 정의된 소스 스키마를 기반으로 샘플 프로필을 생성합니다. `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 소스 XDM 스키마에 해당하는 세그먼트 멤버십, ID 및 프로필 속성을 사용하여 지정된 수의 샘플 프로필과 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
> 응답에서는 대상 인스턴스에 사용되는 세그먼트 멤버십, ID 및 프로필 속성만 반환합니다. 소스 스키마에 다른 필드가 있더라도 이러한 필드는 무시됩니다.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![UI에서 API 응답의 필드에 대한 매핑을 표시하는 이미지입니다.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 속성 | 설명 |
| -------- | ----------- |
| `segmentMembership` | 개인의 세그먼트 멤버십을 설명하는 맵 개체입니다. 자세한 내용은 `segmentMembership`, 읽기 [세그먼트 멤버십 세부 정보](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | 이 프로필이 세그먼트에 대해 자격이 있는 마지막 시간의 타임스탬프입니다. |
| `status` | 세그먼트 멤버십이 현재 요청의 일부로 실현되었는지 여부를 나타내는 문자열 필드입니다. 다음 값이 허용됩니다. <ul><li>`realized`: 프로필은 세그먼트의 일부입니다.</li><li>`exited`: 프로필이 현재 요청의 일부로 세그먼트를 종료하고 있습니다.</li></ul> |
| `identityMap` | 연관된 네임스페이스와 함께 개인의 다양한 ID 값을 설명하는 맵 유형 필드입니다. 자세한 내용은 `identityMap`를 참조하십시오. [스키마 구성 기준](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이제 이 문서를 읽은 후 대상에 구성한 소스 스키마를 기반으로 샘플 프로필을 생성하는 방법을 알 수 있습니다 [활성화 흐름](../../../ui/activate-batch-profile-destinations.md).

이제 이러한 프로필을 사용자 지정하거나 API에서 반환한 대로 사용할 수 있습니다. [파일 기반 대상 구성 테스트](file-based-destination-testing-api.md).
