---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: 브라우저 세부 정보 데이터 유형
topic: overview
description: 이 문서에서는 브라우저 세부 정보 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---


# [!UICONTROL 브라우저 세부 정보] 데이터 유형

[!UICONTROL 브라우저 세부] 정보는 브라우저 또는 응용 프로그램과 관련된 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `acceptLanguage` | 문자열 | IETF 언어 태그([RFC 5646](https://tools.ietf.org/html/rfc5646))입니다. |
| `cookiesEnabled` | 부울 | 사용자 설정이 쿠키 쓰기를 허용하는지 여부를 나타냅니다. |
| `javaEnabled` | 부울 | 관찰된 장치에서 Java가 활성화되었는지 여부를 나타냅니다. |
| `javaScriptEnabled` | 부울 | 관찰된 장치에서 JavaScript가 활성화되었는지 여부를 나타냅니다. |
| `javaScriptVersion` | 문자열 | 관찰 중에 지원되는 JavaScript 버전. |
| `javaVersion` | 문자열 | 관찰 중에 지원되는 Java 버전입니다. |
| `name` | 문자열 | 응용 프로그램 또는 브라우저 이름입니다. |
| `quicktimeVersion` | 문자열 | 관찰 중에 지원되는 Apple Quicktime 버전입니다. |
| `thirdPartyCookiesEnabled` | 부울 | 관찰된 장치에서 타사 쿠키가 활성화되었는지 여부를 나타냅니다. |
| `userAgent` | 문자열 | 클라이언트 요청의 HTTP 사용자-에이전트 문자열. |
| `vendor` | 문자열 | 애플리케이션 또는 브라우저 공급업체 |
| `version` | 문자열 | 응용 프로그램 또는 브라우저 버전. |
| `viewportHeight` | 정수 | 이벤트가 내부에 표시되는 창의 세로 크기(픽셀)입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 높이입니다. |
| `viewportWidth` | 정수 | 이벤트가 내부에 표시되는 창의 가로 크기(픽셀)입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 너비입니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)