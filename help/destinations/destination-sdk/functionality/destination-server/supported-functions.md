---
description: Experience Platform Destination SDK은 페블 템플릿을 사용하므로 Experience Platform에서 내보낸 데이터를 대상에 필요한 형식으로 변환할 수 있습니다.
title: Destination SDK에서 지원되는 변환 함수
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# Destination SDK에서 지원되는 변환 함수

Experience Platform Destination SDK은 [[!DNL Pebble] 템플릿](https://pebbletemplates.io/)을(를) 사용하므로 Experience Platform에서 내보낸 데이터를 대상에 필요한 형식으로 변환할 수 있습니다.

[!DNL Pebble]에서 제공한 기본 버전에 비해 Experience Platform [!DNL Pebble] 구현에 일부 변경 내용이 있습니다. 또한 [!DNL Pebble]에서 제공하는 기본 함수 외에 Adobe에서 Destination SDK에 사용할 수 있는 몇 가지 추가 함수를 만들었습니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 사용 위치 {#where-to-use}

Experience Platform에서 대상에 내보낸 데이터에 대해 [메시지 변환 템플릿을 만드는 중](../../testing-api/streaming-destinations/create-template.md)일 때 이 페이지의 아래에 나열된 지원되는 함수를 사용하십시오.

메시지 변환 템플릿은 스트리밍 대상의 [대상 서버 구성](templating-specs.md)에서 사용됩니다.

## 전제 조건 {#prerequisites}

이 참조 페이지의 개념과 기능을 이해하려면 먼저 [메시지 형식](message-format.md) 문서를 읽으십시오. [!DNL Pebble] 템플릿을 사용하여 및 내보낸 데이터를 변환하려면 먼저 Experience Platform의 [프로필 구조](message-format.md#profile-structure)를 이해해야 합니다.

아래 문서화된 함수로 이동하기 전에 [ID, 특성 및 대상자 멤버십 변환에 대한 템플릿 언어 사용](message-format.md#using-templating) 섹션에서 템플릿 예제를 검토하십시오. 이 예제들의 시작은 매우 간단하고 복잡성이 증가합니다.

## 지원되는 [!DNL Pebble]개 함수 {#supported-functions}

[!DNL Pebble] 태그 섹션에서 Destination SDK은 다음만 지원합니다.

* [필터](https://pebbletemplates.io/wiki/tag/filter/)
* [대상](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [설정](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>템플릿에서 *array* 또는 *map* 요소를 반복할 때 `for`을(를) 사용하는 방법은 다릅니다. 배열을 반복할 때 요소를 직접 가져올 수 있습니다. 맵을 반복하면 키-값 쌍을 가지는 각 맵 항목을 얻습니다.
>
> * 배열 요소의 예로 [identityMap](message-format.md#identities) 네임스페이스의 ID에 대해 생각해 보십시오. 여기서 `identityMap.gaid`, `identityMap.email` 등의 요소를 반복할 수 있습니다.
> * 맵 요소의 예를 보려면 [segmentMembership](message-format.md#segment-membership)을 생각해 보십시오.

[!DNL Pebble] 필터 섹션에서 Destination SDK은 모든 함수를 지원합니다. 아래 예제에서는 Destination SDK 내에서 `date` 함수를 사용하는 방법을 보여 줍니다.

[!DNL Pebble] 함수 섹션에서 Adobe은 [범위](https://pebbletemplates.io/wiki/function/range/) 함수를 지원하지 *않습니다*.

## `date` 함수 사용 방법의 예 {#date-function}

Destination SDK에서 [!DNL Pebble] 함수가 사용되는 방법을 예증하려면 아래 날짜 함수([Pebble 설명서의 링크](https://pebbletemplates.io/wiki/filter/date/))를 사용하여 타임스탬프의 형식을 변환하는 방법을 참조하십시오.

### 활용 사례

`lastQualificationTime` 타임스탬프를 Experience Platform이 내보내는 기본 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 값에서 대상이 선호하는 다른 값으로 변경하려고 합니다.

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

[!DNL Pebble]에서 제공하는 기본 함수 외에 데이터 내보내기에 사용할 수 있는 Adobe에서 만든 추가 함수 아래를 참조하십시오.

### `addedSegments` 및 `removedSegments` 함수 {#addedsegments-removedsegments-functions}

#### 활용 사례

이러한 함수는 프로필에 추가되거나 제거된 대상자 목록을 가져올 때 사용할 수 있습니다.

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

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

이제 Destination SDK에서 지원되는 [!DNL Pebble] 함수와 이러한 함수를 사용하여 필요에 맞게 내보낸 데이터의 형식을 조정하는 방법을 알 수 있습니다. 그런 다음 다음 다음 페이지를 검토해야 합니다.

* [메시지 변형 템플릿 만들기 및 테스트](../../testing-api/streaming-destinations/create-template.md)
* [템플릿 API 작업 렌더링](../../testing-api/streaming-destinations/render-template-api.md)
