---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 실시간 고객 프로필 문제 해결 가이드
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# 실시간 고객 프로필 문제 해결 가이드

이 문서에서는 실시간 고객 프로필에 대한 FAQ와 일반적인 오류에 대한 문제 해결 가이드를 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 가이드를 참조하십시오](../landing/troubleshooting.md).

실시간 고객 프로필은 다양한 엔터프라이즈 데이터 자산의 데이터를 수집한 다음 개별 고객 프로필 및 관련 시간 시리즈 이벤트의 형태로 해당 데이터에 대한 액세스를 제공하는 범용 조회 엔티티 스토어입니다. 이 기능을 통해 마케터는 다양한 채널에서 고객과 연관성 있고 조율된 경험을 제공할 수 있습니다.

## FAQ

다음은 실시간 고객 프로필과 관련하여 자주 묻는 질문에 대한 답변 목록입니다.

### 실시간 고객 프로파일에 허용되는 데이터 유형

문제의 데이터에 데이터를 고유한 개인 **과 연결하는 하나 이상의 ID 값이 포함되어 있는 한, 프로필은** 레코드 **및** 시간 시리즈데이터를 모두 수용합니다.

모든 플랫폼 서비스와 마찬가지로 프로필도 데이터를 XDM(Experience Data Model) 스키마 아래에 의미있게 구조화해야 합니다. 따라서 이 스키마에는 **기본 ID가** 정의되어 있어야 하며 프로필에서 사용할 수 있도록 설정되어 있어야 합니다.

XDM에 익숙하지 않은 경우 [XDM 개요를](../xdm/home.md) 참조하여 자세히 알아보십시오. ID 필드 [설정 및 프로필 스키마](../xdm/tutorials/create-schema-ui.md#identity-field) 활성화 방법에 대한 단계는 XDM 사용자 안내서를 참조하십시오 [](../xdm/tutorials/create-schema-ui.md#profile).

### 프로필 데이터는 어디에 저장됩니까?

실시간 고객 프로필은 다른 인제스트된 플랫폼 데이터가 포함된 데이터 레이크와 별도로 데이터 저장소(&quot;프로필 스토어&quot;라고 함)를 유지합니다.

### 데이터를 이미 Platform(플랫폼)으로 가져온 경우 Profile Store에서 이용할 수 있습니까?

데이터가 비프로필 데이터 세트에 인제스트된 경우 프로필 저장소에서 사용 가능하도록 하려면 해당 데이터를 프로필 사용 가능한 데이터 세트에 다시 인제스트해야 합니다. 기존 프로필 데이터 세트를 활성화할 수 있지만 해당 구성 전에 인제스트한 데이터는 여전히 프로필 저장소에 표시되지 않습니다.

이전에 인제스트한 데이터를 프로필 저장소에 추가하려면 [데이터 세트 구성 자습서에](./tutorials/dataset-configuration.md) 따라 새 데이터 세트를 만들거나 기존 데이터 세트를 프로필 사용 가능하게 전환한 다음 원하는 데이터를 해당 데이터 세트에 다시 인제스트합니다.

### 인제스트한 프로필 데이터를 보려면 어떻게 해야 합니까?

API 또는 UI 사용 여부에 따라 프로필 데이터를 보는 방법에는 여러 가지가 있습니다.

#### API 사용

액세스하려는 프로필 개체의 ID를 알고 있는 경우 프로필 API의 `/entities` (프로필 액세스) 끝점을 사용하여 해당 엔터티를 조회할 수 있습니다. 자세한 내용은 개발자 안내서의 [엔티티](./api/entities.md) 섹션을 참조하십시오.

또한 Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 멤버십에 자격이 있는 고객의 개별 프로필에 액세스할 수도 있습니다. See the [Segmentation Service overview](../segmentation/home.md) for more information.

#### UI 사용

Experience Platform UI에서 **[!UICONTROL 프로필]** 작업 영역의 [찾아보기 **** ] 탭을 사용하여 총 프로필 수를 보고 ID 값별로 개별 프로필을 검색할 수 있습니다. 자세한 내용은 [프로필 사용 안내서를](./ui/user-guide.md) 참조하십시오.

세그먼트 작업 공간의 찾아보기 **[!UICONTROL 탭 아래]** 세그먼트 목록을 **[!UICONTROL 볼 수도]** 있습니다. 세그먼트를 선택하면 해당 세그먼트에 자격이 있는 프로필 샘플이 표시됩니다. 그런 다음 나열된 프로파일 중 하나를 선택하여 세부 사항을 볼 수 있습니다. See the [Segmentation UI overview](../segmentation/ui/overview.md) for more information.

## 오류 코드

다음은 실시간 고객 프로필 API를 사용하여 작업할 때 발생할 수 있는 오류 메시지 목록입니다. 여기에 오류가 표시되지 않으면 일반 [플랫폼 문제 해결 안내서에서 찾을 수 있습니다](../landing/troubleshooting.md) .

### 제공된 경로에 대해 계산된 속성의 스키마를 조회할 수 없습니다.

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

새 계산된 속성을 만들 때 시스템이 요청 페이로드에서 제공하는 스키마를 찾을 수 없을 때 이 오류가 발생합니다. 페이로드 속성에 올바른 테넌트 ID를 제공했는지 `path` 그리고 값이 유효한 스키마 이름 `schema.name` 인지 확인하십시오.

테넌트 ID를 모르는 경우 [스키마 레지스트리 개발자 안내서의 단계에 따라 검색할 수 있습니다](../xdm/api/getting-started.md).

### 지정한 스키마 또는 definedOn에 대해 동일한 이름의 함수가 이미 있습니다.

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

새 계산된 속성을 만들 때 제공된 속성이 이미 아래에 지정된 스키마에 사용되고 있을 때 이 오류가 `name` 발생합니다 `schema.name`. 다시 시도하기 전에 값을 고유한 이름으로 바꾸십시오.

### 식의 반환 스키마가 XDM 스키마의 계산된 속성의 스키마와 같지 않습니다.

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

새 계산된 속성을 만들 때 제공된 속성이 이미 아래에 지정된 스키마에 사용되고 있을 때 이 오류가 `name` 발생합니다 `schema.name`. 다시 시도하기 전에 값을 고유한 이름으로 바꾸십시오.

### 잘못된 삭제 요청(프로필 시스템 작업)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

이 오류는 시스템 삭제 작업에 대해 잘못된 페이로드를 제공했을 때 발생합니다. 페이로드 또는 속성에 올바른 데이터 세트 또는 배치 ID를 각각 제공하는지 `dataSetID` 확인하십시오 `batchID` . 자세한 내용은 프로필 개발자 안내서 [에서 삭제 요청](./api/profile-system-jobs.md#create-a-delete-request) 만들기에 대한 섹션을 참조하십시오.

### 프로필 데이터 세트에 대한 일괄 처리를 찾을 수 없음

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

이 오류는 프로필 데이터에 대한 삭제 요청을 만들려고 시도할 때 올바른 배치를 찾을 수 없을 때 발생합니다. 프로필 사용 데이터 세트에 대한 올바른 ID를 입력했는지 확인한 후 다시 시도하십시오.

### 프로젝션 대상이 아직 만들어지지 않았습니다.

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

이 오류는 요청에 `destinationId` 제공된 것이 잘못된 경우 `POST /config/projections` 발생합니다. 올바른 대상 ID를 제공한 후 다시 시도하십시오. 새 대상을 만들려면 [프로필 개발자 안내서에 설명된 단계를 따르십시오](./api/edge-projections.md#create-a-destination).

### 지원되지 않는 미디어 유형

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

이 오류는 잘못된 Content-Type 헤더로 POST 또는 PUT 요청을 전송할 때 발생합니다. 사용 중인 끝점에 대해 올바른 콘텐츠 형식 값을 제공하는지 다시 확인하십시오.

대부분의 프로필 끝점은 다음 예외를 제외하고 자신의 콘텐츠 형식 헤더에 대해 &quot;application/json&quot;을 허용합니다.

| 끝점 | 컨텐츠 유형 |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;version=1 |