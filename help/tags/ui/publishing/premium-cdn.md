---
title: 태그에 대한 Premium CDN 지원
description: 태그의 프리미엄 CDN 기능과 이 기능을 사용하여 여러 지리적 지역에서 콘텐츠를 전달하는 방법을 알아봅니다.
source-git-commit: 530fc1ad3f389ffb5d77ddf6aa0b0b3208f1d532
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 태그에 대한 Premium CDN 지원(베타)

>[!IMPORTANT]
>
>태그의 프리미엄 CDN 기능은 현재 베타 버전이며 조직에서 아직 액세스할 수 없을 수 있습니다. 이 설명서는 변경될 수 있습니다.

를 사용하는 경우 [Adobe 관리 호스트](./hosts/managed-by-adobe-host.md) 웹 사이트에서 Adobe Experience Platform 태그 자산을 제공하기 위해 이러한 자산은 가장 빠른 다운로드 속도를 제공하기 위해 전 세계 다양한 CDN(Content Delivery Network) 간에 배포됩니다. 그러나 해당 지역 내의 서버에서 모든 웹 사이트 자산을 복제하고 호스팅해야 하는 특정 지역이 있습니다.

이를 설명하기 위해 Experience Platform의 태그는 이러한 특수 영역에 컨텐츠를 전달할 수 있는 프리미엄 CDN 기능을 제공합니다.

Premium CDN 지원은 유료 기능이며, 활성화 및 사용하려면 조직에서 구매해야 합니다. 이 안내서에서는 이 기능을 구입한 후 데이터 수집 UI에서 구성하고 사용하는 방법을 설명합니다.

## 회사에 대해 프리미엄 CDN 활성화

Premium CDN은 회사 수준에서 활성화되어 있습니다. 즉, 이 기능을 사용하려면 회사 편집 권한이 있어야 합니다.

데이터 수집 UI에서 **[!UICONTROL 태그]** > **[!UICONTROL 회사]**. 여기에서 기능을 활성화할 회사를 선택한 다음 을 선택합니다 **[!UICONTROL 구성]** .

![구성할 회사 선택](../../images/ui/publishing/premium-cdn/configure-property.png)

표시되는 구성 대화 상자에서 **[!UICONTROL Premium CDN 활성화]** 선택하기 전에 **[!UICONTROL 저장]** 를 클릭하여 변경 사항을 확인합니다.

![프리미엄 CDN 옵션 활성화](../../images/ui/publishing/premium-cdn/enable-premium-cdn.png)

## 업데이트된 포함 코드로 태그 라이브러리를 다시 빌드하고 설치합니다

프리미엄 CDN 기능을 사용한다고 해서 태그 자산이 즉시 복제되고 새 지역 내에서 사용할 준비가 되는 것은 아닙니다. 이 기능은 이제 이 기능을 선택할 시기를 선택할 수만 있습니다.

>[!IMPORTANT]
>
>Premium CDN을 활성화하기 전에 빌드된 라이브러리는 현재 그대로 계속 작동합니다. 또한 Adobe에서 관리하지 않는 라이브러리에도 적용됩니다. [보관된 환경](./environments.md#archive) 자산 경로에 상대 URL만 사용합니다. Premium CDN을 사용하도록 설정하면 Adobe에서 관리하지 않는 모든 라이브러리는 프리미엄 CDN 기능이 활성화되어 있지 않은 것처럼 동작합니다.

Premium CDN을 활성화하고 새 호스팅 영역에서 사용할 라이브러리를 다시 빌드하면 웹 사이트에 추가할 새 호스팅 영역 포함 코드를 검색할 수 있습니다.

>[!NOTE]
>
>아래에 나열된 라이브러리 포함 코드 [!UICONTROL 표준] 호스팅 영역은 웹 사이트에 이미 있는 페이지 상단 또는 페이지 하단 포함 코드뿐만 아니라 있는 그대로 계속 작동합니다.

다음 방문 **[!UICONTROL 환경]** 새 포함 코드를 찾으려면 라이브러리 편집 화면에서 환경 설치 지침을 클릭하거나 페이지를 참조하십시오. 지원되는 각각의 새로운 호스팅 영역은 [!UICONTROL 표준] 호스팅 영역(premium CDN 없이 지원되는 전세계 영역에 사용됨). 아래 스크린샷은 을 사용하는 중국 지역에 대한 포함 코드를 보여줍니다 `.cn` 를 최상위 도메인(TLD)으로 추가할 수 있습니다.

![중국 지역에 대한 포함 코드](../../images/ui/publishing/premium-cdn/embed-codes.png)

웹 페이지에 적절한 포함 코드를 선택하고 페이지에 붙여넣습니다 `<head>` 태그로 지정합니다. 포함 코드를 사용하여 태그 라이브러리를 설치하는 자세한 내용은 [환경 UI 안내서](./environments.md#installation).

## 다음 단계

이 안내서에서는 태그 구현에 프리미엄 CDN 기능을 활성화하고 설치하는 방법을 다룹니다. 웹 및 모바일 속성에 태그 라이브러리 설치 및 테스트에 대한 자세한 내용은 [게시 개요](./overview.md).
