---
title: B2B 소스 데이터 유형
description: 이 문서에서는 B2B 소스 경험 데이터 모델(XDM) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 3%

---

# [!UICONTROL B2B 소스] 데이터 유형

[!UICONTROL B2B 소스] 는 B2B 엔티티(예: [account](../classes/b2b/business-account.md), [기회](../classes/b2b/business-opportunity.md)또는 [campaign](../classes/b2b/business-campaign.md)).

문자열 기반 식별자에만 의존하는 경우, 여러 시스템의 ID 간에 겹칠 수 있습니다(예: 한 CRM 시스템에서 기회에 문자열 ID를 지정할 수 있지만 동일한 ID가 완전히 다른 기회를 참조할 수 있음). 이를 통해 데이터를 병합할 때 데이터 충돌이 발생할 수 있습니다 [실시간 고객 프로필](../../profile/home.md).

다음 [!UICONTROL B2B 소스] 데이터 유형을 사용하면 엔티티의 원래 문자열 ID를 사용하고 이를 소스 특정 컨텍스트 정보와 결합하여 원본 소스와 관계없이 Platform 시스템에서 완전히 고유하도록 유지할 수 있습니다.

![B2B 소스 구조](../images/data-types/b2b-source.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `sourceID` | 문자열 | 소스 레코드에 대한 고유 ID입니다. |
| `sourceInstanceID` | 문자열 | 소스 데이터의 인스턴스 또는 조직 ID입니다. |
| `sourceKey` | 문자열 | 로 구성된 고유 식별자입니다 `sourceId`, `sourceInstanceId`, 및 `sourceType` 다음 형식으로 함께 연결합니다. `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Marketo과 같은 일부 소스 커넥터는 특정 식별자에 대해 이 값을 자동으로 연결합니다. 다른 항목은 를 사용하여 수동으로 연결해야 합니다 [데이터 준비 `concat` 함수](../../data-prep/functions.md#string), 예: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 문자열 | 소스 데이터를 제공하는 플랫폼의 이름입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
