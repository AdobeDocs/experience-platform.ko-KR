---
title: Platform UI를 사용하여 고객 관리 키 설정 및 구성
description: Azure 테넌트로 CMK 앱을 설정하고 암호화 키 ID를 Adobe Experience Platform으로 보내는 방법에 대해 알아봅니다.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# Platform UI를 사용하여 고객 관리 키 설정 및 구성

이 문서에서는 UI를 사용하여 플랫폼에서 CMK(고객 관리 키) 기능을 활성화하는 프로세스에 대해 설명합니다. API를 사용하여 이 프로세스를 완료하는 방법에 대한 지침은 [API CMK 설정 문서](./api-set-up.md).

## 전제 조건

을(를) 보고 방문하려면 [!UICONTROL 암호화] Adobe Experience Platform의 섹션에서 역할을 만들고 [!UICONTROL 고객 관리 키 관리] 해당 역할에 대한 권한. 을(를) 가진 모든 사용자 [!UICONTROL 고객 관리 키 관리] 권한은 해당 조직에 대해 CMK를 활성화할 수 있습니다.

Experience Platform에서 역할 및 권한 할당에 대한 자세한 내용은 [권한 구성 설명서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

CMK를 활성화하려면 [[!DNL Azure] 키 저장소를 구성해야 합니다.](./azure-key-vault-config.md) 다음 설정으로:

* [제거 보호 활성화](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [일시 삭제 활성화](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [다음을 사용하여 액세스 구성 [!DNL Azure] 역할 기반 액세스 제어](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [구성 [!DNL Azure] 주요 자격 증명 모음](./azure-key-vault-config.md)

## CMK 앱 설정 {#register-app}

Key Vault를 구성한 후 다음 단계는 다음에 연결할 CMK 애플리케이션을 등록하는 것입니다. [!DNL Azure] 테넌트.

### 시작하기

을(를) 보려면 [!UICONTROL 암호화 구성] 대시보드, 선택 **[!UICONTROL 암호화]** 다음 아래에 [!UICONTROL 관리] 왼쪽 탐색 사이드바의 제목.

![암호화 및 고객 관리 키 카드가 강조 표시된 암호화 구성 대시보드.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

선택 **[!UICONTROL 구성]** 을(를) 열려면 [!UICONTROL 고객 관리 키 구성] 보기. 이 작업 공간에는 아래 설명된 단계를 완료하고 Azure 키 자격 증명 모음과의 통합을 수행하는 데 필요한 모든 값이 포함되어 있습니다.

### 인증 URL 복사 {#copy-authentication-url}

등록 프로세스를 시작하려면 다음에서 조직의 애플리케이션 인증 URL을 복사합니다. [!UICONTROL 고객 관리 키 구성] 보기 및 붙여넣기 [!DNL Azure] 환경 **[!DNL Key Vault Crypto Service Encryption User]**. 방법 세부 정보 [역할 할당](#assign-to-role) 다음 섹션에 제공됩니다.

복사 아이콘(![복사 아이콘](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png))에 의해 [!UICONTROL 애플리케이션 인증 URL].

![다음 [!UICONTROL 고객 관리 키 구성] 애플리케이션 인증 url 섹션이 강조 표시된 상태로 봅니다.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

복사 및 붙여넣기 [!UICONTROL 애플리케이션 인증 URL] 를 브라우저에 추가하여 인증 대화 상자를 엽니다. 선택 **[!DNL Accept]** cmk 앱 서비스 주체를 [!DNL Azure] 테넌트. 인증을 확인하면 Experience Cloud 랜딩 페이지로 리디렉션됩니다.

![이 포함된 Microsoft 권한 요청 대화 상자 [!UICONTROL Accept] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>여러 개 있는 경우 [!DNL Microsoft Azure] 가입을 선택하면 Platform 인스턴스를 잘못된 키 저장소에 연결할 수 있습니다. 이 경우 를 교환해야 합니다. `common` 섹션(CMK 디렉토리 ID에 대한 응용 프로그램 인증 URL 이름)<br>의 Portal 설정, 디렉토리 및 가입 페이지에서 CMK 디렉토리 ID를 복사합니다. [!DNL Microsoft Azure] 애플리케이션<br>![다음 [!DNL Microsoft Azure] [디렉토리 ID]가 강조 표시된 Application Portal 설정, 디렉토리 및 가입 페이지입니다.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>그런 다음 브라우저 주소 표시줄에 붙여 넣습니다.<br>![애플리케이션 인증 URL의 &#39;공통&#39; 섹션이 강조 표시된 Google 브라우저 페이지입니다.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### CMK 앱을 역할에 지정 {#assign-to-role}

인증 프로세스를 완료한 후 다음으로 돌아가기 [!DNL Azure] 키 저장소 및 선택 **[!DNL Access control]** 왼쪽 탐색. 여기에서 다음을 선택합니다. **[!DNL Add]** 뒤에 오는 **[!DNL Add role assignment]**.

![다음 [!DNL Microsoft Azure] 대시보드 [!DNL Add] 및 [!DNL Add role assignment] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

다음 화면에서는 이 할당에 대한 역할을 선택하라는 메시지가 표시됩니다. 선택 **[!DNL Key Vault Crypto Service Encryption User]** 선택하기 전 **[!DNL Next]** 계속합니다.

>[!NOTE]
>
>다음 항목이 있는 경우 [!DNL Managed-HSM Key Vault] 계층을 선택한 다음 **[!DNL Managed HSM Crypto Service Encryption User]** 사용자 역할.

![다음 [!DNL Microsoft Azure] 대시보드를 [!DNL Key Vault Crypto Service Encryption User] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

다음 화면에서 다음을 선택합니다. **[!DNL Select members]** 오른쪽 레일에서 대화 상자를 엽니다. 검색 창을 사용하여 CMK 응용 프로그램에 대한 서비스 주체를 찾아 목록에서 선택합니다. 완료되면 다음을 선택합니다. **[!DNL Save]**.

>[!NOTE]
>
>목록에서 애플리케이션을 찾을 수 없는 경우 서비스 주체가 테넌트에 승인되지 않았습니다. 올바른 권한을 보유하는지 확인하려면 [!DNL Azure] 관리자 또는 담당자.

다음을 비교하여 응용 프로그램을 확인할 수 있습니다. [!UICONTROL 애플리케이션 ID] 에 제공됩니다. [!UICONTROL 고객 관리 키 구성] 을 사용하여 보기 [!DNL Application ID] 에 제공됩니다. [!DNL Microsoft Azure] 애플리케이션 개요.

![다음 [!UICONTROL 고객 관리 키 구성] 을 사용하여 보기 [!UICONTROL 애플리케이션 ID] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Azure 도구를 확인하는 데 필요한 모든 세부 정보가 Platform UI에 포함됩니다. 이 수준의 세부 기간은 다른 Azure 도구를 사용하여 이러한 응용 프로그램의 주요 자격 증명 모음에 대한 액세스를 모니터링하고 기록하는 기능을 향상시키려는 사용자의 요구에 따라 제공됩니다. 이러한 식별자를 이해하는 것은 해당 목적 및 Adobe 서비스가 키에 액세스할 수 있도록 하는 데 매우 중요합니다.

## Experience Platform 시 암호화 키 구성 활성화 {#send-to-adobe}

에 CMK 앱을 설치한 후 [!DNL Azure], 암호화 키 식별자를 Adobe에 보낼 수 있습니다. 선택 **[!DNL Keys]** 왼쪽 탐색에서 을 클릭하고 전송할 키의 이름을 입력합니다.

![다음을 포함하는 Microsoft Azure 대시보드 [!DNL Keys] 개체와 강조 표시된 키 이름입니다.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

최신 버전의 키를 선택하면 해당 세부 정보 페이지가 나타납니다. 여기에서 키에 대해 허용되는 작업을 선택적으로 구성할 수 있습니다.

>[!IMPORTANT]
>
>키에 허용되는 최소 필수 작업은 다음과 같습니다. **[!DNL Wrap Key]** 및 **[!DNL Unwrap Key]** 사용 권한. 다음을 포함할 수 있습니다. [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], 및 [!DNL Verify] 원하는 경우

다음 **[!UICONTROL 키 식별자]** 필드에는 키의 URI 식별자가 표시됩니다. 다음 단계에서 사용할 이 URI 값을 복사합니다.

![Microsoft Azure 대시보드 키 세부 정보 및 [!DNL Permitted operations] 및 복사 키 URL 섹션이 강조 표시됩니다.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

를 얻으면 [!DNL Key vault URI]로 돌아갑니다. [!UICONTROL 고객 관리 키 구성] 설명 보기 및 입력 **[!UICONTROL 구성 이름]**. 그런 다음 를 추가합니다. [!DNL Key Identifier] azure 키 세부 정보 페이지에서 **[!UICONTROL 주요 자격 증명 모음 키 식별자]** 및 선택 **[!UICONTROL 저장]**.

![다음 [!UICONTROL 고객 관리 키 구성] 을 사용하여 보기 [!UICONTROL 구성 이름] 및 [!UICONTROL 주요 자격 증명 모음 키 식별자] 강조 표시된 섹션입니다.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

(으)로 돌아갑니다. [!UICONTROL 암호화 구성 대시보드]. 의 상태 [!UICONTROL 고객 관리 키] 구성이 다음으로 표시됨 [!UICONTROL 처리 중].

![다음 [!UICONTROL 암호화 구성] 대시보드 [!UICONTROL 처리 중] 강조 표시된 항목: [!UICONTROL 고객 관리 키] 카드.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## 구성 상태 확인 {#check-status}

처리에 상당한 시간이 걸릴 수 있습니다. 구성의 상태를 확인하려면 로 돌아갑니다. [!UICONTROL 고객 관리 키 구성] 을(를) 보고 아래로 스크롤하여 [!UICONTROL 구성 상태]. 진행률 표시줄은 세 단계 중 한 단계로 진행되었으며 시스템에서 Platform이 키 및 키 저장소에 액세스할 수 있는지 확인하고 있다고 설명합니다.

CMK 구성에는 네 가지 잠재적인 상태가 있습니다. 이는 다음과 같습니다.

* 1단계: Platform에 키 및 키 저장소에 액세스할 수 있는 권한이 있는지 확인합니다.
* 2단계: 키 저장소와 키 이름을 조직의 모든 데이터 저장소에 추가하는 중입니다.
* 3단계: 키 저장소 및 키 이름이 데이터 저장소에 성공적으로 추가되었습니다.
* `FAILED`: 주로 키, 키 보관소 또는 다중 테넌트 앱 설정과 관련된 문제가 발생했습니다.

## 다음 단계

위의 단계를 완료하면 조직에 대해 CMK를 성공적으로 사용할 수 있게 됩니다. 기본 데이터 저장소에 수집된 데이터는 이제 의 키를 사용하여 암호화 및 암호 해독 됩니다. [!DNL Azure] 키 보관소.
