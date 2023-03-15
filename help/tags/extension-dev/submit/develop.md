---
title: 확장 개발
description: 이 문서에서는 태그 확장 개발 프로세스에 대한 일반적인 개요를 제공하고, 보다 자세한 프로세스를 안내하는 추가 설명서에 대한 링크를 제공합니다.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 43%

---

# 확장 개발

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

태그 확장은 자체 요구 사항이 있는 (소규모) 제품으로 간주해야 합니다. Adobe Experience Platform 사용자가 확장의 사용할 방법을 결정하면 확장에서 제공해야 하는 이벤트 유형, 조건 유형, 작업 유형 및 데이터 요소 유형으로 기능을 정렬할 수 있습니다.

이러한 지식을 바탕으로 확장에서 제공해야 하는 구성 요소를 계획할 수 있습니다.

## 안내서

적합한 플랜을 통해 확장 개발 프로세스를 이해하는 데 도움이 됩니다.

* 다음 [시작 안내서](../getting-started.md) 및 기타 문서 **확장 개발** 왼쪽 탐색에는 확장을 이해하는 데 유용한 참조 자료가 있습니다. 여기에는 확장의 기능, 확장과 Adobe Experience Platform 간에 사용자 정보가 저장 및 전달되는 방법, 코드가 라이브러리에 번들로 제공되는 방법, 브라우저에서 런타임 시 확장 코드가 해석 및 사용되는 방법에 대한 세부 정보가 포함됩니다.
* 다음 [확장 튜토리얼 비디오](https://youtu.be/rxjtC9o4rl0) 시작하기에 좋은 장소입니다.
* [확장 소개](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 재생 목록은 확장 패키지를 개발하기 위한 프로세스를 안내합니다.
* [JSON 스키마 아티클 이해](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/유효성 검사기](https://jsonlint.com/).
* JSON 및 JSONP를 강조 및 인쇄하는 [JSON 뷰어](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome 확장.
* 객체에서 JSON 스키마를 생성하기 위한 [jsonschema.net](https://jsonschema.net/#/editor) 편집기.
* 온라인 대화형 JSON 스키마 유효성 검사기인 [JSON 스키마 유효성 검사기](https://www.jsonschemavalidator.net).

## 도구

확장 패키지 개발에 도움이 되는 다양한 npm 툴도 제공됩니다.

* [태그 확장 스캐폴드 도구](https://www.npmjs.com/package/@adobe/reactor-scaffold) 는 로컬 컴퓨터에서 시작 프로젝트를 쉽게 만들 수 있도록 지원합니다.
* [태그 확장 샌드박스](https://www.npmjs.com/package/@adobe/reactor-sandbox) 는 로컬 시스템에서 확장 보기 및 모듈의 유효성을 검사하는 데 도움이 됩니다.
* [태그 확장 패키지](https://www.npmjs.com/package/@adobe/reactor-packager) 는 태그 확장을 zip 파일로 패키지하는 명령줄 유틸리티입니다.
* [태그 확장 업로더](https://www.npmjs.com/package/@adobe/reactor-uploader) 는 기술 계정 자격 증명을 입력하고 확장 패키지를 태그에 업로드하는 데 도움이 되는 대화형 명령줄 도구입니다.
* [태그 확장 릴리스](https://www.npmjs.com/package/@adobe/reactor-releaser) 는 확장을 비공개 가용성으로 릴리스하는 데 도움이 되는 대화형 명령줄 도구입니다.

## 예시 확장

GitHub에는 시작 프로젝트로 검토하거나 사용할 수 있는 다음과 같은 확장이 있습니다.

* [Hello World 예시 확장](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 예시 확장](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 예시 확장](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 예시 확장](https://github.com/jeffchasin/extension-pinterest)

## Slack 작업 영역

확장 작성자가 이를 사용하여 서로 지원할 수 있는 Slack 커뮤니티 작업 영역에 대한 액세스를 요청할 수 있습니다 [요청 양식](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**참고 사항**: 이 Slack 작업 영역에는 Adobe 구성원이 있지만 Adobe이 후원 또는 중재하지 않는 커뮤니티 리소스입니다.
