---
title: 계정 세부 사항 데이터 유형
description: 이 문서에서는 계정 세부 사항 XDM(경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# [!UICONTROL 계정 세부 사항] 데이터 유형

[!UICONTROL 계정 세부 사항] 는 비즈니스 조직과 관련된 세부 사항을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

![데이터 유형 구조](../images/data-types/account-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 통화]](./currency.md) | 조직의 연간 예상 매출액. |
| `DUNSNumber` | 문자열 | 조직의 Dun &amp; Bradstreet D-U-N-S 번호입니다. 이는 고유한 개별 개별 작업을 갖는 Dun &amp; Bradstreet 데이터베이스의 각 비즈니스 위치에 지정된 비표시 9자리 숫자이며 Dun &amp; Bradstreet에 의해 단독으로 유지됩니다. |
| `NAICSCode` | 문자열 | 북미 산업 분류 체계 내의 조직의 분류. |
| `NAICSDescription` | 문자열 | NIC 코드를 기반으로 한 조직의 업무 라인에 대한 간략한 설명입니다. |
| `SICCode` | 문자열 | 조직의 표준 산업 분류(SIC) 코드입니다. 이 코드는 기업이 비즈니스 활동을 기반으로 속한 산업을 분류하는 4자리 코드입니다. |
| `SICDescription` | 문자열 | SIC 코드를 기반으로 한 조직의 업무 라인에 대한 간략한 설명. |
| `companyProductAndServices` | 문자열 | 조직에서 처리하거나 비즈니스를 수행하는 제품 및 서비스입니다. |
| `facebookPageUrl` | 문자열 | 조직의 Facebook 계정에 대한 웹 사이트 링크. |
| `industry` | 문자열 | 이 조직이 속해 있는 업계 자유 형식 필드이므로 쿼리에 구조화된 값을 사용하거나 `xdm:classifier` 속성을 사용합니다. |
| `jigsaw` | 문자열 | 조직에 대한 Data.com 키입니다. |
| `linkedinPageUrl` | 문자열 | 조직의 LinkedIn 계정에 대한 웹 사이트 링크. |
| `logoUrl` | 문자열 | Salesforce 인스턴스의 URL과 결합할 경로(예: `https://yourInstance.salesforce.com/`)를 생성하여 조직과 연결된 소셜 네트워크 프로필 이미지를 요청할 수 있습니다. 생성된 URL은 조직의 소셜 네트워크 프로필 이미지에 대한 HTTP 리디렉션(코드 302)을 반환합니다. |
| `marketSegment` | 문자열 | 조직이 참여하는 명명된 시장 세그먼트입니다. 자유 형식 필드이므로 쿼리에 구조화된 값을 사용하거나 `xdm:identifier` 속성을 사용합니다. |
| `numberOfEmployees` | 정수 | 조직의 직원 수입니다. |
| `organizationType` | 문자열 | 조직 유형을 설명하는 레이블입니다. |
| `primaryEmailDomain` | 문자열 | 조직이 해당 직원에 사용하는 기본 이메일 도메인입니다. |
| `rating` | 이중 | 이 조직에 대한 계산된 점수 또는 별 등급입니다. `1` 가능한 최대 등급을 나타내며 `0` 는 가능한 최소 등급입니다. |
| `tickerSymbol` | 문자열 | 이 계정의 주식 시장 기호입니다. 최대 20자. |
| `twitterHandleUrl` | 문자열 | 조직의 twitter 핸들에 대한 웹 사이트 링크. |
| `website` | 문자열 | 조직 웹 사이트의 URL입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
