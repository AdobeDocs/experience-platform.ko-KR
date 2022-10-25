---
title: Adobe Experience Platform의 고객 관리 키
description: Adobe Experience Platform에 저장된 데이터에 대해 고유한 암호화 키를 설정하는 방법을 알아봅니다.
source-git-commit: f06f00f7581ccd7fe64f5292a53ebb0303c65069
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Adobe Experience Platform의 고객 관리 키

Adobe Experience Platform에 저장된 모든 데이터는 시스템 수준 키를 사용하여 나머지 위치에서 암호화됩니다. 플랫폼 위에 구축된 응용 프로그램을 사용하는 경우 대신 고유한 암호화 키를 사용하도록 선택할 수 있으므로 데이터 보안을 더욱 강화할 수 있습니다.

이 문서에서는 Platform에서 고객 관리 키(CMK) 기능을 활성화하는 프로세스에 대해 설명합니다.

## 프로세스 요약

CMK는 Adobe의 Healthcare Shield 및 Privacy and Security Shield 오퍼링에 포함되어 있습니다. 조직에서 이러한 서비스 중 하나를 구입한 후 기능을 설정하는 1회 프로세스를 시작할 수 있습니다.

>[!WARNING]
>
>CMK를 설정한 후에는 시스템 관리 키로 되돌릴 수 없습니다. 키 및 키 저장소를 [!DNL Azure] 데이터 액세스 권한을 상실하지 않도록 합니다.

프로세스는 다음과 같습니다.

1. [만들기 [!DNL Microsoft Azure] 주요 저장소](#create-key-vault), 그런 다음 [암호화 키 생성](#generate-a-key) (조직의 정책에 따라) 최종적으로 Adobe과 공유될 수 있습니다.
1. 에 API 호출 사용 [CMK 앱 등록](#register-app) 사용 [!DNL Azure] 임차인.
1. [CMK 앱에 대한 서비스 주도자 할당](#assign-to-role) 키 저장소에 적절한 역할을 합니다.
1. 에 API 호출 사용 [암호화 키 ID를 Adobe에 보내기](#send-to-adobe).

설정 프로세스가 완료되면 모든 샌드박스에서 Platform으로 온보딩되는 모든 데이터는 [!DNL Azure] 키 설정, [[!DNL Cosmos DB]](https://docs.microsoft.com/en-us/azure/cosmos-db/) 및 [[!DNL Data Lake Storage]](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 리소스 를 참조하십시오. CMK는 다음을 활용합니다 [!DNL Azure]s [공개 미리 보기 프로그램](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/) 이를 가능하게 하기 위해

## 만들기 [!DNL Azure] 주요 저장소 {#create-key-vault}

CMK는 [!DNL Microsoft Azure] 키 저장소. 시작하려면 다음을 수행해야 합니다 [!DNL Azure] 새 엔터프라이즈 계정을 만들거나 기존 엔터프라이즈 계정을 사용하고 아래 단계에 따라 키 저장소를 만듭니다.

>[!IMPORTANT]
>
>에 대한 Premium 및 Standard 서비스 계층만 [!DNL Azure] 키 저장소가 지원됩니다. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] 및 [!DNL Azure Payments HSM] 지원되지 않습니다. 자세한 내용은 [[!DNL Azure] 설명서](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) 제공 키 관리 서비스에 대한 자세한 정보.

>[!NOTE]
>
>아래 설명서에서는 주요 저장소를 만드는 기본 단계만 다룹니다. 이 지침 외에 조직의 정책에 따라 키 저장소를 구성해야 합니다.

에 로그인합니다. [!DNL Azure] 포털에서 검색 막대를 사용하여 **[!DNL Key vaults]** 서비스 목록 아래에 있습니다.

![주요 자격 증명 모음 검색 및 선택](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

다음 **[!DNL Key vaults]** 서비스를 선택하면 페이지가 나타납니다. 여기에서 을 선택합니다. **[!DNL Create]**.

![키 저장소 만들기](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

제공된 양식을 사용하여 이름 및 할당된 리소스 그룹을 포함하여 키 저장소에 대한 기본 세부 정보를 입력합니다.

>[!WARNING]
>
>대부분의 옵션을 기본값으로 둘 수 있지만, **소프트 삭제 및 제거 보호 옵션을 활성화해야 합니다**. 이러한 기능을 설정하지 않으면 키 저장소가 삭제되면 데이터에 대한 액세스가 손실될 수 있습니다.
>
>![제거 보호 사용](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

여기에서 주요 저장소 작성 워크플로우를 계속 진행하고 조직의 정책에 따라 다양한 옵션을 구성합니다.

일단 도착하시면 **[!DNL Review + create]** 단계에서는 유효성 검사를 수행하는 동안 키 저장소의 세부 정보를 검토할 수 있습니다. 유효성 검사가 전달되면 **[!DNL Create]** 프로세스를 완료합니다.

![주요 자격 증명 모음의 기본 구성](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Microsoft에 방화벽 예외 부여

키 저장소가 특정 가상 네트워크에 대한 공개 액세스를 제한하거나 공개 액세스를 완전히 비활성화하도록 구성된 경우 Microsoft에 방화벽 예외를 부여해야 합니다.

선택 **[!DNL Networking]** 을 클릭합니다. 아래 **[!DNL Firewalls and virtual networks]**, 확인란을 선택합니다. **[!DNL Allow trusted Microsoft services to bypass this firewall]**&#x200B;를 선택하고 을 선택합니다. **[!DNL Apply]**.

![주요 자격 증명 모음의 기본 구성](../images/governance-privacy-security/customer-managed-keys/networking.png)

## 키 생성 {#generate-a-key}

키 저장소를 만들면 새 키를 생성할 수 있습니다. 로 이동합니다 **[!DNL Keys]** 탭을 선택하고 **[!DNL Generate/Import]**.

![키 생성](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

제공된 양식을 사용하여 키의 이름을 지정하고 을(를) 선택합니다. **RSA** 를 입력합니다. 최소한, **[!DNL RSA key size]** 적어도 **3072년** 필요한 비트 수 [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] 또한 RSA 3027과 호환됩니다.

>[!NOTE]
>
>키를 제공할 때 이후 단계에서 사용되므로 이름을 기억하십시오. [Adobe으로 키 보내기](#send-to-adobe).

나머지 컨트롤을 사용하여 생성하거나 가져올 키를 원하는 대로 구성할 수 있습니다. 완료되면 을 선택합니다 **[!DNL Create]**.

![키 구성](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

구성된 키가 저장소의 키 목록에 나타납니다.

![키 추가됨](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## CMK 앱 등록 {#register-app}

키 저장소를 구성했으면 다음 단계는 다음 단계에 연결할 CMK 애플리케이션에 등록하는 것입니다 [!DNL Azure] 임차인.

>[!NOTE]
>
>CMK 앱을 등록하려면 플랫폼 API를 호출해야 합니다. 이러한 호출을 위해 필요한 인증 헤더를 수집하는 방법에 대한 자세한 내용은 [플랫폼 API 인증 안내서](../../landing/api-authentication.md).
>
>반면에 인증 안내서에서는 필요한 사용자에 대해 고유한 값을 생성하는 방법에 대한 지침을 제공합니다 `x-api-key` 요청 헤더, 이 안내서의 모든 API 작업은 정적 값을 사용합니다. `acp_provisioning` 을 가리키도록 업데이트하는 것이 좋습니다. 에 대해 고유한 값을 제공해야 합니다 `{ACCESS_TOKEN}` 및 `{ORG_ID}`하지만,

### 인증 URL 가져오기

등록 프로세스를 시작하려면 앱 등록 종단점에 대한 GET 요청을 수행하여 조직에 필요한 인증 URL을 가져옵니다.

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 `applicationRedirectUrl` 인증 URL을 포함하는 속성입니다.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

복사 및 붙여넣기 `applicationRedirectUrl` 주소를 브라우저에 입력하여 인증 대화 상자를 엽니다. 선택 **[!DNL Accept]** cmk 앱 서비스 주체를 [!DNL Azure] 임차인.

![권한 요청 수락](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

## 역할에 CMK 앱 할당 {#assign-to-role}

인증 프로세스를 완료한 후 다음 위치로 돌아갑니다. [!DNL Azure] 키 저장소 및 선택 **[!DNL Access control]** 을 클릭합니다. 여기에서 을 선택합니다. **[!DNL Add]** 후 **[!DNL Add role assignment]**.

![역할 할당 추가](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

다음 화면에 이 지정에 대한 역할을 선택하라는 메시지가 표시됩니다. 선택 **[!DNL Key Vault Crypto Service Encryption User]** 선택하기 전에 **[!DNL Next]** 계속하십시오.

![역할 선택](../images/governance-privacy-security/customer-managed-keys/select-role.png)

다음 화면에서 **[!DNL Select members]** 오른쪽 레일에서 대화 상자를 엽니다. 검색 막대를 사용하여 CMK 응용 프로그램의 서비스 주체를 찾아 목록에서 선택합니다. 완료되면 을 선택합니다 **[!DNL Save]**.

>[!NOTE]
>
>목록에서 애플리케이션을 찾을 수 없는 경우 서비스 주도자가 테넌트에 허용되지 않습니다. 다음 작업을 수행하십시오. [!DNL Azure] 관리자 또는 담당자가 올바른 권한을 가지고 있는지 확인합니다.

## Adobe으로 키 URI 보내기 {#send-to-adobe}

CMK 앱을 설치한 후 [!DNL Azure]를 입력하면 암호화 키 식별자를 Adobe으로 보낼 수 있습니다. 선택 **[!DNL Keys]** 왼쪽 탐색에서 를 클릭하고 전송할 키 이름이 옵니다.

![키 선택](../images/governance-privacy-security/customer-managed-keys/select-key.png)

최신 버전의 키를 선택하면 해당 세부 정보 페이지가 나타납니다. 여기에서 키에 대해 허용되는 작업을 선택적으로 구성할 수 있습니다. 최소한, 키에 **[!DNL Wrap Key]** 및 **[!DNL Unwrap Key]** 사용 권한.

다음 **[!UICONTROL 키 식별자]** 필드에 키의 URI 식별자가 표시됩니다. 다음 단계에서 사용할 이 URI 값을 복사합니다.

![키 URL 복사](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

키 볼트(Vault) URI를 얻으면 POST 요청을 사용하여 CMK 구성 끝점으로 보낼 수 있습니다.

**요청**

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
          "keyVaultIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 구성에 대한 이름입니다. 다음 위치에서 구성의 상태를 확인하는 데 필요하므로 이 값을 기억하는지 확인합니다. [이후 단계](#check-status). 값은 대/소문자를 구분합니다. |
| `type` | 구성 유형입니다. 을(를) 로 설정해야 합니다. `BYOK_CONFIG`. |
| `imsOrgId` | IMS 조직 ID입니다. 이 값은 `x-gw-ims-org-id` 헤더. |
| `configData` | 구성에 대한 다음 세부 정보를 포함합니다.<ul><li>`providerType`: 을(를) 로 설정해야 합니다. `AZURE_KEYVAULT`.</li><li>`keyVaultIdentifier`: 복사한 키 저장소 URI [이전](#send-to-adobe).</li></ul> |

**응답**

성공적인 응답은 구성 작업의 세부 정보를 반환합니다.

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
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

작업은 몇 분 내에 처리를 완료해야 합니다.

### 구성 상태 확인 {#check-status}

구성 요청의 상태를 확인하기 위해 GET 요청을 수행할 수 있습니다.

**요청**

을(를) 추가해야 합니다 `name` 경로(`config1` 아래 예에서 ) 및 `configType` 쿼리 매개 변수가 `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답은 작업의 상태를 반환합니다.

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
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

다음 `status` 속성에는 다음 의미의 네 개 값 중 하나를 사용할 수 있습니다.

1. `RUNNING`: 플랫폼이 키 및 키 저장소에 액세스할 수 있는지 확인합니다.
1. `UPDATE_EXISTING_RESOURCES`: 시스템에서 조직의 모든 샌드박스의 데이터 저장소에 키 저장소 및 키 이름을 추가합니다.
1. `COMPLETED`: 키 저장소 및 키 이름이 데이터 저장소에 추가되었습니다.
1. `FAILED`: 주로 키, 키 저장소 또는 다중 테넌트 앱 설정과 관련된 문제가 발생했습니다.

## 다음 단계

위의 단계를 완료하여 조직에 대해 CMK를 성공적으로 활성화했습니다. 이제 Platform으로 수집되는 모든 데이터는 암호화되어 사용자의 [!DNL Azure] 키 저장소. 데이터에 대한 플랫폼 액세스를 취소하려는 경우 내의 키 저장소에서 응용 프로그램과 연결된 사용자 역할을 제거할 수 있습니다 [!DNL Azure].

애플리케이션에 대한 액세스를 비활성화한 후 Platform에서 더 이상 데이터에 액세스할 수 없는 데 2~24시간이 소요됩니다. 애플리케이션에 대한 액세스를 다시 활성화할 때 동일한 시간 범위가 데이터를 다시 사용할 수 있게 됩니다.
