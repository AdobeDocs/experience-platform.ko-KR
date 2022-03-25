---
keywords: 시각적 유사성;시각적 유사성;ccai api
solution: Intelligent Services
title: 콘텐츠 및 상거래 AI API의 시각적 유사성
topic-legacy: Developer guide
description: 이미지가 주어지면 시각적 유사성 서비스는 카탈로그에서 시각적으로 유사한 이미지를 자동으로 찾습니다.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 시각적 유사성

>[!NOTE]
>
>[!DNL Content and Commerce AI] 베타 버전입니다. 설명서는 변경될 수 있습니다.

이미지가 주어지면 시각적 유사성 서비스는 카탈로그에서 시각적으로 유사한 이미지를 자동으로 찾습니다.

이 문서에 표시된 예제 요청에서 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/Query_Image.jpeg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 카탈로그에서 시각적으로 유사한 이미지를 검색합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 결정 [!DNL Sensei Content Framework] 이 사용됩니다. 적당한 것으로 확인해 주세요 `analyzer_id` 요청을 수행하기 전에 콘텐츠 및 Commerce AI 베타 팀에 문의하여 귀하의 `analyzer_id` 을 참조하십시오.

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

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 다음 [!DNL Sensei] 요청이 배포되는 서비스 ID입니다. 이 ID는 다음 중 하나를 결정합니다 [!DNL Sensei Content Frameworks] 이 사용됩니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 애플리케이션의 ID입니다. | 예 |
| `data` | 배열에 이미지를 나타내는 각 개체와 함께 JSON 개체를 포함하는 배열입니다. 이 배열의 일부로 전달된 모든 매개 변수는 `data` 배열입니다. 이 표에 요약된 나머지 속성은 내에서 대체할 수 있습니다 `data`. | 예 |
| `content-id` | 응답에서 반환되는 데이터 요소에 대한 고유 ID입니다. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 시각적 유사성 서비스에서 분석할 콘텐츠입니다. 이미지가 요청 본문의 일부인 경우 `-F file=@<filename>` curl 명령에서 이미지를 전달하여 이 매개 변수를 빈 문자열로 둡니다. <br> 이미지가 S3의 파일인 경우 서명된 URL을 전달합니다. 컨텐츠가 요청 본문의 일부인 경우 데이터 요소 목록에는 개체가 하나만 있어야 합니다. 두 개 이상의 개체가 전달되면 첫 번째 개체만 처리됩니다. | 예 |
| `content-type` | 입력이 요청 본문의 일부인지 또는 S3 버킷에 대해 서명된 URL인지를 나타내는 데 사용됩니다. 이 속성의 기본값은 입니다. `inline`. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 입니다. `jpeg`. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값입니다. 값 사용 `0` 모든 결과를 반환합니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수가 될 수 없음). 값 사용 `0` 모든 결과를 반환합니다. 와 함께 사용하는 경우 `threshold`를 반환한 결과 수가 두 제한 집합 중 적은 수입니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `custom` | 전달할 모든 사용자 지정 매개 변수입니다. | 아니요 |
| `historic-metadata` | 메타데이터를 전달할 수 있는 배열입니다. | 아니요 |

**응답**

성공적인 응답은 `response` 를 포함하는 배열 `feature_value` 및 `feature_name` 에 대해 를 참조하십시오.

아래 표시된 예제 응답에서 시각적으로 유사한 다음 이미지가 반환되었습니다.

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
