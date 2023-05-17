---
title: 작성 우수 사례
description: 대상 설명서 페이지를 작성할 때 따라야 하는 규칙과 팁을 확인하여 Adobe Experience Platform 설명서 품질 표준을 충족하는지 알아보십시오.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 작성 우수 사례

## 개요 {#overview}

이 페이지에서는 다음에 따라야 하는 규칙에 대해 설명합니다 [대상 문서 작성](./documentation-instructions.md) Adobe Experience Platform 설명서 품질 표준을 충족하는지 확인합니다.

## 일반 지침 {#general-guidance}

* 을 채울 때 [템플릿](./self-service-template.md) 대상 설명서의 경우 Adobe 기여자 안내서 를 참조하십시오 [연결](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [표](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), [지원되는 markdown 구문](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [작성 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en), 등.
* 제품 설명서에는 관찰 및 견적을 포함하지 마십시오.
* Experience Platform 설명서에서 Adobe 작성자는 **굵게 서식** 다음과 같은 사용자 인터페이스 컨트롤을 참조하십시오.
   * 이동 **[!UICONTROL 연결]** > **[!UICONTROL 대상]**, 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 카탈로그]** 탭. 사용자 인터페이스 컨트롤이 [대상 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## 쓰기 스타일

>[!IMPORTANT]
>
>읽기 [Adobe 설명서 작성 지침 작성](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 대상 설명서 페이지 작성을 시작하기 전에

* 문장을 짧게 유지한 다음 요점을 빨리 이해하세요. 문장이 20단어를 초과하거나 여러 개의 쉼표를 사용하는 경우 구분하는 것이 좋습니다. 길이가 20단어를 초과하는 문장은 독자들에게 특히 도전적일 수 있다.
* 지나치게 예의 바르지 마라. &quot;제발&quot; 또는 &quot;친절하게 하십시오...&quot;를 사용하지 마십시오. 참조하십시오.

## 연결 {#linking}

제공된 설명서 템플릿을 따르고 템플릿에 있는 기존 링크를 편집하지 않습니다. 새 링크를 포함할 때 [설명서에서 링크 사용](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) 기여자 가이드에서 참조할 수 있습니다.

## 브랜딩 지침 {#branding}

* AEP는 승인된 공개 용어가 아닙니다. 먼저 Adobe Experience Platform을 사용한 다음, Experience Platform, 플랫폼 순으로 사용하십시오.
   * **사용 안 함**: AEP에서 YourDestination으로 데이터를 내보내려면 먼저 이러한 사전 요구 사항을 읽고 완료해야 합니다.
   * **사용**: Adobe Experience Platform에서 YourDestination으로 데이터를 내보내려면 먼저 이러한 사전 요구 사항을 읽고 완료해야 합니다.

## 이미지 및 스크린샷 {#images-and-screenshots}

* 에 대한 자세한 정보 [이미지에 연결하는 방법](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), 기여자 안내서 를 참조하십시오.
* 스크린샷을 사용할 때는 스크린샷이 전체 플랫폼 UI 화면을 캡처하는지 확인하십시오.
* 페이지에서 특정 컨트롤이나 레이블을 강조 표시하기 위해 이미지를 표시할 때 Experience Platform 설명서 팀에서 사용하는 마크업 스타일을 따르도록 하십시오. 프로필 기반의 이 강조되는 방법을 확인하십시오. [이 스크린샷](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 사용 `png` 이미지 형식 지정
* 번호가 매겨진 스크린샷을 파일 이름으로 사용하지 마십시오. 이미지 파일 이름은 설명적이어야 합니다.
   * **사용 안 함**: `1.png`, `2.png`, `3.png`
   * **사용**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 설명서에 추가하는 이미지에 대해 대체 텍스트를 사용하고 대체 텍스트에 적절한 문법을 사용하십시오.
   * **사용 안 함**: 대상 연결 세부 정보
   * **사용**: Platform UI의 이미지. 채워진 대상 연결 세부 정보를 표시합니다.

## 프로세스 {#process}

* 다음 [설명서 템플릿](./self-service-template.md) 파트너 피드백을 기반으로 자주 업데이트됩니다. 대상에 대한 문서 작성을 시작하기 전에 [템플릿의 최신 버전](../assets/docs-framework/yourdestination-template.zip).
* 설명서를 작성하고 포크의 분기에서 PR(설명서 가져오기 요청)을 만듭니다 *주 분기 이외의 다른*. 에서 작성할 때 검토용 제출 대상 섹션을 참조하십시오. [GitHub 인터페이스](./use-github-interface-to-create-documentation.md#submit-review) 또는 [로컬 환경](./work-in-local-environment.md#submit-review).
