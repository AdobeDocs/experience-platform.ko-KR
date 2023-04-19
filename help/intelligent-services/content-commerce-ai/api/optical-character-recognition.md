---
keywords: OCR;텍스트 유무;광학 문자 인식
solution: Experience Platform
title: 텍스트 유무 및 광학 문자 인식
description: 콘텐츠 태깅 API에서 텍스트 존재/OCR(Optical Character Recognition) 서비스는 지정된 이미지에 텍스트가 있는지 여부를 나타낼 수 있습니다. 텍스트가 있으면 OCR에서 텍스트를 반환할 수 있습니다.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# 텍스트 유무 및 광학 문자 인식

이미지가 지정된 경우 텍스트 존재/OCR(광학 문자 인식) 서비스는 이미지에 텍스트가 있는지 여부를 나타낼 수 있습니다. 텍스트가 있으면 OCR에서 텍스트를 반환할 수 있습니다.

이 문서에 표시된 예제 요청에서 다음 이미지가 사용되었습니다.

![샘플 이미지](../images/sample_image.png)

**API 형식**

```http
POST /services/v2/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 이미지를 기반으로 텍스트가 있는지 확인합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

인라인 이미지로 실행:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**응답**

성공적인 응답에는 `tags` 요청에서 전달된 각 이미지에 대한 목록입니다. 특정 이미지에 텍스트가 없다면, `is_text_present` 0이고 `tags` 는 빈 목록입니다.

[result0, result1,..]: 각 입력 문서에 대한 응답 목록입니다. 각 결과는 키가 있는 딕트입니다.

1. request_element_id: 이 응답에 대한 입력 파일에 해당하는 인덱스, 요청의 문서 목록에 있는 첫 번째 이미지에 대한 0, 다음 이미지에 대한 1 등이 있습니다.
2. 태그: 사전 목록 각 사전에는 두 개의 키가 있습니다. 이미지에서 인식할 수 있는 단어인 텍스트 및 관련성이 있으며, 전체 이미지와 비교하여 추출된 텍스트 테두리 상자의 영역 비율로 계산됩니다. 0.01은 이미지의 적어도 1%를 차지하는 텍스트로 변환됩니다.
3. is_text_present: 이미지에 텍스트가 있는지 여부에 따라 0 또는 1. 태그가 0이면 목록이 비어 있습니다.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
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
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**요청**

다음 요청은 페이로드에 제공된 입력 이미지를 기반으로 텍스트가 있는지 확인합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

URL을 사용한 실행:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
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
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `documents` | 목록에 있는 각 항목이 하나의 이미지를 나타내는 JSON 요소 목록입니다. 이 목록의 일부로 전달된 모든 매개 변수는 해당 목록 요소에 대해 목록 외부에 지정된 전역 매개 변수를 무시합니다. | 예 |
| `sensei:multipart_field_name` | field_name 입력 파일 경로를 읽을 수 있습니다. | 예 |
| `repo:path` | 이미지 자산에 사전 서명된 URL. | 예 |
| `sensei:repoType` | &quot;HTTP&quot;(사전 서명된 URL의 경우). | 아니요 |
| `dc:format` | 입력 이미지의 인코딩된 형식입니다. 이미지 인코딩에는 jpeg, jpg, png 및 tiff와 같은 이미지 형식만 허용됩니다. dc:format이 허용되는 형식과 일치합니다. | 아니요 |
| `correct_with_dictionary` | 영어 사전으로 단어를 수정할지 말지? 이 기능을 설정하지 않으면 영어 이외의 단어를 인식할 수 있습니다. 기본값은 True입니다. 켜짐) 사전을 켜면 항상 영어 단어를 얻을 필요가 없습니다. 수정하려고 하지만, 일정한 편집 거리 내에 있을 수 없다면 원래 단어를 반환합니다. | 아니요 |
| `filter_with_dictionary` | 영어 사전의 단어만 포함하도록 단어를 필터링할지 여부 이 기능이 켜지면 반환된 단어는 항상 470k 단어로 된 큰 영어에 속합니다. | 아니요 |
| `min_probability` | 인식된 단어의 최소 확률은 얼마입니까? 이미지에서 추출되고 min_probability보다 큰 가능성이 있는 단어만 서비스에 의해 반환됩니다. 기본값은 0.2로 설정됩니다. | 아니요 |
| `min_relevance` | 인식된 단어의 최소 관련성은 무엇입니까? 이미지에서 추출되고 min_relevance보다 더 관련성이 높은 단어만 서비스에 의해 반환됩니다. 기본값은 0.01로 설정됩니다. 관련성은 전체 이미지와 비교하여 추출된 텍스트 테두리 상자의 영역 비율로 계산됩니다. 0.01은 이미지의 적어도 1%를 차지하는 텍스트로 변환됩니다. | 아니요 |

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 문자열 | - | - | - | 텍스트를 추출해야 하는 이미지의 사전 서명된 URL입니다. |
| `sensei:repoType` | 문자열 | - | - | HTTPS | 이미지가 저장되는 리포지토리 유형입니다. |
| `sensei:multipart_field_name` | 문자열 | - | - | - | 미리 서명된 URL을 사용하는 대신 이미지를 다중 부분 인수로 전달할 때 이 방법을 사용합니다. |
| `dc:format` | 문자열 | 예 | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | 처리 전에 허용되는 입력 인코딩 유형에 대해 이미지 인코딩을 검사합니다. |