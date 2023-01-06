---
keywords: Experience Platform;시작하기;컨텐츠 ai;commerce ai;콘텐츠 및 상거래 ai;키워드 추출;키워드 추출
solution: Experience Platform
title: 콘텐츠 및 Commerce AI API의 키워드 추출
description: 키워드 추출 서비스는 텍스트 문서가 지정된 경우 문서의 주제를 가장 잘 설명하는 키워드 또는 키워드 구문을 자동으로 추출합니다. 키워드를 추출하기 위해 명명된 엔터티 인식(NER) 및 비감독 키워드 추출 알고리즘의 조합이 사용됩니다.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 3%

---

# 키워드 추출

>[!NOTE]
>
>[!DNL Content and Commerce AI] 베타 버전입니다. 설명서는 변경될 수 있습니다.

키워드 추출 서비스는 텍스트 문서가 지정된 경우 문서의 주제를 가장 잘 설명하는 키워드 또는 키워드 구문을 자동으로 추출합니다. 키워드를 추출하기 위해 명명된 엔터티 인식(NER) 및 비감독 키워드 추출 알고리즘의 조합이 사용됩니다.

에 의해 인식되는 명명된 엔터티 [!DNL Content and Commerce AI] 다음 표에 나열되어 있습니다.

| 엔티티 이름 | 설명 |
| --- | --- |
| 개인 | 허구까지 포함해서 |
| NORP | 국적 또는 종교나 정치집단. |
| GPE | 국가, 도시 및 주. |
| LOC | GPE가 아닌 위치, 산맥, 물의 시체. |
| FAC | 건물, 공항, 고속도로, 다리 등 |
| 조직 | 회사, 기관, 기관 등 |
| 제품 | 물체, 차량, 식품 등 (서비스 아님) |
| 이벤트 | 이름이 허리케인, 전투, 전쟁, 스포츠 행사 등입니다. |
| WORK_OF_ART | 책, 노래 등의 제목 |
| 법률 | 법으로 만들어진 명명된 문서. |
| 언어 | 이름이 지정된 언어 |

>[!NOTE]
>
>처리 PDF을 계획하는 경우 다음 지침에 따라 건너뜁니다. [PDF 키워드 추출](#pdf-extraction) 이 문서 내에서 사용할 수 있습니다. 또한 docx, ppt, amd xml과 같은 추가 파일 유형에 대한 지원은 나중에 릴리스되도록 설정됩니다.

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 문서에서 키워드를 추출합니다.

입력 파일의 간소화된 JSON:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 결정 [!DNL Sensei Content Framework] 이 사용됩니다. 적당한 것으로 확인해 주세요 `analyzer_id` 요청을 수행하기 전에 키워드 추출 서비스의 경우 `analyzer_id` ID:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 다음 [!DNL Sensei] 요청이 배포되는 서비스 ID입니다. 이 ID는 다음 중 하나를 결정합니다 [!DNL Sensei Content Frameworks] 이 사용됩니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 생성된 애플리케이션의 ID입니다. | 예 |
| `data` | 배열에 문서를 나타내는 각 개체와 함께 JSON 개체를 포함하는 배열입니다. 이 배열의 일부로 전달된 모든 매개 변수는 `data` 배열입니다. 이 표에 요약된 나머지 속성은 내에서 대체할 수 있습니다 `data`. | 예 |
| `language` | 입력 텍스트의 언어입니다. 기본값은 `en`입니다. | 아니요 |
| `content-type` | 입력이 요청 본문의 일부인지 또는 S3 버킷에 대해 서명된 URL인지를 나타내는 데 사용됩니다. 이 속성의 기본값은 입니다. `inline`. | 예 |
| `encoding` | 입력 텍스트의 인코딩 형식입니다. 다음 중 하나일 수 있습니다 `utf-8` 또는 `utf-16`. 이 속성의 기본값은 입니다. `utf-8`. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값입니다. 값 사용 `0` 모든 결과를 반환합니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수가 될 수 없음). 값 사용 `0` 모든 결과를 반환합니다. 와 함께 사용하는 경우 `threshold`를 반환한 결과 수가 두 제한 집합 중 적은 수입니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `custom` | 전달할 모든 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. 자세한 내용은 [부록](#appendix) 를 참조하십시오. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID입니다. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 키워드 추출 서비스에서 사용하는 콘텐츠입니다. 컨텐츠는 원시 텍스트(&#39;인라인&#39; 콘텐츠 유형)일 수 있습니다. <br> 컨텐츠가 S3(&#39;s3-bucket&#39; content-type)의 파일인 경우, 서명된 URL을 전달합니다. 컨텐츠가 요청 본문의 일부인 경우 데이터 요소 목록에는 개체가 하나만 있어야 합니다. 두 개 이상의 개체가 전달되면 첫 번째 개체만 처리됩니다. | 예 |

**응답**

성공적인 응답은 `response` 배열입니다.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## PDF 키워드 추출 {#pdf-extraction}

키워드 추출 서비스는 PDF을 지원하지만 PDF 파일에 새 AnalyzerID를 사용하고 문서 유형을 PDF으로 변경해야 합니다. 자세한 내용은 아래 예를 참조하십시오.

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 PDF 문서에서 키워드를 추출합니다.

>[!CAUTION]
>
>`analyzer_id` 결정 [!DNL Sensei Content Framework] 이 사용됩니다. 적당한 것으로 확인해 주세요 `analyzer_id` 요청을 수행하기 전에 PDF 키워드 추출의 경우 `analyzer_id` ID:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 다음 [!DNL Sensei] 요청이 배포되는 서비스 ID입니다. 이 ID는 다음 중 하나를 결정합니다 [!DNL Sensei Content Frameworks] 이 사용됩니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 생성된 애플리케이션의 ID입니다. | 예 |
| `data` | 배열에 문서를 나타내는 각 개체와 함께 JSON 개체를 포함하는 배열입니다. 이 배열의 일부로 전달된 모든 매개 변수는 `data` 배열입니다. 이 표에 요약된 나머지 속성은 내에서 대체할 수 있습니다 `data`. | 예 |
| `language` | 입력 언어. 기본값은 입니다. `en` (영어) | 아니요 |
| `content-type` | 입력 컨텐츠 유형을 나타내는 데 사용됩니다. 이 옵션은 `file`. | 예 |
| `encoding` | 입력의 인코딩 형식입니다. 이 옵션은 `pdf`. 나중에 지원되는 인코딩 유형은 더 늘어납니다. | 예 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값입니다. 값 사용 `0` 모든 결과를 반환합니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수가 될 수 없음). 값 사용 `0` 모든 결과를 반환합니다. 와 함께 사용하는 경우 `threshold`를 반환한 결과 수가 두 제한 집합 중 적은 수입니다. 이 속성의 기본값은 입니다. `0`. | 아니요 |
| `custom` | 전달할 모든 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. 자세한 내용은 [부록](#appendix) 를 참조하십시오. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID입니다. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 이 옵션은 `file`. | 예 |

**응답**

성공적인 응답은 `response` 배열입니다.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

AEM 클라우드 서비스를 설정, 배포 및 통합하는 방법에 대한 지침이 포함된 PDF 추출 사용에 대한 자세한 정보 및 샘플입니다. 다음 방문 [CCAI PDF 추출 작업자 github 저장소](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## 부록 {#appendix}

다음 표에는 내에서 사용할 수 있는 매개 변수가 포함되어 있습니다 `custom`.

| 이름 | 설명 | 필수입니다 |
| --- | --- | --- |
| `min-n` | 키워드에 필요한 최소 단어 수입니다. | 아니요 |
| `entity-types` | 반환할 엔터티 유형입니다. 이 문서의 시작 부분에서 이름이 지정된 엔티티 인식 테이블을 참조하십시오. | 아니요 |
