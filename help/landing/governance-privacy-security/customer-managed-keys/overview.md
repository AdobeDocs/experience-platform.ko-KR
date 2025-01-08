---
title: Adobe Experience Platform의 고객 관리 키
description: Adobe Experience Platform에 저장된 데이터에 대한 자체 암호화 키를 설정하는 방법에 대해 알아봅니다.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f2737355ca0652f434bd5f86acc65139f767e56f
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Adobe Experience Platform의 고객 관리 키

Adobe Experience Platform에 저장된 데이터는 시스템 수준 키를 사용하여 사용하지 않을 때 암호화됩니다. 플랫폼 위에 구축된 애플리케이션을 사용하는 경우 자체 암호화 키를 대신 사용하도록 선택할 수 있으므로 데이터 보안을 보다 세밀하게 제어할 수 있습니다.

>[!AVAILABILITY]
>
>Experience Platform 구현이 Amazon Web Services(AWS)에서 실행되는 경우 플랫폼 데이터 암호화에 KMS(키 관리 서비스)를 사용할 수 있습니다. 현재 AWS에서 실행 중인 Experience Platform은 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)를 참조하세요. AWS KMS의 암호화 키 생성 및 관리에 대한 자세한 내용은 [AWS KMS 데이터 암호화 안내서](../key-management-service/overview.md)를 참조하세요.

>[!NOTE]
>
>플랫폼의 [!DNL Azure Data Lake] 및 [!DNL Azure Cosmos DB] 프로필 저장소에 저장된 고객 프로필 데이터가 활성화되면 CMK를 사용하여 독점적으로 암호화됩니다. 기본 데이터 저장소의 키 해지 시간은 **몇 분에서 24시간**&#x200B;까지 소요될 수 있으며 임시 또는 보조 데이터 저장소의 경우 **최대 7일**&#x200B;까지 소요될 수 있습니다. 자세한 내용은 [키 액세스 섹션 취소의 의미](#revoke-access)를 참조하세요.

이 문서에서는 Platform에서 CMK(고객 관리 키) 기능을 활성화하는 프로세스에 대한 높은 수준의 개요와 이러한 단계를 완료하는 데 필요한 사전 요구 사항 정보를 제공합니다.

>[!NOTE]
>
>Customer Journey Analytics 고객의 경우 [Customer Journey Analytics 설명서](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=ko)의 지침을 따르십시오.

## 전제 조건

Adobe Experience Platform에서 [!UICONTROL 암호화] 섹션을 보고 방문하려면 역할을 만들고 해당 역할에 [!UICONTROL 고객 관리 키 관리] 권한을 할당해야 합니다. [!UICONTROL 고객 관리 키 관리] 권한이 있는 모든 사용자는 해당 조직에 대해 CMK를 사용할 수 있습니다.

Experience Platform에서 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [권한 구성 설명서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)를 참조하세요.

CMK를 사용하려면 다음 설정으로 [!DNL Azure] 키 저장소를 구성해야 합니다.

* [제거 보호 사용](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [일시 삭제 사용](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [역할 기반 액세스 제어를 사용하여 액세스 구성 [!DNL Azure] 2}](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

프로세스를 더 잘 이해하려면 연결된 설명서를 읽어 보십시오.

## 프로세스 요약 {#process-summary}

CMK는 Adobe의 Healthcare Shield 및 Privacy and Security Shield 오퍼링에 포함되어 있습니다. 조직에서 이러한 서비스 중 하나에 대한 라이선스를 구입한 후 해당 기능을 설정하는 프로세스를 한 번 시작할 수 있습니다.

>[!WARNING]
>
>CMK를 설정한 후에는 시스템 관리 키로 되돌릴 수 없습니다. [!DNL Azure] 내에서 키를 안전하게 관리하고 Key Vault, Key 및 CMK 앱에 대한 액세스 권한을 제공하여 데이터에 대한 액세스 권한을 상실하지 않도록 해야 합니다.

프로세스는 다음과 같습니다.

1. [조직의 정책을 기반으로  [!DNL Azure] 키 저장소를 구성](./azure-key-vault-config.md)한 다음 [암호화 키를 생성](./azure-key-vault-config.md#generate-a-key)하여 궁극적으로 Adobe과 공유합니다.
1. [API 호출](./api-set-up.md#register-app) 또는 [UI](./ui-set-up.md#register-app)를 통해 [!DNL Azure] 테넌트로 CMK 앱을 설정합니다.
1. 암호화 키 ID를 Adobe에 보내고 [UI에서](./ui-set-up.md#send-to-adobe) 또는 [API 호출](./api-set-up.md#send-to-adobe)을(를) 사용하여 기능에 대한 활성화 프로세스를 시작합니다.
1. 구성 상태를 확인하여 CMK가 UI에서 [활성화되었는지](./ui-set-up.md#check-status) 또는 [API 호출](./api-set-up.md#check-status)을(를) 통해 활성화되었는지 확인하십시오.

설정 프로세스가 완료되면 모든 샌드박스에서 플랫폼으로 온보딩되는 모든 데이터는 [!DNL Azure] 키 설정을 사용하여 암호화됩니다. CMK를 사용하려면 [공개 미리 보기 프로그램](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/)의 일부일 수 있는 [!DNL Microsoft Azure] 기능을 활용하게 됩니다.

## 키 액세스 취소의 의미 {#revoke-access}

Key Vault, 키 또는 CMK 앱에 대한 액세스를 취소하거나 비활성화하면 플랫폼 작업에 대한 변경 내용 중지를 포함하여 심각한 차질이 발생할 수 있습니다. 이러한 키가 비활성화되면 Platform의 데이터에 액세스할 수 없게 되고 이 데이터를 사용하는 다운스트림 작업이 중단됩니다. 주요 구성을 변경하기 전에 다운스트림 영향을 완전히 이해하는 것이 중요합니다.

데이터에 대한 Platform 액세스를 취소하기로 결정한 경우 [!DNL Azure] 내의 Key Vault에서 응용 프로그램과 연결된 사용자 역할을 제거하면 됩니다.

### 전파 타임라인 {#propagation-timelines}

[!DNL Azure] 키 저장소에서 키 액세스가 해지되면 변경 사항이 다음과 같이 전파됩니다.

| **저장소 유형** | **설명** | **타임라인** |
|---|---|---|
| 기본 데이터 저장소 | 이러한 저장소에는 Azure Data Lake 및 Azure Cosmos DB 프로필 저장소가 포함됩니다. 키 액세스가 취소되면 데이터에 액세스할 수 없게 됩니다. | **몇 분에서 24시간**&#x200B;까지. |
| 캐시된/임시 데이터 저장소 | 성능 및 핵심 애플리케이션 기능에 사용되는 데이터 저장소를 포함합니다. 키 해제의 영향이 지연됩니다. | **최대 7일**. |

예를 들어 프로필 대시보드는 데이터가 만료되고 새로 고쳐지기 전까지 최대 7일 동안 해당 캐시의 데이터를 계속 표시합니다. 마찬가지로 애플리케이션에 대한 액세스를 다시 활성화하면 이러한 저장소에서 데이터 가용성을 복원하는 데 동일한 시간이 소요됩니다.

>[!NOTE]
>
>기본이 아닌(캐시된/임시) 데이터에 대한 7일 데이터 세트 만료에 대한 두 가지 사용 사례별 예외가 있습니다. 이러한 기능에 대한 자세한 내용은 해당 설명서 를 참조하십시오.<ul><li>[Adobe Journey Optimizer URL 단축기](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[Edge 예측](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 다음 단계

프로세스를 시작하려면 [Key Vault 구성](./azure-key-vault-config.md) 및 [Adobe과 공유할 암호화 키 생성](./azure-key-vault-config.md#generate-a-key)부터 시작합니다. [!DNL Azure] 
