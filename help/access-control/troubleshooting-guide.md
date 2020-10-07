---
keywords: Experience Platform;home;popular topics;troubleshooting;access control
solution: Experience Platform
title: 액세스 제어 문제 해결 가이드
topic: troubleshooting guide
description: 이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# 액세스 제어 문제 해결 가이드

이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 다른 [!DNL Platform] 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 가이드를 참조하십시오](../landing/troubleshooting.md).

[!DNL Experience Platform] 사용자는 사용 권한 및 샌드박스 연결을 통해 [Adobe Admin Console의](http://adminconsole.adobe.com) 제품 프로필을 활용하여 역할 기반의 액세스 제어를 제공할 수 있습니다.  자세한 내용은 [액세스 제어 개요를](home.md) 참조하십시오.

## 현재 액세스 권한은 어디에서 찾을 수 있습니까?

IMS 조직의 시스템 관리자, 제품 관리자 또는 제품 프로필 관리자인 경우, 할당된 제품 프로필과 Adobe Admin Console 내에서 제공하는 권한을 볼 수 있습니다. 제품 [프로필의 권한을 보기 위해 탐색하는 방법에 대한 지침은](./ui/overview.md) 액세스 제어 사용 안내서 [!DNL Admin Console] 를 참조하십시오.

관리자가 아닌 경우에도 액세스 제어 API의 `/acl/effective-policies` 끝점으로 요청을 보내 현재 액세스 권한을 볼 수 있습니다. 자세한 내용은 [액세스 제어 개발자 안내서의](./api/effective-policies.md) &quot;효과적인 정책 보기&quot; 섹션을 참조하십시오.

## UI의 일부 기능을 사용할 수 [!DNL Platform] 없습니다. 이러한 기능에 대한 액세스는 권한에 의해 어떻게 제어됩니까?

특정 기능에 대한 액세스 권한이 없는 경우 해당 [!DNL Platform] 기능은 [!DNL Experience Platform] UI에서 숨겨지거나 흐리게 표시됩니다. 예를 들어 &quot;[!UICONTROL 프로필]&quot; 탭을 보려면 &quot;프로필[!UICONTROL 보기]&quot; 또는 &quot;프로필[!UICONTROL 관리]&quot; 권한이 있어야합니다. 기능에 대한 추가 권한이 필요한 경우 관리자에게 [!DNL Experience Platform] 문의하십시오.

## 권한은 어떻게 그룹화되며 어떤 그룹에 사용하고자 하는 권한이 포함되어 있습니까?

권한은 적용되는 기능(예: 및)에 따라 그룹화되고 [!DNL Platform] [!DNL Data Management] [!DNL Profile Management]분류됩니다. 사용 가능한 권한 및 해당 권한이 속한 그룹의 전체 목록은 액세스 제어 개요의 [권한 섹션](home.md#permissions) 을 참조하십시오.

역할 기반 [액세스 제어](home.md) 제공에 대한 자세한 내용은 액세스 제어 개요를 참조하십시오.