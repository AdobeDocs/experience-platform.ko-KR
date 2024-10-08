---
title: 라이브러리에서 리소스 제거
description: 태그 라이브러리에서 리소스를 제거하는 방법을 알아봅니다.
exl-id: ad1dd093-962c-4f6d-85eb-c5ed1b644927
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 80%

---

# 라이브러리에서 리소스 제거

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

더 이상 리소스가 빌드에 영향을 주지 않게 하려면 해당 리소스를 포함하는 라이브러리에서 해당 리소스를 제거하고 새 빌드를 만들어야 합니다.

>[!IMPORTANT]
>
>라이브러리의 리소스는 상호 종속되어 있습니다. 빌드에서 리소스를 제거하면 빌드에서 다른 리소스의 동작이 변경될 수 있습니다.

제거 프로세스는 라이브러리가 있는 상태에 따라 약간 다르게 작동합니다.

## 개발 라이브러리

개발 라이브러리의 리소스는 직접 조작할 수 있습니다.

1. 라이브러리를 엽니다.
1. 리소스를 제거합니다.
1. 라이브러리를 저장합니다.
1. 라이브러리를 빌드합니다.

## 제출 및 승인된 라이브러리

제출되거나 승인된 라이브러리에 있는 리소스는 직접 조작할 수 없습니다. 라이브러리를 다시 개발 상태로 이동해야 합니다.

1. 라이브러리를 거부합니다(라이브러리를 다시 개발로 이동).
1. 위의 &quot;개발 라이브러리&quot;에 나와 있는 단계에 따라 개발 라이브러리에서 리소스를 제거합니다.

## 프로덕션 라이브러리

프로덕션 라이브러리에서 리소스를 제거하는 것은 가장 복잡한 경우입니다. 이 상태에서는 라이브러리 리소스를 조작할 수 없으며 이러한 라이브러리를 다시 개발 상태로 이동할 수도 없습니다.

대신 리소스를 비활성화해야 합니다. 이러한 비활성화는 다른 변경처럼 개발 라이브러리에 추가하는 변경 사항입니다. 이러한 변경 사항이 프로덕션에 제출되면 리소스가 프로덕션 라이브러리에서 이동됩니다.

1. 리소스를 비활성화합니다.
   1. 목록 보기에서 리소스를 선택합니다.
   1. **[!UICONTROL 사용 안 함]**&#x200B;을 선택하세요.
1. 새 개발 라이브러리를 만듭니다.
1. 비활성화된 리소스의 `latest` 버전을 추가합니다.
1. 저장하고 빌드합니다.
1. 라이브러리를 프로덕션으로 승격하는 일반 프로세스를 따릅니다.
1. 리소스를 제거하려면 프로덕션에 게시합니다.
