---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo 소스 커넥터 인증
description: 이 문서에서는 Marketo 인증 자격 증명을 생성하는 방법에 대한 정보를 제공합니다.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 인증 [!DNL Marketo Engage] 소스 커넥터

만들기 전에 [!DNL Marketo Engage] (이하 &quot;라 한다)[!DNL Marketo]&quot;) 소스 커넥터는 먼저 를 통해 사용자 지정 서비스를 설정해야 합니다 [!DNL Marketo] 인터페이스와 함께 Munchkin ID, 클라이언트 ID 및 클라이언트 암호 값을 검색합니다.

아래 설명서에서는 자격 증명을 획득하여 자격 증명을 만드는 방법에 대해 설명합니다 [!DNL Marketo] 소스 커넥터.

## 새 역할 설정

인증 자격 증명을 획득하는 첫 번째 단계는 를 통해 새 역할을 설정하는 것입니다. [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) 인터페이스.

에 로그인합니다. [!DNL Marketo] 을(를) 선택합니다. **[!DNL Admin]** 상단 탐색 막대에서 을 클릭합니다.

![새 역할에 대한 관리자](../images/marketo/home.png)

다음 *[!DNL Users & Role]s* 페이지에는 사용자, 역할 및 로그인 기록에 대한 정보가 포함되어 있습니다. 새 역할을 만들려면 **[!DNL Roles]** 상단 헤더에서 을(를) 선택하고 을(를) 선택합니다. **[!DNL New Role]**.

![새로운 역할](../images/marketo/new-role.png)

**[!DNL Create New Role]** 대화 상자가 표시됩니다. 이름과 설명을 입력한 다음 이 역할에 부여할 권한을 선택합니다. 권한은 특정 작업 영역으로 제한되어 있고 사용자는 권한이 있는 작업 영역에서만 작업을 수행할 수 있습니다.

부여할 권한을 선택했으면 을 선택합니다 **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

을 사용하여 역할을 만들 때 API에 대한 제한된 권한을 관리할 수 있습니다 [!DNL Marketo]. 액세스 API를 선택하는 대신 다음 권한을 선택하여 최소 액세스 수준을 가진 역할을 제공할 수 있습니다.

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## 새 사용자 설정

역할과 유사하게, **[!DNL Users & Roles]** 페이지. 다음 **[!DNL Users]** 페이지는 현재 Marketo에서 프로비저닝된 활성 사용자 목록을 제공합니다. 선택 **[!DNL Invite New User]** 새 사용자를 프로비저닝하려면

![invite-new-user](../images/marketo/invite-new-user.png)

팝업 대화 상자 메뉴가 나타납니다. 이메일, 이름, 성 및 이유에 대한 적절한 정보를 제공합니다. 이 단계에서는 초대하는 새 사용자 계정의 액세스에 대한 만료 날짜를 설정할 수도 있습니다. 완료되면 을 선택합니다 **[!DNL Next]**.

>[!IMPORTANT]
>
>새 사용자를 설정할 때는 만들어지는 사용자 지정 서비스에 대해서만 액세스를 할당해야 합니다.

![user-info](../images/marketo/new-user-info.png)

에서 적절한 필드를 선택합니다 **[!DNL Permissions]** step 을 선택한 후 **[!DNL API Only]** 새 사용자에게 API 역할을 제공하는 확인란. 선택 **[!DNL Next]** 계속 진행합니다.

![권한](../images/marketo/permissions.png)

프로세스를 완료하려면 **[!DNL Send]**.

![메시지](../images/marketo/message.png)

## 사용자 지정 서비스 설정

새 사용자를 설정하면 새 자격 증명을 검색하도록 사용자 지정 서비스를 설정할 수 있습니다. Admin 페이지에서 **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

다음 **[!DNL Installed services]** 페이지에 기존 서비스 목록이 포함되어 있으므로 새 사용자 지정 서비스를 만들려면 **[!DNL New]** 그런 다음 **[!DNL New Service]**.

![신규 서비스](../images/marketo/new-service.png)

새 서비스에 설명 표시 이름을 제공한 다음 을 선택합니다 **[!DNL Custom]** 에서 **[!DNL Service]** 드롭다운 메뉴 아래의 제품에서 사용할 수 있습니다. 적절한 설명을 입력한 다음 **[!DNL API Only User]** 드롭다운 메뉴 아래의 제품에서 사용할 수 있습니다. 필요한 세부 정보를 입력했으면 을 선택합니다 **[!DNL Create]** 새 사용자 지정 서비스를 만들려면

![만들기](../images/marketo/create.png)

## 클라이언트 ID 및 클라이언트 암호 가져오기

새 사용자 지정 서비스를 만들어 클라이언트 ID 및 클라이언트 암호 관련 값을 검색할 수 있습니다. 에서 **[!DNL Installed Services]** 메뉴에서 액세스할 사용자 지정 서비스를 찾은 다음 **[!DNL View Details]**.

![세부 사항 보기](../images/marketo/view-details.png)

클라이언트 ID와 클라이언트 암호가 포함된 대화 상자가 나타납니다.

![자격 증명](../images/marketo/credentials.png)

## Munchkin ID 가져오기

인증을 위해 완료해야 하는 마지막 단계입니다 [!DNL Marketo] 소스 커넥터는 Munchkin ID를 검색하는 것입니다. Admin 페이지에서 **[!DNL Munchkin]** 아래에 **[!DNL Integration]** 패널.

![admin-munchkin](../images/marketo/admin-munchkin.png)

다음 *[!DNL Munchkin]* 페이지의 맨 위에 고유한 Munchkin ID가 나열된 페이지가 나타납니다.

![munchkin-id](../images/marketo/munchkin-id.png)

클라이언트 ID 및 클라이언트 암호와 결합하여 Munchkin ID를 사용하여 새 계정을 구성하고 [새로 만들기 [!DNL Marketo] 소스 연결](../../../tutorials/ui/create/adobe-applications/marketo.md) Experience Platform에서 확인하십시오.
