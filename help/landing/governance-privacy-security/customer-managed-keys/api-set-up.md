---
title: API를 사용하여 고객 관리 키 설정 및 구성
description: Azure 테넌트로 CMK 앱을 설정하고 암호화 키 ID를 Adobe Experience Platform으로 보내는 방법에 대해 알아봅니다.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# API를 사용하여 고객 관리 키 설정 및 구성

이 문서에서는 API를 사용하여 Adobe Experience Platform에서 CMK(고객 관리 키) 기능을 활성화하는 프로세스에 대해 설명합니다. UI를 사용하여 이 프로세스를 완료하는 방법에 대한 지침은 [UI CMK 설정 문서](./ui-set-up.md).

## 전제 조건

을(를) 보고 방문하려면 [!UICONTROL 암호화] Adobe Experience Platform의 섹션에서 역할을 만들고 [!UICONTROL 고객 관리 키 관리] 해당 역할에 대한 권한. 을(를) 가진 모든 사용자 [!UICONTROL 고객 관리 키 관리] 권한은 해당 조직에 대해 CMK를 활성화할 수 있습니다.

Experience Platform에서 역할 및 권한 할당에 대한 자세한 내용은 [권한 구성 설명서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

CMK를 활성화하려면 [[!DNL Azure] 키 저장소를 구성해야 합니다.](./azure-key-vault-config.md) 다음 설정으로:

* [제거 보호 활성화](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [일시 삭제 활성화](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [다음을 사용하여 액세스 구성 [!DNL Azure] 역할 기반 액세스 제어](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [구성 [!DNL Azure] 주요 자격 증명 모음](./azure-key-vault-config.md)

## CMK 앱 설정 {#register-app}

Key Vault를 구성한 후 다음 단계는 다음에 연결할 CMK 애플리케이션에 등록하는 것입니다. [!DNL Azure] 테넌트.

### 시작하기

CMK 앱을 등록하려면 Platform API를 호출해야 합니다. 이러한 호출을 수행하는 데 필요한 인증 헤더를 수집하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [Platform API 인증 안내서](../../api-authentication.md).

반면에 인증 안내서에서는 필요한 항목에 대해 고유한 값을 생성하는 방법에 대한 지침을 제공합니다 `x-api-key` 요청 헤더, 이 안내서의 모든 API 작업은 정적 값을 사용합니다. `acp_provisioning` 대신, 에 대한 고유한 값을 제공해야 합니다. `{ACCESS_TOKEN}` 및 `{ORG_ID}`, 그러나 .

이 안내서에 표시된 모든 API 호출에서 `platform.adobe.io` 는 루트 경로로 사용되며 기본값은 VA7 영역입니다. 조직에서 다른 지역을 사용하는 경우 `platform` 뒤에 대시 및 조직에 지정된 지역 코드가 있어야 합니다. `nld2` NLD2 또는 `aus5` AUS5의 경우(예: `platform-aus5.adobe.io`). 조직의 지역을 모르는 경우 시스템 관리자에게 문의하십시오.

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

성공적인 응답은 다음을 반환합니다. `applicationRedirectUrl` 속성, 인증 URL 포함.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

복사 및 붙여넣기 `applicationRedirectUrl` 를 브라우저에 입력하여 인증 대화 상자를 엽니다. 선택 **[!DNL Accept]** cmk 앱 서비스 주체를 [!DNL Azure] 테넌트.

![이 포함된 Microsoft 권한 요청 대화 상자 [!UICONTROL Accept] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### CMK 앱을 역할에 지정 {#assign-to-role}

인증 프로세스를 완료한 후 다음으로 돌아가기 [!DNL Azure] 키 저장소 및 선택 **[!DNL Access control]** 왼쪽 탐색. 여기에서 다음을 선택합니다. **[!DNL Add]** 뒤에 오는 **[!DNL Add role assignment]**.

![을 사용하는 Microsoft Azure 대시보드 [!DNL Add] 및 [!DNL Add role assignment] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

다음 화면에서는 이 할당에 대한 역할을 선택하라는 메시지가 표시됩니다. 선택 **[!DNL Key Vault Crypto Service Encryption User]** 선택하기 전 **[!DNL Next]** 계속합니다.

![다음을 포함하는 Microsoft Azure 대시보드 [!DNL Key Vault Crypto Service Encryption User] 강조 표시됨.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

다음 화면에서 다음을 선택합니다. **[!DNL Select members]** 오른쪽 레일에서 대화 상자를 엽니다. 검색 창을 사용하여 CMK 응용 프로그램에 대한 서비스 주체를 찾아 목록에서 선택합니다. 완료되면 다음을 선택합니다. **[!DNL Save]**.

>[!NOTE]
>
>목록에서 애플리케이션을 찾을 수 없는 경우 서비스 주체가 테넌트에 승인되지 않았습니다. 올바른 권한을 보유하는지 확인하려면 [!DNL Azure] 관리자 또는 담당자.

## Experience Platform 시 암호화 키 구성 활성화 {#send-to-adobe}

에 CMK 앱을 설치한 후 [!DNL Azure], 암호화 키 식별자를 Adobe에 보낼 수 있습니다. 선택 **[!DNL Keys]** 왼쪽 탐색에서 을 클릭하고 전송할 키의 이름을 입력합니다.

![다음을 포함하는 Microsoft Azure 대시보드 [!DNL Keys] 개체와 강조 표시된 키 이름입니다.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

최신 버전의 키를 선택하면 해당 세부 정보 페이지가 나타납니다. 여기에서 키에 대해 허용되는 작업을 선택적으로 구성할 수 있습니다.

>[!IMPORTANT]
>
>키에 허용되는 최소 필수 작업은 다음과 같습니다. **[!DNL Wrap Key]** 및 **[!DNL Unwrap Key]** 사용 권한. 다음을 포함할 수 있습니다. [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], 및 [!DNL Verify] 원하는 경우

다음 **[!UICONTROL 키 식별자]** 필드에는 키의 URI 식별자가 표시됩니다. 다음 단계에서 사용할 이 URI 값을 복사합니다.

![Microsoft Azure 대시보드 키 세부 정보 및 [!DNL Permitted operations] 및 복사 키 URL 섹션이 강조 표시됩니다.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

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
| `name` | 구성의 이름입니다. 다음에서 구성 상태를 확인하는 데 필요하므로 이 값을 기억해야 합니다. [이후 단계](#check-status). 값은 대/소문자를 구분합니다. |
| `type` | 구성 유형. 을(를) (으)로 설정해야 합니다. `BYOK_CONFIG`. |
| `imsOrgId` | 자신의 조직 ID. 이 ID는 아래에 제공된 값과 동일한 값이어야 합니다. `x-gw-ims-org-id` 머리글입니다. |
| `configData` | 이 속성에는 구성에 대한 다음 세부 정보가 포함됩니다.<ul><li>`providerType`: 다음으로 설정되어야 합니다. `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: 복사한 주요 자격 증명 모음 URI [이전](#send-to-adobe).</li></ul> |

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

다음을 추가해야 합니다. `name` 경로( )에 체크 인하려는 구성`config1` 아래 예에서) 및에 `configType` 쿼리 매개 변수가 로 설정됨 `BYOK_CONFIG`.

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

다음 `status` 속성은 다음 의미를 갖는 네 개의 값 중 하나를 가질 수 있습니다.

1. `RUNNING`: 플랫폼이 키 및 키 저장소에 액세스할 수 있는지 확인합니다.
1. `UPDATE_EXISTING_RESOURCES`: 시스템에서 조직의 모든 샌드박스에 있는 데이터 저장소에 키 저장소 및 키 이름을 추가하고 있습니다.
1. `COMPLETED`: 키 저장소 및 키 이름이 데이터 저장소에 성공적으로 추가되었습니다.
1. `FAILED`: 주로 키, 키 보관소 또는 다중 테넌트 앱 설정과 관련된 문제가 발생했습니다.

## 다음 단계

위의 단계를 완료하면 조직에 대해 CMK를 성공적으로 사용할 수 있게 됩니다. 기본 데이터 저장소에 수집된 데이터는 이제 의 키를 사용하여 암호화 및 암호 해독 됩니다. [!DNL Azure] 키 보관소. Adobe Experience Platform의 데이터 암호화에 대한 자세한 내용은 [암호화 설명서](../encryption.md).
