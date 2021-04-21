---
keywords: Experience Platform;홈;인기 항목;문제 해결;액세스 제어
solution: Experience Platform
title: 액세스 제어 문제 해결 안내서
topic-legacy: troubleshooting guide
description: 이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 액세스 제어 문제 해결 가이드

이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 다른 [!DNL Platform] 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

[!DNL Experience Platform] 는  [Adobe 관리 콘솔의 제품 프로필](http://adminconsole.adobe.com) 을 활용하여 역할 기반의 액세스 제어 기능을 제공하고, 사용자와 사용 권한 및 샌드박스를 연결합니다.  자세한 내용은 [액세스 제어 개요](home.md)를 참조하십시오.

## 현재 액세스 권한은 어디에서 찾을 수 있습니까?

IMS 조직의 시스템 관리자, 제품 관리자 또는 제품 프로필 관리자는 할당된 제품 프로필과 Adobe Admin Console 내에서 제공하는 권한을 볼 수 있습니다. [!DNL Admin Console]에서 제품 프로필의 권한을 보는 방법에 대한 지침은 [액세스 제어 사용 안내서](./ui/overview.md)를 참조하십시오.

관리자가 아닌 경우에도 액세스 제어 API의 `/acl/effective-policies` 끝점에 요청을 보내 현재 액세스 권한을 볼 수 있습니다. 자세한 내용은 [액세스 제어 개발자 안내서](./api/effective-policies.md)의 &quot;효과적인 정책 보기&quot; 섹션을 참조하십시오.

## [!DNL Platform] UI의 일부 기능을 사용할 수 없습니다. 이러한 기능에 대한 액세스는 권한을 통해 어떻게 제어됩니까?

특정 [!DNL Platform] 기능에 대한 액세스 권한이 없는 경우 해당 기능은 [!DNL Experience Platform] UI에서 숨겨지거나 흐리게 표시됩니다. 예를 들어 &quot;[!UICONTROL Profiles]&quot; 탭을 보려면 &quot;[!UICONTROL View Profiles]&quot; 또는 &quot;[!UICONTROL Manage Profiles]&quot; 권한이 있어야 합니다. [!DNL Experience Platform] 기능에 대한 추가 권한이 필요한 경우 관리자에게 문의하십시오.

## 권한은 어떻게 그룹화되며 사용 권한을 포함하는 그룹은 무엇입니까?

권한은 적용되는 [!DNL Platform] 기능(예: [!DNL Data Management] 및 [!DNL Profile Management])으로 그룹화되고 분류됩니다. 사용 가능한 권한 및 해당 권한이 속한 그룹의 전체 목록을 보려면 액세스 제어 개요에서 [권한 섹션](home.md#permissions)을 참조하십시오.

역할 기반 액세스 제어 제공에 대한 자세한 내용은 [액세스 제어 개요](home.md)를 참조하십시오.
