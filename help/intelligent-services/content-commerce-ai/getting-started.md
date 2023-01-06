---
keywords: Experience Platform;시작하기;컨텐츠 ai;commerce ai;콘텐츠 및 상거래 ai
solution: Experience Platform
title: 콘텐츠 및 Commerce AI 시작하기
description: Content and Commerce AI는 Adobe I/O API를 사용합니다. Adobe I/O API 및 I/O 콘솔 통합을 호출하려면 먼저 인증 자습서를 완료해야 합니다.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# 콘텐츠 및 Commerce AI 시작하기

>[!NOTE]
>
>콘텐츠 및 상거래 AI는 베타에 있습니다. 설명서는 변경될 수 있습니다.

[!DNL Content and Commerce AI] 는 Adobe I/O API를 사용합니다. Adobe I/O API 및 I/O 콘솔 통합을 호출하려면 먼저 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en).

하지만, **API 추가** 단계. API는 다음 스크린샷에 표시된 대로 Adobe Experience Platform 대신 Experience Cloud 아래에 있습니다.

![콘텐츠 및 상거래 AI 추가](./images/add-api.png)

인증 자습서를 완료하면 아래와 같이 모든 Adobe I/O API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Postman 환경 만들기(선택 사항)

Adobe Developer 콘솔 내에서 프로젝트 및 API를 설정하면 Postman용 환경 파일을 다운로드할 수 있습니다. 아래 **[!UICONTROL API]** 프로젝트의 왼쪽 레일에서 **[!UICONTROL 콘텐츠 및 상거래 AI]**. 레이블이 &quot;&quot;인 카드가 포함된 새 탭이 열립니다[!DNL Try it out]&quot;. 선택 **Postman 다운로드** postman 환경을 구성하는 데 사용되는 JSON 파일을 다운로드하려면 다음을 수행하십시오.

![postman용 다운로드](./images/add-to-postman.png)

파일을 다운로드했으면 Postman을 열고 을 선택합니다. **톱니바퀴 아이콘** 오른쪽 상단에서 **환경 관리** 대화 상자.

![톱니바퀴 아이콘](./images/select-gear-icon.png)

다음 을 선택합니다. **가져오기** 내 **환경 관리** 대화 상자.

![가져오기](./images/import.png)

리디렉션되고 컴퓨터에서 환경 파일을 선택하라는 메시지가 표시됩니다. 이전에 다운로드한 JSON 파일을 선택한 다음 을 선택합니다 **열기** 를 눌러 환경을 로드합니다.

![](./images/choose-your-file.png)

![](./images/click-open.png)

를 클릭하면 *환경 관리* 새 환경 이름이 채워진 탭입니다. Postman에서 사용할 수 있는 변수를 보고 편집할 환경 이름을 선택합니다. 여전히 수동으로 `JWT_TOKEN` 및 `ACCESS_TOKEN`. 이러한 값은 를 완료하는 동안 얻어야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

완료되면 변수가 아래 스크린샷과 비슷하게 표시됩니다. 선택 **업데이트** 를 클릭하여 환경 설정을 완료합니다.

![](./images/final-environment.png)

이제 오른쪽 상단 모서리의 드롭다운 메뉴에서 환경을 선택하고 저장된 값을 자동으로 채울 수 있습니다. 언제든지 값을 다시 편집하여 모든 API 호출을 업데이트할 수 있습니다.

![예](./images/select-environment.png)

Postman을 사용하여 Adobe I/O API 작업에 대한 자세한 내용은 미디어 게시물 을 참조하십시오 [Adobe I/O에서 JWT 인증에 Postman 사용](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

## 다음 단계 {#next-steps}

자격 증명이 모두 있으면 사용자 정의 작업자를 설정할 준비가 된 것입니다 [!DNL Content and Commerce AI]. 다음 문서는 확장성 프레임워크 및 환경 설정을 이해하는 데 도움이 됩니다.

확장성 프레임워크에 대한 자세한 내용은 [확장성 소개](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) 문서. 이 문서에서는 사전 요구 사항 및 프로비저닝 요구 사항에 대해 설명합니다.

에 대한 환경 설정에 대해 자세히 알아보려면 [!DNL Content and Commerce AI]에 대한 안내서를 읽어 보십시오. [개발자 환경 설정](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). 이 문서에서는 Asset compute 서비스에 대해 개발할 수 있는 설정 지침을 제공합니다.
