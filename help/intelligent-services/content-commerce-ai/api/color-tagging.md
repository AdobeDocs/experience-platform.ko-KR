---
keywords: Experience Platform;시작하기;컨텐츠;컨텐츠 태그 지정;색상 태그 지정;색상 추출;
solution: Experience Platform
title: 콘텐츠 태깅 API의 색상 태깅
description: 색상 태깅 서비스는 이미지가 제공되면 픽셀 색상의 히스토그램을 계산하고 주요 색상별로 버킷으로 정렬할 수 있습니다.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# 색상 태깅

색상 태깅 서비스는 이미지가 제공되면 픽셀 색상의 히스토그램을 계산하고 주요 색상별로 버킷으로 정렬할 수 있습니다. 이미지 픽셀의 색상은 색상 스펙트럼을 나타내는 40개의 주요 색상으로 그룹화됩니다. 그런 다음 40개 색상 중에서 색상 값의 히스토그램이 계산됩니다. 이 서비스에는 두 가지 변형이 있습니다.

**색상 태그 지정(전체 이미지)**

이 방법은 전체 이미지에서 색상 히스토그램을 추출합니다.

**색상 태깅(마스크 사용)**

이 방법은 딥러닝 기반 전경 추출기를 사용하여 전경에서 객체를 식별합니다. 전경 객체가 추출되면 전체 이미지와 함께 전경 및 배경 영역 모두에 대한 주요 색상에 대해 히스토그램이 계산됩니다.

**톤 추출**

위에서 언급한 변형 외에도 다음에 대한 색조 히스토그램을 검색하도록 서비스를 구성할 수 있습니다.

- 전체 이미지(전체 이미지 변형을 사용할 때)
- 전체 이미지, 전경 및 배경 영역(마스킹과 함께 변형을 사용할 때)

이 문서에 표시된 예에는 다음 이미지가 사용되었습니다.

![테스트 이미지](../images/QQAsset1.jpg)

**API 형식**

```http
POST /services/v2/predict
```

**요청 - 전체 이미지 변형**

다음 예제 요청에서는 색상 태깅을 위해 전체 이미지 방법을 사용하고 페이로드에 제공된 입력 매개 변수를 기반으로 이미지에서 색상을 추출합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

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

성공한 응답은 추출된 색상의 세부 정보를 반환합니다. 각 색상은 `feature_value` 키: 다음 정보가 들어 있습니다.

- 색상 이름
- 이미지를 기준으로 이 색상이 표시되는 비율
- 색상의 RGB 값

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`은(는) 발견된 색상이 흰색임을 의미하며 이미지의 58.34%에서 찾을 수 있고 평균 RGB 값은 254, 254, 243입니다.

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

여기의 결과에 &quot;전체&quot; 이미지 영역에서 추출된 색상이 있습니다.

**요청 - 마스킹된 이미지 변형**

다음 예제 요청에서는 색상 태깅에 마스킹 방법을 사용합니다. 이 기능은 를 설정하여 사용할 수 있습니다. `enable_mask` 매개 변수 `true` 요청에서.

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

>[!NOTE]
>
>또한 `retrieve_tone` 매개 변수도 로 설정됩니다. `true` 위의 요청에서. 이를 통해 이미지의 전체, 전경 및 배경 영역에서 따뜻한 톤, 중간 톤 및 차가운 톤에 대한 톤 분포 히스토그램을 검색할 수 있습니다.

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

이제 전체 이미지의 색상 외에 전경색과 배경색도 볼 수 있습니다. 위의 각 영역에 대해 톤 검색이 활성화되므로 톤의 히스토그램을 검색할 수도 있습니다.

**입력 매개 변수**

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| --- | --- | --- | --- | --- | --- |
| `documents` | array(Document-Object) | 예 | - | 아래 참조 | 목록의 각 항목이 하나의 문서를 나타내는 JSON 요소 목록입니다. |
| `top_n` | 숫자 | 아니요 | 0 | 음이 아닌 정수 | 반환할 결과 수. 0: 모든 결과를 반환합니다. 임계값과 함께 사용할 경우 반환되는 결과 수는 두 제한 중 더 적습니다. |
| `min_coverage` | 숫자 | 아니요 | 0.05 | 실수 | 결과를 반환해야 하는 적용 범위의 임계값. 매개 변수를 제외하여 모든 결과를 반환합니다. |
| `resize_image` | 숫자 | 아니요 | True | True/False | 입력 이미지의 크기를 조정할지 여부를 지정합니다. 기본적으로 이미지 크기는 색상 추출을 수행하기 전에 320*320픽셀로 조정됩니다. 디버깅을 위해 를 로 설정하여 전체 이미지에서도 코드를 실행하도록 허용할 수 있습니다. `False`. |
| `enable_mask` | 숫자 | 아니요 | False | True/False | 색상 추출 활성화/비활성화 |
| `retrieve_tone` | 숫자 | 아니요 | False | True/False | 톤 추출 활성화/비활성화 |

**문서 객체**

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 문자열 | - | - | - | 문서의 사전 서명된 URL. |
| `sensei:repoType` | 문자열 | - | - | HTTPS | 이미지가 저장되는 저장소의 유형입니다. |
| `sensei:multipart_field_name` | 문자열 | - | - | - | 사전 서명된 URL을 사용하는 대신 이미지 파일을 다중 부분 인수로 전달할 때 사용합니다. |
| `dc:format` | 문자열 | 예 | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | 이미지 인코딩이 처리되기 전에 허용된 입력 인코딩 유형에 대해 확인됩니다. |