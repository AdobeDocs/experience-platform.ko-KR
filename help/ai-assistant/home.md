---
title: Adobe Experience Platform의 AI Assistant 개요
description: AI 어시스턴트, 그 미묘한 차이와 사용 사례, 그리고 이를 사용하여 Adobe Experience Platform 및 Real-Time Customer Data Platform을 통해 워크플로를 가속화하는 방법에 대해 알아봅니다.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: fc87c28d7019e123d974e4d2ad307928a3d3fe89
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 8%

---

# Adobe Experience Platform의 AI 지원

Adobe Experience Platform의 AI Assistant에 대해 알아보려면 이 문서를 참조하십시오.

Adobe Experience Platform의 AI Assistant는 Adobe 애플리케이션에서 워크플로를 가속화하는 데 사용할 수 있는 대화형 경험입니다. AI Assistant를 사용하여 제품 지식을 보다 잘 이해하고, 문제를 해결하거나, 정보를 검색하고, 운영 통찰력을 찾을 수 있습니다. AI Assistant는 Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer 및 Customer Journey Analytics을 지원합니다.

![처음 사용자 경험이 트리거된 AI Assistant 인터페이스입니다.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>AI Assistant를 사용하려면 [사용자 계약](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)에 동의해야 합니다. 사용자 계약에는 공개 베타 계약도 포함되어 있습니다. 추가 AI Assistant 기능이 Beta 용량으로 롤아웃될 때 이를 사용할 수 있도록 합니다.

+++사용자 계약 인터페이스를 보려면 선택

![사용자 계약의 첫 페이지입니다.](./images/user-agreement-1.png)

![사용자 계약의 마지막 페이지입니다.](./images/user-agreement-2.png)

+++

## AI Assistant 이해 {#understanding-ai-assistant}

AI Assistant는 데이터베이스에 질의한 다음 데이터베이스의 데이터를 사람이 읽을 수 있는 답변으로 변환하여 제출된 질문에 응답합니다.

기본 데이터의 이러한 내부 표현은 **[!DNL Knowledge Graph]**&#x200B;이라고도 합니다. 이는 특정 질문에 대한 개념, 데이터 및 메타데이터의 포괄적인 웹입니다.

[!DNL Knowledge Graph]은(는) 쿼리가 제출될 때마다 참조되는 하위 그래프로 구성됩니다.

* 고객 운영 통찰력.
* 다양한 메타 스토어에서 고객 운영 통찰력.
* Experience League 설명서입니다.

AI Assistant를 쿼리하기 전에 고려해야 할 두 가지 유형의 질문이 있습니다.

### 제품 지식 {#product-knowledge}

제품 지식은 Experience League 설명서에 기반을 둔 개념과 주제를 의미합니다. 제품 지식 질문은 다음 하위 그룹에 추가로 지정할 수 있습니다.

| 제품 지식 | 예시 |
| --- | --- |
| 뾰족한 학습 | <ul><li>ID와 기본 또는 외래 키 간의 차이점은 무엇입니까?</li><li>프로필 풍부성은 어떻게 계산됩니까?</li></ul> |
| 검색 열기 | <ul><li>이 데이터 세트를 내보내려면 어떻게 해야 합니까?</li><li>의료 서비스 고객을 위한 스키마가 있습니까?</li></ul> |
| 문제 해결 | <ul><li>프로필에 대해 Adobe 소유의 스키마를 켤 수 없는 이유는 무엇입니까?</li><li>세그먼트를 삭제할 수 없는 이유</li></ul> |

{style="table-layout:auto"}

### 운영 인사이트 {#operational-insights}

>[!IMPORTANT]
>
>Operational Insights 답변은 Beta 버전입니다. **Operational Insights 보기** 권한에 대한 액세스 권한이 있는 모든 사용자는 Operational Insights 응답에 액세스할 수 있습니다.

운영 인사이트는 카운트, 조회 및 계보 영향을 포함하여 AI 비서가 메타 데이터 개체(속성, 대상, 데이터 흐름, 데이터 세트, 대상, 여정, 스키마 및 소스)에 대해 생성하는 답변을 말합니다. 샌드박스 내의 데이터는 보지 않습니다.

* 보유한 데이터 세트는 몇 개입니까?
* 사용된 적이 없는 스키마 속성 수는 몇 개입니까?
* 활성화된 대상은 무엇입니까?

다음 도메인에서 운영 통찰력에 대해 AI Assistant에 질문할 수 있습니다.

| 도메인 | 지원되는 메타데이터 | 지원되지 않는 메타데이터 |
| --- | --- | --- |
| 속성 | <ul><li>속성 이름 검색</li><li>속성 - 스키마 관계</li><li>속성 - 데이터 세트 관계</li><li>속성 - 대상 관계</li><li>속성 - 대상 관계</li></ul> | <ul><li>Attribute 클래스</li><li>감사</li><li>사용 중단 상태</li><li>레이블</li><li>속성에 저장된 값</li></ul> |
| 대상자 | <ul><li>대상자 수</li><li>대상자 유형(스트리밍 또는 일괄 처리)</li><li>생성/수정 날짜</li><li>활성화 상태</li><li>프로필 개수</li><li>중복 대상자</li><li>대상 정의 검색</li><li>대상 - 대상 관계</li><li>대상 - 속성 관계</li><li>대상자 - 데이터 세트 관계</li><li>대상 - 대상 관계</li><li>이름 검색</li><li>이름 및 ID 검색 | <ul><li>대상 겹침</li><li>대상자 활성화</li><li>대상자 - 캠페인 관계</li><li>감사</li><li>만들기/수정</li><li>레이블</li><li>프로필 자격 트렌드</li></ul> |
| 데이터 흐름 | <ul><li>데이터 흐름 카운트</li><li>데이터 흐름 상태</li><li>데이터 흐름 - 데이터 세트 관계</li><li>데이터 흐름 - 소스 관계</li></ul> | <ul><li>생성/수정</li><li>데이터 흐름 일괄 처리 관계</li><li>프로필 개수 수집</li></ul> |
| 데이터 세트 | <ul><li>데이터 세트 수</li><li>프로필 활성화 상태</li><li>생성/수정 날짜</li><li>데이터 세트 - 스키마 관계</li><li>데이터 세트 - 대상 관계</li><li>데이터 세트 - 속성 관계</li><li>데이터 세트 - 데이터 흐름 관계</li><li>이름 검색 </li><li>이름 및 ID 검색</li></ul> | <ul><li>감사</li><li>제작자</li><li>데이터 세트 - 일괄 처리 관계</li><li>데이터 세트 생성/수정</li><li>데이터 세트 크기</li><li>프로필 수</li><li>행 수</li><li>값 검색</li></ul> |
| 대상 | <ul><li>구성된 대상 카운트</li><li>대상 - 대상 관계</li><li>대상 속성 관계</li></ul> | <ul><li>계정 설정</li><li>계정 자격 증명 정보</li><li>고유 프로필 활성화됨</li></ul> |
| 여정 | <ul><li>카운트</li><li>이름 검색</li><li>이름 및 ID 검색</li><li>여정 상태</li><li>트리거된 상태(대상자 대 이벤트)</li><li>생성/수정 날짜</li><li>반복 빈도</li></ul> | <ul><li>속성 - 여정 관계</li><li>감사</li><li>생성/수정</li><li>제작자</li><li>이벤트</li><li>여정 - 데이터 세트</li><li>여정 - 스키마</li><li>오퍼</li><li>프로필 자격 트렌드</li><li>단계 이벤트</li></ul> |
| 스키마 | <ul><li>스키마 카운트</li><li>생성/수정 날짜</li><li>스키마 - 속성 관계</li><li>스키마 - 데이터 세트 관계</li><li>스키마 - 대상 관계</li><li>프로필 활성화 상태</li><li>이름 검색</li><li>이름 및 ID 검색</li></ul> | <ul><li>감사</li><li>생성/수정</li><li>제작자</li><li>필드 그룹</li><li>ID</li><li>ID 네임스페이스</li><li>레이블</li><li>프로필 수</li></ul> |
| 소스 | <ul><li>계정 수</li><li>계정 상태</li><li>각 계정에 대한 활성/비활성 데이터 흐름</li><li>Source 커넥터 - 데이터 흐름 관계</li><li>Source 계정 - 데이터 흐름 관계</li></ul> | <ul><li>계정 자격 증명 정보</li><li>계정 설정</li><li>데이터 수집 지표</li><li>프로필 수</li><li>Source - 일괄 처리 관계</li></ul> |

{style="table-layout:auto"}

운영 통찰력 질문에 대한 답변이 UI의 현재 상태를 반영하지 않을 수 있습니다. 이러한 질문을 뒷받침하는 데이터는 24시간마다 한 번씩 업데이트됩니다. 예를 들어 사용자가 낮에 Real-Time CDP에서 수행하는 변경 사항은 밤에 데이터 스토어와 동기화된 다음 아침에 사용자 질문에 대해 사용할 수 있게 됩니다. 객체와 관련된 특정 데이터를 조회하려면 샌드박스에 로그인해야 합니다.

### 기능 범위 {#feature-scope}

현재 AI Assistant의 범위는 다음과 같습니다.

* [제품 지식](./home.md#product-knowledge): AI Assistant는 Experience Platform, Real-time Customer Data Platform 및 Adobe Journey Optimizer에 대한 제품 지식 질문에 답변할 수 있습니다. Customer Journey Analytics을 위해 제품 지식 항목을 자세히 살펴볼 수도 있지만, Customer Journey Analytics UI를 통해서만 가능합니다.
* [작동 인사이트](./home.md#operational-insights): 특성, 대상, 데이터 흐름, 데이터 세트, 대상, 여정, 스키마 및 원본과 같은 데이터 개체에 대한 작동 인사이트에 대한 질문과 함께 AI Assistant에 물을 수 있습니다.

## 다음 단계

이제 AI Assistant에 대해 전반적으로 이해했으므로 워크플로우 동안 AI Assistant를 계속 사용하여 사용할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [AI Assistant UI 안내서](./ui-guide.md)
* [기능 액세스](./access.md)
* [질문 안내서](./questions.md)
* [AI Assistant의 개인정보 보호, 보안 및 거버넌스](./privacy.md)
* [FAQ](./faq.md)
