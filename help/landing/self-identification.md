---
title: 자체 식별 설문 조사를 사용하여 Experience Platform 개인 프로필 구축
description: 자기 식별 설문 조사 UI를 사용하여 직무 기능 및 관련 목표에 따라 관련 콘텐츠를 수신하는 방법에 대해 알아봅니다.
badge: Beta
exl-id: 80b3f55f-1eab-4a99-be75-49bd091f9739
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 16%

---

# 자체 식별 설문 조사를 사용하여 Experience Platform 개인 프로필 구축

>[!NOTE]
>
>그 자기 식별 조사는 베타에 있다. 기능 및 설명서는 변경될 수 있습니다.

자가 식별 설문 조사는 Adobe Experience Platform UI 홈 페이지에 표시되는 짧은 설문지입니다. 설문지를 작성하시면 직무에 대한 정보와 일반적인 목표를 알 수 있습니다. 그런 다음 이 정보를 사용하여 제품 내 안내서를 보다 효과적으로 조정하고 궁극적으로 목표에 더 적합한 콘텐츠를 제공합니다.

이 문서에서는 Experience Platform UI에서 자체 식별 설문 조사를 사용하여 목표 및 작업에 따라 관련 콘텐츠를 수신하는 방법과 UI를 사용하여 개인 프로필 속성을 재구성하는 방법에 대한 정보를 제공합니다.

Adobe Experience Platform에 대한 자세한 내용은 [Experience Platform 개요](home.md)를 참조하세요.

## Experience Platform UI의 자체 식별 설문 조사

로그인 시 Experience Platform UI 홈 페이지의 오른쪽 하단에 본인 확인 설문 조사 프롬프트가 표시됩니다.

설문 조사를 시작하려면 **[!UICONTROL 시작]**&#x200B;을 선택하세요.

![자체 식별 설문 조사를 시작하라는 알림 메시지가 표시된 Experience Platform UI 홈 페이지입니다.](./images/survey/survey-prompt.png)

첫 번째 설문 조사 질문에 자신의 작품을 가장 잘 설명하는 함수를 선택합니다.

사용 가능한 옵션은 다음과 같습니다.

* 관리
* 엔지니어링
* 개인정보 보호 및 거버넌스
* 마케팅
* 기타

>[!NOTE]
>
>옵션 목록에서 두 개 이상의 함수를 선택할 수 있습니다. [!UICONTROL 기타]를 선택하면 목표에 대한 세부 정보를 입력하라는 메시지가 표시됩니다.

계속하려면 현재 작업을 가장 잘 설명하는 함수를 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택하세요.

![두 개의 작업 기능이 선택된 자체 식별 설문 조사.](./images/survey/select-functions.png)

그런 다음 작업에 가장 잘 적용되는 특정 목표를 선택합니다.

사용 가능한 목표 목록은 다음과 같습니다.

* 사용자 생성 및 관리
* 역할, 권한 및 제품 프로필 할당
* 라이선스 사용, 샌드박스 및 알림 관리
* 데이터 수집을 위한 시스템 구성
* 내 조직의 데이터 구조 모델링
* 통찰력을 생성하기 위해 데이터 쿼리, 필터링 및 최적화
* 동의 및 데이터 정책 구성
* 데이터 거버넌스 및 개인정보 보호 규정 준수
* 마케팅 전략 개발
* 대상자 생성, 관리 및 분류
* 비즈니스 영향 분석을 위한 대시보드 설정
* 다운스트림 타겟팅을 위해 데이터를 대상으로 활성화

완료되면 **[!UICONTROL 제출]**&#x200B;을 선택하세요.

![자체 식별 설문 조사에 선택할 수 있는 목표 목록이 표시됩니다.](./images/survey/select-objectives.png)

자체 식별 조사가 완료되면 **[!UICONTROL 완료]**&#x200B;를 선택하세요.

![자체 식별 설문 조사의 마지막 확인 단계입니다.](./images/survey/survey-complete.png)

>[!NOTE]
>
>목표 및 권장 사항(있는 경우)은 선택한 Job 기능에 따라 변경됩니다.

## 설문 조사 응답 업데이트

Experience Cloud 환경 설정 메뉴를 사용하여 작업 기능 및 개체를 업데이트합니다. 환경 설정 메뉴에 액세스하려면 위쪽 탐색에서 프로필 아이콘을 선택한 다음 **[!UICONTROL 환경 설정]**&#x200B;을 선택하십시오.

![프로필 아이콘과 환경 설정 단추가 선택된 Experience Platform UI 홈 페이지입니다.](./images/survey/preferences.png)

그런 다음 프로필 환경 설정 메뉴의 [!UICONTROL 일반] 섹션에서 **[!UICONTROL 작업 기능 및 목표 업데이트]**&#x200B;를 선택합니다.

![Experience Platform UI 프로필 환경 설정 페이지의 일반 섹션](./images/survey/update.png)

자체 식별 설문 조사가 표시되어 응답을 다시 구성하고 프로필을 업데이트할 수 있습니다.

![Experience Platform UI 프로필 환경 설정 페이지에 사용자가 개인 프로필을 업데이트할 수 있도록 하는 자체 식별 설문 조사가 표시됩니다.](./images/survey/new-survey.png)

## 다음 단계

이 문서를 읽은 후에는 Experience Platform UI 사용 시 더 관련성 있는 콘텐츠를 받기 위해 작업 기능 및 목표에 대한 정보를 제출하고 업데이트했습니다. Experience Platform UI에 대한 자세한 내용은 [Experience Platform 개요](home.md)를 참조하십시오.
