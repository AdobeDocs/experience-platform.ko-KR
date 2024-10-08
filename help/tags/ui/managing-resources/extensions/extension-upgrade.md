---
title: 확장 업그레이드
description: 확장 업그레이드가 확장 카탈로그에 어떻게 패키지화되고 표시되는지 알아봅니다.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 72%

---

# 확장 업그레이드

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

확장 개발자는 확장에 새로운 기능을 지속적으로 추가하고 버그를 자주 수정합니다. 이러한 업데이트는 새로운 버전의 확장에 패키지화되어 확장 카탈로그에서 업그레이드로 사용할 수 있습니다.

## 확장 카탈로그

확장 개발자가 새로운 버전의 확장을 제공하면 확장 카탈로그에서 해당하는 새로운 버전을 사용할 수 있게 됩니다. 카탈로그에는 최신 버전의 확장만 표시됩니다. `latest` 이외의 다른 확장 버전은 설치할 수 없습니다.

속성에 대한 확장을 설치하면 현재 사용 가능한 버전이 설치되고, 새 버전이 카탈로그에 추가되더라도 해당 시점부터 해당 특정 버전과 함께 속성이 유지됩니다.

## 업그레이드 알림

속성에 대한 확장을 설치했는데 카탈로그에서 최신 버전을 사용할 수 있는 경우 Installed Extensions를 보면 확장 카드에 [!UICONTROL Upgrade] 단추가 표시됩니다.

또한 해당 확장에서 제공하는 리소스를 편집할 때도 알림이 표시됩니다.

## 영구 업그레이드

카탈로그에서 사용 가능한 최신 버전으로 업그레이드하려면 직접 해당 업그레이드를 설치해야 합니다. 업그레이드는 배포된 태그에 영향을 주기 전에 라이브러리에 추가하고, 테스트하고, 게시해야 하는 &quot;변경 사항&quot;입니다.

업그레이드를 가볍게 생각해서는 안 됩니다. 새로운 확장을 테스트하고 배포할 준비가 되어 있지 않으면 업그레이드하지 마십시오. 업그레이드가 속성에 추가되면 모든 라이브러리에 포함되어 있어야 합니다. 업그레이드된 확장을 포함하지 않는 모든 라이브러리는 작성할 때 실패합니다.

현재는 확장을 이전 버전으로 다운그레이드하는 기능이 없습니다. 업그레이드했으면(게시 여부에 관계없이) 새 확장 버전이 속성에 유지됩니다.

## 업그레이드 프로세스

업그레이드 설치 방법은 처음 확장을 설치하는 방법과 거의 동일합니다.

1. **[!UICONTROL 업그레이드]**&#x200B;를 선택하여 [!UICONTROL 확장 구성] 화면으로 이동합니다.
1. 원하는 대로 구성을 변경합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

업그레이드는 실제로 **[!UICONTROL 저장]**&#x200B;을 누를 때까지 수행되지 않습니다. 언제든지 그 전에 [!UICONTROL 취소]를 선택하여 현재 설치된 버전을 유지할 수 있습니다. **[!UICONTROL 저장]**&#x200B;을(를) 선택하면 되돌릴 수 없습니다.

`Approved` 또는 `Submitted` 상태의 라이브러리가 있는 경우 확장 업그레이드가 허용되지 않습니다.  그 이유는 다음 빌드가 반드시 새 확장 버전을 포함해야 하기 때문입니다.  `Approved`또는 `Submitted`인 라이브러리의 경우 다음 빌드는 프로덕션 빌드입니다.  프로덕션 빌드는 최신 버전을 포함하지 않아서 실패하게 되므로, 확장을 업그레이드하기 _전에_ `Approved` 또는 `Submitted` 상태의 라이브러리를 게시하거나 거부하는 것이 워크플로우입니다.

## 업그레이드 게시

업그레이드된 확장이 속성에 설치되고 나면 해당 시점부터 모든 라이브러리에 해당 확장을 포함해야 합니다. 포함되지 않은 모든 라이브러리에 대해 빌드 오류 메시지가 표시됩니다.

그 외에 업그레이드된 확장을 라이브러리에 추가하는 것은 라이브러리에 [다른 변경 사항을 추가](../../publishing/libraries.md)하는 것과 같습니다.

[!UICONTROL 라이브러리 편집] 화면에서 &quot;[!UICONTROL 변경된 모든 리소스 추가]&quot; 단추를 사용하거나 &quot;[!UICONTROL 리소스 추가]&quot; 단추를 사용하여 업그레이드된 확장을 직접 선택할 수 있습니다.

>[!TIP]
>
> 확장 개발자가 새 기능을 활성화하기 위해 확장 보기에 새 구성 항목을 추가할 수 있습니다. 새 확장으로 업그레이드한 후 빌드가 실패하여 해당 확장으로 빌드 오류를 구분한 경우 맨 먼저 해야 할 작업은 확장의 Configure 페이지로 이동한 후 저장하는 것입니다(변경하지 않았더라도). 그런 다음 라이브러리에 새로운 변경 사항을 추가하고 다시 빌드합니다.

라이브러리에 확장 업그레이드를 추가한 후 [게시 플로우](../../publishing/publishing-flow.md)에 설명된 단계에 따라 라이브러리를 프로덕션에 게시할 수 있습니다.
