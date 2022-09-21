---
title: 확장 구성
description: Adobe Experience Platform UI 또는 데이터 수집 UI에서 사용자로부터 전역 설정을 수집하도록 태그 확장을 구성하는 방법을 알아봅니다.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 68%

---

# 확장 구성

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../term-updates.md)를 참조하십시오.

확장 구성은 확장이 사용자로부터 전역 설정을 수집하는 방식입니다. 예를 들어, 사용자가 비콘 전송 작업을 사용하여 비콘을 전송할 수 있도록 해주는 확장을 생각해보면 비콘에는 항상 계정 ID가 포함되어야 합니다. 비콘 전송 작업을 구성할 때마다 계정 ID를 요청하여 사용자에게 문제를 유발하는 것은 바람직하지 않습니다. 대신, 확장 구성 보기에서 계정 ID를 한 번 요청해야 합니다. 비콘이 전송될 때마다 비콘 전송 작업 라이브러리 모듈은 확장 구성에서 계정 ID를 가져와 비콘에 추가할 수 있습니다.

사용자가 Adobe Experience Platform에서 태그 속성에 확장을 설치하면 확장이 제공할 확장 구성 보기가 표시됩니다. 확장 구성을 완료하지 않으면 확장 설치를 완료할 수 없습니다. 확장 구성에 대한 보기를 만드는 방법을 알아보려면 [보기](./web/views.md)에 대한 문서를 참조하십시오.

확장 구성 보기에서 설정을 저장하면 태그 런타임 라이브러리에 해당 설정이 표시됩니다. 그런 다음 [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings)를 호출하여 확장 라이브러리 모듈에서 이러한 설정에 액세스할 수 있습니다.

확장 구성은 사용하지 않도록 선택할 수 있는 선택 기능입니다.
