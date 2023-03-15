---
keywords: Experience Platform;홈;인기 항목;etl;ETL;etl 변형;ETL 변형
solution: Experience Platform
title: 샘플 ETL 변형
description: 이 문서에서는 ETL(추출, 변환, 로드) 개발자에게 발생할 수 있는 다음 예제 변환을 보여 줍니다.
exl-id: 8084f5fd-b621-4515-a329-5a06c137d11c
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# 샘플 ETL 변형

이 문서에서는 ETL(추출, 변환, 로드) 개발자에게 발생할 수 있는 다음 예제 변환을 보여 줍니다.

## 플랫 CSV에서 계층으로

### 샘플 파일

샘플 CSV 및 JSON 파일은 공개 ETL 참조에서 사용할 수 있습니다 [!DNL GitHub] Adobe에 의해 유지 관리되는 리포지토리:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

### CSV 예

다음 CRM 데이터를 (으)로 내보냈습니다 `CRM_profiles.csv`:

```shell
TITLE   F_NAME  L_NAME  GENDER  DOB EMAIL   CRMID   ECID    LOYALTYID   ECID2   PHONE   STREET  CITY    STATE   COUNTRY ZIP LAT LONG
Mr  Ewart   Bennedsen   M   2004-09-25  ebennedsenex@jiathis.com    71a16013-d805-7ece-9ac4-8f2cd66e8eaa    87098882279810196101440938110216748923  2e33192000007456-0365c00000000000   55019962992006103186215643814973128178  256-284-7231    72 Buhler Crossing  Anniston    Alabama US  36205   33.708276   -85.7922905
Dr  Novelia Ansteys F   1987-10-31  nansteysdk@spotify.com  2eeb6532-82e1-0d58-8955-bf97de66a6f5    50829196174854544323574004005273946998  2e3319208000765b-3811c00000000001   65233136134594262632703695260919939885  704-181-6371    79 Northfield Hill  Charlotte   North Carolina  US  28299   35.2188655  -80.8108885
Mr  Ulises  Mochan  M   1996-03-20  umochanco@gnu.org   6f393075-addb-bdd6-73f8-31c393b700f5    70086119428645095847094710218289660855  2e33192080003023-26b2000000000002   82011353387947708954389153068944017636  720-837-4159    00671 Mifflin Trail Lacolle Qu√&copy;bec CA  E5A 45.08338    -73.36585
Mrs Friederike  Durrell F   1979-01-3   fdurrellbj@utexas.edu   33d018ec-5fed-f1a3-56aa-079370a9511b    50164729868919217963697788808932473456  2e33192080006dfc-0cdf400000000003   64452712468609735658703639722261004071  798-528-3458    47 Fremont Hill Independencia   Veracruz Llave  MX  91891   19.3803931  -99.1476905
Rev Evita   Bingall F   1974-02-28  ebingallod@mac.com  8c93db88-f328-8efb-dc73-d5654d371cbe    74973364195185450328832136951985519627  2e331920800038db-0559e00000000004   58945501950285346322834356669253860483  397-178-5897    56 Crescent Oaks Court  Buenavista  Oaxaca  MX  71730   19.4458447  -99.1497665
Mr  Eugenie Bechley F   1969-05-19  ebechley9r@telegraph.co.uk  b0c76a3f-6526-0ad0-e050-48143b687d18    67119779213799783658184754966135750376  2e331920800001a4-24b2800000000005   59715249079109455676103900762283358508  718-374-7456    5760 Southridge Junction    Staten Island   New York    US  10310   40.6307451  -74.1181235
Dr  Cammi   Haslen  F   1973-12-17  chaslenqv@ehow.com  56059cd5-5006-ce5f-2f5f-15b4d856a204    61747117963243728095047674165570746095  2e33192080007c25-2ec0600000000006   86268258269066295956223980330791223320  865-538-8291    83 Veith Street Knoxville   Tennessee   US  37995   35.95   -84.05
```

### 매핑

CRM 데이터에 대한 매핑 요구 사항은 다음 표에 요약되어 있으며 다음 변환을 포함합니다.
- ID 열 대상 `identityMap` 속성
- 생년월일(DOB) - 연월일
- 문자열을 중복 또는 짧은 정수로 바꿉니다.

| CSV 열 | XDM 경로 | 데이터 서식 |
| ---------- | -------- | --------------- |
| 제목 | person.name.courtesyTitle | 문자열로 복사 |
| F_NAME | person.name.firstName | 문자열로 복사 |
| L_NAME | person.name.lastName | 문자열로 복사 |
| 성별 | person.gender | Gender를 해당 person.gender 열거형 값으로 변환 |
| DOB | person.birthDayAndMonth: &quot;MM-DD&quot;<br/>person.birthDate: &quot;YYYY-MM-DD&quot;<br/>person.birthYear: YYYY | birthDayAndMonth를 문자열로 변환<br/>birthDate를 문자열로 변환<br/>birthYear를 짧은 int로 변환 |
| 이메일 | personalEmail.address | 문자열로 복사 |
| CRMID | identityMap.CRMID[{&quot;id&quot;:x, primary:false}] | idMap의 CRMID 배열에 문자열로 복사하고 기본 을 false로 설정합니다. |
| ECID | identityMap.ECID[{&quot;id&quot;:x, primary: false}] | idMap에서 ECID 배열의 첫 번째 항목에 문자열로 복사하고 기본 을 false로 설정합니다. |
| 충혈- | identityMap.LOYALTYID[{&quot;id&quot;:x, primary:true}] | identityMap의 LOYALTYID 배열에 문자열로 복사하고 Primary를 true로 설정합니다. |
| ECID2 | identityMap.ECID[{&quot;id&quot;:x, primary:false}] | idMap에서 ECID 배열의 두 번째 항목에 문자열로 복사하고 기본 을 false로 설정합니다. |
| 전화 | homePhone.number | 문자열로 복사 |
| 상세 주소 | homeAddress.street1 | 문자열로 복사 |
| 도시 | homeAddress.city | 문자열로 복사 |
| 시/도 | homeAddress.stateProvince | 문자열로 복사 |
| 국가 | homeAddress.country | 문자열로 복사 |
| ZIP | homeAddress.postalCode | 문자열로 복사 |
| LAT | homeAddress.latitude | double로 변환 |
| LONG | homeAddress.longitude | double로 변환 |


### 출력 XDM

다음 샘플은에 표시된 대로 XDM으로 변환된 CSV의 처음 두 행을 보여 줍니다. `CRM_profiles.json`:

```json
{
   "person": {
      "name": {
         "courtesyTitle": "Mr",
         "firstName": "Ewart",
         "lastName": "Bennedsen"
      },
      "gender": "male",
      "birthDayAndMonth": "09-25",
      "birthDate": "2004-09-25",
      "birthYear": 2004
   },
   "identityMap": {
      "CRMID": [{
         "id": "71a16013-d805-7ece-9ac4-8f2cd66e8eaa",
         "primary": false
      }],
      "ECID": [{
         "id": "87098882279810196101440938110216748923",
         "primary": false
      },
      {
         "id": "55019962992006103186215643814973128178",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e33192000007456-0365c00000000000",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "256-284-7231"
   },
   "personalEmail": {
      "address": "ebennedsenex@jiathis.com"
   },
   "homeAddress": {
      "street1": "72 Buhler Crossing",
      "city": "Anniston",
      "stateProvince": "Alabama",
      "country": "US",
      "postalCode": "36205",
      "_schema": {
         "latitude": 33.708276,
         "longitude": -85.7922905
      }
   }
},{
   "person": {
      "name": {
         "courtesyTitle": "Dr",
         "firstName": "Novelia",
         "lastName": "Ansteys"
      },
      "gender": "female",
      "birthDayAndMonth": "10-31",
      "birthDate": "1987-10-31",
      "birthYear": 1987
   },
   "identityMap": {
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
         "primary": false
      }],
      "ECID": [{
         "id": "50829196174854544323574004005273946998",
         "primary": false
      },
      {
         "id": "65233136134594262632703695260919939885",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "704-181-6371"
   },
   "personalEmail": {
      "address": "nansteysdk@spotify.com"
   },
   "homeAddress": {
      "street1": "79 Northfield Hill",
      "city": "Charlotte",
      "stateProvince": "North Carolina",
      "country": "US",
      "postalCode": "28299",
      "_schema": {
         "latitude": 35.2188655,
         "longitude": -80.8108888
      }
   }
}
```

## XDM 스키마에 대한 데이터 프레임

데이터 프레임의 계층 구조(예: Parquet 파일)는 업로드할 XDM 스키마의 계층과 일치해야 합니다.

### 데이터 프레임 예

다음 예제 데이터 프레임의 구조가 를 구현하는 스키마에 매핑되었습니다. [!DNL XDM Individual Profile] 클래스 및 에는 해당 형식의 스키마와 관련된 가장 일반적인 필드가 포함되어 있습니다.

```python
[
    StructField("person", StructType(
        [
            StructField("name", StructType(
                [
                    StructField("courtesyTitle", StringType()),
                    StructField("firstName", StringType()),
                    StructField("lastName", StringType())
                ]
            )),
            StructField("gender", StringType()),
            StructField("birthDayAndMonth", StringType()),
            StructField("birthDate", StringType()),
            StructField("birthYear", LongType())
        ]
    )),
    StructField("identityMap", MapType(
        StructField("CRMID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("ECID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("LOYALTYID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        ))
    )),
    StructField("homePhone", StructType(
        [
            StructField("number", StringType())
        ]
    )),
    StructField("personalEmail", StructType(
        [
            StructField("address", StringType())
        ]
    )),
    StructField("homeAddress", StructType(
        [
            StructField("street1", StringType()),
            StructField("city", StringType()),
            StructField("stateProvince", StringType()),
            StructField("country", StringType()),
            StructField("postalCode", StringType()),
            StructField("_schema", StructType(
                [
                    StructField("latitude", DoubleType()),
                    StructField("latitude", DoubleType()),
                ]
            ))
        ]
    ))    
]
```

Adobe Experience Platform에서 사용하기 위해 데이터 프레임을 구성할 때 필드가 제대로 매핑되도록 하려면 계층 구조가 기존 XDM 스키마와 정확히 일치하는지 확인하는 것이 중요합니다.

## ID와 ID 맵

### ID 배열

```json
[
  {
    "xdm:id": "someone1@example.com",
    "xdm:namespace": {
      "xdm:code": "Email"
    }
  },
  {
    "xdm:id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
    "xdm:namespace": {
      "xdm:code": "CRMID"
    }
  },
  {
    "xdm:id": "2e3319208000765b-3811c00000000001",
    "xdm:namespace": {
      "xdm:code": "LOYALTYID"
    }
  }
]
```

### 매핑

ID 배열에 대한 매핑 요구 사항은 다음 표에 요약되어 있습니다.

| ID 필드 | identityMap 필드 | 데이터 형식 |
| -------------- | ----------------- | --------- |
| id[0].id | identityMap[이메일][{"id"}] | 문자열로 복사 |
| id[1].id | identityMap[CRMID][{"id"}] | 문자열로 복사 |
| id[2].id | identityMap[충혈-][{"id"}] | 문자열로 복사 |

### 출력 XDM

다음은 XDM으로 변환된 ID 배열입니다.

```JSON
"identityMap": {
      "Email": [{
         "id": "someone1@example.com"
      }],
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5"
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001"
      }]
   }
```
