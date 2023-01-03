---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 실시간 고객 프로필 문제 해결 안내서
topic-legacy: guide
type: Documentation
description: 이 문서에서는 실시간 고객 프로필에 대해 자주 묻는 질문에 대한 답변과 Adobe Experience Platform을 사용하여 프로필 데이터를 작업할 때 일반적인 오류에 대한 문제 해결 안내서를 제공합니다.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 실시간 고객 프로필 문제 해결 안내서

이 문서에서는 실시간 고객 프로필에 대해 자주 묻는 질문과 일반적인 오류에 대한 문제 해결 안내서를 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결은 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

사용 [!DNL Real-Time Customer Profile]를 사용하면 온라인, 오프라인, CRM 및 타사 등 여러 채널의 데이터를 결합하여 각 개별 고객을 전체적으로 확인할 수 있습니다. 이를 통해 마케터는 여러 채널에서 고객을 위해 조정되고 일관되고 적절한 경험을 제공할 수 있습니다.

## FAQ

다음은 실시간 고객 프로필에 대해 자주 묻는 질문에 대한 답변 목록입니다.

### 실시간 고객 프로필에는 어떤 종류의 데이터가 수락됩니까?

프로필은 두 가지를 모두 허용합니다 **레코드** 및 **시계열** 데이터에 고유한 개인 사용자와 연결하는 하나 이상의 ID 값이 포함되어 있는 한, 데이터에 있는 모든 데이터가 있어야 합니다.

모든 플랫폼 서비스와 마찬가지로, 프로필도 데이터를 XDM(Experience Data Model) 스키마 아래에 의미상 구조화해야 합니다. 따라서 이 스키마에는 **기본 ID** 정의되며 프로필에서 사용할 수 있습니다.

XDM에 익숙하지 않다면 [XDM 개요](../xdm/home.md) 추가 정보 다음으로, 방법에 대한 절차를 알려면 XDM 사용 안내서 를 참조하십시오 [id 필드 설정](../xdm/tutorials/create-schema-ui.md#identity-field) 및 [프로필에 대한 스키마 활성화](../xdm/tutorials/create-schema-ui.md#profile).

### 프로필 데이터는 어디에 저장됩니까?

실시간 고객 프로필은 수집된 다른 플랫폼 데이터가 포함된 데이터 레이크와 별도로 자체 데이터 저장소(&quot;프로필 저장소&quot;라고 함)를 유지 관리합니다.

### 이미 Platform에 데이터를 수집한 경우 프로필 스토어에서 사용할 수 있습니까?

데이터가 비프로필 데이터 세트에 수집된 경우 프로필 저장소에서 사용할 수 있도록 하려면 해당 데이터를 프로필 사용 데이터 세트에 다시 수집해야 합니다. 프로필에 대해 기존 데이터 세트를 활성화할 수 있지만, 해당 구성 전에 수집된 데이터는 여전히 프로필 저장소에 표시되지 않습니다.

이전에 수집된 데이터를 프로필 저장소에 추가하려면 다음을 수행하십시오. [데이터 세트 구성 자습서](./tutorials/dataset-configuration.md) 새 데이터 세트를 만들거나 기존 데이터 세트를 프로필에 사용할 수 있도록 전환한 다음 원하는 데이터를 해당 데이터 세트에 다시 인제스트합니다.

### 수집된 프로필 데이터를 보려면 어떻게 해야 합니까?

API를 사용하는지 또는 UI를 사용하는지에 따라 프로필 데이터를 보는 방법에는 여러 가지가 있습니다.

#### API 사용

액세스하려는 프로필 엔티티의 ID를 알고 있는 경우 `/entities` (프로필 액세스) 종단점을 사용하여 해당 엔티티를 조회합니다. 의 섹션을 참조하십시오. [개체](./api/entities.md) 를 참조하십시오.

Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 멤버십에 자격이 있는 고객의 개별 프로필에 액세스할 수도 있습니다. 자세한 내용은 [세그먼테이션 서비스 개요](../segmentation/home.md) 추가 정보.

#### UI 사용

Experience Platform UI에서 **[!UICONTROL 찾아보기]** 탭에서 다음을 수행합니다. **[!UICONTROL 프로필]** workspace를 사용하면 총 프로필 수를 보고 id 값으로 개별 프로필을 검색할 수 있습니다. 자세한 내용은 [프로필 사용 안내서](./ui/user-guide.md) 추가 정보.

또한 **[!UICONTROL 찾아보기]** 탭에서 다음을 수행합니다. **[!UICONTROL 세그먼트]** 작업 공간. 세그먼트를 선택하면 해당 세그먼트에 적합한 프로필 샘플이 표시됩니다. 그런 다음 나열된 프로필 중 하나를 선택하여 세부 정보를 볼 수 있습니다. 자세한 내용은 [세그먼테이션 UI 개요](../segmentation/ui/overview.md) 추가 정보.

## 오류 코드

다음은 실시간 고객 프로필 API를 사용하여 작업할 때 발생할 수 있는 오류 메시지 목록입니다. 표시되는 오류가 여기에 나열되지 않으면 일반적으로 찾을 수 있습니다 [플랫폼 문제 해결 안내서](../landing/troubleshooting.md) 을 가리키도록 업데이트하는 것이 좋습니다.

### 제공된 경로에 대해 계산된 특성의 스키마를 조회할 수 없습니다

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

새 계산된 속성을 만들 때 시스템이 요청 페이로드에 제공된 스키마를 찾을 수 없을 때 이 오류가 발생합니다. 페이로드의 `path` 속성 및 `schema.name` 는 유효한 스키마 이름입니다.

임차인 ID를 모를 경우 [스키마 레지스트리 개발자 안내서](../xdm/api/getting-started.md).

### 지정한 스키마 또는 definedOn에 대해 같은 이름의 함수가 이미 있습니다.

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

새 계산된 속성을 만들 때 제공된 `name` 속성이 이미 `schema.name`. 다시 시도하기 전에 값을 고유한 이름으로 바꾸십시오.

### 식의 반환 스키마가 XDM 스키마에 있는 계산된 특성의 스키마와 다릅니다

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

새 계산된 속성을 만들 때 제공된 `name` 속성이 이미 `schema.name`. 다시 시도하기 전에 값을 고유한 이름으로 바꾸십시오.

### 잘못된 삭제 요청(프로필 시스템 작업)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

시스템 삭제 작업에 대해 잘못된 페이로드를 제공하면 이 오류가 발생합니다. 페이로드 아래에 올바른 데이터 세트 또는 배치 ID를 제공하는지 확인합니다 `dataSetID` 또는 `batchID` 각각 Null 포인터 예외가 발생합니다. 의 섹션을 참조하십시오. [삭제 요청 만들기](./api/profile-system-jobs.md#create-a-delete-request) 자세한 내용은 프로필 개발자 안내서를 참조하십시오.

### 프로필 데이터 세트에 대한 일괄 처리를 찾을 수 없습니다.

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

이 오류는 프로필 데이터에 대한 삭제 요청을 만들 때 유효한 배치를 찾을 수 없을 때 발생합니다. 다시 시도하기 전에 프로필 사용 데이터 세트에 올바른 ID를 입력했는지 확인합니다.

### 투영 대상이 아직 생성되지 않았습니다.

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

이 오류는 `destinationId` 에서 제공 `POST /config/projections` 요청이 잘못되었습니다. 올바른 대상 ID를 제공한 후 다시 시도하십시오. 새 대상을 만들려면 [프로필 개발자 안내서](./api/edge-projections.md#create-a-destination).

### 지원되지 않는 미디어 유형

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

이 오류는 잘못된 Content-Type 헤더로 POST 또는 PUT 요청을 보낼 때 발생합니다. 사용 중인 끝점에 유효한 Content-Type 값을 제공하는지 다시 확인하십시오.

대부분의 프로필 엔드포인트는 다음 예외를 제외하고 Content-Type 헤더에 대해 &quot;application/json&quot;을 허용합니다.

| 끝점 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
