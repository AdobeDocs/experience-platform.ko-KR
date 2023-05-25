---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리;쿼리 편집기;쿼리 편집기;쿼리 편집기;
solution: Experience Platform
title: 쿼리 서비스 자격 증명 안내서
description: Adobe Experience Platform Query Service는 쿼리를 작성하여 실행하고, 이전에 실행한 쿼리를 보고, 조직 내에서 사용자가 저장한 쿼리에 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: aed521bf50c301148c10b98021f1a3df0ed45278
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 3%

---

# 자격 증명 안내서

Adobe Experience Platform Query Service를 사용하면 외부 클라이언트와 연결할 수 있습니다. 만료 자격 증명 또는 만료되지 않는 자격 증명을 사용하여 이러한 외부 클라이언트에 연결할 수 있습니다.

## 자격 증명 만료 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="클라이언트의 SSL 모드"
>abstract="쿼리 서비스에 연결된 클라이언트에서 SSL을 활성화해야 합니다. SSL 모드가 “필수”로 설정되어 있는지 확인합니다."

만료되는 자격 증명을 사용하여 외부 클라이언트에 대한 연결을 빠르게 설정할 수 있습니다.

![만료 자격 증명 섹션이 강조 표시된 쿼리 대시보드 자격 증명 탭입니다.](../images/ui/credentials/expiring-credentials.png)

다음 **[!UICONTROL 자격 증명 만료]** 섹션은 다음 정보를 제공합니다.

- **[!UICONTROL 호스트]**: 클라이언트를 연결할 호스트의 이름입니다. Platform UI의 상단 리본에 표시된 조직 이름이 통합됩니다.
- **[!UICONTROL 포트]**: 연결할 호스트의 포트 번호입니다.
- **[!UICONTROL 데이터베이스]**: 클라이언트를 연결할 데이터베이스의 이름입니다.
- **[!UICONTROL 사용자 이름]**: 쿼리 서비스에 연결하는 데 사용되는 사용자 이름입니다.
- **[!UICONTROL 암호]**: 쿼리 서비스에 연결하는 데 사용되는 암호입니다. 보안을 위해 UI의 암호가 해시되었습니다. 복사 아이콘(![복사 아이콘](../images/ui/credentials/copy-icon.png))을 클릭하여 해시되지 않은 전체 자격 증명을 클립보드에 복사합니다.
- **[!UICONTROL PSQL 명령]**: 명령줄에서 PSQL을 사용하여 쿼리 서비스에 연결할 모든 관련 정보를 자동으로 삽입하는 명령입니다.
- **[!UICONTROL 만료]**: 만료될 자격 증명의 만료일 및 시간입니다. 토큰의 기본 유효 기간은 24시간이지만 Admin Console의 고급 설정에서 변경할 수 있습니다.

>[!TIP]
>
>만료되는 자격 증명 연결의 세션 수명을 쿼리 서비스로 변경하려면 다음 위치로 이동합니다. [Admin Console](https://adminconsole.adobe.com/) 화면에 표시할 옵션을 선택하십시오. **설정** > **개인 정보 보호 및 보안** > **인증 설정** > **고급 설정** > **최대 세션 수명**.
>
>![개인 정보 및 보안, 인증 설정 및 최대 세션 수명이 강조 표시된 Admin Console 설정 탭입니다.](../images/ui/credentials/max-session-life.png)
>
>에 대한 자세한 내용은 Adobe 도움말 설명서 를 참조하십시오. [고급 설정](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) Admin Console 제공.

## 만료되지 않는 자격 증명 {#non-expiring-credentials}

만료되지 않는 자격 증명을 사용하여 외부 클라이언트에 대한 보다 영구적인 연결을 설정할 수 있습니다.

>[!NOTE]
>
>만료되지 않는 자격 증명에는 다음과 같은 제한이 있습니다.<br><ul><li>사용자는 다음으로 구성된 사용자 이름 및 암호로 로그인해야 합니다. `{technicalAccountId}:{credential}`. 자세한 내용은 [자격 증명 생성](#generate-credentials) 섹션.</li><li>만료되는 자격 증명을 만들 때 사용자가 스키마 및 데이터 세트를 볼 수 있는 기본 권한 집합이 있는 새 역할이 만들어집니다. 쿼리 서비스와 함께 사용할 수 있도록 &#39;쿼리 관리&#39; 권한도 이 역할에 할당됩니다.</li><li>서드파티 클라이언트는 쿼리 개체를 나열할 때 예상과 다르게 수행할 수 있습니다. 예를 들어 다음과 같은 일부 타사 클라이언트 [!DNL DB Visualizer] 왼쪽 패널에 보기 이름이 표시되지 않습니다. 그러나 SELECT 쿼리 내에서 를 호출한 경우에는 보기 이름에 액세스할 수 있습니다. 마찬가지로, [!DNL PowerUI] 대시보드 생성을 위해 선택할 SQL을 통해 생성된 임시 뷰를 나열하지 않을 수 있습니다.</li></ul>

### 사전 요구 사항

만료되지 않는 자격 증명을 생성하려면 Adobe Admin Console에서 다음 단계를 완료해야 합니다.

1. 에 로그인 [Adobe Admin Console](https://adminconsole.adobe.com/) 맨 위 탐색 막대에서 관련 조직을 선택합니다.
2. [제품 프로필을 선택합니다.](../../access-control/ui/browse.md)
3. [두 구성 **샌드박스** 및 **쿼리 서비스 통합 관리** 권한](../../access-control/ui/permissions.md) 제품 프로필.
4. [제품 프로필에 새 사용자 추가](../../access-control/ui/users.md) 따라서 구성된 권한이 부여됩니다.
5. [사용자를 제품 프로필 관리자로 추가](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 모든 활성 제품 프로필에 대한 계정 만들기를 허용합니다.
6. [사용자를 제품 프로필 개발자로 추가](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html) 통합을 만들려면.

권한을 할당하는 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오. [액세스 제어](../../access-control/home.md).

이제 사용자가 만료되는 자격 증명 기능을 사용할 수 있도록 Adobe Developer 콘솔에 필요한 모든 권한이 구성됩니다.

### 자격 증명 생성 {#generate-credentials}

만료되지 않는 자격 증명 세트를 만들려면 Platform UI로 돌아가서 를 선택합니다. **[!UICONTROL 쿼리]** 을(를) 왼쪽 탐색에서 [!UICONTROL 쿼리] 작업 영역. 그런 다음 **[!UICONTROL 자격 증명]** 탭 뒤에 오는 **[!UICONTROL 자격 증명 생성]**.

![인증서 탭 및 인증서 생성 이 강조 표시된 쿼리 대시보드입니다.](../images/ui/credentials/generate-credentials.png)

자격 증명을 생성할 수 있는 대화 상자가 나타납니다. 만료되지 않는 자격 증명을 만들려면 다음 세부 정보를 제공해야 합니다.

- **[!UICONTROL 이름]**: 생성 중인 자격 증명의 이름입니다.
- **[!UICONTROL 설명]**: (선택 사항) 생성 중인 자격 증명에 대한 설명입니다.
- **[!UICONTROL 할당 대상:]**: 자격 증명을 할당할 사용자입니다. 이 값은 자격 증명을 만드는 사용자의 이메일 주소여야 합니다.
- **[!UICONTROL 암호]** (선택 사항) 자격 증명에 대한 선택적 암호입니다. 암호를 설정하지 않으면 Adobe이 자동으로 암호를 생성합니다.

필요한 세부 정보를 모두 제공했으면 을 선택합니다. **[!UICONTROL 자격 증명 생성]** 자격 증명을 생성합니다.

![자격 증명 생성 대화 상자가 강조 표시됩니다.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>날짜 **[!UICONTROL 자격 증명 생성]** 을 선택하면 구성 JSON 파일이 로컬 컴퓨터에 다운로드됩니다. Adobe이 **아님** 생성된 자격 증명을 기록하려면 다운로드한 파일을 안전하게 저장하고 자격 증명을 기록해야 합니다.
>
>또한 자격 증명을 90일 동안 사용하지 않으면 자격 증명이 삭제됩니다.

구성 JSON 파일에는 기술 계정 이름, 기술 계정 ID 및 자격 증명과 같은 정보가 포함되어 있습니다. 다음 형식으로 제공됩니다.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

생성된 자격 증명을 저장한 후 을(를) 선택합니다 **[!UICONTROL 닫기]**. 이제 만료되지 않는 모든 자격 증명 목록을 볼 수 있습니다.

![만료되지 않는 자격 증명 섹션이 강조 표시된 쿼리 대시보드 자격 증명 탭](../images/ui/credentials/list-credentials.png)

만료되지 않는 자격 증명을 편집하거나 삭제할 수 있습니다. 만료되지 않는 자격 증명을 편집하려면 연필 아이콘(![연필 아이콘.](../images/ui/credentials/edit-icon.png) 참조). 만료되지 않는 자격 증명을 삭제하려면 삭제 아이콘(![휴지통 아이콘](../images/ui/credentials/delete-icon.png)).

만료되지 않는 자격 증명을 편집할 때 모달이 표시됩니다. 업데이트할 다음 세부 정보를 제공할 수 있습니다.

- **[!UICONTROL 이름]**: 생성 중인 자격 증명의 이름입니다.
- **[!UICONTROL 설명]**: (선택 사항) 생성 중인 자격 증명에 대한 설명입니다.
- **[!UICONTROL 할당 대상:]**: 자격 증명을 할당할 사용자입니다. 이 값은 자격 증명을 만드는 사용자의 이메일 주소여야 합니다.

![계정 업데이트 대화 상자](../images/ui/credentials/update-credentials.png)

필요한 세부 정보를 모두 제공했으면 을 선택합니다. **[!UICONTROL 계정 업데이트]** 자격 증명 업데이트를 완료합니다.

## 자격 증명을 사용하여 외부 클라이언트에 연결 {#use-credential-to-connect}

만료 전 또는 만료되지 않는 자격 증명을 사용하여 Aqua Data Studio, Looker 또는 Power BI 같은 외부 클라이언트와 연결할 수 있습니다. 이러한 자격 증명에 대한 입력 방법은 외부 클라이언트에 따라 달라집니다. 이러한 자격 증명 사용에 대한 특정 지침은 외부 클라이언트의 설명서를 참조하십시오.

이 이미지는 만료되지 않는 자격 증명의 암호를 제외하고 UI에서 발견된 각 매개 변수의 위치를 나타냅니다. 만료되지 않는 자격 증명은 JSON 구성 파일에서 제공되지만, 아래에서 만료되는 자격 증명을 볼 수 있습니다. **자격 증명** UI의 탭입니다.

![만료되는 자격 증명 섹션이 강조 표시된 쿼리 작업 영역 자격 증명 탭입니다.](../images/ui/credentials/expiring-credentials.png)

아래 표에는 일반적으로 외부 클라이언트에 연결하는 데 필요한 매개 변수가 나와 있습니다.

>[!NOTE]
>
>만료되지 않는 자격 증명을 사용하여 호스트에 연결할 때에도 목록에 있는 모든 매개 변수를 사용해야 합니다 [!UICONTROL 자격 증명 만료] 암호와 사용자 이름을 제외한 섹션입니다.
>사용자 이름과 암호를 입력하는 형식은 이 예제와 같이 콜론으로 구분된 값을 사용합니다 `username:{your_username}` 및 `password:{password_string}`.

| 매개변수 | 설명 | 예 |
|---|---|---|
| **서버/호스트** | 접속 중인 서버/호스트의 이름입니다. <ul><li>이 값은 만료 중인 자격 증명과 만료되지 않는 자격 증명 모두에 사용되며 다음 형식을 사용합니다. `server.adobe.io`. 값은 다음에서 찾을 수 있습니다. **[!UICONTROL 호스트]** 다음에서 [!UICONTROL 자격 증명 만료] 섹션.</ul></li> | `acme.platform.adobe.io` |
| **포트** | 연결 중인 서버/호스트의 포트입니다. <ul><li>이 값은 만료 중인 자격 증명과 만료되지 않는 자격 증명 모두에 사용되며 아래에 있습니다. **[!UICONTROL 포트]** 다음에서 [!UICONTROL 자격 증명 만료] 섹션.</ul></li> | `80` |
| **데이터베이스** | 연결 중인 데이터베이스입니다. <ul><li>이 값은 만료 중인 자격 증명과 만료되지 않는 자격 증명 모두에 사용되며 아래에 있습니다. **[!UICONTROL 데이터베이스]** 다음에서 [!UICONTROL 자격 증명 만료] 섹션. </ul></li> | `prod:all` |
| **사용자 이름** | 외부 클라이언트에 연결하는 사용자의 사용자 이름입니다. <ul><li>이 값은 만료되는 자격 증명과 만료되지 않는 자격 증명 모두에 사용됩니다. 다음 앞에 영숫자 문자열 형식을 사용합니다. `@AdobeOrg`. 이 값은 다음에서 찾을 수 있습니다 **[!UICONTROL 사용자 이름]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **암호** | 외부 클라이언트에 연결하는 사용자의 암호입니다. <ul><li>만료되는 자격 증명을 사용하는 경우 다음에서 찾을 수 있습니다. **[!UICONTROL 암호]** 다음 범위 내 [!UICONTROL 자격 증명 만료] 섹션.</li><li>만료되지 않는 자격 증명을 사용하는 경우 이 값은 technicalAccountID의 연결된 인수와 구성 JSON 파일에서 가져온 자격 증명입니다. 암호 값은 다음 형식을 사용합니다. `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>만료될 자격 증명 암호는 1,000자 이상의 영숫자 문자열입니다. 예시는 제공되지 않을 것입니다.</li><li>만료되지 않는 자격 증명 암호는 다음과 같습니다.<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 다음 단계

만료될 때까지 및 만료되지 않는 자격 증명이 모두 작동하는 방식을 이해했으므로 이러한 자격 증명을 사용하여 외부 클라이언트에 연결할 수 있습니다. 외부 클라이언트에 대한 자세한 내용은 [클라이언트를 Query Service에 연결 안내서](../clients/overview.md).
