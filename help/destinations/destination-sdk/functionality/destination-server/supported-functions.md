---
description: Experience Platform Destination SDK은 페블 템플릿을 사용하여 Experience Platform에서 내보낸 데이터를 대상에 필요한 형식으로 변환할 수 있습니다.
title: Destination SDK에서 지원되는 변형 함수
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---


# Destination SDK에서 지원되는 변형 함수

Experience Platform Destination SDK 사용 [[!DNL Pebble] 템플릿](https://pebbletemplates.io/)Experience Platform에서 내보낸 데이터를 대상에 필요한 형식으로 변환할 수 있습니다.

Experience Platform [!DNL Pebble] 구현에는 [!DNL Pebble]. 또한, [!DNL Pebble], Adobe은 Destination SDK과 함께 사용할 수 있는 몇 가지 추가 기능을 만들었습니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 사용 위치 {#where-to-use}

다음의 경우에 이 페이지에서 지원되는 함수를 사용하십시오 [메시지 변환 템플릿 만들기](../../testing-api/streaming-destinations/create-template.md) Experience Platform에서 대상으로 내보낸 데이터의 경우입니다.

메시지 변환 템플릿은 [대상 서버 구성](templating-specs.md) 스트리밍 대상

## 사전 요구 사항 {#prerequisites}

이 참조 페이지의 개념과 함수를 이해하려면 다음을 참조하십시오 [메시지 형식](message-format.md) 먼저 문서를 작성합니다. 다음을 이해해야 합니다 [프로필의 구조](message-format.md#profile-structure) 를 사용 전에 Experience Platform에서 [!DNL Pebble] 및 내보낸 데이터를 변환하는 템플릿입니다.

아래 설명된 기능으로 이동하기 전에 섹션에서 템플릿 예제를 검토하십시오 [ID, 속성 및 세그먼트 멤버십 변환에 템플릿 언어 사용](message-format.md#using-templating). 그곳의 예들은 매우 간단하고 복잡성이 증가하기 시작합니다.

## 지원됨 [!DNL Pebble] 함수 {#supported-functions}

에서 [!DNL Pebble] 태그 섹션, Destination SDK은 다음과 같은 경우에만 지원합니다.

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [설정됨](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>사용 `for` 는 를 반복할 때 다릅니다 *배열* 또는 *맵* 템플릿의 요소입니다. 배열을 반복할 때 요소를 직접 가져올 수 있습니다. 맵을 반복하면 키-값 쌍이 있는 각 맵 항목을 얻습니다.
>
> * 배열 요소의 예를 보려면 [identityMap](message-format.md#identities) 네임스페이스, 다음과 같은 요소를 반복할 수 있습니다. `identityMap.gaid`, `identityMap.email`또는 과 비슷합니다.
> * 맵 요소의 예는 다음과 같습니다 [segmentMembership](message-format.md#segment-membership).


에서 [!DNL Pebble] 필터 섹션, Destination SDK은 모든 함수를 지원합니다. 아래 추가 예는 `date` 함수는 Destination SDK 내에서 사용할 수 있습니다.

에서 [!DNL Pebble] 함수 섹션, Adobe 기능 *not* 지원 [범위](https://pebbletemplates.io/wiki/function/range/) 함수 위에 있어야 합니다.

## 방법의 예 `date` 함수가 사용됨 {#date-function}

어떻게 [!DNL Pebble] 함수는 Destination SDK에서 사용되며 날짜 함수([페블 설명서에 연결](https://pebbletemplates.io/wiki/filter/date/))을 사용하여 타임스탬프의 형식을 변형합니다.

### 사용 사례

을(를) 변경하려는 경우 `lastQualificationTime` 기본 타임스탬프 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) Experience Platform이 대상에서 선호하는 다른 값으로 내보내는 값입니다.

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

## Adobe에 의해 추가된 함수 {#functions-added-by-adobe}

에서 제공하는 기본 함수 외에도 [!DNL Pebble]데이터 내보내기에 사용할 수 있는 Adobe에서 만든 추가 기능 아래를 참조하십시오.

### `addedSegments` 및 `removedSegments` 함수 {#addedsegments-removedsegments-functions}

#### 사용 사례

이러한 함수를 사용하여 프로필에 추가되거나 프로필에서 제거된 세그먼트 목록을 가져올 수 있습니다.

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

이제 누가 [!DNL Pebble] 함수는 Destination SDK에서 지원되며, 함수를 사용하여 필요에 따라 내보낸 데이터의 형식을 조정하는 방법을 설명합니다. 다음으로, 다음 페이지를 검토해야 합니다.

* [메시지 변환 템플릿 만들기 및 테스트](../../testing-api/streaming-destinations/create-template.md)
* [템플릿 API 작업 렌더링](../../testing-api/streaming-destinations/render-template-api.md)
