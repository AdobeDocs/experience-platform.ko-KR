---
title: 작성 모범 사례
description: 대상 설명서 페이지를 작성할 때 따라야 하는 규칙과 팁이 Adobe Experience Platform 설명서 품질 표준을 충족하는지 알아봅니다.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 작성 모범 사례

## 개요 {#overview}

이 페이지에서는 [대상 설명서를 작성](./documentation-instructions.md) 페이지를 작성할 때 Adobe Experience Platform 설명서 품질 표준을 충족하도록 따라야 하는 규칙에 대해 설명합니다.

## 일반 지침 {#general-guidance}

* 대상 설명서의 [템플릿](./self-service-template.md)을(를) 채우는 경우 [연결](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), [테이블](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), [지원되는 Markdown 구문](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), [작성 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) 등에 대한 자세한 내용은 Adobe 기여자 안내서를 참조하십시오.
* 제품 설명서에 관찰 및 추정을 포함하지 마십시오.
* Experience Platform 설명서에서 Adobe 작성자는 **굵은 서식**&#x200B;을 사용하여 다음과 같은 사용자 인터페이스 컨트롤을 참조합니다.
   * **[!UICONTROL 연결]** > **[!UICONTROL 대상]**(으)로 이동한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. [대상 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination)에서 사용자 인터페이스 컨트롤을 문서화하는 방법의 예를 봅니다.

## 쓰기 스타일

>[!IMPORTANT]
>
>대상 설명서 페이지 작성을 시작하기 전에 [Adobe 설명서에 대한 작성 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html)을 읽으십시오.

* 문장을 짧게 유지하고 요점을 빨리 파악하세요. 문장의 길이가 20단어 이상이거나 여러 개의 쉼표를 사용하는 경우 별도의 문장으로 구분하는 것을 고려하십시오. 길이가 20단어가 넘는 문장은 독자들에게 특히 어려울 수 있다.
* 너무 예의바르게 굴지 마라. 기술 설명서에서 &quot;제발&quot; 또는 &quot;친절하게...&quot;를 사용하지 마십시오.

## 연결 {#linking}

제공된 설명서 템플릿을 따르고 템플릿의 기존 링크를 편집하지 마십시오. 새 링크를 포함할 때는 참가자 안내서의 [설명서에서 링크 사용](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html)을 읽어 보십시오.

## 브랜딩 지침 {#branding}

* AEP는 승인된 공개 용어가 아닙니다. 처음 사용 시 Adobe Experience Platform을 사용한 다음 Experience Platform, 플랫폼을 사용하십시오.
   * **사용하지 않음**: AEP에서 YourDestination으로 데이터를 내보내려면 먼저 이러한 필수 구성 요소를 읽고 완료해야 합니다.
   * **사용**: Adobe Experience Platform에서 YourDestination으로 데이터를 내보내려면 먼저 이러한 필수 구성 요소를 읽고 완료해야 합니다.

## 이미지 및 스크린샷 {#images-and-screenshots}

* [이미지에 연결하는 방법](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images)에 대한 자세한 내용은 기여자 안내서를 참조하십시오.
* 스크린샷을 사용할 때는 스크린샷이 전체 Platform UI 화면을 캡처하는지 확인하십시오.
* 이미지를 표시하여 페이지의 특정 컨트롤이나 레이블을 강조 표시할 때는 Experience Platform 설명서 팀에서 사용하는 마크업 스타일을 따라야 합니다. [이 스크린샷](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency)에서 프로필 기반이 어떻게 강조 표시되는지 확인하십시오.
* `png` 형식 이미지를 사용하십시오.
* 번호가 매겨진 스크린샷을 파일 이름으로 사용하지 마십시오. 이미지 파일 이름은 설명적이어야 합니다.
   * **사용하지 않음**: `1.png`, `2.png`, `3.png`
   * **사용**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 설명서에 추가하는 이미지에 대해서는 대체 텍스트를 사용하고 대체 텍스트에 적절한 문법을 사용하십시오.
   * **사용하지 않음**: 대상 연결 세부 정보
   * **사용**: 채워진 대상 연결 세부 정보를 표시하는 플랫폼 UI의 이미지입니다.

## 프로세스 {#process}

* [설명서 템플릿](./self-service-template.md)은(는) 파트너 피드백을 기반으로 자주 업데이트되지 않습니다. 대상에 대한 설명서 작성을 시작하기 전에 [최신 버전의 템플릿을 다운로드했는지 확인](../assets/docs-framework/yourdestination-template.zip)하십시오.
* 설명서를 작성하고 포크 *주 분기 이외의 분기*&#x200B;에서 설명서 가져오기 요청(PR)을 만듭니다. [GitHub 인터페이스](./use-github-interface-to-create-documentation.md#submit-review) 또는 [로컬 환경](./work-in-local-environment.md#submit-review)에서 작성할 때 검토용 제출 대상을 참조하십시오.
