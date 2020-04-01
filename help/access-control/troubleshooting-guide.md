---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 액세스 제어 문제 해결 가이드
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# 액세스 제어 문제 해결 가이드

이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 다른 플랫폼 서비스와 관련된 질문 및 문제 해결에 대해서는 Experience Platform [문제 해결 안내서를](../landing/troubleshooting.md)참조하십시오.

Adobe Experience Platform은 Adobe Admin [Console의](http://adminconsole.adobe.com) 제품 프로필을 활용하여 역할 기반의 **액세스 제어를**&#x200B;제공하고 사용자에게 사용 권한 및 샌드박스를 연결합니다.  자세한 내용은 [액세스 제어 개요를](home.md) 참조하십시오.

## 현재 액세스 권한은 어디에서 찾을 수 있습니까?

IMS 조직의 시스템 관리자, 제품 관리자 또는 제품 프로필 관리자인 경우 Adobe Admin Console에서 할당된 제품 프로필 및 해당 관리자가 제공하는 권한을 볼 수 있습니다. 관리 콘솔을 탐색하여 제품 프로필의 권한을 보는 방법에 대한 지침은 [액세스 제어 사용 안내서를](./ui/overview.md) 참조하십시오.

관리자가 아닌 경우에도 액세스 제어 API의 `/acl/effective-policies` 끝점으로 요청을 보내 현재 액세스 권한을 볼 수 있습니다. 자세한 내용은 [액세스 제어 개발자 안내서의](./api/effective-policies.md) &quot;효과적인 정책 보기&quot; 섹션을 참조하십시오.

## 플랫폼 UI의 일부 기능을 사용할 수 없습니다. 이러한 기능에 대한 액세스는 권한에 의해 어떻게 제어됩니까?

특정 플랫폼 기능에 대한 액세스 권한이 없는 경우 해당 기능은 경험 플랫폼 UI에서 숨겨지거나 흐리게 표시됩니다. 예를 들어 &quot;프로필&quot; 탭을 보려면 &quot;프로필 보기&quot; 또는 &quot;프로필 관리&quot; 권한이 있어야 합니다. Experience Platform 기능에 대한 추가 권한이 필요한 경우 관리자에게 문의하십시오.

## 사용 권한은 어떻게 그룹화되며 사용 권한을 포함하는 그룹은 무엇입니까?

사용 권한은 적용되는 플랫폼 기능(예: 데이터 관리 및 프로필 관리)으로 그룹화되고 분류됩니다. 사용 가능한 권한 및 해당 권한이 속한 그룹의 전체 목록은 액세스 제어 개요의 [권한 섹션을](home.md#permissions) 참조하십시오.

역할 기반 액세스 제어 제공에 대한 자세한 내용은 [액세스 제어 개요를](home.md) 참조하십시오.