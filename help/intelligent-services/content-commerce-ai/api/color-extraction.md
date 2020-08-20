---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;color extraction;Color extraction
solution: Experience Platform
title: 색상 추출
topic: Developer guide
description: 이미지 제공 시 색상 추출 서비스는 픽셀 색상의 막대 그래프를 계산하고 기본 색상을 기준으로 버킷으로 정렬할 수 있습니다.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 2%

---


# 색상 추출

>[!NOTE]
>
>[!DNL Content and Commerce AI] 가 베타 버전입니다. 설명서는 변경될 수 있습니다.

이미지 제공 시 색상 추출 서비스는 픽셀 색상의 히스토그램을 계산한 다음 주 색상을 버킷으로 정렬할 수 있습니다. 이미지 픽셀의 색상은 색상 스펙트럼을 나타내는 40개의 우수한 색상으로 버킷팅됩니다. 그런 다음 색상 값의 히스토그램은 이러한 40가지 색상 중에서 계산됩니다. 서비스에는 다음과 같은 두 가지 변형이 있습니다.

**색상 추출(전체 이미지)**

이 방법은 전체 이미지 전체에 대해 색상 막대 그래프를 추출합니다.

**색상 추출(마스크 포함)**

이 메서드는 딥 러닝 기반 전경 추출기를 사용하여 전경의 개체를 식별합니다. 그 모델은 전자 상거래 이미지 카탈로그를 통해 교육된다. 전경 오브젝트가 추출되면 히스토그램은 이전에 설명한 대로 주요 색상 위에 계산됩니다.

다음 이미지가 이 문서에 표시된 예에서 사용되었습니다.

![테스트 이미지](../images/test_image.jpeg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 예제 요청에서는 색상 추출을 위해 전체 이미지 방법을 사용합니다.

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 이미지에서 색상을 추출합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 사용할 항목 [!DNL Sensei Content Framework] 을 결정합니다. 요청하기 `analyzer_id` 전에 적절한 것이 있는지 확인하십시오.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID. 이 ID는 어떤 것이 사용되는지 [!DNL Sensei Content Frameworks] 를 결정합니다. | 예 |
| `application-id` | 만든 응용 프로그램의 ID입니다. | 예 |
| `data` | JSON 개체를 포함하는 배열. 배열의 각 개체는 이미지를 나타냅니다. 이 배열의 일부로 전달되는 모든 매개 변수는 배열 외부에 지정된 전역 매개 변수를 `data` 무시합니다. 이 표에 나와 있는 나머지 속성은 내에서 재정의할 수 있습니다 `data`. | 예 |
| `content-id` | 응답에서 반환되는 데이터 요소의 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 색상 추출 서비스에서 분석하기 위한 컨텐츠입니다. 이미지가 요청 본문에 포함된 경우 말림 명령 `-F file=@<filename>` 에서 이미지를 전달하여 이 매개 변수를 빈 문자열로 남겨둡니다. <br> 이미지가 S3의 파일인 경우 서명된 URL을 전달합니다. 컨텐츠가 요청 본문에 포함된 경우 데이터 요소 목록에는 하나의 객체만 있어야 합니다. 두 개 이상의 개체가 전달되면 첫 번째 개체만 처리됩니다. | 예 |
| `content-type` | 입력이 요청 본체의 일부인지 또는 S3 버킷에 대해 서명된 URL인지 나타내는 데 사용됩니다. 이 속성의 기본값은 입니다 `inline`. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 입니다 `jpeg`. | 아니요 |
| `threshold` | 결과를 반환해야 하는 상단의 점수(0-1)입니다. 값을 사용하여 모든 결과 `0` 를 반환합니다. 이 속성의 기본값은 입니다 `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수일 수 없음) 값을 사용하여 모든 결과 `0` 를 반환합니다. 이와 함께 사용할 경우 반환되는 결과 `threshold`의 수가 두 제한 중 더 적습니다. 이 속성의 기본값은 입니다 `0`. | 아니요 |
| `custom` | 전달할 사용자 지정 매개 변수입니다. | 아니요 |
| `historic-metadata` | 메타데이터를 전달할 수 있는 배열입니다. | 아니요 |

**응답**

성공적인 응답은 추출된 색상의 세부 정보를 반환합니다. 각 색상은 다음 정보가 포함된 `feature_value` 키로 표시됩니다.

- 색상 이름
- 이미지에 대해 이 색상이 나타나는 비율
- 색상의 RGB 값

아래의 첫 번째 예제 개체에서 `feature_value` `White,0.82,239,239,239` 는 발견된 색상이 흰색이고, 흰색은 이미지의 82%에서 발견되며, RGB 값이 239,239,239임을 의미합니다.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.82,239,239,239"
              },
              {
                "feature_value": "Dark_Blue,0.11,41,60,86",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Royal_Blue,0.08,63,91,123"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| 속성 | 설명 |
| --- | --- |
| `content_id` | POST 요청에 업로드된 이미지의 이름입니다. |
| `feature_value` | 개체에 속성 이름이 같은 키가 포함된 배열. 이러한 키에는 색상 이름을 나타내는 문자열, 에서 전송된 이미지와 관련하여 이 색상이 나타나는 비율 `content_id`및 색상의 RGB 값이 포함됩니다. |
