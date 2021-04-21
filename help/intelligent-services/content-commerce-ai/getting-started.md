---
keywords: Experience Platform;시작;내용 ai;커머스 ai;컨텐트 및 상거래 ai;;시작하기;content ai;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform, Intelligent Services
title: Content and Commerce AI 시작하기
topic-legacy: Getting started
description: Content and Commerce AI는 Adobe I/O API를 활용합니다. Adobe I/O API 및 I/O 콘솔 통합을 호출하려면 먼저 인증 자습서를 완료해야 합니다.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Content and Commerce AI 시작하기

>[!NOTE]
>
>콘텐츠 및 상거래 AI가 베타 버전입니다. 설명서는 변경될 수 있습니다.

[!DNL Content and Commerce AI] Adobe I/O API를 활용합니다. Adobe I/O API 및 I/O 콘솔 통합을 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다.

그러나 **API 추가** 단계에 도달하면 다음 스크린샷과 같이 API는 Adobe Experience Platform 대신 Experience Cloud 아래에 있습니다.

![콘텐츠 및 상거래 AI 추가](./images/add-api.png)

인증 자습서를 완료하면 아래와 같이 모든 Adobe I/O API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## 포스트만 환경 만들기(선택 사항)

Adobe 개발자 콘솔에서 프로젝트 및 API를 설정한 경우 Postman용 환경 파일을 다운로드할 수 있습니다. 프로젝트의 왼쪽 레일에서 **[!UICONTROL APIs]** 아래에서 **[!UICONTROL Content and Commerce AI]**&#x200B;을 선택합니다. &quot;[!DNL Try it out]&quot; 카드가 포함된 새 탭이 열립니다. 포스트만 환경을 구성하는 데 사용되는 JSON 파일을 다운로드하려면 **포스트맨용 다운로드**&#x200B;를 선택합니다.

![postman 다운로드](./images/add-to-postman.png)

파일을 다운로드한 후 Postman을 열고 오른쪽 상단의 **톱니바퀴 아이콘**&#x200B;을 선택하여 **환경 관리** 대화 상자를 엽니다.

![톱니바퀴 아이콘](./images/select-gear-icon.png)

그런 다음 **환경 관리** 대화 상자 내에서 **가져오기**&#x200B;를 선택합니다.

![import](./images/import.png)

리디렉션되고 컴퓨터에서 환경 파일을 선택하라는 메시지가 표시됩니다. 이전에 다운로드한 JSON 파일을 선택한 다음 **열기**&#x200B;를 선택하여 환경을 로드합니다.

![](./images/choose-your-file.png)

![](./images/click-open.png)

새 환경 이름이 채워진 *환경 관리* 탭으로 다시 리디렉션됩니다. Postman에서 사용 가능한 변수를 보고 편집할 환경 이름을 선택합니다. 여전히 `JWT_TOKEN` 및 `ACCESS_TOKEN`을 수동으로 채워야 합니다. 이러한 값은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료하는 동안 얻어야 합니다.

![](./images/re-direct.png)

완료되면, 변수는 아래 스크린샷과 비슷해야 합니다. 환경 설정을 완료하려면 **업데이트**&#x200B;를 선택하십시오.

![](./images/final-environment.png)

이제 오른쪽 상단의 드롭다운 메뉴에서 환경을 선택하고 저장된 값을 자동으로 채울 수 있습니다. 언제든지 값을 다시 편집하여 모든 API 호출을 업데이트할 수 있습니다.

![example](./images/select-environment.png)

Postman을 사용하여 Adobe I/O API를 사용하는 작업에 대한 자세한 내용은 Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)의 JWT 인증에 Postman을 사용하여 [의 중간 게시물을 참조하십시오.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md)를 읽는 방법을 참조하십시오.

## 다음 단계 {#next-steps}

자격 증명이 모두 준비되면 [!DNL Content and Commerce AI]에 대한 사용자 지정 작업자를 설정할 준비가 됩니다. 다음 문서는 확장 프레임워크 및 환경 설정을 이해하는 데 도움이 됩니다.

확장성 프레임워크에 대한 자세한 내용을 보려면 [확장 기능 소개](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) 문서를 읽어 보십시오. 이 문서에서는 사전 요구 사항 및 프로비저닝 요구 사항에 대해 간략히 설명합니다.

[!DNL Content and Commerce AI]에 대한 환경 설정에 대한 자세한 내용을 보려면 [개발자 환경 설정](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)에 대한 안내서를 읽어 보십시오. 이 문서에서는 Asset compute 서비스를 개발할 수 있도록 하는 설정 지침을 제공합니다.
