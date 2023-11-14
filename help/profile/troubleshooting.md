---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 실시간 고객 프로필 문제 해결 안내서
type: Documentation
description: 이 문서에서는 실시간 고객 프로필에 대해 자주 묻는 질문에 대한 답변과 Adobe Experience Platform을 사용하여 프로필 데이터 작업 시 발생하는 일반적인 오류에 대한 문제 해결 안내서를 제공합니다.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 실시간 고객 프로필 문제 해결 안내서

이 문서에서는 실시간 고객 프로필에 대해 자주 묻는 질문에 대한 답변과 일반적인 오류에 대한 문제 해결 안내서를 제공합니다. Adobe Experience Platform의 기타 서비스와 관련된 질문 및 문제 해결은 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

포함 [!DNL Real-Time Customer Profile]에서는 온라인, 오프라인, CRM 및 서드파티를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 이를 통해 마케터는 여러 채널에서 고객을 위해 조정되고 일관되며 관련 있는 경험을 제공할 수 있습니다.

## FAQ

다음은 실시간 고객 프로필에 대한 FAQ 응답 목록입니다.

### 실시간 고객 프로필에는 어떤 종류의 데이터가 허용됩니까?

프로필에서 둘 다 수락 **기록** 및 **시계열** 해당 데이터에 고유한 개별 사용자와 데이터를 연결하는 id 값이 하나 이상 포함되어 있는 한 데이터도 마찬가지입니다.

모든 Platform 서비스와 마찬가지로 Profile은 데이터를 XDM(Experience Data Model) 스키마에서 의미론적으로 구조화해야 합니다. 결과적으로 이 스키마에는 **기본 ID** 을(를) 정의하고 프로필에서 사용할 수 있도록 설정합니다.

XDM에 익숙하지 않은 경우 [XDM 개요](../xdm/home.md) 자세히 알아보십시오. 다음으로, XDM 사용 안내서 를 참조하십시오. [id 필드 설정](../xdm/tutorials/create-schema-ui.md#identity-field) 및 [프로필에 대한 스키마 활성화](../xdm/tutorials/create-schema-ui.md#profile).

### 프로필 데이터는 어디에 저장되어 있습니까?

실시간 고객 프로필은 수집된 다른 플랫폼 데이터를 포함하는 데이터 레이크와 별도로 자체 데이터 저장소(이하 &quot;프로필 저장소&quot;)를 유지 관리합니다.

### 이미 데이터를 Platform으로 수집한 경우 Profile Store에서 사용할 수 있도록 할 수 있습니까?

비프로필 데이터 세트로 데이터가 수집된 경우 해당 데이터를 프로필 스토어에서 사용할 수 있도록 하려면 해당 데이터를 프로필 활성화 데이터 세트로 다시 수집해야 합니다. 프로필에 대해 기존 데이터 세트를 활성화할 수 있지만, 해당 구성 전에 수집된 데이터는 여전히 프로필 스토어에 표시되지 않습니다.

이전에 수집된 데이터를 프로필 스토어에 추가하려면 다음을 수행합니다. [데이터 세트 구성 자습서](./tutorials/dataset-configuration.md) 새 데이터 세트를 만들거나 프로필에 대해 사용할 수 있도록 기존 데이터 세트를 변환한 다음 원하는 데이터를 해당 데이터 세트로 다시 수집합니다.

### 수집된 프로필 데이터는 어떻게 볼 수 있습니까?

API를 사용하는지 UI를 사용하는지에 따라 프로필 데이터를 보는 방법은 여러 가지가 있습니다.

#### API 사용

액세스하려는 프로필 엔티티의 ID를 알고 있는 경우 `/entities` (프로필 액세스) 프로필 API의 끝점으로 해당 엔터티를 조회합니다. 의 섹션을 참조하십시오. [엔티티](./api/entities.md) 자세한 내용은 개발자 안내서를 참조하십시오.

또한 Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 대상 멤버십에 대한 자격이 있는 고객의 개별 프로필에 액세스할 수도 있습니다. 다음을 참조하십시오. [세그먼테이션 서비스 개요](../segmentation/home.md) 추가 정보.

#### UI 사용

Experience Platform UI에서 **[!UICONTROL 찾아보기]** 의 탭 **[!UICONTROL 프로필]** 작업 공간에서는 총 프로필 수를 보고 id 값으로 개별 프로필을 검색할 수 있습니다. 다음을 참조하십시오. [프로필 사용 안내서](./ui/user-guide.md) 추가 정보.

또한 아래에서 대상자 목록을 볼 수도 있습니다. **[!UICONTROL 찾아보기]** 의 탭 **[!UICONTROL 대상]** 작업 영역. 대상을 선택하면 해당 대상에 적합한 프로필 샘플이 표시됩니다. 그런 다음 나열된 프로필 중 하나를 선택하여 세부 정보를 볼 수 있습니다. 다음을 참조하십시오. [세그멘테이션 UI 개요](../segmentation/ui/overview.md) 추가 정보.

## 오류 코드

다음은 실시간 고객 프로필 API로 작업할 때 발생할 수 있는 오류 메시지 목록입니다. 오류가 여기에 나열되지 않으면 일반에서 찾을 수 있습니다 [플랫폼 문제 해결 안내서](../landing/troubleshooting.md) 대신,

### 제공된 경로에 대해 계산된 특성의 스키마를 조회할 수 없음

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

새 계산된 속성을 만들 때 시스템이 요청 페이로드에 제공된 스키마를 찾을 수 없을 때 이 오류가 발생합니다. 페이로드에 올바른 테넌트 ID를 입력했는지 확인합니다. `path` 속성 및 그 값 `schema.name` 은(는) 유효한 스키마 이름입니다.

테넌트 ID를 모를 경우 의 단계에 따라 검색할 수 있습니다. [스키마 레지스트리 개발자 안내서](../xdm/api/getting-started.md).

### 지정한 스키마 또는 definedOn에 이름이 같은 함수가 이미 있습니다.

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

새 계산된 속성을 만들 때 이 오류는 제공된 `name` 속성은 아래에 표시된 스키마에 이미 사용되고 있습니다. `schema.name`. 값을 고유한 이름으로 바꾼 후 다시 시도하십시오.

### 표현식의 반환 스키마가 XDM 스키마에서 계산된 속성의 스키마와 동일하지 않습니다.

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

새 계산된 속성을 만들 때 이 오류는 제공된 `name` 속성은 아래에 표시된 스키마에 이미 사용되고 있습니다. `schema.name`. 값을 고유한 이름으로 바꾼 후 다시 시도하십시오.

### 잘못된 삭제 요청(프로필 시스템 작업)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

이 오류는 시스템 삭제 작업에 잘못된 페이로드가 제공되었을 때 발생합니다. 페이로드의 아래에 유효한 데이터 세트 또는 배치 ID를 제공하는지 확인합니다. `dataSetID` 또는 `batchID` 각각 속성입니다. 의 섹션을 참조하십시오. [삭제 요청 만들기](./api/profile-system-jobs.md#create-a-delete-request) 자세한 내용은 프로필 개발자 안내서를 참조하십시오.

### 프로필 데이터 세트에 대한 배치를 찾을 수 없음

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

이 오류는 프로필 데이터에 대한 삭제 요청을 만들 때 유효한 일괄 처리를 찾을 수 없을 때 발생합니다. 프로필 사용 데이터 세트에 대한 올바른 ID를 입력했는지 확인한 후 다시 시도하십시오.

### 프로젝션 대상이 아직 생성되지 않았습니다.

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

이 오류는 다음 경우에 발생합니다. `destinationId` 에 제공됨 `POST /config/projections` 요청이 잘못되었습니다. 유효한 대상 ID를 입력했는지 다시 한 번 확인하십시오. 새 대상을 만들려면 다음에 설명된 단계를 수행합니다. [프로필 개발자 안내서](./api/edge-projections.md#create-a-destination).

### 지원되지 않는 미디어 유형

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

이 오류는 잘못된 Content-Type 헤더가 있는 POST 또는 PUT 요청을 보낼 때 발생합니다. 사용 중인 끝점에 대해 유효한 Content-Type 값을 제공하고 있는지 다시 확인합니다.

대부분의 프로필 엔드포인트는 콘텐츠 유형 헤더에 &quot;application/json&quot;을 허용하며 다음과 같은 경우는 예외입니다.

| 엔드포인트 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; 버전=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; 버전=1 |
