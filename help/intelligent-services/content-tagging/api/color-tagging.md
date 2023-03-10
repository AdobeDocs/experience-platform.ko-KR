---
keywords: Experience Platform;시작하기;콘텐츠 ai;상거래 ai;콘텐츠 태그 지정;색상 태그 지정;색상 추출;
solution: Experience Platform
title: 콘텐츠 태깅 API의 색상 태깅
description: 색상 태깅 서비스는 이미지가 제공되면 픽셀 색상의 히스토그램을 계산하고 주요 색상별로 버킷으로 정렬할 수 있습니다.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 색상 태깅

색상 태깅 서비스는 이미지가 제공되면 픽셀 색상의 히스토그램을 계산하고 주요 색상별로 버킷으로 정렬할 수 있습니다. 이미지 픽셀의 색상은 색상 스펙트럼을 나타내는 40개의 주요 색상으로 그룹화됩니다. 그런 다음 40개 색상 중에서 색상 값의 히스토그램이 계산됩니다. 이 서비스에는 두 가지 변형이 있습니다.

**색상 태그 지정(전체 이미지)**

이 방법은 전체 이미지에서 색상 히스토그램을 추출합니다.

**색상 태깅(마스크 사용)**

이 방법은 딥러닝 기반 전경 추출기를 사용하여 전경에서 오브젝트를 식별한다. 모델은 전자 상거래 이미지 카탈로그에 대해 교육됩니다. 전경 객체가 추출되면 앞에서 설명한 대로 지배적인 색상에 대해 히스토그램이 계산됩니다.

이 문서에 표시된 예에는 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/QQAsset1.jpg)

**API 형식**

```http
POST /services/v2/predict
```

**요청**

다음 예제 요청에서는 색상 태깅에 전체 이미지 메서드를 사용합니다.

다음 요청은 페이로드에 제공된 입력 매개변수를 기반으로 이미지에서 색상을 추출합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `application-id` | 생성된 애플리케이션의 ID. | 예 |
| `documents` | 목록의 각 항목이 하나의 문서를 나타내는 JSON 요소 목록입니다. | 예 |
| `top_n` | 반환할 결과 수(음수가 될 수 없음). 값 사용 `0` 모든 결과를 반환합니다. 과 함께 사용할 때 `threshold`반환된 결과 수가 설정된 제한 중 더 적습니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `min_coverage` | 결과를 반환해야 하는 적용 범위의 임계값. 매개 변수를 제외하여 모든 결과를 반환합니다. | 아니요 |
| `resize_image` | 입력 이미지의 크기를 조정할지 여부를 나타냅니다. 기본적으로 색상 태깅을 수행하기 전에 이미지 크기가 320*320픽셀로 조정됩니다. 디버깅 목적을 위해 False로 설정하여 코드가 전체 이미지에서도 실행되도록 할 수 있습니다. | 아니요 |
| `enable_mask` | 마스크 내의 색상 태그 지정을 활성화/비활성화합니다. | 아니요 |

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 문자열 | - | - | - | 주요 구문을 추출할 문서의 사전 서명된 URL입니다. |
| `sensei:repoType` | 문자열 | - | - | HTTPS | 이미지가 저장되는 저장소의 유형입니다. |
| `sensei:multipart_field_name` | 문자열 | - | - | - | 사전 서명된 URL을 사용하는 대신 이미지 파일을 다중 부분 인수로 전달할 때 사용합니다. |
| `dc:format` | 문자열 | 예 | - | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | 이미지 인코딩이 처리되기 전에 허용된 입력 인코딩 유형에 대해 확인됩니다. |

**응답**

성공한 응답은 추출된 색상의 세부 정보를 반환합니다. 각 색상은 `feature_value` 키: 다음 정보가 들어 있습니다.

- 색상 이름
- 이미지를 기준으로 이 색상이 표시되는 비율
- 색상의 RGB 값

아래의 첫 번째 예제 객체에서 `feature_value` / `Mud_Green,0.069,102,72,95` 은 찾은 색상이 진녹색임을 의미하며, 진녹색은 이미지의 6.9%에서 발견되며, 102,72,95의 RGB 값을 갖습니다.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
      "invocations": [
        {
          "sensei:outputs": {
            "result": {
              "sensei:multipart_field_name": "result",
              "dc:format": "application/json"
            }
          },
          "message": null,
          "status": "200"
        }
      ]
    }
  ],
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
