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

이 문서에서는 UI를 사용하여 플랫폼에서 CMK(고객 관리 키) 기능을 활성화하는 프로세스에 대해 설명합니다. API를 사용하여 이 프로세스를 완료하는 방법에 대한 지침은 [API CMK 설정 문서](./api-set-up.md)를 참조하십시오.

## 전제 조건

Adobe Experience Platform에서 [!UICONTROL 암호화] 섹션을 보고 방문하려면 역할을 만들고 해당 역할에 [!UICONTROL 고객 관리 키 관리] 권한을 할당해야 합니다. [!UICONTROL 고객 관리 키 관리] 권한이 있는 모든 사용자는 해당 조직에 대해 CMK를 사용할 수 있습니다.

Experience Platform에서 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [권한 구성 설명서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)를 참조하세요.

CMK를 사용하려면 다음 설정으로 [[!DNL Azure] Key Vault를 구성](./azure-key-vault-config.md)해야 합니다.

* [제거 보호 사용](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [일시 삭제 사용](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [역할 기반 액세스 제어를 사용하여 액세스 구성 [!DNL Azure] 2}](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [ [!DNL Azure] Key Vault 구성](./azure-key-vault-config.md)

## CMK 앱 설정 {#register-app}

키 저장소를 구성한 후 다음 단계는 [!DNL Azure] 테넌트에 연결할 CMK 응용 프로그램을 등록하는 것입니다.

### 시작하기

[!UICONTROL 암호화 구성] 대시보드를 보려면 왼쪽 탐색 사이드바의 [!UICONTROL 관리] 제목 아래에서 **[!UICONTROL 암호화]**&#x200B;를 선택하십시오.

![암호화 및 고객 관리 키 카드가 강조 표시된 암호화 구성 대시보드입니다.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

**[!UICONTROL 구성]**&#x200B;을 선택하여 [!UICONTROL 고객 관리 키 구성] 보기를 엽니다. 이 작업 공간에는 아래 설명된 단계를 완료하고 Azure 키 자격 증명 모음과의 통합을 수행하는 데 필요한 모든 값이 포함되어 있습니다.

### 인증 URL 복사 {#copy-authentication-url}

등록 프로세스를 시작하려면 [!UICONTROL 고객 관리 키 구성] 보기에서 조직의 응용 프로그램 인증 URL을 복사하여 [!DNL Azure] 환경 **[!DNL Key Vault Crypto Service Encryption User]**&#x200B;에 붙여 넣으십시오. [역할을 할당](#assign-to-role)하는 방법에 대한 자세한 내용은 다음 섹션에 나와 있습니다.

복사 아이콘(![복사 아이콘)을 선택합니다.[!UICONTROL 응용 프로그램 인증 url]의 ](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png)).

![응용 프로그램 인증 url 섹션이 강조 표시된 [!UICONTROL 고객 관리 키 구성] 보기.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

[!UICONTROL 응용 프로그램 인증 url]을(를) 복사하여 브라우저에 붙여 넣어 인증 대화 상자를 엽니다. [!DNL Azure] 테넌트에 CMK 앱 서비스 주체를 추가하려면 **[!DNL Accept]**&#x200B;을(를) 선택하십시오. 인증을 확인하면 Experience Cloud 랜딩 페이지로 리디렉션됩니다.

![강조 표시된 [!UICONTROL Accept]의 Microsoft 권한 요청 대화 상자.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>[!DNL Microsoft Azure]개의 구독이 여러 개 있는 경우 Platform 인스턴스를 잘못된 키 자격 증명 모음에 연결할 수 있습니다. 이 경우 응용 프로그램 인증 URL 이름의 `common` 섹션을 CMK 디렉터리 ID로 바꿔야 합니다.<br>[!DNL Microsoft Azure] 응용 프로그램의 Portal 설정, 디렉터리 및 구독 페이지에서 CMK 디렉터리 ID를 복사합니다.<br>![디렉터리 ID가 강조 표시된 [!DNL Microsoft Azure] 응용 프로그램 Portal 설정, 디렉터리 및 구독 페이지입니다.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>다음 브라우저 주소 표시줄에 붙여 넣습니다.<br>![응용 프로그램 인증 URL의 &#39;공통&#39; 섹션이 강조 표시된 Google 브라우저 페이지입니다.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### CMK 앱을 역할에 지정 {#assign-to-role}

인증 프로세스를 완료한 후 [!DNL Azure] Key Vault로 다시 이동하고 왼쪽 탐색에서 **[!DNL Access control]**&#x200B;을(를) 선택합니다. 여기에서 **[!DNL Add]**, **[!DNL Add role assignment]**&#x200B;을(를) 차례로 선택합니다.

![[!DNL Add] 및 [!DNL Add role assignment]이(가) 강조 표시된 [!DNL Microsoft Azure] 대시보드입니다.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

다음 화면에서는 이 할당에 대한 역할을 선택하라는 메시지가 표시됩니다. 계속하려면 **[!DNL Next]**&#x200B;을(를) 선택하기 전에 **[!DNL Key Vault Crypto Service Encryption User]**&#x200B;을(를) 선택하십시오.

>[!NOTE]
>
>[!DNL Managed-HSM Key Vault] 계층이 있는 경우 **[!DNL Managed HSM Crypto Service Encryption User]** 사용자 역할을 선택해야 합니다.

![강조 표시된 [!DNL Key Vault Crypto Service Encryption User]의 [!DNL Microsoft Azure] 대시보드입니다.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

다음 화면에서 **[!DNL Select members]**&#x200B;을(를) 선택하여 오른쪽 레일에서 대화 상자를 엽니다. 검색 창을 사용하여 CMK 응용 프로그램에 대한 서비스 주체를 찾아 목록에서 선택합니다. 완료되면 **[!DNL Save]**&#x200B;을(를) 선택합니다.

>[!NOTE]
>
>목록에서 애플리케이션을 찾을 수 없는 경우 서비스 주체가 테넌트에 승인되지 않았습니다. 올바른 권한이 있는지 확인하려면 [!DNL Azure] 관리자 또는 담당자에게 문의하세요.

[!UICONTROL 고객 관리 키 구성] 보기에 제공된 [!UICONTROL 응용 프로그램 ID]와 [!DNL Microsoft Azure] 응용 프로그램 개요에 제공된 [!DNL Application ID]을(를) 비교하여 응용 프로그램을 확인할 수 있습니다.

![응용 프로그램 ID [!UICONTROL 이(가) 강조 표시된 [!UICONTROL 고객 관리 키 구성] 보기.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)]

Azure 도구를 확인하는 데 필요한 모든 세부 정보가 Platform UI에 포함됩니다. 이 수준의 세부 기간은 다른 Azure 도구를 사용하여 이러한 응용 프로그램의 주요 자격 증명 모음에 대한 액세스를 모니터링하고 기록하는 기능을 향상시키려는 사용자의 요구에 따라 제공됩니다. 이러한 식별자를 이해하는 것은 해당 목적 및 Adobe 서비스가 키에 액세스할 수 있도록 하는 데 매우 중요합니다.

## Experience Platform 시 암호화 키 구성 활성화 {#send-to-adobe}

[!DNL Azure]에 CMK 앱을 설치한 후 암호화 키 식별자를 Adobe에 보낼 수 있습니다. 왼쪽 탐색에서 **[!DNL Keys]**&#x200B;을(를) 선택한 다음 보낼 키의 이름을 선택합니다.

![[!DNL Keys] 개체와 키 이름이 강조 표시된 Microsoft Azure 대시보드.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

최신 버전의 키를 선택하면 해당 세부 정보 페이지가 나타납니다. 여기에서 키에 대해 허용되는 작업을 선택적으로 구성할 수 있습니다.

>[!IMPORTANT]
>
>키에 대해 허용되는 최소 필수 작업은 **[!DNL Wrap Key]** 및 **[!DNL Unwrap Key]** 권한입니다. 원하는 대로 [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] 및 [!DNL Verify]을(를) 포함할 수 있습니다.

**[!UICONTROL 키 식별자]** 필드에 키의 URI 식별자가 표시됩니다. 다음 단계에서 사용할 이 URI 값을 복사합니다.

![[!DNL Permitted operations] 및 복사 키 URL 섹션이 강조 표시된 Microsoft Azure 대시보드 키 세부 정보](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

[!DNL Key vault URI]을(를) 얻었으면 [!UICONTROL 고객 관리 키 구성] 보기로 돌아가서 설명하는 **[!UICONTROL 구성 이름]**&#x200B;을(를) 입력하십시오. 그런 다음 Azure 키 세부 정보 페이지에서 가져온 [!DNL Key Identifier]을(를) **[!UICONTROL Key 자격 증명 모음 키 식별자]**&#x200B;에 추가하고 **[!UICONTROL 저장]**&#x200B;을(를) 선택합니다.

![[!UICONTROL 구성 이름] 및 [!UICONTROL Key Vault 키 식별자] 섹션이 강조 표시된 [!UICONTROL 고객 관리 키 구성] 보기.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

[!UICONTROL 암호화 구성 대시보드]로 돌아갔습니다. [!UICONTROL 고객 관리 키] 구성의 상태가 [!UICONTROL 처리 중]으로 표시됩니다.

![암호화 구성] 대시보드([!UICONTROL 처리 중])가 [!UICONTROL 고객 관리 키] 카드에 강조 표시되어 있습니다.](../../images/governance-privacy-security/customer-managed-keys/processing.png)[!UICONTROL 

## 구성 상태 확인 {#check-status}

처리에 상당한 시간이 걸릴 수 있습니다. 구성 상태를 확인하려면 [!UICONTROL 고객 관리 키 구성] 보기로 돌아가서 [!UICONTROL 구성 상태](으)로 스크롤합니다. 진행률 표시줄은 세 단계 중 한 단계로 진행되었으며 시스템에서 Platform이 키 및 키 저장소에 액세스할 수 있는지 확인하고 있다고 설명합니다.

CMK 구성에는 네 가지 잠재적인 상태가 있습니다. 이는 다음과 같습니다.

* 1단계: Platform에 키 및 키 저장소에 액세스할 수 있는 권한이 있는지 확인합니다.
* 2단계: 키 저장소와 키 이름을 조직의 모든 데이터 저장소에 추가하는 중입니다.
* 3단계: 키 저장소 및 키 이름이 데이터 저장소에 성공적으로 추가되었습니다.
* `FAILED`: 주로 키, 키 자격 증명 모음 또는 다중 테넌트 앱 설정과 관련된 문제가 발생했습니다.

## 다음 단계

위의 단계를 완료하면 조직에 대해 CMK를 성공적으로 사용할 수 있게 됩니다. 기본 데이터 저장소에 수집된 데이터는 이제 [!DNL Azure] 키 저장소의 키를 사용하여 암호화 및 암호 해독됩니다.
