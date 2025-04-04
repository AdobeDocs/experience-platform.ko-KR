---
keywords: Experience Platform;홈;인기 항목;문제 해결;액세스 제어
solution: Experience Platform
title: 액세스 제어 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform의 액세스 제어에 대한 FAQ에 대한 답변을 제공합니다.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 액세스 제어 문제 해결 안내서

이 문서에서는 Adobe Experience Platform의 액세스 제어에 대한 FAQ에 대한 답변을 제공합니다. 다른 [!DNL Experience Platform] 서비스와 관련된 질문 및 문제 해결은 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

[!DNL Experience Platform]은(는) [Adobe Admin Console](https://adminconsole.adobe.com)의 제품 프로필을 활용하여 역할 기반 액세스 제어를 제공하고 사용자와 권한 및 샌드박스를 연결합니다.  자세한 내용은 [액세스 제어 개요](home.md)를 참조하십시오.

## 현재 액세스 권한은 어디에서 찾을 수 있습니까?

조직의 시스템 관리자, 제품 관리자 또는 제품 프로필 관리자인 경우 할당된 제품 프로필과 Adobe Admin Console 내에서 제공하는 권한을 볼 수 있습니다. 제품 프로필의 권한을 보기 위해 [!DNL Admin Console]을(를) 탐색하는 방법에 대한 지침은 [액세스 제어 사용 안내서](./ui/overview.md)를 참조하세요.

관리자가 아닌 경우에도 액세스 제어 API의 `/acl/effective-policies` 끝점에 요청을 전송하여 현재 액세스 권한을 볼 수 있습니다. 자세한 내용은 [액세스 제어 개발자 안내서](./api/effective-policies.md)의 &quot;유효 정책 보기&quot; 섹션을 참조하십시오.

## [!DNL Experience Platform] UI의 일부 기능을 사용할 수 없습니다. 이러한 기능에 대한 액세스는 권한으로 어떻게 제어됩니까?

특정 [!DNL Experience Platform] 기능에 대한 액세스 권한이 없는 경우 해당 기능이 [!DNL Experience Platform] UI에서 숨겨지거나 회색으로 표시됩니다. 예를 들어 &quot;[!UICONTROL 프로필]&quot; 탭을 보려면 &quot;[!UICONTROL 프로필 보기]&quot; 또는 &quot;[!UICONTROL 프로필 관리]&quot; 권한이 있어야 합니다. [!DNL Experience Platform] 기능에 대한 추가 권한이 필요한 경우 관리자에게 문의하십시오.

## 권한은 어떻게 그룹화되며, 사용할 권한이 포함된 그룹은 무엇입니까?

권한은 적용되는 [!DNL Experience Platform] 기능(예: [!DNL Data Management] 및 [!DNL Profile Management])별로 그룹화되고 분류됩니다. 사용 가능한 권한 및 해당 그룹이 속한 그룹의 전체 목록을 보려면 액세스 제어 개요에서 [권한 섹션](home.md#permissions)을 참조하십시오.

역할 기반 액세스 제어를 제공하는 방법에 대한 자세한 내용은 [액세스 제어 개요](home.md)를 참조하십시오.

## Adobe IO에서 Business ID로 마이그레이션한 후 권한은 어떻게 됩니까?

액세스 컨트롤은 권한 부여에 사용자 ID(사용자에게 할당된 내부 고유 ID)를 사용합니다. 조직이 Adobe ID에서 Business ID로 마이그레이션되면 사용자 ID가 변경되고 액세스 제어가 새로 생성된 사용자 ID를 사용하게 되므로 해당 사용자에 대해 설정된 모든 권한이 손실됩니다. 조직이 Business ID로 마이그레이션되는 경우 Adobe 담당자에게 문의하여 사용자 ID를 Adobe ID에서 Business ID로 마이그레이션하십시오.
