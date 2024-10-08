---
keywords: 시각적 유사성;시각적 유사성;ccai api
solution: Experience Platform
title: 콘텐츠 및 Commerce AI API의 시각적 유사성
description: 시각적 유사성 서비스는 이미지가 제공되면 카탈로그에서 시각적으로 유사한 이미지를 자동으로 검색합니다.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# 시각적 유사성

>[!NOTE]
>
>[!DNL Content and Commerce AI]이(가) 베타 버전입니다. 설명서는 변경될 수 있습니다.

시각적 유사성 서비스는 이미지가 제공되면 카탈로그에서 시각적으로 유사한 이미지를 자동으로 검색합니다.

이 문서에 표시된 예제 요청에서는 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/Query_Image.jpeg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 카탈로그에서 시각적으로 유사한 이미지를 검색합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id`은(는) 사용할 [!DNL Sensei Content Framework]을(를) 결정합니다. 요청하기 전에 적절한 `analyzer_id`이(가) 있는지 확인하십시오. 이 서비스에 대한 `analyzer_id`을(를) 받으려면 콘텐츠 및 Commerce AI 베타 팀에 문의하세요.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
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
            "custom": {}
            }]
          }
      }
    ]
}'
```

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID입니다. 이 ID는 [!DNL Sensei Content Frameworks] 중 어느 것을 사용할지 결정합니다. 사용자 지정 서비스의 경우 콘텐츠 및 Commerce AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 생성된 애플리케이션의 ID. | 예 |
| `data` | 배열에 있는 각 객체가 이미지를 나타내는 JSON 객체를 포함하는 배열입니다. 이 배열의 일부로 전달된 모든 매개 변수는 `data` 배열 외부에 지정된 전역 매개 변수를 재정의합니다. 이 표에 요약된 나머지 속성은 `data` 내에서 재정의할 수 있습니다. | 예 |
| `content-id` | 응답에서 반환되는 데이터 요소에 대한 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 지정됩니다. | 아니요 |
| `content` | 시각적 유사성 서비스에서 분석할 콘텐츠입니다. 이미지가 요청 본문의 일부인 경우 curl 명령에서 `-F file=@<filename>`을(를) 사용하여 이미지를 전달하고 이 매개 변수는 빈 문자열로 둡니다. <br> 이미지가 S3의 파일인 경우 서명된 url을 전달합니다. 콘텐츠가 요청 본문에 포함되는 경우 데이터 요소 목록에는 개체가 하나만 있어야 합니다. 두 개 이상의 개체가 전달되면 첫 번째 개체만 처리됩니다. | 예 |
| `content-type` | 입력이 요청 본문의 일부인지 S3 버킷에 대한 서명된 URL인지 여부를 나타내는 데 사용됩니다. 이 속성의 기본값은 `inline`입니다. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 `jpeg`입니다. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수 임계값(0~1)입니다. `0` 값을 사용하여 모든 결과를 반환합니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `top-N` | 반환할 결과 수(음수일 수 없음). `0` 값을 사용하여 모든 결과를 반환합니다. `threshold`과(와) 함께 사용할 경우 반환되는 결과 수는 설정된 제한 중 작은 수 중 하나입니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `custom` | 전달할 모든 사용자 지정 매개 변수입니다. | 아니요 |
| `historic-metadata` | 메타데이터를 전달할 수 있는 배열입니다. | 아니요 |

**응답**

성공한 응답은 카탈로그에 있는 시각적으로 유사한 각 이미지에 대해 `feature_value` 및 `feature_name`을(를) 포함하는 `response` 배열을 반환합니다.

아래 표시된 예제 응답에서 다음과 같은 시각적으로 유사한 이미지가 반환되었습니다.

![유사한 이미지](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
