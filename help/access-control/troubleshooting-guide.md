---
keywords: Experience Platform;홈;인기 항목;문제 해결;액세스 제어
solution: Experience Platform
title: Access Control 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 액세스 제어 문제 해결 가이드

이 문서에서는 Adobe Experience Platform의 액세스 제어에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 기타 관련 질문 및 문제 해결 [!DNL Platform] 서비스, [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

[!DNL Experience Platform] 에서는 제품 프로필을 활용합니다 [Adobe Admin Console](https://adminconsole.adobe.com) 역할 기반 액세스 제어를 제공하기 위해 사용자와 권한 및 샌드박스를 연결합니다.  자세한 내용은 [액세스 제어 개요](home.md) 추가 정보.

## 현재 액세스 권한은 어디에서 찾을 수 있습니까?

IMS 조직의 시스템 관리자, 제품 관리자 또는 제품 프로필 관리자인 경우 할당된 제품 프로필과 Adobe Admin Console 내에서 제공하는 권한을 볼 수 있습니다. 자세한 내용은 [액세스 제어 사용 안내서](./ui/overview.md) 탐색 방법에 대한 지침 [!DNL Admin Console] 제품 프로필의 권한을 보려면

관리자가 아닌 사용자에게는 `/acl/effective-policies` 액세스 제어 API의 끝점입니다. 의 &quot;유효 정책 보기&quot; 섹션을 참조하십시오. [access control 개발자 안내서](./api/effective-policies.md) 추가 정보.

## 의 일부 기능 [!DNL Platform] UI를 사용할 수 없습니다. 권한은 이러한 기능에 대한 액세스를 어떻게 제어합니까?

특정 [!DNL Platform] 이 기능은 [!DNL Experience Platform] UI. 예를 들어 &quot;[!UICONTROL 프로필]&quot; 탭에서 &quot;[!UICONTROL 프로필 보기]&quot; 또는 &quot;[!UICONTROL 프로필 관리]&quot; 사용 권한. 에 대한 추가 권한이 필요한 경우 관리자에게 문의하십시오 [!DNL Experience Platform] 기능.

## 사용 권한을 그룹화하고 사용 권한을 포함하는 그룹은 무엇입니까?

권한은 [!DNL Platform] 이 기능들이 (예: [!DNL Data Management] 및 [!DNL Profile Management]). 사용 가능한 권한 및 해당 권한이 속한 그룹의 전체 목록을 보려면 [권한 섹션](home.md#permissions) 액세스 제어 개요

자세한 내용은 [액세스 제어 개요](home.md) 역할 기반 액세스 제어 제공에 대한 자세한 정보.

## Adobe IO에서 비즈니스 ID로 마이그레이션한 후 권한은 어떻게 됩니까?

액세스 제어는 권한 부여에 사용자 ID(사용자에게 할당된 내부 고유 ID)를 사용합니다. 조직이 Adobe ID에서 비즈니스 ID로 마이그레이션되면 사용자 ID가 변경되고 액세스 제어가 새로 생성된 사용자 ID를 사용하므로 해당 사용자에 대해 설정된 모든 권한이 손실됩니다. 조직이 비즈니스 ID로 마이그레이션된 경우 Adobe 담당자에게 문의하여 사용자 ID를 Adobe ID에서 비즈니스 ID로 마이그레이션하십시오.
