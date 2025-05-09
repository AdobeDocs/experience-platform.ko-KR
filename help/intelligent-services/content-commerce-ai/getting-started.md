---
keywords: Experience Platform;시작하기;컨텐츠;컨텐츠 태깅
solution: Experience Platform
title: 콘텐츠 태깅 시작
description: 컨텐츠 태깅은 Adobe I/O API를 사용합니다. Adobe I/O API 및 I/O 콘솔 통합을 호출하려면 먼저 인증 자습서를 완료해야 합니다.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 7%

---

# 콘텐츠 태깅 시작

[!DNL Content tagging]이(가) Adobe I/O API를 사용합니다. Adobe I/O API 및 I/O 콘솔 통합을 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다.

그러나 **API 추가** 단계로 이동하면 다음 스크린샷과 같이 API가 Adobe Experience Platform 대신 Creative Cloud 아래에 있습니다.

![콘텐츠 태그 추가](./images/add-api-updated.png)

인증 자습서를 완료하면 아래와 같이 모든 Adobe I/O API 호출에서 필요한 각 헤더의 값이 제공됩니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Postman 환경 만들기(선택 사항)

Adobe Developer Console 내에서 프로젝트 및 API를 설정한 후에는 Postman용 환경 파일을 다운로드할 수 있는 옵션이 있습니다. 프로젝트의 왼쪽 레일 **[!UICONTROL API]**&#x200B;에서 **[!UICONTROL 콘텐츠 태그 지정]**&#x200B;을 선택합니다. 레이블이 &quot;[!DNL Try it out]&quot;인 카드가 들어 있는 새 탭이 열립니다. **Postman용 다운로드**&#x200B;를 선택하여 postman 환경을 구성하는 데 사용되는 JSON 파일을 다운로드합니다.

![postman용 다운로드](./images/add-to-postman-updated.png)

파일을 다운로드한 후 Postman을 열고 오른쪽 상단에서 **톱니바퀴 아이콘**&#x200B;을 선택하여 **환경 관리** 대화 상자를 엽니다.

![톱니바퀴 아이콘](./images/select-gear-icon.png)

그런 다음 **환경 관리** 대화 상자에서 **가져오기**&#x200B;를 선택합니다.

![가져오기](./images/import-updated.png)

리디렉션되고 컴퓨터에서 환경 파일을 선택하라는 메시지가 표시됩니다. 이전에 다운로드한 JSON 파일을 선택한 다음 **열기**&#x200B;를 선택하여 환경을 로드합니다.

![](./images/choose-your-file.png)

![](./images/click-open.png)

새 환경 이름이 채워진 *환경 관리* 탭으로 다시 리디렉션됩니다. 환경 이름을 선택하여 Postman에서 사용할 수 있는 변수를 보고 편집합니다. `JWT_TOKEN` 및 `ACCESS_TOKEN`을(를) 수동으로 채워야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료하는 동안 이러한 값을 가져와야 합니다.

![](./images/re-direct-updated.png)

완료되면 변수가 아래 스크린샷과 유사하게 표시됩니다. 환경 설정을 완료하려면 **업데이트**&#x200B;를 선택하세요.

![](./images/final-environment-updated.png)

이제 오른쪽 상단의 드롭다운 메뉴에서 환경을 선택하고 저장된 모든 값을 자동으로 채울 수 있습니다. 모든 API 호출을 업데이트하려면 언제든지 값을 다시 편집하면 됩니다.

![예](./images/select-environment-updated.png)

Postman을 사용하여 Adobe I/O API를 사용하는 방법에 대한 자세한 내용은 [Adobe I/O에서 JWT 인증을 위해 Postman 사용](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)의 Medium 게시물을 참조하십시오.

## 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md)에 대한 섹션을 참조하십시오.

## 다음 단계 {#next-steps}

모든 자격 증명을 획득하면 [!DNL Content tagging]에 대한 사용자 지정 작업자를 설정할 수 있습니다. 다음 문서는 확장성 프레임워크 및 환경 설정을 이해하는 데 도움이 됩니다.

Extensibility Framework에 대해 자세히 알아보려면 먼저 [Extensibility 소개](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=ko) 문서를 읽으십시오. 이 문서에서는 사전 요구 사항 및 프로비저닝 요구 사항을 간략하게 설명합니다.

[!DNL Content tagging]에 대한 환경 설정에 대해 자세히 알아보려면 [개발자 환경 설정](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html?lang=ko)에 대한 안내서를 읽어 보십시오. 이 문서에서는 Asset compute 서비스에 대해 개발할 수 있는 설정 지침을 제공합니다.
