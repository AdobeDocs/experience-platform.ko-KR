---
title: 계정 대상자
description: 계정 대상자를 만들고 사용하여 다운스트림 대상의 계정 프로필을 타겟팅하는 방법을 알아봅니다.
badgeLimitedAvailability: label="제한된 가용성" type="Caution"
badgeB2B: label="B2B 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 계정 대상자

>[!AVAILABILITY]
>
>계정 대상은 다음에서만 사용할 수 있습니다. [Real-time Customer Data Platform B2B 에디션](../../rtcdp/b2b-overview.md). 또한 계정 대상자 기능은 현재 **제한된 가용성**. 이 기능에 대한 액세스 권한을 요청하려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.

Adobe Experience Platform을 사용하면 계정 세분화를 통해 사용자 기반 대상에서 계정 기반 대상으로의 마케팅 세분화 경험을 전체적으로 쉽고 정교하게 만들 수 있습니다.

계정 대상은 계정 기반 대상에 대한 입력으로 사용할 수 있으며, 이를 통해 다운스트림 서비스의 해당 계정 내에서 사용자를 타겟팅할 수 있습니다. 예를 들어 계정 기반 대상을 사용하여 다음을 수행하는 모든 계정의 레코드를 검색할 수 있습니다 **아님** coo(최고 운영 책임자) 또는 CMO(최고 마케팅 책임자)라는 직함을 가진 모든 사람에 대한 연락처 정보가 있습니다.

## 용어 {#terminology}

계정 대상을 시작하기 전에 다양한 대상 유형 간의 차이점을 검토하십시오.

- **계정 대상자**: 계정 대상자는 을 사용하여 생성된 대상자입니다. **account** 프로필 데이터. 계정 프로필 데이터를 사용하여 다운스트림 계정 내에서 사용자를 타겟팅하는 대상을 만들 수 있습니다. 계정 프로필에 대한 자세한 내용은 [계정 프로필 개요](../../rtcdp/accounts/account-profile-overview.md).
- **사용자 대상**: 사람 대상자는 을 사용하여 만들어진 대상자입니다. **고객** 프로필 데이터. 고객 프로필 데이터를 사용하여 비즈니스 고객을 타겟팅하는 대상을 만들 수 있습니다. 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).
- **잠재 고객**: 잠재 고객은 를 사용하여 생성된 대상입니다. **잠재 고객** 프로필 데이터. Prospect 프로필 데이터를 사용하여 인증되지 않은 사용자로부터 대상을 만들 수 있습니다. 잠재 고객 프로필에 대한 자세한 내용은 [잠재 고객 프로필 개요](../../profile/ui/prospect-profile.md).

## 액세스 {#access}

계정 대상자에 액세스하려면 다음을 선택합니다. **[!UICONTROL 대상]** 다음에서 **[!UICONTROL 계정]** 섹션.

![Accounts 섹션 내에서 Audiences 버튼이 강조 표시됩니다.](../images/ui/account-audiences/select.png)

다음 [!UICONTROL 찾아보기] 조직의 모든 계정 대상자 목록을 표시하는 페이지가 표시됩니다.

![조직에 속한 계정 대상이 표시됩니다.](../images/ui/account-audiences/browse.png)

이 보기에는 이름, 프로필 수, 원본, 라이프사이클 상태, 만든 날짜 및 마지막으로 업데이트한 날짜 등 대상에 대한 정보가 나열됩니다.

## 대상자 만들기 {#create}

계정 대상자를 만들려면 다음을 선택합니다. **[!UICONTROL 대상자 만들기]** 다음에 있음 [!UICONTROL 찾아보기] 페이지를 가리키도록 업데이트하는 중입니다.

![다음 [!UICONTROL 대상자 만들기] [계정 대상자 찾아보기] 페이지에서 버튼이 강조 표시됩니다.](../images/ui/account-audiences/select-create-audience.png)

세그먼트 빌더 가 나타납니다. 계정 속성은 왼쪽 탐색 모음에 표시됩니다.

![세그먼트 빌더 가 표시됩니다. 속성만 표시됩니다.](../images/ui/account-audiences/segment-builder.png)

계정 대상을 만들 때는 아래에 이벤트가 나열되어 있습니다. **[!UICONTROL 사람]**, 이러한 속성은 사용자와 연결되므로 고유한 탭이 되지 않습니다.

![다음 내에 있는 이벤트를 찾을 위치입니다. [!UICONTROL 사람] 폴더가 강조 표시됩니다.](../images/ui/account-audiences/attributes.png)

세그먼트 빌더 사용에 대한 자세한 내용은 [세그먼트 빌더 UI 안내서](./segment-builder.md).

## 대상자 활성화 {#activate}

>[!NOTE]
>
>계정 대상자를 지원하는 대상의 수는 제한되어 있습니다. 이 프로세스를 계속하기 전에 활성화하려는 대상이 계정 대상자를 지원하는지 확인하십시오.

계정 대상을 만든 후 대상을 다른 다운스트림 서비스로 활성화할 수 있습니다.

활성화하려는 대상을 선택한 후 다음을 수행합니다 **[!UICONTROL 대상에 활성화]**.

![다음 [!UICONTROL 대상에 활성화] 선택한 대상자의 빠른 작업 메뉴에서 버튼이 강조 표시됩니다.](../images/ui/account-audiences/activate.png)

다음 [!UICONTROL 대상 활성화] 페이지가 나타납니다. 지원되는 대상 및 필드 매핑에 대한 세부 정보를 포함하여 활성화 프로세스에 대한 자세한 내용은 [계정 대상자 활성화](/help/destinations/ui/activate-account-audiences.md) 튜토리얼.

## 다음 단계 {#next-steps}

이제 이 안내서를 읽고 Adobe Experience Platform에서 계정 대상을 만들고 사용하는 방법을 더 잘 이해할 수 있습니다. Platform에서 다른 유형의 대상을 사용하는 방법에 대해 알아보려면 [세그먼테이션 서비스 UI 안내서](./overview.md).
