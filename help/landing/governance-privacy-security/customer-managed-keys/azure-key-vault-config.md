---
title: Azure Key Vault 구성
description: Azure를 사용하여 새 엔터프라이즈 계정을 만들거나 기존 엔터프라이즈 계정을 사용하여 Key Vault를 만드는 방법을 알아봅니다.
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# 구성 [!DNL Azure] 주요 자격 증명 모음

CMK(고객 관리 키)는 [!DNL Microsoft Azure] 키 보관소. 시작하려면 다음을 사용하여 작업해야 합니다. [!DNL Azure] 새 enterprise 계정을 만들거나 기존 enterprise 계정을 사용하고 아래 단계에 따라 Key Vault를 만듭니다.

>[!IMPORTANT]
>
>에 대한 Premium 및 표준 서비스 계층만 [!DNL Azure] Key Vault가 지원됩니다. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] 및 [!DNL Azure Payments HSM] 은(는) 지원되지 않습니다. 다음을 참조하십시오. [[!DNL Azure] 설명서](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) 제공되는 주요 관리 서비스에 대한 자세한 정보.

>[!NOTE]
>
>아래 설명서에서는 Key Vault를 만드는 기본 단계만 다룹니다. 이 지침 외에 조직의 정책에 따라 Key Vault를 구성해야 합니다.

에 로그인합니다 [!DNL Azure] 포털 및 검색 창에서 찾기 **[!DNL Key vaults]** 서비스 목록 아래에.

![의 검색 기능 [!DNL Microsoft Azure] 포함 [!DNL Key vaults] 검색 결과에서 강조 표시됩니다.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

다음 **[!DNL Key vaults]** 서비스를 선택하면 페이지가 나타납니다. 여기에서 다음을 선택합니다. **[!DNL Create]**.

![다음 [!DNL Key vaults] 의 대시보드 [!DNL Microsoft Azure] 포함 [!DNL Create] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

제공된 양식을 사용하여 이름 및 할당된 리소스 그룹을 포함하여 Key Vault에 대한 기본 세부 정보를 입력합니다.

>[!WARNING]
>
>대부분의 옵션은 기본값으로 둘 수 있지만 **일시 삭제 및 제거 보호 옵션을 활성화했는지 확인합니다.**. 이러한 기능을 켜지 않으면 Key Vault가 삭제될 경우 데이터에 대한 액세스 권한이 손실될 수 있습니다.
>
>![다음 [!DNL Microsoft Azure] [!DNL Create a Key Vault] 소프트 삭제 및 제거 보호 기능이 강조 표시된 워크플로우입니다.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

여기에서 Key Vault 생성 워크플로우를 계속 진행하고 조직의 정책에 따라 다양한 옵션을 구성합니다.

다음에 도착하면 **[!DNL Review + create]** 단계에서는 유효성 검사를 진행하는 동안 Key Vault의 세부 사항을 검토할 수 있습니다. 유효성 검사가 성공하면 다음을 선택합니다. **[!DNL Create]** 을 클릭하여 프로세스를 완료합니다.

![[만들기]가 강조 표시된 Microsoft Azure 키 저장소 검토 및 만들기 페이지입니다.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## 네트워킹 옵션 구성 {#configure-network-options}

Key Vault가 특정 가상 네트워크에 대한 공개 액세스를 제한하거나 공개 액세스를 완전히 비활성화하도록 구성된 경우 권한을 부여해야 합니다 [!DNL Microsoft] 방화벽 예외입니다.

선택 **[!DNL Networking]** 왼쪽 탐색. 아래 **[!DNL Firewalls and virtual networks]**, 확인란을 선택합니다. **[!DNL Allow trusted Microsoft services to bypass this firewall]**&#x200B;을 선택한 다음 을 선택합니다. **[!DNL Apply]**.

![다음 [!DNL Networking] 탭 / [!DNL Microsoft Azure] 포함 [!DNL Networking] 및 [!DNL Allow trusted Microsoft surfaces to bypass this firewall] 강조 표시된 예외.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### 키 생성 {#generate-a-key}

Key Vault를 만든 후에는 새 키를 생성할 수 있습니다. 다음 위치로 이동 **[!DNL Keys]** 탭하고 선택 **[!DNL Generate/Import]**.

![다음 [!DNL Keys] 탭 / [!DNL Azure] 포함 [!DNL Generate import] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

제공된 양식을 사용하여 키의 이름을 입력한 다음 을 선택합니다 **RSA** 키 유형. 최소한, **[!DNL RSA key size]** 은(는) 이상이어야 합니다. **3072** 다음에 필요한 비트 수 [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] 는 RSA 3027과도 호환됩니다.

>[!NOTE]
>
>키를 Adobe에 보내는 데 필요하므로 키에 제공한 이름을 기억하십시오.

나머지 컨트롤을 사용하여 생성하거나 가져올 키를 원하는 대로 구성합니다. 완료되면 다음을 선택합니다. **[!DNL Create]**.

![을 사용하여 키 대시보드 만들기 [!DNL 3072] 강조 표시된 비트입니다.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

구성된 키가 자격 증명 모음의 키 목록에 나타납니다.

![다음 [!DNL Keys] 키 이름이 강조 표시된 작업 공간.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 다음 단계

고객 관리 키 기능을 설정하는 1회 프로세스를 계속하려면 다음 중 하나를 사용하여 계속합니다. [API](./api-set-up.md) 또는 [UI](./ui-set-up.md) 고객 관리 키 설정 안내서입니다.
