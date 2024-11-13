---
title: AI Assistant를 사용하여 XDM 필드 검색
description: XDM(Experience Data Model) 필드 검색을 위해 AI Assistant를 사용하는 방법에 대해 알아보려면 이 문서 를 참조하십시오.
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# AI Assistant를 사용한 XDM 필드 검색

>[!AVAILABILITY]
>
>이 기능은 Alpha 중이며 조직에서 사용하지 못할 수 있습니다. Alpha 프로그램에 참여하고 이 기능에 액세스하려면 Adobe 계정 팀에 문의하십시오.

AI Assistant를 사용하여 Experience Platform 내에서 타깃팅된 대상을 생성하는 데 사용할 수 있는 XDM(Experience Data Model) 필드를 검색하고 검색할 수 있습니다.

AI Assistant에서 XDM 필드 검색에 대해 지원되는 쿼리 및 프롬프트 패턴은 다음 표를 참조하십시오.

>[!TIP]
>
>쿼리 및 프롬프트 패턴은 다양한 사용 사례에서 동일할 수 있지만, 특정 샌드박스에 사용되는 XDM 필드 및 스키마에 따라 질문의 정확한 공식이 달라집니다.

| 쿼리 유형 | 쿼리/프롬프트 패턴 | 예시 |
| --- | --- | --- |
| 데이터 도메인 또는 영역별 XDM 필드 검색 | {DATA_DOMAIN/AREA}을(를) 표시하는 데 사용되는 XDM 필드 표시 | <ul><li>동의 데이터를 표시하는 데 사용되는 XDM 필드를 표시합니다.</li><li>이메일 구독에 대한 정보를 표시하는 데 사용되는 XDM 필드 표시</li></ul> |
| 일반 필드 이름별 XDM 필드 검색 | <ul><li>{DATA_DOMAIN/AREA}과(와) 관련된 XDM 필드 표시</li><li>{GENERAL_FIELD_NAME}이(가) 포함된 XDM 필드.</li></ul> | <ul><li>주문과 관련된 XDM 필드 표시.</li><li>인터랙션 세부 정보와 관련된 XDM 필드 표시.</li><li>방문자 ID가 포함된 XDM 필드는 무엇입니까?</li><li>제품 카테고리를 포함하는 XDM 필드는 무엇입니까?</li></ul> |
| 데이터 모델 계보를 통한 XDM 필드 검색 | <ul><li>{GENERAL_FIELD_NAME}이(가) 포함된 {FIELD_GROUP/CLASS_NAME}의 모든 필드를 표시합니다.</li><li>XDM 필드 {GENERAL_FIELD_NAME}의 {FIELD_GROUP/CLASS_NAME}은(는) 무엇입니까?</li></ul> | <ul><li>제품 데이터가 포함된 필드 그룹의 모든 필드를 표시합니다.</li><li>분석 데이터가 포함된 필드 그룹의 모든 필드를 표시합니다.</li><li>XDM 필드 이름의 클래스는 무엇입니까?</li><li>XDM 필드 이메일 구독의 클래스는 무엇입니까?</li></ul> |
| 필드 이름과 함께 향상된 설명을 가져오도록 메시지 표시 | {FIELD_DISCOVERY_QUERY}. 향상된 설명도 포함됩니다. | <ul><li>동의 데이터를 표시하는 데 사용되는 XDM 필드를 표시합니다. 필드에 대한 향상된 설명도 포함합니다.</li><li>인터랙션 세부 정보와 관련된 XDM 필드 표시. 필드에 대한 향상된 설명도 포함합니다.</li></ul> |

{style="table-layout:auto"}