---
keywords: Experience Platform;시작하기;컨텐츠 ai;commerce ai;콘텐츠 및 상거래 ai;색상 추출;색상 추출
solution: Experience Platform
title: 콘텐츠 및 Commerce AI API의 색상 추출
description: 색상 추출 서비스에서는 이미지가 지정된 경우 픽셀 색상의 히스토그램을 계산하고 우세한 색상으로 버킷으로 정렬할 수 있습니다.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# 색상 추출

>[!NOTE]
>
>[!DNL Content and Commerce AI] 베타 버전입니다. 설명서는 변경될 수 있습니다.

색상 추출 서비스에서는 이미지가 지정된 경우 픽셀 색상의 히스토그램을 계산하고 우세한 색상으로 버킷으로 정렬할 수 있습니다. 이미지 픽셀의 색상은 색상 스펙트럼을 나타내는 40개의 중심 색상으로 그룹화됩니다. 그런 다음 색상 값의 히스토그램이 이러한 40개 색상 중에서 계산됩니다. 이 서비스에는 두 가지 변형이 있습니다.

**색상 추출(전체 이미지)**

이 방법은 전체 이미지에 걸쳐 색상 히스토그램을 추출합니다.

**색상 추출(마스크 포함)**

이 방법에서는 딥 러닝 기반의 전경 추출기를 사용하여 전경에 있는 객체를 식별합니다. 그 모델은 전자 상거래 이미지의 카탈로그를 통해 교육된다. 전경 객체가 추출되면 히스토그램이 이전에 설명한 대로 우위 색상으로 계산됩니다.

이 문서에 표시된 예에서 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/QQAsset1.jpg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 예제 요청에서는 색상 추출에 전체 이미지 메서드를 사용합니다.

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 이미지에서 색상을 추출합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 결정 [!DNL Sensei Content Framework] 이 사용됩니다. 적당한 것으로 확인해 주세요 `analyzer_id` 요청을 수행하기 전에 색상 추출 서비스의 경우, `analyzer_id` ID:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

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
| `analyzer_id` | 다음 [!DNL Sensei] 요청이 배포되는 서비스 ID입니다. 이 ID는 다음 중 하나를 결정합니다 [!DNL Sensei Content Frameworks] 이 사용됩니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 애플리케이션의 ID입니다. | 예 |
| `data` | JSON 개체를 포함하는 배열입니다. 배열에 있는 각 개체는 이미지를 나타냅니다. 이 배열의 일부로 전달된 모든 매개 변수는 `data` 배열입니다. 이 표에 요약된 나머지 속성은 내에서 대체할 수 있습니다 `data`. | 예 |
| `content-id` | 응답에서 반환되는 데이터 요소에 대한 고유 ID입니다. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 색상 추출 서비스에서 분석할 콘텐츠입니다. 이미지가 요청 본문의 일부인 경우 `-F file=@<filename>` curl 명령에서 이미지를 전달하여 이 매개 변수를 빈 문자열로 둡니다. <br> 이미지가 S3의 파일인 경우 서명된 URL을 전달합니다. 컨텐츠가 요청 본문의 일부인 경우 데이터 요소 목록에는 개체가 하나만 있어야 합니다. 두 개 이상의 개체가 전달되면 첫 번째 개체만 처리됩니다. | 예 |
| `content-type` | 입력이 요청 본문의 일부인지 또는 S3 버킷에 대해 서명된 URL인지를 나타내는 데 사용됩니다. 이 속성의 기본값은 입니다. `inline`. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 입니다. `jpeg`. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값입니다. 값 사용 `0` 모든 결과를 반환합니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수가 될 수 없음). 값 사용 `0` 모든 결과를 반환합니다. 와 함께 사용하는 경우 `threshold`를 반환한 결과 수가 두 제한 집합 중 적은 수입니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `custom` | 전달할 모든 사용자 지정 매개 변수입니다. | 아니요 |
| `historic-metadata` | 메타데이터를 전달할 수 있는 배열입니다. | 아니요 |

**응답**

성공적인 응답은 추출된 색상의 세부 정보를 반환합니다. 각 색상은 `feature_value` key - 다음 정보를 포함합니다.

- 색상 이름
- 이 색상이 이미지와 관련하여 나타나는 백분율입니다
- 색상의 RGB 값

아래의 첫 번째 예제 개체에서는 `feature_value` 의 `White,0.59,251,251,243` 즉, 흰색은 흰색이고, 흰색은 이미지의 59%에서 발견되며, RGB 값은 251,251,243입니다.

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
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
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
| `feature_value` | 개체의 속성 이름이 같은 키가 들어 있는 배열입니다. 이러한 키에는 색상 이름을 나타내는 문자열이 포함되어 있으며 색상은 `content_id`, 및 RGB 값의 색상. |
