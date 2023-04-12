---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리;쿼리 편집기;쿼리 편집기;쿼리 편집기;쿼리 편집기;
solution: Experience Platform
title: Query Service 자격 증명 안내서
description: Adobe Experience Platform Query Service는 쿼리를 작성 및 실행하고, 이전에 실행된 쿼리를 보고, 조직 내의 사용자가 저장한 쿼리에 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 3%

---

# 자격 증명 안내서

Adobe Experience Platform 쿼리 서비스를 통해 외부 클라이언트와 연결할 수 있습니다. 만료 자격 증명 또는 만료되지 않은 자격 증명을 사용하여 이러한 외부 클라이언트에 연결할 수 있습니다.

## 만료 자격 증명 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="클라이언트의 SSL 모드"
>abstract="쿼리 서비스에 연결된 클라이언트에서 SSL을 활성화해야 합니다. SSL 모드가 “필수”로 설정되어 있는지 확인합니다."

만료 자격 증명을 사용하여 외부 클라이언트에 대한 연결을 빠르게 설정할 수 있습니다.

![만료 자격 증명 섹션이 강조 표시된 쿼리 대시보드 자격 증명 탭](../images/ui/credentials/expiring-credentials.png)

다음 **[!UICONTROL 만료 자격 증명]** 이 섹션에서는 다음 정보를 제공합니다.

- **[!UICONTROL 호스트]**: 클라이언트를 연결할 호스트의 이름입니다. 플랫폼 UI의 위쪽 리본에 표시된 조직의 이름이 통합됩니다.
- **[!UICONTROL 포트]**: 연결할 호스트의 포트 번호입니다.
- **[!UICONTROL 데이터베이스]**: 클라이언트를 연결할 데이터베이스의 이름입니다.
- **[!UICONTROL 사용자 이름]**: Query Service에 연결하는 데 사용되는 사용자 이름입니다.
- **[!UICONTROL 암호]**: Query Service에 연결하는 데 사용되는 암호입니다. UI의 암호가 보안을 위해 해시되었습니다. 복사 아이콘(![복사 아이콘.](../images/ui/credentials/copy-icon.png))을 클릭하여 해시되지 않은 전체 자격 증명을 클립보드에 복사합니다.
- **[!UICONTROL PSQL 명령]**: 명령줄에서 PSQL을 사용하여 Query Service에 연결할 관련 정보를 모두 자동으로 삽입한 명령입니다.
- **[!UICONTROL 만료]**: 만료 자격 증명을 위한 만료 날짜 및 시간입니다. 토큰의 기본 유효 기간은 24시간이지만 Admin Console의 고급 설정에서 변경할 수 있습니다.

>[!TIP]
>
>Query Service에 대한 만료 자격 증명 연결에 대한 세션 기간을 변경하려면 [Admin Console](https://adminconsole.adobe.com/) 화면 옵션에서 다음 항목을 선택합니다. **설정** > **개인 정보 및 보안** > **인증 설정** > **고급 설정** > **최대 세션 수명**.
>
>![개인 정보 및 보안, 인증 설정 및 최대 세션 시간이 강조 표시된 Admin Console 설정 탭입니다.](../images/ui/credentials/max-session-life.png)
>
>자세한 내용은 Adobe 도움말 설명서를 참조하십시오 [고급 설정](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) admin console에서 제공.

## 만료되지 않은 자격 증명 {#non-expiring-credentials}

만료되지 않은 자격 증명을 사용하여 외부 클라이언트에 보다 영구적인 연결을 설정할 수 있습니다.

### 사전 요구 사항

만료되지 않은 자격 증명을 생성하려면 먼저 Adobe Admin Console에서 다음 단계를 완료해야 합니다.

1. 에 로그인합니다. [Adobe Admin Console](https://adminconsole.adobe.com/) 위쪽 탐색 모음에서 관련 조직을 선택합니다.
2. [제품 프로필을 선택합니다.](../../access-control/ui/browse.md)
3. [두 구성 모두 **샌드박스** 및 **Query Service 통합 관리** 권한](../../access-control/ui/permissions.md) 를 입력합니다.
4. [제품 프로필에 새 사용자 추가](../../access-control/ui/users.md) 따라서 구성된 권한이 부여됩니다.
5. [사용자를 제품 프로필 관리자로 추가](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 을 클릭하여 활성 제품 프로필에 대해 계정을 만들 수 있습니다.
6. [사용자를 제품 프로필 개발자로 추가](https://helpx.adobe.com/enterprise/using/manage-developers.html) 통합을 생성할 수 있습니다.

권한을 할당하는 방법에 대한 자세한 내용은 [액세스 제어](../../access-control/home.md).

이제 사용자가 만료 자격 증명 기능을 사용할 수 있도록 필요한 모든 권한이 Adobe Developer 콘솔에 구성됩니다.

### 자격 증명 생성

만료되지 않은 자격 증명 세트를 만들려면 Platform UI로 돌아가서 를 선택합니다 **[!UICONTROL 쿼리]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 쿼리] 작업 공간. 다음으로, **[!UICONTROL 자격 증명]** 탭 뒤에 **[!UICONTROL 자격 증명 생성]**.

![자격 증명 탭과 자격 증명 생성을 강조 표시한 쿼리 대시보드입니다.](../images/ui/credentials/generate-credentials.png)

자격 증명을 생성할 수 있는 대화 상자가 나타납니다. 만료되지 않은 자격 증명을 만들려면 다음 세부 정보를 제공해야 합니다.

- **[!UICONTROL 이름]**: 생성 중인 자격 증명의 이름입니다.
- **[!UICONTROL 설명]**: (선택 사항) 생성 중인 자격 증명에 대한 설명입니다.
- **[!UICONTROL 지정 대상]**: 자격 증명을 할당할 사용자입니다. 이 값은 자격 증명을 만드는 사용자의 이메일 주소여야 합니다.
- **[!UICONTROL 암호]** (선택 사항) 자격 증명을 위한 선택적 암호입니다. 암호를 설정하지 않으면 Adobe에서 자동으로 암호를 생성합니다.

필요한 세부 정보를 모두 제공했으면 을 선택합니다 **[!UICONTROL 자격 증명 생성]** 자격 증명을 생성하기 위해

![자격 증명 생성 대화 상자가 강조 표시됩니다.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>When **[!UICONTROL 자격 증명 생성]** 이 선택되면 구성 JSON 파일이 로컬 시스템에 다운로드됩니다. Adobe은 **not** 생성된 자격 증명을 기록하려면 다운로드한 파일을 안전하게 저장하고 자격 증명 기록을 유지해야 합니다.
>
>또한 자격 증명이 90일 동안 사용되지 않으면 자격 증명이 만료됩니다.

구성 JSON 파일에는 기술 계정 이름, 기술 계정 ID 및 자격 증명과 같은 정보가 포함되어 있습니다. 다음 형식으로 제공됩니다.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

생성된 자격 증명을 저장한 후 **[!UICONTROL 닫기]**. 이제 만료되지 않은 자격 증명 목록을 볼 수 있습니다.

![만료되지 않은 자격 증명 섹션이 강조 표시된 쿼리 대시보드 자격 증명 탭.](../images/ui/credentials/list-credentials.png)

만료되지 않은 자격 증명을 편집하거나 삭제할 수 있습니다. 만료되지 않은 자격 증명을 편집하려면 연필 아이콘(![연필 아이콘.](../images/ui/credentials/edit-icon.png) 참조). 만료되지 않은 자격 증명을 삭제하려면 삭제 아이콘(![휴지통 아이콘](../images/ui/credentials/delete-icon.png)).

만료되지 않은 자격 증명을 편집할 때 모달이 나타납니다. 업데이트할 다음 세부 정보를 제공할 수 있습니다.

- **[!UICONTROL 이름]**: 생성 중인 자격 증명의 이름입니다.
- **[!UICONTROL 설명]**: (선택 사항) 생성 중인 자격 증명에 대한 설명입니다.
- **[!UICONTROL 지정 대상]**: 자격 증명을 할당할 사용자입니다. 이 값은 자격 증명을 만드는 사용자의 이메일 주소여야 합니다.

![계정 업데이트 대화 상자](../images/ui/credentials/update-credentials.png)

필요한 세부 정보를 모두 제공했으면 을 선택합니다 **[!UICONTROL 계정 업데이트]** 자격 증명에 대한 업데이트를 완료합니다.

## 자격 증명을 사용하여 외부 클라이언트에 연결 {#use-credential-to-connect}

만료되거나 만료되지 않은 자격 증명을 사용하여 Aqua Data Studio, Looker 또는 Power BI과 같은 외부 클라이언트와 연결할 수 있습니다. 이러한 자격 증명에 대한 입력 방법은 외부 클라이언트에 따라 달라집니다. 이러한 자격 증명 사용에 대한 특정 지침은 외부 클라이언트의 설명서를 참조하십시오.

이 이미지는 만료되지 않은 자격 증명의 암호를 제외하고 UI에 있는 각 매개 변수의 위치를 나타냅니다. 만료되지 않은 자격 증명은 JSON 구성 파일에서 제공되지만, **자격 증명** 탭(UI에 있음).

![만료 자격 증명 섹션이 강조 표시된 쿼리 작업 공간 자격 증명 탭](../images/ui/credentials/expiring-credentials.png)

아래 표에서는 외부 클라이언트에 연결하는 데 일반적으로 필요한 매개 변수를 간략하게 설명합니다.

>[!NOTE]
>
>만료되지 않은 자격 증명을 사용하여 호스트에 연결할 때에도 [!UICONTROL 만료 자격 증명] 암호 및 사용자 이름을 제외한 섹션을 참조하십시오.
>사용자 이름과 암호를 입력하는 형식은 이 예제에서 보듯이 콜론 구분 값을 사용합니다 `username:{your_username}` 및 `password:{password_string}`.

| 매개 변수 | 설명 | 예 |
|---|---|---|
| **서버/호스트** | 연결할 서버/호스트의 이름입니다. <ul><li>이 값은 만료 자격 증명과 만료 전 자격 증명 모두에 사용되며 `server.adobe.io`. 값은 **[!UICONTROL 호스트]** 에서 [!UICONTROL 만료 자격 증명] 섹션을 참조하십시오.</ul></li> | `acme.platform.adobe.io` |
| **포트** | 연결할 서버/호스트의 포트입니다. <ul><li>이 값은 만료 자격 증명과 만료 전 자격 증명 모두에 사용되며 **[!UICONTROL 포트]** 에서 [!UICONTROL 만료 자격 증명] 섹션을 참조하십시오.</ul></li> | `80` |
| **데이터베이스** | 연결할 데이터베이스입니다. <ul><li>이 값은 만료 자격 증명과 만료되지 않은 자격 증명 모두에 사용되며 **[!UICONTROL 데이터베이스]** 에서 [!UICONTROL 만료 자격 증명] 섹션을 참조하십시오. </ul></li> | `prod:all` |
| **사용자 이름** | 외부 클라이언트에 연결하는 사용자의 사용자 이름입니다. <ul><li>이 값은 만료 자격 증명과 만료 전 자격 증명 모두에 사용됩니다. 이전 영숫자 문자열을 사용합니다 `@AdobeOrg`. 이 값은 **[!UICONTROL 사용자 이름]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **암호** | 외부 클라이언트에 연결하는 사용자의 암호입니다. <ul><li>만료 자격 증명을 사용하는 경우 다음 위치에서 찾을 수 있습니다. **[!UICONTROL 암호]** 내 [!UICONTROL 만료 자격 증명] 섹션을 참조하십시오.</li><li>만료되지 않은 자격 증명을 사용하는 경우 이 값은 technicalAccountID에서 연결된 인수와 구성 JSON 파일에서 가져온 자격 증명입니다. 암호 값은 다음 형식을 사용합니다. `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>만료 자격 증명 암호는 1,000자 이상의 영숫자 문자열입니다. 예가 없습니다.</li><li>만료되지 않은 자격 증명 암호는 다음과 같습니다.<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 다음 단계

만료 자격 증명과 만료 전 자격 증명이 모두 작동하는 방식을 이해하므로 이러한 자격 증명을 사용하여 외부 클라이언트에 연결할 수 있습니다. 외부 클라이언트에 대한 자세한 내용은 [Query Service에 클라이언트 연결 안내서](../clients/overview.md).
