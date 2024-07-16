---
title: API를 사용하여 고객 관리 키 설정 및 구성
description: Azure 테넌트로 CMK 앱을 설정하고 암호화 키 ID를 Adobe Experience Platform으로 보내는 방법에 대해 알아봅니다.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# API를 사용하여 고객 관리 키 설정 및 구성

이 문서에서는 API를 사용하여 Adobe Experience Platform에서 CMK(고객 관리 키) 기능을 활성화하는 프로세스에 대해 설명합니다. UI를 사용하여 이 프로세스를 완료하는 방법에 대한 지침은 [UI CMK 설정 문서](./ui-set-up.md)를 참조하십시오.

## 전제 조건

Adobe Experience Platform에서 [!UICONTROL 암호화] 섹션을 보고 방문하려면 역할을 만들고 해당 역할에 [!UICONTROL 고객 관리 키 관리] 권한을 할당해야 합니다. [!UICONTROL 고객 관리 키 관리] 권한이 있는 모든 사용자는 해당 조직에 대해 CMK를 사용할 수 있습니다.

Experience Platform에서 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [권한 구성 설명서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)를 참조하세요.

CMK를 사용하려면 다음 설정으로 [[!DNL Azure] Key Vault를 구성](./azure-key-vault-config.md)해야 합니다.

* [제거 보호 사용](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [일시 삭제 사용](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [역할 기반 액세스 제어를 사용하여 액세스 구성 [!DNL Azure] 2}](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [ [!DNL Azure] Key Vault 구성](./azure-key-vault-config.md)

## CMK 앱 설정 {#register-app}

키 저장소를 구성한 후 다음 단계는 [!DNL Azure] 테넌트에 연결할 CMK 응용 프로그램에 등록하는 것입니다.

### 시작하기

CMK 앱을 등록하려면 Platform API를 호출해야 합니다. 이러한 호출을 수행하는 데 필요한 인증 헤더를 수집하는 방법에 대한 자세한 내용은 [Platform API 인증 안내서](../../api-authentication.md)를 참조하십시오.

인증 가이드는 필요한 `x-api-key` 요청 헤더에 대한 고유한 값을 생성하는 방법에 대한 지침을 제공하지만 이 가이드의 모든 API 작업은 정적 값 `acp_provisioning`을(를) 대신 사용합니다. 그러나 `{ACCESS_TOKEN}` 및 `{ORG_ID}`에 대한 고유한 값을 제공해야 합니다.

이 안내서에 표시된 모든 API 호출에서 `platform.adobe.io`이(가) 루트 경로로 사용되며 기본값은 VA7 영역입니다. 조직에서 다른 지역을 사용하는 경우 `platform` 뒤에 대시가 있고 조직에 할당된 지역 코드가 있어야 합니다. NLD2의 경우 `nld2`, AUS5의 경우 `aus5`(예: `platform-aus5.adobe.io`). 조직의 지역을 모르는 경우 시스템 관리자에게 문의하십시오.

### 인증 URL 가져오기 {#fetch-authentication-url}

등록 프로세스를 시작하려면 앱 등록 끝점에 조직의 필수 인증 URL을 가져오도록 GET 요청을 만듭니다.

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답이 인증 URL이 포함된 `applicationRedirectUrl` 속성을 반환합니다.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

`applicationRedirectUrl` 주소를 복사하여 브라우저에 붙여 넣어 인증 대화 상자를 엽니다. [!DNL Azure] 테넌트에 CMK 앱 서비스 주체를 추가하려면 **[!DNL Accept]**&#x200B;을(를) 선택하십시오.

![강조 표시된 [!UICONTROL Accept]의 Microsoft 권한 요청 대화 상자.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### CMK 앱을 역할에 지정 {#assign-to-role}

인증 프로세스를 완료한 후 [!DNL Azure] Key Vault로 다시 이동하고 왼쪽 탐색에서 **[!DNL Access control]**&#x200B;을(를) 선택합니다. 여기에서 **[!DNL Add]**, **[!DNL Add role assignment]**&#x200B;을(를) 차례로 선택합니다.

![강조 표시된 [!DNL Add] 및 [!DNL Add role assignment]의 Microsoft Azure 대시보드.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

다음 화면에서는 이 할당에 대한 역할을 선택하라는 메시지가 표시됩니다. 계속하려면 **[!DNL Next]**&#x200B;을(를) 선택하기 전에 **[!DNL Key Vault Crypto Service Encryption User]**&#x200B;을(를) 선택하십시오.

>[!NOTE]
>
>[!DNL Managed-HSM Key Vault] 계층이 있는 경우 **[!DNL Managed HSM Crypto Service Encryption User]** 사용자 역할을 선택해야 합니다.

![강조 표시된 [!DNL Key Vault Crypto Service Encryption User]의 Microsoft Azure 대시보드.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

다음 화면에서 **[!DNL Select members]**&#x200B;을(를) 선택하여 오른쪽 레일에서 대화 상자를 엽니다. 검색 창을 사용하여 CMK 응용 프로그램에 대한 서비스 주체를 찾아 목록에서 선택합니다. 완료되면 **[!DNL Save]**&#x200B;을(를) 선택합니다.

>[!NOTE]
>
>목록에서 애플리케이션을 찾을 수 없는 경우 서비스 주체가 테넌트에 승인되지 않았습니다. 올바른 권한이 있는지 확인하려면 [!DNL Azure] 관리자 또는 담당자에게 문의하세요.

## Experience Platform 시 암호화 키 구성 활성화 {#send-to-adobe}

[!DNL Azure]에 CMK 앱을 설치한 후 암호화 키 식별자를 Adobe에 보낼 수 있습니다. 왼쪽 탐색에서 **[!DNL Keys]**&#x200B;을(를) 선택한 다음 보낼 키의 이름을 선택합니다.

![[!DNL Keys] 개체와 키 이름이 강조 표시된 Microsoft Azure 대시보드.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

최신 버전의 키를 선택하면 해당 세부 정보 페이지가 나타납니다. 여기에서 키에 대해 허용되는 작업을 선택적으로 구성할 수 있습니다.

>[!IMPORTANT]
>
>키에 대해 허용되는 최소 필수 작업은 **[!DNL Wrap Key]** 및 **[!DNL Unwrap Key]** 권한입니다. 원하는 대로 [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] 및 [!DNL Verify]을(를) 포함할 수 있습니다.

**[!UICONTROL 키 식별자]** 필드에 키의 URI 식별자가 표시됩니다. 다음 단계에서 사용할 이 URI 값을 복사합니다.

![[!DNL Permitted operations] 및 복사 키 URL 섹션이 강조 표시된 Microsoft Azure 대시보드 키 세부 정보](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Key Vault URI를 얻으면 CMK 구성 엔드포인트에 대한 POST 요청을 사용하여 URI를 전송할 수 있습니다.

>[!NOTE]
>
>키 저장소와 키 이름만 Adobe과 함께 저장되고 키 버전은 저장되지 않습니다.

**요청**

+++ CMK 구성 끝점에 주요 자격 증명 모음 URI를 전송하는 샘플 요청입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 구성의 이름입니다. [이후 단계](#check-status)에서 구성 상태를 확인하는 데 필요하므로 이 값을 기억해야 합니다. 값은 대/소문자를 구분합니다. |
| `type` | 구성 유형. `BYOK_CONFIG`(으)로 설정해야 합니다. |
| `imsOrgId` | 조직 ID입니다. 이 ID는 `x-gw-ims-org-id` 헤더에 제공된 값과 같아야 합니다. |
| `configData` | 이 속성에는 구성에 대한 다음 세부 정보가 포함됩니다.<ul><li>`providerType`: `AZURE_KEYVAULT`(으)로 설정해야 합니다.</li><li>`keyVaultKeyIdentifier`: [이전](#send-to-adobe)에 복사한 키 자격 증명 모음 URI입니다.</li></ul> |

+++

**응답**

+++ 성공한 응답은 구성 작업의 세부 정보를 반환합니다.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

작업은 몇 분 안에 처리를 완료해야 합니다.

## 구성 상태 확인 {#check-status}

구성 요청의 상태를 확인하려면 GET 요청을 수행하면 됩니다.

**요청**

확인할 구성의 `name`을(를) 경로(아래 예에서 `config1`)에 추가하고 `BYOK_CONFIG`(으)로 설정된 `configType` 쿼리 매개 변수를 포함해야 합니다.

+++ 구성 요청의 상태를 확인하는 샘플 요청입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**응답**

+++ 성공한 응답은 작업 상태를 반환합니다.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

`status` 특성은 다음 의미를 갖는 네 가지 값 중 하나를 가질 수 있습니다.

1. `RUNNING`: 플랫폼에서 키 및 키 자격 증명 모음에 액세스할 수 있는지 확인합니다.
1. `UPDATE_EXISTING_RESOURCES`: 시스템에서 조직의 모든 샌드박스에 있는 데이터 저장소에 키 저장소 및 키 이름을 추가하고 있습니다.
1. `COMPLETED`: 키 자격 증명 모음 및 키 이름이 데이터 저장소에 추가되었습니다.
1. `FAILED`: 주로 키, 키 자격 증명 모음 또는 다중 테넌트 앱 설정과 관련된 문제가 발생했습니다.

## 다음 단계

위의 단계를 완료하면 조직에 대해 CMK를 성공적으로 사용할 수 있게 됩니다. 기본 데이터 저장소에 수집된 데이터는 이제 [!DNL Azure] 키 저장소의 키를 사용하여 암호화 및 암호 해독됩니다. Adobe Experience Platform의 데이터 암호화에 대한 자세한 내용은 [암호화 설명서](../encryption.md)를 참조하세요.
