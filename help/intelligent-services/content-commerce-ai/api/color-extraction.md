---
keywords: Experience Platform;시작하기;내용 ai;커머스 ai;내용 및 상거래 ai;색상 추출;색상 추출;시작하기;content ai;commerce ai;color extraction;getting started;content ai;content and commerce ai;color extraction;
solution: Experience Platform, Intelligent Services
title: 컨텐츠 및 상거래 AI API의 색상 추출
topic-legacy: Developer guide
description: 이미지 제공 시 색상 추출 서비스를 사용하면 픽셀 색상의 막대 그래프를 계산하고 우세한 색상을 버킷으로 정렬할 수 있습니다.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# 색상 추출

>[!NOTE]
>
>[!DNL Content and Commerce AI] 베타 버전임 설명서는 변경될 수 있습니다.

이미지 제공 시 색상 추출 서비스를 사용하면 픽셀 색상의 막대 그래프를 계산하고 우세한 색상을 버킷으로 정렬할 수 있습니다. 이미지 픽셀의 색상은 색상 스펙트럼을 나타내는 40개의 탁월한 색상으로 버킷팅됩니다. 그런 다음 색상 값의 막대 그래프가 해당 40색 중에서 계산됩니다. 서비스는 다음과 같은 2가지 변형이 있습니다.

**색상 추출(전체 이미지)**

이 방법은 전체 이미지의 색상 막대 그래프를 추출합니다.

**색상 추출(마스크 포함)**

이 메서드는 깊은 학습 기반 전경 돌출을 사용하여 전경 안의 개체를 식별합니다. 그 모델은 전자 상거래 이미지 카탈로그로 교육된다. 전경 오브젝트가 추출되면 막대 그래프가 이전에 설명한 대로 주요 색상 위에 계산됩니다.

다음 이미지가 이 문서에 표시된 예에서 사용되었습니다.

![테스트 이미지](../images/QQAsset1.jpg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 예제 요청에서는 색상 추출을 위해 전체 이미지 방법을 사용합니다.

다음 요청은 페이로드에서 제공하는 입력 매개 변수를 기반으로 이미지에서 색상을 추출합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 사용할 항목 [!DNL Sensei Content Framework] 을 결정합니다. 요청을 하기 전에 적절한 `analyzer_id`이 있는지 확인하십시오. 색상 추출 서비스의 경우 `analyzer_id` ID는 다음과 같습니다.
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
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID. 이 ID는 [!DNL Sensei Content Frameworks] 중 어느 것이 사용되는지 결정합니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 응용 프로그램의 ID. | 예 |
| `data` | JSON 개체를 포함하는 배열입니다. 배열의 각 객체는 이미지를 나타냅니다. 이 배열의 일부로 전달되는 모든 매개 변수는 `data` 배열 외부에 지정된 전역 매개 변수를 무시합니다. 이 표에 나와 있는 나머지 속성은 `data` 내에서 재정의할 수 있습니다. | 예 |
| `content-id` | 응답에서 반환되는 데이터 요소의 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 색상 추출 서비스에서 분석하려는 내용. 이미지가 요청 본문에 포함된 경우 말림 명령에 `-F file=@<filename>`을 사용하여 이미지를 전달하고 이 매개 변수를 빈 문자열로 남겨둡니다. <br> 이미지가 S3의 파일인 경우 서명된 URL을 전달합니다. 컨텐츠가 요청 본문에 포함된 경우 데이터 요소 목록에는 하나의 객체만 있어야 합니다. 두 개 이상의 객체가 전달되면 첫 번째 객체만 처리됩니다. | 예 |
| `content-type` | 입력이 요청 본문과 S3 버킷에 대한 서명된 URL인지 여부를 나타내는 데 사용됩니다. 이 속성의 기본값은 `inline`입니다. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 `jpeg`입니다. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값. 모든 결과를 반환하려면 `0` 값을 사용합니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `top-N` | 반환할 결과 수입니다(음수가 될 수 없음). 모든 결과를 반환하려면 `0` 값을 사용합니다. `threshold`과 함께 사용할 경우 반환되는 결과 수가 두 제한 중 하나 보다 적습니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `custom` | 전달할 사용자 지정 매개 변수입니다. | 아니요 |
| `historic-metadata` | 메타데이터를 전달할 수 있는 배열입니다. | 아니요 |

**응답**

성공적인 응답은 추출된 색상의 세부 정보를 반환합니다. 각 색상은 다음 정보가 포함된 `feature_value` 키로 표시됩니다.

- 색상 이름
- 이미지에 대해 이 색상이 나타나는 비율
- 색상의 RGB 값

아래의 첫 번째 예제 객체에서 `White,0.59,251,251,243`의 `feature_value`은 검색된 색상이 흰색이고, 흰색은 이미지의 59%에서 발견되며 RGB 값이 251,251,243임을 의미합니다.

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
| `feature_value` | 개체에 속성 이름이 같은 키가 포함된 배열입니다. 이러한 키에는 색상 이름, `content_id`에서 전송된 이미지에 대해 이 색상이 나타나는 백분율 및 색상의 RGB 값을 나타내는 문자열이 포함되어 있습니다. |
