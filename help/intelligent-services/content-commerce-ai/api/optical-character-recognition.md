---
keywords: OCR;텍스트 유무;광학 문자 인식
solution: Experience Platform
title: 텍스트 유무 및 광학 문자 인식
description: Content and Commerce AI API에서 텍스트 유무/OCR(Optical Character Recognition) 서비스는 지정된 이미지에 텍스트가 있는지 여부를 나타낼 수 있습니다. 텍스트가 있으면 OCR에서 텍스트를 반환할 수 있습니다.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# 텍스트 유무 및 광학 문자 인식

>[!NOTE]
>
>콘텐츠 및 상거래 AI는 베타에 있습니다. 설명서는 변경될 수 있습니다.

이미지가 지정된 경우 텍스트 존재/OCR(광학 문자 인식) 서비스는 이미지에 텍스트가 있는지 여부를 나타낼 수 있습니다. 텍스트가 있으면 OCR에서 텍스트를 반환할 수 있습니다.

이 문서에 표시된 예제 요청에서 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/shef.jpeg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 이미지를 기반으로 텍스트가 있는지 확인합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 결정 [!DNL Sensei Content Framework] 이 사용됩니다. 적당한 것으로 확인해 주세요 `analyzer_id` 요청을 수행하기 전에 콘텐츠 및 Commerce AI 베타 팀에 문의하여 귀하의 `analyzer_id` 을 참조하십시오.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
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
    }]
  }'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 다음 [!DNL Sensei] 요청이 배포되는 서비스 ID입니다. 이 ID는 다음 중 하나를 결정합니다 [!DNL Sensei Content Frameworks] 이 사용됩니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 애플리케이션의 ID입니다. | 예 |
| `data` | 배열에 있는 각 개체와 함께 전달된 한 이미지를 나타내는 JSON 개체가 포함된 배열입니다. 이 배열의 일부로 전달된 모든 매개 변수는 `data` 배열입니다. 이 표에 요약된 나머지 속성은 내에서 대체할 수 있습니다 `data`. | 예 |
| `language` | 입력 텍스트의 언어입니다. 기본값은 `en`입니다. | 아니요 |
| `content-type` | 입력이 요청 본문의 일부인지 또는 S3 버킷에 대해 서명된 URL인지를 나타내는 데 사용됩니다. 이 속성의 기본값은 입니다. `inline`. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 입니다. `jpeg`. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값입니다. 값 사용 `0` 모든 결과를 반환합니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수가 될 수 없음). 값 사용 `0` 모든 결과를 반환합니다. 와 함께 사용하는 경우 `threshold`를 반환한 결과 수가 두 제한 집합 중 적은 수입니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `custom` | 전달할 모든 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID입니다. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 컨텐츠는 원시 이미지(&#39;인라인&#39; 콘텐츠 유형)일 수 있습니다. <br> 컨텐츠가 S3(&#39;s3-bucket&#39; content-type)의 파일인 경우, 서명된 URL을 전달합니다. | 예 |

**응답**

성공적인 응답에는 `feature_value` 배열입니다. 텍스트를 읽고 왼쪽에서 오른쪽으로 반환됩니다. 즉, &quot;I love Adobe&quot;이 감지되면 페이로드가 별도의 개체에 &quot;I&quot;, &quot;love&quot; 및 &quot;Adobe&quot;을 반환합니다. 객체에서 `feature_name` 여기에 단어와 `feature_value` 에는 해당 텍스트에 대한 신뢰 지표가 포함되어 있습니다.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
