---
keywords: 대상 계정 업데이트,대상 계정
title: 대상 계정 업데이트
type: 튜토리얼
description: 이 자습서는 Adobe Experience Platform UI에서 대상 계정을 업데이트하는 단계를 나열합니다
exl-id: afb41878-4205-4c64-af4d-e2740f852785
translation-type: tm+mt
source-git-commit: 07869d63f395bbab6c49a3976051facdf94d43b7
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 대상 계정 업데이트

## 개요 {#overview}

**[!UICONTROL Accounts]** 탭에는 다양한 대상으로 설정한 연결에 대한 세부 정보가 표시됩니다. 각 대상에 대한 모든 정보는 아래 표를 참조하십시오.

![계정 탭](../assets/ui/update-accounts/destination-accounts.png)

| 요소 | 설명 |
|---|---|
| [!UICONTROL Platform] | 연결을 설정한 대상. |
| [!UICONTROL Connection Type] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상:S3 또는 FTP일 수 있습니다.</li><li>실시간 광고 대상:서버 간</li><li>Amazon S3 클라우드 스토리지 대상:액세스 키 </li><li>SFTP 클라우드 스토리지 대상:SFTP에 대한 기본 인증</li></ul> |
| [!UICONTROL Username] | [연결 대상 마법사](../catalog/email-marketing/overview.md#connect-destination)에서 선택한 사용자 이름입니다. |
| [!UICONTROL Destinations] | 대상에 대해 만들어진 기본 정보와 연결된 고유한 성공적인 대상 흐름 수를 나타냅니다. |
| [!UICONTROL Authorized] | 이 대상에 대한 연결이 허가된 날짜입니다. |

## 계정 업데이트 {#update}

기존 대상에 대한 연결 세부 정보를 업데이트하려면 아래 단계를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 막대에서 **[!UICONTROL Destinations]**&#x200B;를 선택합니다. 상단 헤더에서 **[!UICONTROL Accounts]**&#x200B;을 선택하여 기존 계정을 봅니다.

   ![계정 탭](../assets/ui/update-accounts/accounts-tab.png)

2. 정렬 패널을 시작하려면 왼쪽 상단에 있는 필터 아이콘 ![필터 아이콘](../assets/ui/update-accounts/filter.png)을 선택합니다. 정렬 패널은 모든 대상 목록을 제공합니다. 목록에서 둘 이상의 대상을 선택하여 선택한 대상과 연관된 계정의 필터링된 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/update-accounts/filter-accounts.png)

3. 계정의 정보를 편집하려면 **[!UICONTROL Platform]** 열에서 ![계정 편집 단추](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]** 단추를 선택합니다.

   ![계정 탭](../assets/ui/update-accounts/accounts-edit.png)

4. 업데이트된 계정 자격 증명을 입력합니다.

   * `OAuth2` 연결 유형을 사용하는 계정의 경우 **[!UICONTROL Reconnect OAuth]**&#x200B;을 선택하여 계정 자격 증명을 갱신합니다.

      ![세부 정보 OAuth 편집](../assets/ui/update-accounts/edit-details-oauth.png)


   * `Access Key` 또는 `ConnectionString` 연결 유형을 사용하는 계정의 경우 액세스 ID, 비밀 키 또는 연결 문자열 등의 정보를 포함하여 계정 인증 정보를 편집할 수 있습니다.

      ![세부 사항 액세스 키 편집](../assets/ui/update-accounts/edit-details-key.png)

5. 자격 증명 업데이트를 완료하려면 **[!UICONTROL Save]**&#x200B;을 선택합니다.
