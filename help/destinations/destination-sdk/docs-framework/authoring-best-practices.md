---
title: 작성 모범 사례
description: 대상 설명서 페이지를 작성할 때 따라야 하는 규칙과 팁이 Adobe Experience Platform 설명서 품질 표준을 충족하는지 알아봅니다.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: 0b9b724c2530e43ce681011d12fc1341148ddbf5
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 작성 모범 사례

## 개요 {#overview}

이 페이지에서는 다음 경우에 따라야 하는 규칙에 대해 설명합니다. [대상 설명서 작성](./documentation-instructions.md) Adobe Experience Platform 설명서 품질 표준을 충족하는지 확인합니다.

## 일반 지침 {#general-guidance}

* 다음을 채울 때 [템플릿](./self-service-template.md) 대상 설명서에 대한 자세한 내용은 Adobe 기여자 안내서 를 참조하십시오. [연결](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [표](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), [지원되는 markdown 구문](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [작성 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)등.
* 제품 설명서에 관찰 및 추정을 포함하지 마십시오.
* Experience Platform 설명서에서 Adobe 작성자는 **굵은 서식** 다음과 같이 사용자 인터페이스 컨트롤을 참조하십시오.
   * 다음으로 이동 **[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 카탈로그]** 탭. 사용자 인터페이스 컨트롤이 [대상 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## 쓰기 스타일

>[!IMPORTANT]
>
>읽기 [Adobe 설명서 작성 지침 작성](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 대상 설명서 페이지 작성을 시작하기 전에

* 문장을 짧게 유지하고 요점을 빨리 파악하세요. 문장의 길이가 20단어 이상이거나 여러 개의 쉼표를 사용하는 경우 별도의 문장으로 구분하는 것을 고려하십시오. 길이가 20단어가 넘는 문장은 독자들에게 특히 어려울 수 있다.
* 너무 예의바르게 굴지 마라. 기술 설명서에서 &quot;제발&quot; 또는 &quot;친절하게...&quot;를 사용하지 마십시오.

## 연결 {#linking}

제공된 설명서 템플릿을 따르고 템플릿의 기존 링크를 편집하지 마십시오. 새 링크를 포함할 때 다음을 참조하십시오. [설명서에서 링크 사용](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) 콘텐츠 작가 가이드.

## 브랜딩 지침 {#branding}

* AEP는 승인된 공개 용어가 아닙니다. 처음 사용 시 Adobe Experience Platform을 사용한 다음 Experience Platform, 플랫폼을 사용하십시오.
   * **사용하지 않음**: AEP에서 YourDestination으로 데이터를 내보내려면 먼저 이러한 사전 요구 사항을 읽고 완료해야 합니다.
   * **사용**: Adobe Experience Platform에서 YourDestination으로 데이터를 내보내려면 먼저 이러한 사전 요구 사항을 읽고 완료해야 합니다.

## 이미지 및 스크린샷 {#images-and-screenshots}

* 다음에 대한 정보: [이미지에 연결하는 방법](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), 기여자 안내서 를 참조하십시오.
* 스크린샷을 사용할 때는 스크린샷이 전체 Platform UI 화면을 캡처하는지 확인하십시오.
* 이미지를 표시하여 페이지의 특정 컨트롤이나 레이블을 강조 표시할 때는 Experience Platform 설명서 팀에서 사용하는 마크업 스타일을 따라야 합니다. 에서 프로필 기반 이 어떻게 강조 표시되는지 확인합니다 [이 스크린샷](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 다음을 사용하십시오. `png` 이미지 형식을 지정합니다.
* 번호가 매겨진 스크린샷을 파일 이름으로 사용하지 마십시오. 이미지 파일 이름은 설명적이어야 합니다.
   * **사용하지 않음**: `1.png`, `2.png`, `3.png`
   * **사용**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 설명서에 추가하는 이미지에 대해서는 대체 텍스트를 사용하고 대체 텍스트에 적절한 문법을 사용하십시오.
   * **사용하지 않음**: 대상 연결 세부 정보
   * **사용**: 채워진 대상 연결 세부 정보를 보여주는 Platform UI의 이미지.

## 프로세스 {#process}

* 다음 [설명서 템플릿](./self-service-template.md) 은 파트너 피드백을 기반으로 자주 업데이트되지 않습니다. 대상에 대한 설명서 작성을 시작하기 전에 [템플릿의 최신 버전](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* 설명서를 작성하고 포크의 분기에서 설명서 가져오기 요청(PR)을 만듭니다 *주분지 제외*. 에서 작성할 때 검토용 제출 대상 섹션을 참조하십시오. [GitHub 인터페이스](./use-github-interface-to-create-documentation.md#submit-review) 또는 [로컬 환경](./work-in-local-environment.md#submit-review).
