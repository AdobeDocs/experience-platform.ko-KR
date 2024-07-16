---
title: Experience Platform 태그(중국)
description: 태그의 Experience Platform 태그(중국) 기능과 여러 지리적 영역에서 태그를 사용하여 콘텐츠를 전달하는 방법에 대해 알아봅니다.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Experience Platform 태그(중국)

[Adobe 관리 호스트](./hosts/managed-by-adobe-host.md)를 사용하여 웹 사이트에서 Adobe Experience Platform 태그 자산을 전달하는 경우 이러한 자산은 가장 빠른 다운로드 속도를 제공하기 위해 전 세계의 다양한 CDN(콘텐츠 전달 네트워크) 간에 배포됩니다. 그러나 모든 웹 사이트 자산을 복제하고 해당 지역 내의 서버에서 호스팅해야 하는 특정 지역이 있습니다.

이러한 문제를 해결하기 위해 Experience Platform의 태그는 이러한 특수 지역에 콘텐츠를 전달할 수 있는 Experience Platform 태그(중국) 기능을 제공합니다.

Experience Platform 태그(중국) 지원은 유료 기능이며, 활성화하고 사용하려면 조직에서 구매해야 합니다. 이 안내서에서는 구입한 후 Experience Platform UI 또는 데이터 수집 UI에서 이 기능을 구성하고 사용하는 방법을 다룹니다.

## 조직에 대한 Experience Platform 태그(중국) 활성화

Experience Platform 태그(중국)는 회사 수준에서 사용할 수 있습니다. 조직이 Experience Platform 태그(중국) 기능을 구입하면 Adobe 관리자가 회사의 UI에서 해당 기능을 활성화합니다.

## 업데이트된 포함 코드를 사용하여 태그 라이브러리 다시 빌드 및 설치

Experience Platform 태그(중국)가 활성화되면 태그 자산이 즉시 복제되고 새 지역 내에서 사용할 준비가 된 것은 아닙니다. 이는 이제 이 기능에 옵트인할 시기를 선택할 수 있음을 의미합니다.

>[!IMPORTANT]
>
>중국에서 태그를 활성화하기 전에 빌드된 라이브러리는 오늘날과 정확히 동일한 상태로 계속 작동합니다. [보관된 환경](./environments.md#archive)에서는 Adobe 경로에 상대 URL만 사용하므로 라이브러리가 관리하지 않는 라이브러리에도 적용됩니다. Experience Platform 태그(중국)를 활성화한 후에는 Adobe에서 관리하지 않는 라이브러리를 빌드하면 중국 기능의 태그가 활성화되지 않은 것처럼 동작합니다.

중국에서 태그를 활성화하고 새 호스팅 영역에서 사용하려는 라이브러리를 다시 빌드하면 새 호스팅 영역 포함 코드를 검색하여 웹 사이트에 추가할 수 있습니다.

>[!NOTE]
>
>[!UICONTROL 표준] 호스팅 영역에 나열된 라이브러리 포함 코드는 그대로 작동하며 웹 사이트에 이미 있는 모든 Page Top 또는 Page Bottom 포함 코드도 계속 작동합니다.

**[!UICONTROL 환경]** 페이지를 방문하거나 라이브러리 편집 화면에서 환경 설치 지침을 보고 새 포함 코드를 찾습니다. 새로 지원되는 호스팅 영역은 [!UICONTROL Standard] 호스팅 영역(Experience Platform 태그(중국) 없이 지원되는 전 세계 영역에 사용됨) 다음에 표시됩니다. 아래 스크린샷은 `.cn`을(를) 최상위 도메인(TLD)으로 사용하는 중국 지역에 대한 포함 코드를 보여 줍니다.

![중국 지역의 포함 코드](../../images/ui/publishing/premium-cdn/embed-codes.png)

웹 페이지에 적합한 포함 코드를 선택하고 문서의 `<head>` 태그 내에 붙여 넣으십시오. 포함 코드를 사용하여 태그 라이브러리를 설치하는 방법에 대한 자세한 내용은 [환경 UI 안내서](./environments.md#installation)를 참조하십시오.

## 다음 단계

이 안내서에서는 태그 구현에 Experience Platform 태그(중국) 기능을 활성화하고 설치하는 방법을 다룹니다. 웹 및 모바일 속성에서 태그 라이브러리를 설치하고 테스트하는 방법에 대한 자세한 내용은 [게시 개요](./overview.md)를 참조하십시오.
