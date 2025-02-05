---
keywords: Experience Platform;시작하기;기여도 ai;인기 주제;기여도 ai 입력;기여도 ai 출력;기여도 ai 문제 해결;기여도 ai 오류
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Attribution AI 오류 문제 해결
description: Attribution AI에서 일반적인 오류에 대한 답변을 찾아보십시오.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Attribution AI 오류 문제 해결

이 문서에서는 Attribution AI에 대해 자주 묻는 질문에 대한 답변을 제공합니다.

## Chrome 시크릿 내 Attribution AI에 액세스할 수 없음

Google Chrome의 시크릿 모드 보안 설정의 업데이트로 인해 Google Chrome의 시크릿 모드에서 로드 오류가 발생합니다. experience.adobe.com 을 신뢰할 수 있는 도메인으로 만들기 위해 Chrome과 함께 문제가 활발하게 진행되고 있습니다.

![오류 이미지](./images/faq/error.PNG){width=500}

### 권장 수정 사항

이 문제를 해결하려면 experience.adobe.com 을 항상 쿠키를 사용할 수 있는 사이트로 추가해야 합니다. **chrome://settings/cookies**(으)로 이동하여 시작하십시오. 그런 다음 **사용자 지정된 동작** 섹션까지 아래로 스크롤한 다음 &quot;항상 쿠키를 사용할 수 있는 사이트&quot; 옆에 있는 **추가** 단추를 선택합니다. 표시되는 팝오버에서 `[*.]experience.adobe.com`을(를) 복사하여 붙여 넣은 다음 **이 사이트에 타사 쿠키 포함** 확인란을 선택합니다. 완료되면 **추가**&#x200B;를 선택하고 시크릿으로 Attribution AI을 다시 로드합니다.

![권장 수정](./images/faq/cookies2.gif)
