---
title: 쿼리 서비스의 유사 항목 일치
description: 선택한 문자열과 거의 일치하여 여러 데이터 세트의 결과를 결합하는 Experience Platform 데이터에 대해 일치 작업을 수행하는 방법을 알아봅니다.
exl-id: ec1e2dda-9b80-44a4-9fd5-863c45bc74a7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# 쿼리 서비스의 유사 항목 일치

Adobe Experience Platform 데이터에서 &#39;유사 항목&#39; 일치를 사용하여 동일한 문자가 있는 문자열을 검색할 필요 없이 가장 가능성이 높고 대략적인 일치를 반환합니다. 이를 통해 데이터를 보다 유연하게 검색할 수 있으며, 시간과 노력을 절약하여 데이터에 보다 쉽게 액세스할 수 있습니다.

유사 항목 일치는 검색 문자열의 포맷을 다시 지정하는 대신 두 시퀀스 간의 유사성 비율을 분석하고 유사성 백분율을 반환합니다. [!DNL regex] 또는 [!DNL difflib]에 비해 함수가 더 복잡한 상황에서 문자열을 일치시키는 데 더 적합하므로 이 프로세스에 [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/)을(를) 사용하는 것이 좋습니다.

이 사용 사례에서 제공하는 예제는 두 개의 서로 다른 여행사 데이터 세트에서 호텔 객실 검색의 유사한 속성을 일치시키는 데 중점을 둡니다. 이 문서에서는 별도의 큰 데이터 소스로부터의 유사성 정도별로 문자열을 일치시키는 방법을 보여 줍니다. 이 예에서 퍼지 일치는 Luma 및 Acme 여행사의 룸 기능에 대한 검색 결과를 비교합니다.

## 시작하기 {#getting-started}

이 프로세스의 일부로 머신 러닝 모델을 교육해야 하므로 이 문서에서는 하나 이상의 머신 러닝 환경에 대한 작업 지식을 가정합니다.

이 예제에서는 [!DNL Python] 및 [!DNL Jupyter Notebook] 개발 환경을 사용합니다. 사용할 수 있는 옵션은 많지만 계산 요구 사항이 낮은 오픈 소스 웹 응용 프로그램이므로 [!DNL Jupyter Notebook]을(를) 사용하는 것이 좋습니다. [공식 Jupyter 사이트](https://jupyter.org/)에서 다운로드할 수 있습니다.

시작하기 전에 필요한 라이브러리를 가져와야 합니다. [!DNL FuzzyWuzzy]은(는) [!DNL difflib] 라이브러리의 맨 위에 빌드되고 문자열을 일치시키는 데 사용되는 오픈 소스 [!DNL Python] 라이브러리입니다. [!DNL Levenshtein Distance]을(를) 사용하여 시퀀스와 패턴 간의 차이를 계산합니다. [!DNL FuzzyWuzzy]에는 다음 요구 사항이 있습니다.

- [!DNL Python] 2.4 이상
- [!DNL Python-Levenshtein]

명령줄에서 다음 명령을 사용하여 [!DNL FuzzyWuzzy]을(를) 설치합니다.

```console
pip install fuzzywuzzy
```

또는 다음 명령을 사용하여 [!DNL Python-Levenshtein]도 설치하십시오.

```console
pip install fuzzywuzzy[speedup]
```

[!DNL Fuzzywuzzy]에 대한 추가 기술 정보는 [공식 설명서](https://pypi.org/project/fuzzywuzzy/)에서 찾을 수 있습니다.

### 쿼리 서비스에 연결

연결 자격 증명을 제공하여 기계 학습 모델을 쿼리 서비스에 연결해야 합니다. 만료 전 및 비만료 자격 증명을 모두 제공할 수 있습니다. 필요한 자격 증명을 얻는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. [!DNL Jupyter Notebook]을(를) 사용하는 경우 [쿼리 서비스에 연결하는 방법](../clients/jupyter-notebook.md)에 대한 전체 안내서를 읽어 보십시오.

또한 선형 대수를 사용하려면 [!DNL numpy] 패키지를 [!DNL Python] 환경으로 가져와야 합니다.

```python
import numpy as np
```

[!DNL Jupyter Notebook]에서 쿼리 서비스에 연결하려면 아래 명령이 필요합니다.

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

[!DNL Jupyter Notebook] 인스턴스가 이제 쿼리 서비스에 연결되어 있습니다. 연결에 성공하면 메시지가 표시되지 않습니다. 연결에 실패하면 오류가 표시됩니다.

### Luma 데이터 세트에서 데이터 그리기 {#luma-dataset}

분석할 데이터는 다음 명령을 사용하여 첫 번째 데이터 세트에서 가져옵니다. 간결성을 위해, 예들은 컬럼의 처음 10개의 결과들로 제한되었다.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

반환된 배열을 표시하려면 **Output**&#x200B;을(를) 선택하십시오.

+++출력

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Acme 데이터 세트에서 데이터 가져오기 {#acme-dataset}

이제 다음 명령을 사용하여 두 번째 데이터 세트에서 분석용 데이터를 가져옵니다. 다시, 간결성을 위해, 예들은 컬럼의 처음 10개의 결과들로 제한되었다.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

반환된 배열을 표시하려면 **Output**&#x200B;을(를) 선택하십시오.

+++출력

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### 흐릿한 채점 함수 만들기 {#fuzzy-scoring}

그런 다음 FuzzyWuzzy 라이브러리에서 `fuzz`을(를) 가져오고 문자열의 부분 비율 비교를 실행해야 합니다. 부분 비율 함수를 사용하면 하위 문자열 일치를 수행할 수 있습니다. 이렇게 하면 가장 짧은 문자열이 사용되며 길이가 같은 모든 하위 문자열과 일치합니다. 이 함수는 최대 100%의 백분율 유사성 비율을 반환합니다. 예를 들어, 부분 비율 함수는 다음 문자열 &#39;Deluxe Room&#39;, &#39;1 King Bed&#39; 및 &#39;Deluxe King Room&#39;을 비교하고 69%의 유사성 점수를 반환합니다.

호텔 룸 일치 사용 사례에서는 다음 명령을 사용하여 이 작업을 수행합니다.

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

그런 다음 [!DNL SciPy] 라이브러리에서 `cdist`을(를) 가져와 두 입력 컬렉션의 각 쌍 간 거리를 계산합니다. 이것은 각 여행사가 제공한 모든 호텔 객실 쌍 사이의 점수를 계산합니다.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### 퍼지 조인 점수를 사용하여 두 열 간의 매핑 만들기

이제 열에 거리를 기준으로 점수가 매겨졌으므로 쌍을 인덱싱하고 특정 비율보다 높은 점수를 얻은 일치 항목만 유지할 수 있습니다. 이 예는 70% 이상의 점수와 일치하는 쌍만 유지합니다.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

다음 명령을 사용하여 결과를 표시할 수 있습니다. 간결성을 위해 결과는 10개의 행으로 제한됩니다.

```python
matched_pairs[:10]
```

결과를 보려면 **출력**&#x200B;을 선택하세요.

+++출력

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

그런 다음 SQL을 사용하여 다음 명령과 일치하는 결과를 얻습니다.

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## 매핑을 적용하여 쿼리 서비스에서 퍼지 조인 수행 {#mappings-for-query-service}

다음으로, 점수가 높은 일치 쌍이 SQL을 사용하여 연결되어 새 데이터 세트를 만듭니다.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

이 조인 결과를 보려면 **출력**&#x200B;을 선택하십시오.

+++출력

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Experience Platform에 유사 항목 일치 결과 저장 {#save-to-platform}

마지막으로, 유사 항목 일치 결과는 SQL을 사용하여 Adobe Experience Platform에서 사용할 데이터 세트로 저장할 수 있습니다.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```
