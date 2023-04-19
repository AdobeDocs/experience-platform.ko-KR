---
keywords: Experience Platform;시작하기;컨텐츠;컨텐츠 태깅;색상 태깅;색상 추출;
solution: Experience Platform
title: 컨텐츠 태깅 API의 색상 태깅
description: 색상 태깅 서비스에서는 이미지가 지정된 경우 픽셀 색상의 히스토그램을 계산하고 우세한 색상을 버킷으로 정렬할 수 있습니다.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e6ea347252b898f73c2bc495b0324361ee6cae9b
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 5%

---

# 색상 태깅

색상 태깅 서비스에서는 이미지가 지정된 경우 픽셀 색상의 히스토그램을 계산하고 우세한 색상을 버킷으로 정렬할 수 있습니다. 이미지 픽셀의 색상은 색상 스펙트럼을 나타내는 40개의 중심 색상으로 그룹화됩니다. 그런 다음 색상 값의 히스토그램이 이러한 40개 색상 중에서 계산됩니다. 이 서비스에는 두 가지 변형이 있습니다.

**색상 태깅(전체 이미지)**

이 방법은 전체 이미지에 걸쳐 색상 히스토그램을 추출합니다.

**색상 태깅(마스크 포함)**

이 방법에서는 딥 러닝 기반의 전경 추출기를 사용하여 전경 상태의 객체를 식별합니다. 전경 객체가 추출되면 히스토그램이 전체 이미지와 함께 전경 영역과 배경 영역 모두에 대해 우세한 색상으로 계산됩니다.

**톤 추출**

위에 언급된 변형 외에도, 다음에 대한 색상 히스토그램을 검색하도록 서비스를 구성할 수 있습니다.

- 전체 이미지(전체 이미지 변형을 사용할 때)
- 전체 이미지, 전경 및 배경 영역(마스크와 함께 변형을 사용할 때)

이 문서에 표시된 예에서 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/QQAsset1.jpg)

**API 형식**

```http
POST /services/v2/predict
```

**요청 - 전체 이미지 변형**

다음 예제 요청에서는 색상 태깅에 전체 이미지 방법을 사용하고 페이로드에 제공된 입력 매개 변수를 기반으로 이미지에서 색상을 추출합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**응답 - 전체 이미지 변형**

성공적인 응답은 추출된 색상의 세부 정보를 반환합니다. 각 색상은 `feature_value` key - 다음 정보를 포함합니다.

- 색상 이름
- 이 색상이 이미지와 관련하여 나타나는 백분율입니다
- 색상의 RGB 값

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`즉, 발견된 색은 이미지의 58.34%에서 발견되는 흰색이며, 평균 RGB 값이 254, 254, 243입니다.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

여기서의 결과에 &quot;전체&quot; 이미지 영역에서 색상이 추출되었습니다.

**요청 - 마스킹된 이미지 변형**

다음 예제 요청에서는 색상 태깅에 마스킹 방법을 사용합니다. 이 설정을 `enable_mask` 매개 변수 대상 `true` 참조하십시오.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>참고: 또한 `retrieve_tone` 매개 변수 대상 `true` 위의 요청에서. 이렇게 하면 이미지의 전체, 전경 및 배경 영역에서 따뜻한 색상, 중립적이고 시원한 톤 위에 색조 분포 히스토그램을 검색할 수 있습니다.

**응답 - 마스킹된 이미지 변형**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

이제 전체 이미지의 색상 외에도 전경 영역과 배경 영역에서 색상을 볼 수 있습니다. 위의 각 영역에 대해 톤 검색을 활성화하므로 톤 히스토그램도 검색할 수 있습니다.

**입력 매개 변수**

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| --- | --- | --- | --- | --- | --- |
| `documents` | 배열(Document-Object) | 예 | - | 아래를 참조하십시오 | 목록에 있는 각 항목이 하나의 문서를 나타내는 json 요소 목록입니다. |
| `top_n` | 숫자 | 아니요 | 0 | 음수가 아닌 정수 | 반환할 결과 수입니다. 0, 모든 결과를 반환합니다. 임계값과 함께 사용하는 경우 반환되는 결과 수가 두 제한 중 하나가 되지 않습니다. |
| `min_coverage` | 숫자 | 아니요 | 0.05 | 실수 | 결과를 반환해야 하는 범위 위의 임계값입니다. 모든 결과를 반환하려면 매개 변수를 제외하십시오. |
| `resize_image` | 숫자 | 아니요 | True | True/False | 입력 이미지의 크기를 조정할지 여부를 지정합니다. 기본적으로 색상 추출을 수행하기 전에 이미지 크기가 320*320픽셀로 조정됩니다. 디버깅을 위해 이 값을 False로 설정하여 코드가 전체 이미지에서도 실행되도록 허용할 수 있습니다. |
| `enable_mask` | 숫자 | 아니요 | False | True/False | 색상 추출 활성화/비활성화 |
| `retrieve_tone` | 숫자 | 아니요 | False | True/False | 톤 추출 활성화/비활성화 |

**문서 객체**

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 문자열 | - | - | - | 키 구문을 추출할 문서의 사전 서명된 URL입니다. |
| `sensei:repoType` | 문자열 | - | - | HTTPS | 문서가 저장되는 리포지토리 유형입니다. |
| `sensei:multipart_field_name` | 문자열 | - | - | - | 사전 서명된 URL을 사용하는 대신 문서를 다중 부분 인수로 전달할 때 이를 사용합니다. |
| `dc:format` | 문자열 | 예 | - | &quot;text/plain&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-office.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml&quot; | 문서 인코딩은 처리 전에 허용되는 입력 인코딩 유형에 대해 확인됩니다. |