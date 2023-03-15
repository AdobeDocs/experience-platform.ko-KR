---
title: SRI(Subresource Integrity) 지원
description: Adobe Experience Platform에서 SRI(Subresource Integrity)가 어떻게 지원되는지 알아봅니다.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 72%

---

# SRI(Subresource integrity) 지원

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

이 문서에서는 Adobe Experience Platform에서 SRI(Subresource Integrity)가 지원되는 방법을 다룹니다.

최신 웹 사이트는 웹 주변의 다양한 위치에서 이미지, 콘텐츠 및 스크립트를 참조하여 제작됩니다. SRI를 사용하면 브라우저에서 요청된 파일의 내용이 예기치 않게 수정되지 않았는지 확인할 수 있습니다.

사용 사례들은 상호 보완적이지만 SRI는 신뢰할 수 있는 소스의 파일만 웹 사이트에서 사용할 수 있도록 하는 CSP(콘텐츠 보안 정책)와 다릅니다. SRI는 이러한 파일의 콘텐츠가 귀하의 기대에 부합되게 함으로써 한 단계 더 나아갑니다.

>[!NOTE]
>
>SRI에 대한 자세한 내용은 [MDN 웹 문서](https://developer.mozilla.org/ko-KR/docs/Web/Security/Subresource_Integrity)를 참조하십시오.

SRI 유효성 검사 프로세스는 다음과 같이 요약할 수 있습니다.

1. 유효성을 검사할 자산의 암호화 해시를 생성합니다.
1. 웹 사이트에서 해시는 파일을 로드하는 HTML 요소의 `integrity` 속성에 배치됩니다.
1. 브라우저에서 `integrity` 속성을 확인하면 브라우저가 리소스를 요청하고 자체 버전의 암호화 해시를 독립적으로 생성합니다.
1. 브라우저는 `integrity` 해시를 생성한 해시와 비교합니다. 일치하는 경우, 자산이 허용됩니다. 일치하지 않으면, 자산이 차단됩니다.

## 태그 관리 시스템의 제한 사항

TMS(태그 관리 시스템)로서, Adobe Experience Platform의 태그는 한 개로 페이지에 로드하는 컴파일된 JavaScript 라이브러리 빌드를 제공합니다 `<script>` 요소(포함 코드). TMS에서 제공하는 동적 기능은 다른 작업을 변경하지 않고도 해당 스크립트의 콘텐츠를 동적으로 교환함으로써 수행됩니다.

그러나 스크립트 내용이 변경되면 해당 콘텐츠의 암호화 해시도 변경됩니다. 따라서 TMS에서 SRI를 사용할 수 있는 유일한 방법은 새 빌드를 게시하는 동시에 포함 코드를 업데이트하는 것입니다. 이 과정은 많은 경우, TMS를 처음 사용하는 목적을 무효화합니다.

태그에 다음으로 좋은 보안 옵션은 콘텐츠 보안 정책을 구현하는 것입니다. 자세한 내용은 다음 안내서를 참조하십시오. [CSP 및 태그](./content-security-policy.md).

## 빌드 배포에 SRI 통합하기

라이브러리 빌드에 SRI를 계속 사용하려면 자체 호스팅을 사용해야 합니다. Adobe 관리 호스팅을 사용하는 경우, 새 빌드 콘텐츠가 포함 코드의 `integrity` 속성과 일치하지 않는 시간이 없으면 SRI를 사용할 수 없습니다.

포함 코드 업데이트 프로세스를 자동화하면 사이트의 구조에 따라 복잡성이 높아지지만 일반적인 단계는 다음과 같이 요약할 수 있습니다.

1. SFTP 배달을 통해서 또는 사용자 인터페이스에서 아카이브를 다운로드하여 프로덕션 라이브러리 빌드를 검색합니다.
1. 기본 빌드의 암호화 해시를 생성합니다.
1. 포함 코드의 `integrity` 속성이 새 해시로 업데이트되고 참조된 빌드가 동일한 배포의 일부로 업데이트되는지 확인합니다.

>[!IMPORTANT]
>
>이 접근법은 기본 빌드만 다룹니다. 존재할 수 있는 작은 파일이 포함되지 않습니다.

## 다음 단계

이 문서에서는 태그와 함께 SRI를 사용하는 제한 사항과 이러한 제한 사항에도 불구하고 라이브러리 빌드 배포에 SRI를 통합하는 데 필요한 단계를 다룹니다. 아직 이 문서를 보유하고 있지 않은 경우 다음 안내서를 읽어 보는 것이 좋습니다 [CSP 및 태그](./content-security-policy.md) 다른 보안 옵션을 사용할 수 있습니다.
