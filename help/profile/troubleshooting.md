---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 실시간 고객 프로필 문제 해결 안내서
topic-legacy: guide
type: Documentation
description: 이 문서에서는 실시간 고객 프로필과 관련하여 자주 묻는 질문에 대한 답변과 Adobe Experience Platform을 사용하여 프로필 데이터를 작업할 때 발생하는 오류에 대한 문제 해결 안내서를 제공합니다.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 실시간 고객 프로필 문제 해결 가이드

이 문서에서는 실시간 고객 프로파일에 대한 FAQ와 일반적인 오류에 대한 문제 해결 안내서를 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

[!DNL Real-time Customer Profile]을 사용하면 온라인, 오프라인, CRM 및 제3자 등 다양한 채널의 데이터를 취합하여 각 개별 고객의 전체 상황을 파악할 수 있습니다. 이를 통해 마케터는 다양한 채널에서 고객의 관심사와 연관성 있고 조율된 경험을 일관되게 제공할 수 있습니다.

## FAQ

다음은 실시간 고객 프로필과 관련하여 자주 묻는 질문에 대한 답변 목록입니다.

### 실시간 고객 프로파일에 허용되는 데이터 유형은 무엇입니까?

해당 데이터에 고유 개인에게 데이터를 연결하는 ID 값이 하나 이상 포함되어 있는 경우 프로필은 **record** 및 **타임 시리즈** 데이터를 모두 허용합니다.

모든 플랫폼 서비스와 마찬가지로, 프로필의 데이터는 XDM(Experience Data Model) 스키마 아래에서 의미있게 구조화되어야 합니다. 따라서 이 스키마는 **기본 ID**&#x200B;가 정의되어 있어야 하며 Profile에서 사용할 수 있도록 활성화되어 있어야 합니다.

XDM에 익숙하지 않은 경우 [XDM 개요](../xdm/home.md)로 시작하여 자세한 내용을 확인하십시오. 다음으로 [ID 필드 설정](../xdm/tutorials/create-schema-ui.md#identity-field) 및 [프로필](../xdm/tutorials/create-schema-ui.md#profile)에 대한 스키마 활성화 방법에 대한 단계는 XDM 사용자 안내서를 참조하십시오.

### 프로필 데이터는 어디에 저장됩니까?

실시간 고객 프로필은 인제스트된 다른 플랫폼 데이터가 포함된 데이터 레이크와 별도로 데이터 저장소(&quot;프로필 스토어&quot;라고 함)를 유지합니다.

### 데이터를 이미 Platform(플랫폼)으로 인제스트한 경우 프로필 스토어에서 사용할 수 있습니까?

데이터를 비프로필 데이터 세트에 인제스트한 경우 프로필 스토어에서 사용할 수 있도록 하려면 해당 데이터를 프로필 사용 데이터 세트에 다시 인제스트해야 합니다. 기존 프로필 데이터 세트를 활성화할 수 있지만 해당 구성 전에 인제스트한 데이터는 여전히 프로필 저장소에 표시되지 않습니다.

이전에 인제스트한 데이터를 프로필 저장소에 추가하려면 [데이터 집합 구성 자습서](./tutorials/dataset-configuration.md)에 따라 새 데이터 집합을 만들거나 기존 데이터 집합을 Profile에서 사용할 수 있도록 변환한 다음 원하는 데이터를 해당 데이터 집합에 다시 인제스트합니다.

### 인제스트한 프로필 데이터를 보려면 어떻게 해야 합니까?

API 사용 여부에 따라 프로필 데이터를 보는 방법에는 여러 가지가 있습니다.

#### API 사용

액세스하려는 프로필 엔터티의 ID를 알고 있는 경우 프로필 API의 `/entities`(프로필 액세스) 끝점을 사용하여 해당 엔터티를 조회할 수 있습니다. 자세한 내용은 개발자 안내서의 [개체](./api/entities.md)에 있는 섹션을 참조하십시오.

Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 멤버십에 자격이 있는 고객의 개별 프로파일에 액세스할 수도 있습니다. 자세한 내용은 [세그멘테이션 서비스 개요](../segmentation/home.md)를 참조하십시오.

#### UI 사용

Experience Platform UI에서 **[!UICONTROL Profiles]** 작업 영역의 **[!UICONTROL Browse]** 탭을 사용하여 총 프로필 수를 보고 ID 값으로 개별 프로필을 검색할 수 있습니다. 자세한 내용은 [프로필 사용 안내서](./ui/user-guide.md)를 참조하십시오.

**[!UICONTROL Segments]** 작업 영역의 **[!UICONTROL Browse]** 탭 아래에 세그먼트 목록을 볼 수도 있습니다. 세그먼트를 선택하면 해당 세그먼트에 자격이 있는 프로필 샘플이 표시됩니다. 그런 다음 이러한 프로파일 중 하나를 선택하여 해당 프로파일을 세부적으로 볼 수 있습니다. 자세한 내용은 [세그멘테이션 UI 개요](../segmentation/ui/overview.md)를 참조하십시오.

## 오류 코드

다음은 실시간 고객 프로필 API를 사용하여 작업할 때 발생할 수 있는 오류 메시지 목록입니다. 여기에 발생한 오류가 표시되지 않으면 일반 [플랫폼 문제 해결 안내서](../landing/troubleshooting.md)에서 해당 오류를 찾을 수 있습니다.

### 제공된 경로에 대해 계산된 속성의 스키마를 조회할 수 없습니다.

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

새 계산된 속성을 만들 때 시스템이 요청 페이로드에서 제공하는 스키마를 찾을 수 없을 때 이 오류가 발생합니다. 페이로드의 `path` 속성에 올바른 테넌트 ID를 입력했는지, `schema.name` 값이 유효한 스키마 이름인지 확인하십시오.

테넌트 ID를 모르는 경우 [스키마 레지스트리 개발자 안내서](../xdm/api/getting-started.md)의 단계에 따라 해당 테넌트를 검색할 수 있습니다.

### 지정된 스키마 또는 definedOn에 대해 동일한 이름의 함수가 이미 있습니다.

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

새 계산된 속성을 만들 때 제공된 `name` 속성이 `schema.name`에 지정된 스키마에 이미 사용되고 있을 때 이 오류가 발생합니다. 다시 시도하기 전에 값을 고유한 이름으로 바꾸십시오.

### 표현식 반환 스키마가 XDM 스키마의 계산된 속성의 스키마와 동일하지 않습니다.

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

새 계산된 속성을 만들 때 제공된 `name` 속성이 `schema.name`에 지정된 스키마에 이미 사용되고 있을 때 이 오류가 발생합니다. 다시 시도하기 전에 값을 고유한 이름으로 바꾸십시오.

### 잘못된 삭제 요청(프로필 시스템 작업)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

이 오류는 시스템 삭제 작업에 대해 잘못된 페이로드가 제공될 때 발생합니다. 페이로드의 `dataSetID` 또는 `batchID` 속성 아래에 올바른 데이터 세트 또는 일괄 처리 ID를 각각 제공해야 합니다. 자세한 내용은 프로필 개발자 안내서의 [삭제 요청 만들기](./api/profile-system-jobs.md#create-a-delete-request)에 대한 섹션을 참조하십시오.

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

이 오류는 프로필 데이터에 대한 삭제 요청을 만들려고 시도할 때 유효한 배치를 찾을 수 없을 때 발생합니다. 다시 시도하기 전에 프로필 사용 데이터 세트에 대한 올바른 ID를 입력했는지 확인하십시오.

### 투영 대상이 아직 생성되지 않았습니다.

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

이 오류는 `POST /config/projections` 요청에 제공된 `destinationId`이(가) 잘못된 경우에 발생합니다. 다시 시도하기 전에 올바른 대상 ID를 제공했는지 다시 확인하십시오. 새 대상을 만들려면 [프로필 개발자 안내서](./api/edge-projections.md#create-a-destination)에 설명된 단계를 따르십시오.

### 지원되지 않는 미디어 유형

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

이 오류는 잘못된 Content-Type 헤더로 POST 또는 PUT 요청을 보낼 때 발생합니다. 사용 중인 끝점에 대해 올바른 콘텐츠 형식 값을 제공하는지 다시 확인하십시오.

대부분의 프로필 끝점은 다음 예외를 제외하고 자신의 콘텐츠 형식 헤더에 대해 &quot;application/json&quot;을 허용합니다.

| 끝점 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;version=1 |
