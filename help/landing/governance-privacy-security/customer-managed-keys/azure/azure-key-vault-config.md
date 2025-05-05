---
title: 고객 관리 키에 대한 Azure Key Vault 구성
description: Azure를 사용하여 새 엔터프라이즈 계정을 만들거나 기존 엔터프라이즈 계정을 사용하여 Key Vault를 만드는 방법을 알아봅니다.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: f4100506947da7584de5b9fb42946ac877c8c102
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---

# 고객 관리 키에 대한 [!DNL Azure] Key Vault 구성

[!DNL Microsoft Azure] 키 보관소와 AWS [!DNL Key Management Service (KMS)]의 CMK(Customer Managed Keys) 지원 키. 구현이 [!DNL Azure]에서 호스팅되는 경우 아래 단계에 따라 키 자격 증명 모음을 만드십시오. AWS 호스팅 구현의 경우 [AWS KMS 구성 안내서](../aws/configure-kms.md)를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Azure] Key Vault에 대한 Standard, Premium 및 Managed HSM 계층만 지원됩니다. [!DNL Azure Dedicated HSM] 및 [!DNL Azure Payments HSM]은(는) 지원되지 않습니다. 제공되는 키 관리 서비스에 대한 자세한 내용은 [[!DNL Azure] 설명서](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services)를 참조하세요.

>[!NOTE]
>
>아래 설명서에서는 Key Vault를 만드는 기본 단계만 다룹니다. 이 지침 외에 조직의 정책에 따라 Key Vault를 구성해야 합니다.

[!DNL Azure] 포털에 로그인하고 검색 창을 사용하여 서비스 목록에서 **[!DNL Key vaults]**&#x200B;을(를) 찾습니다.

![검색 결과에 [!DNL Key vaults]이(가) 강조 표시된 [!DNL Microsoft Azure]의 검색 기능.](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

서비스를 선택하면 **[!DNL Key vaults]** 페이지가 나타납니다. 여기에서 **[!DNL Create]**&#x200B;을(를) 선택합니다.

[!DNL Create]이(가) 강조 표시된 [!DNL Microsoft Azure]의 [!DNL Key vaults] 대시보드입니다.![&#128279;](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

제공된 양식을 사용하여 이름 및 할당된 리소스 그룹을 포함하여 Key Vault에 대한 기본 세부 정보를 입력합니다.

>[!WARNING]
>
>대부분의 옵션은 기본값으로 둘 수 있지만 **일시 삭제 및 제거 보호 옵션을 사용하도록 설정해야 합니다**. 이러한 기능을 켜지 않으면 Key Vault가 삭제될 경우 데이터에 대한 액세스 권한이 손실될 수 있습니다.
>
>![일시 삭제 및 제거 보호가 강조 표시된 [!DNL Microsoft Azure] [!DNL Create a Key Vault] 워크플로우입니다.](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

여기에서 Key Vault 생성 워크플로우를 계속 진행하고 조직의 정책에 따라 다양한 옵션을 구성합니다.

**[!DNL Review + create]** 단계에 도달하면 유효성 검사를 진행하는 동안 Key Vault의 세부 사항을 검토할 수 있습니다. 유효성 검사가 성공하면 **[!DNL Create]**&#x200B;을(를) 선택하여 프로세스를 완료합니다.

![Microsoft Azure 키 자격 증명 모음 검토 및 만들기 페이지의 [만들기]가 강조 표시되어 있습니다.](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## 액세스 구성 {#configure-access}

그런 다음 주요 자격 증명 모음에 대해 Azure 역할 기반 액세스 제어를 사용하도록 설정합니다. 왼쪽 탐색의 [!DNL Settings] 섹션에서 **[!DNL Access configuration]**&#x200B;을(를) 선택한 다음 **[!DNL Azure role-based access control]**&#x200B;을(를) 선택하여 설정을 사용하도록 설정합니다. CMK 앱은 나중에 Azure 역할과 연결해야 하므로 이 단계는 필수입니다. 역할 할당은 [API](./api-set-up.md#assign-to-role) 및 [UI](./ui-set-up.md#assign-to-role) 워크플로 모두에서 문서화되었습니다.

![[!DNL Access configuration] 및 [!DNL Azure role-based access control]이(가) 강조 표시된 [!DNL Microsoft Azure] 대시보드입니다.](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## 네트워킹 옵션 구성 {#configure-network-options}

특정 가상 네트워크에 대한 공개 액세스를 제한하거나 공개 액세스를 완전히 사용하지 않도록 Key Vault가 구성된 경우 [!DNL Microsoft]에 방화벽 예외를 부여해야 합니다.

왼쪽 탐색에서 **[!DNL Networking]**&#x200B;을(를) 선택합니다. **[!DNL Firewalls and virtual networks]**&#x200B;에서 **[!DNL Allow trusted Microsoft services to bypass this firewall]** 확인란을 선택한 다음 **[!DNL Apply]**&#x200B;을(를) 선택합니다.

![[!DNL Networking] 및 [!DNL Allow trusted Microsoft surfaces to bypass this firewall] 예외가 강조 표시된 [!DNL Microsoft Azure]의 [!DNL Networking] 탭입니다.](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### 키 생성 {#generate-a-key}

Key Vault를 만든 후에는 새 키를 생성할 수 있습니다. **[!DNL Keys]** 탭으로 이동하여 **[!DNL Generate/Import]**&#x200B;을(를) 선택합니다.

![강조 표시된 [!DNL Generate import]이(가) 있는 [!DNL Azure]의 [!DNL Keys] 탭.](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

제공된 양식을 사용하여 키의 이름을 입력하고 키 유형으로 **RSA** 또는 **RSA-HSM**&#x200B;을(를) 선택하십시오. [!DNL Azure] 호스팅 구현의 경우 **[!DNL RSA key size]**&#x200B;은(는) [!DNL Azure Cosmos DB]에 필요한 최소 **3072**&#x200B;비트여야 합니다. [!DNL Azure Data Lake Storage]은(는) RSA 3027과도 호환됩니다.

>[!NOTE]
>
>키를 Adobe에 보내는 데 필요하므로 키에 제공한 이름을 기억하십시오.

나머지 컨트롤을 사용하여 생성하거나 가져올 키를 원하는 대로 구성합니다. 완료되면 **[!DNL Create]**&#x200B;을(를) 선택합니다.

![[!DNL 3072]비트가 강조 표시된 [!DNL Create a key] 대시보드입니다.](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

구성된 키가 자격 증명 모음의 키 목록에 나타납니다.

![키 이름이 강조 표시된 [!DNL Keys] 작업 영역입니다.](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 다음 단계

고객 관리 키 기능 설정을 위한 1회 프로세스를 계속하려면 플랫폼의 호스팅 환경에 대한 설정 안내서를 따르십시오.

- [!DNL Azure]의 경우 [API](./api-set-up.md) 또는 [UI](./ui-set-up.md) 설치 가이드를 사용하십시오.
- AWS의 경우 [AWS KMS 구성 가이드](../aws/configure-kms.md) 및 [UI 설치 가이드](../aws/ui-set-up.md)를 참조하십시오.
