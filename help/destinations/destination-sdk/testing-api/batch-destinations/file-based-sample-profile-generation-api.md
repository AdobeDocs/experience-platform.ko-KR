---
description: 이 페이지에서는 Destination SDK의 /sample-profiles API 엔드포인트를 사용하여 소스 스키마를 기반으로 샘플 프로필을 생성하는 방법을 설명합니다. 이러한 샘플 프로필을 사용하여 파일 기반 대상 구성을 테스트할 수 있습니다.
title: 소스 스키마를 기반으로 샘플 프로필 생성
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# 소스 스키마를 기반으로 샘플 프로필 생성

파일 기반 대상을 테스트하는 첫 번째 단계는 `/sample-profiles` 끝점을 사용하여 기존 소스 스키마를 기반으로 하는 샘플 프로필을 생성하는 것입니다.

샘플 프로필은 프로필의 JSON 구조를 이해하는 데 도움이 될 수 있습니다. 또한 추가적인 대상 테스트를 위해 자신의 프로필 데이터로 사용자 정의할 수 있는 기본값을 제공합니다.

## 시작하기 {#getting-started}

계속하기 전에 [시작 안내서](../../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 전제 조건 {#prerequisites}

`/sample-profiles` 끝점을 사용하기 전에 다음 조건을 충족하는지 확인하십시오.

* Destination SDK을 통해 만든 기존 파일 기반 대상이 있으며 [대상 카탈로그](../../../ui/destinations-workspace.md)에서 볼 수 있습니다.
* Experience Platform UI에서 대상에 대한 활성화 플로우를 하나 이상 만들었습니다. `/sample-profiles` 끝점은 활성화 흐름에 정의한 소스 스키마를 기반으로 프로필을 만듭니다. 활성화 흐름을 만드는 방법을 알아보려면 [활성화 자습서](../../../ui/activate-batch-profile-destinations.md)를 참조하세요.
* API 요청을 성공적으로 수행하려면 테스트할 대상 인스턴스에 해당하는 대상 인스턴스 ID가 필요합니다. Experience Platform UI에서 대상과의 연결을 검색할 때 API 호출에 사용해야 하는 대상 인스턴스 ID를 URL에서 가져옵니다.

  URL에서 대상 인스턴스 ID를 가져오는 방법을 보여 주는 ![UI 이미지.](../../assets/testing-api/get-destination-instance-id.png)

## 대상 테스트를 위한 샘플 프로필 생성 {#generate-sample-profiles}

테스트할 대상의 대상 인스턴스 ID로 `/sample-profiles` 끝점에 GET 요청을 수행하여 소스 스키마를 기반으로 샘플 프로필을 생성할 수 있습니다.

**API 형식**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 쿼리 매개변수 | 설명 |
| -------- | ----------- |
| `destinationInstanceId` | 샘플 프로필을 생성하고 있는 대상 인스턴스의 ID입니다. 이 ID를 얻는 방법에 대한 자세한 내용은 [필수 구성 요소](#prerequisites) 섹션을 참조하십시오. |
| `count` | *선택 사항*. 생성할 샘플 프로필 수입니다. 매개 변수는 `1 - 1000` 사이의 값을 사용할 수 있습니다. 이 속성이 정의되지 않으면 API는 단일 샘플 프로필을 생성합니다. |

**요청**

다음 요청은 해당 `destinationInstanceId`을(를) 사용하여 대상 인스턴스에 정의된 소스 스키마를 기반으로 샘플 프로필을 생성합니다.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 지정된 수의 샘플 프로필과 함께, 소스 XDM 스키마에 해당하는 대상 멤버십, ID 및 프로필 속성이 포함된 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
> 응답에서는 대상 인스턴스에 사용된 대상 멤버십, ID 및 프로필 속성만 반환합니다. 소스 스키마에 다른 필드가 있더라도 무시됩니다.

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

![API 응답의 필드에 대한 UI의 매핑을 보여 주는 이미지입니다.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 속성 | 설명 |
| -------- | ----------- |
| `segmentMembership` | 개인의 대상 멤버십을 설명하는 맵 개체입니다. `segmentMembership`에 대한 자세한 내용은 [대상 멤버십 세부 정보](../../../../xdm/field-groups/profile/segmentation.md)를 참조하세요. |
| `lastQualificationTime` | 이 프로필이 세그먼트에 대해 마지막으로 적격한 타임스탬프입니다. |
| `status` | 대상자 멤버십이 현재 요청의 일부로 실현되었는지 여부를 나타내는 문자열 필드입니다. 다음 값이 허용됩니다. <ul><li>`realized`: 프로필이 세그먼트에 속합니다.</li><li>`exited`: 프로필이 현재 요청의 일부로 대상을 종료합니다.</li></ul> |
| `identityMap` | 연관된 네임스페이스와 함께 개인에 대한 다양한 ID 값을 설명하는 맵 유형 필드입니다. `identityMap`에 대한 자세한 내용은 [스키마 컴포지션의 기준](../../../../xdm/schema/composition.md#identityMap)을 참조하십시오. |

{style="table-layout:auto"}

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. Experience Platform 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상 [활성화 흐름](../../../ui/activate-batch-profile-destinations.md)에서 구성한 소스 스키마를 기반으로 샘플 프로필을 생성하는 방법을 이해할 수 있습니다.

이제 이러한 프로필을 사용자 지정하거나 API에서 반환된 프로필을 사용하여 [파일 기반 대상 구성을 테스트](file-based-destination-testing-api.md)할 수 있습니다.
