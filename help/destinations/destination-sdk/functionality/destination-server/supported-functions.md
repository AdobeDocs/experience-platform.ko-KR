---
description: Experience Platform Destination SDK은 페블 템플릿을 사용하므로 Experience Platform에서 내보낸 데이터를 대상에 필요한 형식으로 변환할 수 있습니다.
title: Destination SDK에서 지원되는 변환 함수
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---


# Destination SDK에서 지원되는 변환 함수

Experience Platform Destination SDK 사용 [[!DNL Pebble] 템플릿](https://pebbletemplates.io/)를 사용하면 Experience Platform에서 내보낸 데이터를 대상에 필요한 형식으로 변환할 수 있습니다.

Experience Platform [!DNL Pebble] 에서 제공하는 기본 버전에 비해 구현에는 몇 가지 변경 사항이 있습니다. [!DNL Pebble]. 또한 기본 제공 기능 외에도 [!DNL Pebble], Adobe에서 Destination SDK과 함께 사용할 수 있는 몇 가지 추가 기능을 만들었습니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 사용 위치 {#where-to-use}

다음과 같은 경우 이 페이지의 아래에 나열된 지원되는 함수를 사용하십시오. [메시지 변환 템플릿 만들기](../../testing-api/streaming-destinations/create-template.md) Experience Platform에서 대상으로 내보낸 데이터입니다.

메시지 변환 템플릿은에서 사용됩니다. [대상 서버 구성](templating-specs.md) 스트리밍 대상용입니다.

## 사전 요구 사항 {#prerequisites}

이 참조 페이지의 개념과 기능을 이해하려면 [메시지 포맷](message-format.md) 문서 먼저. 다음을 이해해야 합니다. [프로필 구조](message-format.md#profile-structure) 을(를) 사용하기 전에 Experience Platform에서 [!DNL Pebble] 및 내보낸 데이터를 변환할 템플릿.

아래 문서화된 기능으로 이동하기 전에 섹션의 템플릿 예를 검토하십시오 [ID, 속성 및 세그먼트 멤버십 변환에 템플릿 언어 사용](message-format.md#using-templating). 이 예제들의 시작은 매우 간단하고 복잡성이 증가합니다.

## 지원됨 [!DNL Pebble] 함수 {#supported-functions}

다음에서 [!DNL Pebble] 태그 섹션의 Destination SDK은 다음 항목만 지원합니다.

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [설정됨](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>사용 `for` 다음을 반복할 때 다름 *배열* 또는 *맵* 템플릿에 있는 요소입니다. 배열을 반복할 때 요소를 직접 가져올 수 있습니다. 맵을 반복하면 키-값 쌍을 가지는 각 맵 항목을 얻습니다.
>
> * 배열 요소의 예제를 보려면 [identityMap](message-format.md#identities) 네임스페이스: 다음과 같은 요소를 반복할 수 있습니다. `identityMap.gaid`, `identityMap.email`또는 이와 유사한 형식으로 프로필 스크립트에서 참조할 수 있습니다.
> * 맵 요소의 예제에 대해 생각해 보십시오 [segmentMembership](message-format.md#segment-membership).


다음에서 [!DNL Pebble] 필터 섹션, Destination SDK은 모든 함수를 지원합니다. 아래 예는 다음 방법을 보여 줍니다. `date` 함수는 Destination SDK 내에서 사용할 수 있습니다.

다음에서 [!DNL Pebble] 함수 섹션, Adobe *아님* 지원 [범위](https://pebbletemplates.io/wiki/function/range/) 함수.

## 방법 예 `date` 함수 사용 {#date-function}

방법을 예시 [!DNL Pebble] 함수는 Destination SDK에서 사용되며 아래 날짜 함수([자갈 설명서의 링크](https://pebbletemplates.io/wiki/filter/date/))는 타임스탬프의 형식을 변환하는 데 사용됩니다.

### 사용 사례

을(를) 변경하려는 경우 `lastQualificationTime` 기본의 타임스탬프 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) Experience Platform이 내보내는 값을 대상이 선호하는 다른 값으로 설정합니다.

### 예

#### 입력

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### 형식

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### 출력

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Adobe이 추가한 함수 {#functions-added-by-adobe}

기본 제공 기능 외에도 [!DNL Pebble]에서 데이터 내보내기에 사용할 수 있는 Adobe에서 만든 추가 함수 를 아래를 참조하십시오.

### `addedSegments` 및 `removedSegments` 함수 {#addedsegments-removedsegments-functions}

#### 사용 사례

이러한 함수는 프로필에 추가되거나 제거된 세그먼트 목록을 가져올 때 사용할 수 있습니다.

#### 예

##### 입력

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### 형식

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### 출력

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## 다음 단계 {#next-steps}

이제 다음 항목을 알 수 있습니다. [!DNL Pebble] 함수는 Destination SDK에서 지원되며, 함수를 사용하여 사용자의 요구 사항에 맞게 내보낸 데이터의 형식을 조정하는 방법도 있습니다. 그런 다음 다음 다음 페이지를 검토해야 합니다.

* [메시지 변형 템플릿 만들기 및 테스트](../../testing-api/streaming-destinations/create-template.md)
* [템플릿 API 작업 렌더링](../../testing-api/streaming-destinations/render-template-api.md)
