---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;브라우저;브라우저 세부 정보;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 브라우저 세부 정보 데이터 유형
description: 브라우저 세부 정보 XDM 데이터 유형에 대해 알아봅니다.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 7%

---

# [!UICONTROL 브라우저 세부 정보] 데이터 유형

[!UICONTROL 브라우저 세부 정보] 는 브라우저 또는 애플리케이션과 관련된 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `acceptLanguage` | 문자열 | IETF 언어 태그([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | 부울 | 사용자의 설정에서 쿠키 쓰기를 허용하는지 여부를 나타냅니다. |
| `javaEnabled` | 부울 | 관찰이 수행된 디바이스에서 Java가 활성화되었는지 여부를 나타냅니다. |
| `javaScriptEnabled` | 부울 | 관찰이 수행된 디바이스에서 JavaScript가 활성화되었는지 여부를 나타냅니다. |
| `javaScriptVersion` | 문자열 | 관찰 도중 지원되는 JavaScript 버전. |
| `javaVersion` | 문자열 | 관찰 도중 지원되는 Java 버전. |
| `name` | 문자열 | 애플리케이션 또는 브라우저 이름. |
| `quicktimeVersion` | 문자열 | 관찰 도중 지원되는 Apple Quicktime 버전. |
| `thirdPartyCookiesEnabled` | 부울 | 관찰이 수행된 장치에서 서드파티 쿠키가 활성화되었는지 여부를 나타냅니다. |
| `userAgent` | 문자열 | 클라이언트 요청의 HTTP 사용자 에이전트 문자열입니다. |
| `vendor` | 문자열 | 애플리케이션 또는 브라우저 공급업체. |
| `version` | 문자열 | 애플리케이션 또는 브라우저 버전. |
| `viewportHeight` | 정수 | 이벤트가 내부에 표시된 윈도우(픽셀) 세로 크기입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 높이입니다. |
| `viewportWidth` | 정수 | 이벤트가 내부에 표시된 윈도우(픽셀) 가로 크기입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 폭입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
