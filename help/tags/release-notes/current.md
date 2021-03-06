---
title: 태그에 대한 릴리스 노트
description: Adobe Experience Platform의 태그에 대한 최신 릴리스 정보입니다.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 6%

---

# Adobe Experience Platform의 태그에 대한 릴리스 노트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../term-updates.md)를 참조하십시오.

## 2021년 11월 15일

**태그의 ES6 코드 수락** - 이제 태그에서 ES6 코드를 포함하는 확장 및 사용자 지정 코드를 사용할 수 있습니다. 확장 카탈로그에는 ES6 코드가 포함된 각 확장의 카드 내에 ES6+ 레이블이 표시됩니다. IE10 및 IE11은 ES6 코드를 지원하지 않습니다. 태그 라이브러리에서 ES6 코드를 사용하기 전에 지능을 적절하게 사용하십시오.

**Terser를 JavaScript 압축기로 사용** - Uglifier가 Terser로 대체되었습니다. 이 릴리스부터 모든 태그 라이브러리는 브라우저에서 축소됩니다.

## 2021년 10월 21일

**이벤트 전달에서 인증된 종단점으로 데이터 보내기** - 암호를 사용하여 다음 인증 프로토콜이 필요한 종단점에 데이터를 보낼 수 있습니다.

* **[!UICONTROL 토큰]**: 인증 토큰 값을 나타내는 단일 문자열입니다.
* **[!UICONTROL 단순 HTTP]**: 사용자 이름과 암호로 두 개의 문자열 속성을 포함합니다.
* **[!UICONTROL OAuth2]**: 을(를) 지원하는 여러 특성을 포함합니다 [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) 지정합니다.

자세한 내용은 [데이터 수집 UI에서 비밀 관리](../ui/event-forwarding/secrets.md) 또는 [Reactor API의 암호 관리](../api/guides/secrets.md).

## 2021년 7월 19일

**속성 관리 권한에 대한 조정** - 속성 관리 권한이 사용자에게 새 속성을 만들 수 있는 권한이 있지만 커뮤니티 스레드에 요약된 대로 속성을 만든 후에는 볼 수 없는 문제가 발생했습니다 [여기](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). 이제 문서에 설명된 대로 강제 적용되는 권한을 통해 수정 사항이 적용됩니다.

>[!NOTE]
>
>사용자 그룹에 새 &quot;속성 편집&quot; 권한을 지정하는 경우 속성 구성 화면의 필드를 사용하도록 UI가 업데이트되지 않습니다. 이 문제에 대한 수정 사항은 향후 릴리스에서 구현될 예정입니다.

## 2021년 5월 17일

**저장하지 않은 변경 사항 처리 개선** - 설정 보기(확장, 데이터 요소 및 규칙 구성 요소)에서 이동할 때마다 변경 사항을 취소할지 여부를 묻는 메시지가 표시되었습니다. 하지만 그것을 결정하는 논리는 훌륭하지 않았고, 그래서 당신이 받은 대부분의 시간 동안 아무것도 없음에도 불구하고 변화를 저장하라는 요청을 받았습니다.  그게 수정되었습니다  이제부터 실제로 변경 작업을 수행한 경우에만 해당 메시지가 표시됩니다.

## 2021년 5월 10일

**간소화된 게시** - 더 이상 스테이징 환경에 빌드할 필요가 없습니다.  적절한 권한이 있는 경우 성공적으로 빌드하고 다른 라이브러리가 업스트림으로 없는 한 제출됨 상태를 완전히 건너뛰고 개발 프로그램에서 직접 게시할 수 있습니다.

## 2021년 4월 22일

**Adobe Experience Platform의 데이터 수집** - Adobe에 데이터를 전송하는 것은 사이트 또는 구성에 태그를 앱에 배포하는 것만이 아닙니다.  Experience Platform SDK 및 Edge 네트워크를 사용하려면 다른 플랫폼 기능에 액세스해야 합니다.  이렇게 하려면 몇 가지 다른 도구에 로그인해야 했지만, 이제 한 곳에서 함께 사용할 수 있습니다.

Platform의 데이터 수집은 6가지 기능으로 구성되며 새로 간소화된 탐색에는 회사 및 사용자 계정이 액세스할 수 있는 항목만 포함됩니다.  일부 기능 이름이 Experience Platform의 이름 지정 패턴과 일치하도록 업데이트되었습니다.

* 클라이언트(이전에 클라이언트측으로 액세스됨)
* 데이터 저장소(이전에 Edge 구성으로 액세스됨)
* 서버(이전에 서버 측으로 액세스됨)
* 앱 구성
* 스키마
* ID

Experience Platform 및 데이터 수집이 지속적으로 발전함에 따라 더 많은 업데이트가 있기를 기대합니다.

## 2021년 2월 18일

* React-spectrum v3로 데이터 수집 UI가 업데이트되었습니다.
* 확장 카드를 최신 스펙트럼 패턴으로 업데이트했습니다
* 앱 전체에서 이름 필드의 크기가 늘었습니다

## 2021년 1월 13일

**일반 공급: 이벤트 전달** 이벤트 수준 데이터를 Adobe Experience Platform Edge Network에 전송한 다음 이벤트 전달을 사용하여 클라이언트가 아닌 Adobe 서버를 사용하여 Adobe이 아닌 엔드포인트로 해당 데이터를 변환, 강화 및 전송합니다.

자세한 내용은 [이벤트 전달 개요](../ui/event-forwarding/overview.md) 및 [시작 안내서](../ui/event-forwarding/getting-started.md) 추가 정보.
