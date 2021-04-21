---
keywords: OCR;텍스트 존재;광학 문자 인식
solution: Experience Platform, Intelligent Services
title: 텍스트 존재 및 광학 문자 인식
topic-legacy: Developer guide
description: Content and Commerce AI API에서 OCR(Text Presence/Optical Character Recognition) 서비스는 텍스트가 지정된 이미지에 있는지 여부를 나타낼 수 있습니다. 텍스트가 있는 경우 OCR에서 텍스트를 반환할 수 있습니다.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# 텍스트 존재 및 광학 문자 인식

>[!NOTE]
>
>콘텐츠 및 상거래 AI가 베타 버전입니다. 설명서는 변경될 수 있습니다.

이미지 제공 시 텍스트 존재/OCR(Optical Character Recognition) 서비스는 이미지에 텍스트가 있는지 여부를 나타낼 수 있습니다. 텍스트가 있는 경우 OCR에서 텍스트를 반환할 수 있습니다.

다음 이미지가 이 문서에 표시된 예제 요청에서 사용되었습니다.

![테스트 이미지](../images/shef.jpeg)

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 이미지를 기반으로 텍스트가 있는지 확인합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 사용할 항목 [!DNL Sensei Content Framework] 을 결정합니다. 요청을 하기 전에 적절한 `analyzer_id`이 있는지 확인하십시오. 이 서비스에 대한 `analyzer_id`을(를) 받으려면 콘텐츠 및 상거래 AI 베타 팀에 문의하십시오.

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
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID. 이 ID는 [!DNL Sensei Content Frameworks] 중 어느 것이 사용되는지 결정합니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 응용 프로그램의 ID. | 예 |
| `data` | 배열에서 전달되는 하나의 이미지를 나타내는 각 객체가 포함된 JSON 객체가 포함된 배열입니다. 이 배열의 일부로 전달되는 모든 매개 변수는 `data` 배열 외부에 지정된 전역 매개 변수를 무시합니다. 이 표에 나와 있는 나머지 속성은 `data` 내에서 재정의할 수 있습니다. | 예 |
| `language` | 입력 텍스트 언어 기본값은 `en`입니다. | 아니요 |
| `content-type` | 입력이 요청 본문과 S3 버킷에 대한 서명된 URL인지 여부를 나타내는 데 사용됩니다. 이 속성의 기본값은 `inline`입니다. | 아니요 |
| `encoding` | 입력 이미지의 파일 형식입니다. 현재 JPEG 및 PNG 이미지만 처리할 수 있습니다. 이 속성의 기본값은 `jpeg`입니다. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값. 모든 결과를 반환하려면 `0` 값을 사용합니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `top-N` | 반환할 결과 수입니다(음수가 될 수 없음). 모든 결과를 반환하려면 `0` 값을 사용합니다. `threshold`과 함께 사용할 경우 반환되는 결과 수가 두 제한 중 하나 보다 적습니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `custom` | 전달할 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 컨텐츠는 원시 이미지(&#39;인라인&#39; 컨텐트 유형)일 수 있습니다. <br> 내용이 S3(&#39;s3-bucket&#39; content-type)의 파일인 경우 서명된 URL을 전달합니다. | 예 |

**응답**

성공적인 응답은 `feature_value` 배열에서 검색된 텍스트를 반환합니다. 텍스트를 읽고 왼쪽에서 오른쪽으로 위쪽으로 반환됩니다. 즉, &quot;Adobe을 사랑해요&quot;가 감지되면 페이로드가 별도의 개체에 &quot;I&quot;, &quot;love&quot; 및 &quot;Adobe&quot;을 반환합니다. 객체에는 해당 텍스트에 대한 신뢰 지표가 포함된 `feature_name` 및 `feature_value`이 제공됩니다.

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
