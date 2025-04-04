---
title: B2B Source 데이터 유형
description: B2B Source XDM(Experience Data Model) 데이터 유형에 대해 알아봅니다.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL B2B Source] 데이터 형식

[!UICONTROL B2B Source]은(는) B2B 엔터티(예: [account](../classes/b2b/business-account.md), [opportunity](../classes/b2b/business-opportunity.md) 또는 [campaign](../classes/b2b/business-campaign.md))의 복합 식별자를 나타내는 표준 XDM(Experience Data Model) 데이터 형식입니다.

문자열 기반 식별자에만 의존하는 경우 여러 시스템에서 ID 간에 겹치는 경우가 있습니다(예: 한 CRM 시스템에서 영업 기회에 문자열 ID를 제공할 수 있지만, 동일한 ID가 완전히 다른 영업 기회를 의미할 수 있음). 이렇게 하면 [실시간 고객 프로필](../../profile/home.md)에서 데이터를 병합할 때 데이터가 충돌할 수 있습니다.

[!UICONTROL B2B Source] 데이터 형식을 사용하면 엔터티의 원래 문자열 ID를 사용하고 이를 소스별 컨텍스트 정보와 결합하여 원본과 관계없이 Experience Platform 시스템에서 완전히 고유한 상태를 유지할 수 있습니다.

![B2B Source 구조](../images/data-types/b2b-source.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `sourceID` | 문자열 | 소스 레코드에 대한 고유 ID. |
| `sourceInstanceID` | 문자열 | 소스 데이터의 인스턴스 또는 조직 ID입니다. |
| `sourceKey` | 문자열 | `sourceId`, `sourceInstanceId` 및 `sourceType`이(가) 연결된 `[sourceID]@[sourceInstanceID].[sourceType]` 형식의 고유 식별자입니다.<br><br>Marketo과 같은 일부 소스 커넥터는 특정 식별자에 대해 이 값을 자동으로 연결합니다. 다른 항목은 [데이터 준비 `concat` 함수](../../data-prep/functions.md#string)를 사용하여 수동으로 연결해야 합니다. 예: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 문자열 | 소스 데이터를 제공하는 플랫폼의 이름입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
