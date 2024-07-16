---
title: 계정 세부 정보 데이터 유형
description: 계정 세부 사항 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 11%

---

# [!UICONTROL 계정 세부 정보] 데이터 형식

[!UICONTROL 계정 세부 정보]은(는) 비즈니스 조직과 관련된 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다.

![데이터 형식 구조](../images/data-types/account-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 통화]](./currency.md) | 조직의 예상 연간 매출액. |
| `DUNSNumber` | 문자열 | 조직의 Dun &amp; Bradstreet D-U-N-S 번호. 이는 고유하고 별개이며 서로 구분되는 Dun &amp; Bradstreet 데이터베이스의 각 사업장에 할당된 9자리 비식별 번호로 Dun &amp; Bradstreet가 단독으로 관리합니다. |
| `NAICSCode` | 문자열 | 북미 산업 분류 체계 내에서 조직의 분류. |
| `NAICSDescription` | 문자열 | NAICS 코드를 기반으로 한 조직의 기간 업무에 대한 간략한 설명. |
| `SICCode` | 문자열 | 조직의 표준 산업 분류(SIC) 코드입니다. 기업 활동을 기반으로 기업이 속한 업계를 분류하는 4자리 코드다. |
| `SICDescription` | 문자열 | SIC 코드를 기반으로 한 조직의 기간 업무에 대한 간략한 설명. |
| `companyProductAndServices` | 문자열 | 조직에서 처리하거나 비즈니스를 수행하는 제품 및 서비스. |
| `facebookPageUrl` | 문자열 | 조직의 Facebook 계정에 대한 웹 사이트 링크입니다. |
| `industry` | 문자열 | 이 조직이 속해 있는 산업입니다. 자유 형식의 필드이며 쿼리에 대해 구조화된 값을 사용하거나 `xdm:classifier` 속성을 사용하는 것이 좋습니다. |
| `jigsaw` | 문자열 | 조직의 Data.com 키입니다. |
| `linkedinPageUrl` | 문자열 | 조직의 LinkedIn 계정에 대한 웹 사이트 링크입니다. |
| `logoUrl` | 문자열 | 조직과 연결된 소셜 네트워크 프로필 이미지를 요청할 URL을 생성하기 위해 Salesforce 인스턴스의 URL과 결합할 경로(예: `https://yourInstance.salesforce.com/`)입니다. 생성된 URL은 조직의 소셜 네트워크 프로필 이미지에 대한 HTTP 리디렉션(코드 302)을 반환합니다. |
| `marketSegment` | 문자열 | 조직이 참여하는 지정된 시장 대상자입니다. 자유 형식의 필드이며 쿼리에 대해 구조화된 값을 사용하거나 `xdm:identifier` 속성을 사용하는 것이 좋습니다. |
| `numberOfEmployees` | 정수 | 조직의 직원 수. |
| `organizationType` | 문자열 | 조직 유형을 설명하는 레이블입니다. |
| `primaryEmailDomain` | 문자열 | 조직에서 직원에게 사용하는 기본 이메일 도메인입니다. |
| `rating` | 더블 | 이 조직에 대한 계산된 점수 또는 별점. `1`은(는) 가능한 최대 등급을 나타내고 `0`은(는) 가능한 최소 등급입니다. |
| `tickerSymbol` | 문자열 | 해당 계정의 스톡 마켓 기호. 최대 20자. |
| `twitterHandleUrl` | 문자열 | 조직의 twitter 핸들에 대한 웹 사이트 링크입니다. |
| `website` | 문자열 | 조직 웹 사이트의 URL. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
