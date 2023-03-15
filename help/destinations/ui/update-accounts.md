---
keywords: 대상 계정 업데이트, 대상 계정, 계정 업데이트 방법, 대상 업데이트
title: 대상 계정 업데이트
type: Tutorial
description: 이 자습서에는 Adobe Experience Platform UI에서 대상 계정을 업데이트하는 단계가 나와 있습니다
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 대상 계정 업데이트

## 개요 {#overview}

다음 **[!UICONTROL 계정]** 탭에는 다양한 대상과 함께 설정한 연결에 대한 세부 사항이 표시됩니다. 다음을 참조하십시오. [계정 개요](../ui/destinations-workspace.md#accounts) 각 대상 계정에서 확인할 수 있는 모든 정보에 대해 설명합니다.

이 튜토리얼에서는 Experience Platform UI를 사용하여 대상 계정 세부 사항을 업데이트하는 단계를 설명합니다.

대상 계정 세부 사항을 업데이트하여 현재 사용 중인 대상의 현재 계정 또는 만료된 계정에 대한 자격 증명을 새로 고치고 다시 인증할 수 있습니다. 일반적으로 OAuth 및 전달자 토큰은 대상 플랫폼에 따라 수명이 제한됩니다. 이러한 토큰이 만료되면 아래에 설명된 워크플로우에서 새로 고칠 수 있습니다. 이 워크플로우는 OAuth 워크플로를 통과하거나 토큰을 다시 삽입하도록 안내합니다. 마찬가지로 다운스트림 플랫폼에서 암호 또는 사용자 액세스가 변경된 경우 자격 증명을 새로 고칠 수 있습니다.

배치 대상의 경우 액세스 또는 비밀 키가 변경된 경우 이를 업데이트할 수 있습니다. 또한 파일을 암호화하려는 경우 RSA 공개 키를 삽입할 수 있으며 내보낸 파일은 향후 암호화됩니다.

![계정 탭](../assets/ui/update-accounts/destination-accounts.png)

## 계정 업데이트 {#update}

기존 대상에 대한 연결 세부 사항을 업데이트하려면 아래 단계를 따르십시오.

1. 에 로그인합니다 [EXPERIENCE PLATFORM UI](https://platform.adobe.com/) 및 선택 **[!UICONTROL 대상]** 왼쪽 탐색 모음에서 을 클릭합니다. 선택 **[!UICONTROL 계정]** 을 클릭하여 기존 계정을 확인합니다.

   ![계정 탭](../assets/ui/update-accounts/accounts-tab.png)

2. 필터 아이콘 선택 ![필터 아이콘](../assets/ui/update-accounts/filter.png) 왼쪽 상단에서 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상의 목록을 제공합니다. 목록에서 대상을 두 개 이상 선택하여 선택한 대상과 연관된 계정의 필터링된 선택을 확인할 수 있습니다.

   ![대상 계정 필터링](../assets/ui/update-accounts/filter-accounts.png)

3. 줄임표(`...`)을 클릭하여 제품에서 사용할 수 있습니다. 옵션을 제공하는 팝업 패널이 나타납니다. **[!UICONTROL 세그먼트 활성화]**, **[!UICONTROL 세부 정보 편집]**, 및 **[!UICONTROL 삭제]** 계정입니다. 다음 항목 선택 ![세부 정보 편집 단추](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 세부 정보 편집]** 단추를 클릭하여 계정 정보를 편집합니다.

   ![계정 편집](../assets/ui/update-accounts/accounts-edit.png)

4. 업데이트된 계정 자격 증명을 입력합니다.

   * 를 사용하는 계정의 경우 `OAuth1` 또는 `OAuth2` 연결 유형, 선택 **[!UICONTROL OAuth에 다시 연결]** 계정 자격 증명을 갱신할 수 있습니다. 계정의 이름과 설명을 업데이트할 수도 있습니다.

   ![세부 정보 OAuth 편집](../assets/ui/update-accounts/edit-details-oauth.png)

   * 를 사용하는 계정의 경우 `Access Key` 또는 `ConnectionString` 연결 유형에서는 액세스 ID, 비밀 키 또는 연결 문자열과 같은 정보를 포함하여 계정 인증 정보를 편집할 수 있습니다. 계정의 이름과 설명을 업데이트할 수도 있습니다.

   ![세부 정보 편집 액세스 키](../assets/ui/update-accounts/edit-details-key.png)

   * 를 사용하는 계정의 경우 `Bearer token` 연결 유형에서 필요한 경우 새 전달자 토큰을 입력할 수 있습니다. 계정의 이름과 설명을 업데이트할 수도 있습니다.

   ![세부 정보 전달자 토큰 편집](../assets/ui/update-accounts/edit-details-bearer.png)

   * 를 사용하는 계정의 경우 `Server to server` 연결 유형에서는 계정의 이름 및 설명을 업데이트할 수 있습니다.

   ![세부 정보 편집 서버 간](../assets/ui/update-accounts/edit-details-s2s.png)

5. 선택 **[!UICONTROL 저장]** 계정 세부 사항 업데이트를 마칩니다.

## 다음 단계

이 자습서에 따라 **[!UICONTROL 대상]** 기존 계정을 업데이트할 작업 영역입니다.

대상에 대한 자세한 내용은 [대상 개요](../catalog/overview.md).